---
title : "API Gateway & Secrets"
weight : 3
chapter : false
pre : " <b> 5.4.3. </b> "
---

The final step of the Backend section is to expose connection endpoints (API Gateway) and configure security.

#### 1. Create API Gateway Trigger

1.  Re-open the **`ragsearch`** Lambda Function.
2.  In the Function overview section, click **Add trigger**.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.26.png)

3.  Select source: **API Gateway**.
    *   Intent: **Create a new API**.
    *   API type: **HTTP API**.
    *   Security: **IAM**.
4.  Click **Add**.

![alt text](/images/5-Workshop/5.3-Infrastructure/3.27.png)

👉 **Important:** After creation, copy the **API Endpoint** URL (format `https://...amazonaws.com`) and save it to Notepad.

#### 2. Create Secrets Manager

1.  Search for the **Secrets Manager** service -> Select **Store a new secret**.
2.  Secret type: Select **Other type of secret**.
3.  **Key/value pairs**:
    *   Key: `JWT_SECRET`
    *   Value: `(Enter any random password of your choice)`
4.  Click **Next** -> Name the Secret (arbitrary) -> **Next** -> **Store**.


#### 3. Update ARN for Lambda

The Lambda functions need to know each other's addresses (ARNs) to call one another.

1.  Open 3 browser tabs corresponding to the 3 Lambda functions (`ragsearch`, `generate_contract`, `CallLLM`).
2.  Copy the **Function ARN** of each function (Located at the top right corner of the Function overview section).
3.  Return to the **Environment variables** configuration tab of the **`ragsearch`** function.
4.  Click **Edit** and add the following variables:
    *   `LAMBDA_RETRIEVAL_ARN`: Paste the ARN of the `ragsearch` function.
    *   `LAMBDA_REVIEW_ARN`: Paste the ARN of the `CallLLM` function.
    *   `LAMBDA_GENERATE_ARN`: Paste the ARN of the `generate_contract` function.
5.  Click **Save**.

![alt text](/images/5-Workshop/5.3-Infrastructure/3.28.png)