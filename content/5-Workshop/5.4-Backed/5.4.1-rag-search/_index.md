---
title : "Create Lambda RAG Search"
weight : 1
chapter : false
pre : " <b> 5.4.1. </b> "
---

The `ragsearch` function is the most critical component, responsible for searching legal data and answering questions.

#### 1. Function Initialization

1.  Access the **Lambda** service -> Select **Create function**.
2.  Choose **Author from scratch**.
3.  Fill in the basic information:
    *   **Function name**: `ragsearch`
    *   **Runtime**: `Python 3.12`
    *   **Architecture**: `x86_64`
4.  Click **Create function**.

![alt text](/images/5-Workshop/5.3-Infrastructure/3.14.png)

#### 2. Update Code

1.  In the **Code** tab, open the `lambda_function.py` file.
2.  Clear all default content.
3.  Open the `ragsearch.py` file in the source code folder, copy the entire content, and paste it into the code window on the AWS Console.
```python
import json
import os
import math
import logging
from typing import List, Dict, Any, Tuple

import boto3
from botocore.exceptions import ClientError

logger = logging.getLogger()
logger.setLevel(logging.INFO)

# -----------------------------------------------------------------------------
# Config
# -----------------------------------------------------------------------------

AWS_REGION = os.getenv("AWS_REGION", "ap-southeast-1")
EMBED_MODEL_ID = os.getenv("EMBED_MODEL_ID", "cohere.embed-multilingual-v3")

LEGAL_INDEX_BUCKET = os.getenv("LEGAL_INDEX_BUCKET")  # Name of S3 bucket
LEGAL_INDEX_KEY = os.getenv("LEGAL_INDEX_KEY", "index/legal_chunks_with_emb.jsonl")

if not LEGAL_INDEX_BUCKET:
    raise RuntimeError("LEGAL_INDEX_BUCKET env var is required")

s3 = boto3.client("s3", region_name=AWS_REGION)
bedrock = boto3.client("bedrock-runtime", region_name=AWS_REGION)


# -----------------------------------------------------------------------------
# Global cache
# -----------------------------------------------------------------------------

INDEX_CACHE = {
    "loaded": False,
    "chunks": [],   # list of dict (metadata + text, no embedding)
    "vectors": []   # list of list[float]
}


# -----------------------------------------------------------------------------
# Helpers
# -----------------------------------------------------------------------------

def cosine_similarity(a: List[float], b: List[float]) -> float:
    if not a or not b or len(a) != len(b):
        return 0.0
    dot = 0.0
    na = 0.0
    nb = 0.0
    for x, y in zip(a, b):
        dot += x * y
        na += x * x
        nb += y * y
    if na == 0.0 or nb == 0.0:
        return 0.0
    return dot / math.sqrt(na * nb)

def get_embedding(text: str) -> List[float]:
    if not text or not text.strip():
        raise ValueError("Query text is empty")

    model_id = EMBED_MODEL_ID

    # If Cohere Embed v3 (english/multilingual)
    if model_id.startswith("cohere.embed-"):
        # Query → use search_query
        body_dict = {
            "texts": [text],
            "input_type": "search_query"
            # Can add "truncate": "END" if needed
        }
    else:
        # Default: Titan embeddings
        body_dict = {
            "inputText": text
        }

    body = json.dumps(body_dict)

    try:
        response = bedrock.invoke_model(
            modelId=model_id,
            body=body,
            contentType="application/json",
            accept="application/json",
        )
    except ClientError as e:
        logger.error("Bedrock invoke_model failed: %s", e)
        raise

    response_body = json.loads(response["body"].read())

    # Parse output depending on model
    if model_id.startswith("cohere.embed-"):
        # "embeddings": [ [1024 floats] ]
        embeddings = response_body.get("embeddings")
        if not embeddings or not isinstance(embeddings, list):
            raise ValueError("No embeddings found in Cohere response")
        return embeddings[0]
    else:
        # Titan: {"embedding": [..]}
        embedding = response_body.get("embedding")
        if not embedding:
            raise ValueError("No embedding found in Titan response")
        return embedding


def load_index_if_needed():
    if INDEX_CACHE["loaded"]:
        return

    logger.info(
        "Loading legal index from s3://%s/%s ...",
        LEGAL_INDEX_BUCKET, LEGAL_INDEX_KEY
    )

    try:
        obj = s3.get_object(Bucket=LEGAL_INDEX_BUCKET, Key=LEGAL_INDEX_KEY)
    except ClientError as e:
        logger.error("Failed to get index object from S3: %s", e)
        raise

    chunks: List[Dict[str, Any]] = []
    vectors: List[List[float]] = []

    for line in obj["Body"].iter_lines():
        if not line:
            continue
        try:
            rec = json.loads(line.decode("utf-8"))
        except json.JSONDecodeError:
            logger.warning("Invalid JSON line in index, skipped")
            continue

        emb = rec.get("embedding")
        text = (rec.get("text") or "").strip()
        if not emb or not text:
            # Skip record missing embedding / text
            continue

        # Separate embedding from metadata
        rec_no_emb = dict(rec)
        rec_no_emb.pop("embedding", None)

        vectors.append(emb)
        chunks.append(rec_no_emb)

    INDEX_CACHE["chunks"] = chunks
    INDEX_CACHE["vectors"] = vectors
    INDEX_CACHE["loaded"] = True

    logger.info(
        "Loaded %d chunks with embeddings into cache",
        len(chunks)
    )


def parse_event_body(event: Dict[str, Any]) -> Dict[str, Any]:
    if "body" not in event:
        return event
    body = event["body"]
    if event.get("isBase64Encoded"):
        body = base64.b64decode(body).decode("utf-8")  # need import base64 if used
    try:
        data = json.loads(body)
    except json.JSONDecodeError:
        raise ValueError("Request body must be valid JSON")
    return data


def apply_filters(rec: Dict[str, Any], filters: Dict[str, Any]) -> bool:
    """
    filters format:
    {
      "source_type": ["legal", "template"],
      "doc_category": ["luat", "nghi_dinh"],
      "field": ["Xây dựng - Đô thị"]
    }
    Returns True if record PASSES filter.
    """
    if not filters:
        return True

    # source_type
    st_list = filters.get("source_type")
    if st_list:
        st_val = rec.get("source_type")
        if st_val not in st_list:
            return False

    # doc_category
    cat_list = filters.get("doc_category")
    if cat_list:
        cat_val = rec.get("doc_category")
        if cat_val not in cat_list:
            return False

    # field
    field_list = filters.get("field")
    if field_list:
        field_val = rec.get("field")
        if field_val not in field_list:
            return False

    return True


def search_index(query: str, top_k: int, filters: Dict[str, Any]) -> List[Dict[str, Any]]:
    load_index_if_needed()

    q_emb = get_embedding(query)

    scores: List[Tuple[float, int]] = []

    for i, vec in enumerate(INDEX_CACHE["vectors"]):
        s = cosine_similarity(q_emb, vec)
        scores.append((s, i))

    # sort from high to low
    scores.sort(key=lambda x: x[0], reverse=True)

    results: List[Dict[str, Any]] = []
    for score, idx in scores:
        if score <= 0:
            break
        rec = INDEX_CACHE["chunks"][idx]

        if not apply_filters(rec, filters):
            continue

        # copy metadata + add score
        res = dict(rec)
        res["score"] = score
        results.append(res)

        if len(results) >= top_k:
            break

    return results


def make_response(status_code: int, body: Dict[str, Any]) -> Dict[str, Any]:
    return {
        "statusCode": status_code,
        "headers": {
            "Content-Type": "application/json",
            "Access-Control-Allow-Origin": "*",  # for demo
        },
        "body": json.dumps(body, ensure_ascii=False),
    }


# -----------------------------------------------------------------------------
# Lambda handler
# -----------------------------------------------------------------------------

def lambda_handler(event, context):
    logger.info("Received event: %s", json.dumps(event)[:1000])

    try:
        body = parse_event_body(event)

        # ==================================================================
        # 🔥 NEW CODE: KEEP WARM HANDLING
        # ==================================================================
        if body.get("keep_warm"):
            logger.info("Keep-warm ping received. Checking index cache...")
            
            # Important: Call this function to load file from S3 into RAM (if not present)
            # Helps the next user avoid waiting (Cold Start)
            load_index_if_needed()
            
            return make_response(200, {"message": "Pong! I am warm and index is loaded."})
        # ==================================================================

        query = (body.get("query") or "").strip()
        if not query:
            return make_response(400, {"error": "query is required"})

        language = (body.get("language") or "vi").lower()
        top_k = body.get("top_k") or 10
        try:
            top_k = int(top_k)
            if top_k <= 0:
                top_k = 10
        except Exception:
            top_k = 10

        filters = body.get("filters") or {}

        # Perform search (once index is confirmed loaded)
        results = search_index(query=query, top_k=top_k, filters=filters)

        resp = {
            "query": query,
            "language": language,
            "top_k": top_k,
            "results": results,
        }
        return make_response(200, resp)

    except ValueError as ve:
        return make_response(400, {"error": str(ve)})

    except ClientError as ce:
        logger.error("AWS client error: %s", ce)
        return make_response(
            502,
            {"error": "Upstream AWS error", "details": str(ce)},
        )

    except Exception as e:
        logger.error("Unexpected error: %s", e)
        return make_response(
            500,
            {"error": "Internal server error", "details": str(e)},
        )
```
4.  Click the **Deploy** button (grey button) to save changes.

![alt text](/images/5-Workshop/5.3-Infrastructure/3.13.png)

#### 3. Configuration

Switch to the **Configuration** tab to set technical parameters.

**A. General configuration**
1.  Select **General configuration** on the left menu -> Click **Edit**.
2.  **Memory**: Increase to `3000 MB`.
3.  **Timeout**: Increase to `1 min 0 sec`.
4.  Click **Save**.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.15.png)


**B. Environment variables**
1.  Select **Environment variables** on the left menu -> Click **Edit**.
2.  Click **Add environment variable** and add the following 2 lines:
    *   Key: `LEGAL_INDEX_BUCKET` | Value: `<Your-S3-Bucket-Name>`
    *   Key: `LEGAL_INDEX_KEY` | Value: `legal-corpus/index/legal_chunks_with_emb.jsonl`
3.  Click **Save**.

![alt text](/images/5-Workshop/5.3-Infrastructure/3.16.png)

#### 4. Permissions

1.  Select **Permissions** on the left menu.
2.  Click on the **Role name** (blue link) to open the IAM Role page.
3.  In the opened IAM page: Click **Add permissions** -> **Attach policies**.
4.  Search for and check the following 2 policies:
    *   `AmazonBedrockFullAccess`
    *   `AmazonS3FullAccess`
5.  Click **Add permissions**.

![alt text](/images/5-Workshop/5.3-Infrastructure/3.17.png)