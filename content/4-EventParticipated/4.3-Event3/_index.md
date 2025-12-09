---
title: "AWS Cloud Mastery Series #1"
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

### AI/ML/GenAI on AWS
#### Saturday, 15/11/2025 – AWS Vietnam Office


### I. General information about the event

* **Event name:** AI/ML/GenAI on AWS
* **Time:** 8:30 – 12:00, 15/11/2025
* **Venue:** AWS Vietnam Office
* **Objectives:**

  * Provide an overview of AI/ML and GenAI on the AWS platform.
  * Clarify the concept of *foundation models* and practical application patterns.
  * Present the AI/ML service ecosystem on AWS, from “ready-made” services to platforms for building custom models.
  * Demonstrate how to build GenAI applications using Amazon Bedrock, RAG, and AgentCore.


### II. Main contents by timeline

### 1. Opening session – Introduction to GenAI and Foundation Models (8:30 – 9:00)

Presenter **Lâm Tuấn Kiệt** focused on laying the foundation for **Generative AI (GenAI)**:

* **What is GenAI:**

  * Unlike traditional ML models that mainly “classify” or “predict”, GenAI can *generate new* content: text, images, audio, source code, etc.
  * GenAI is built on very large-scale **foundation models** (billions of parameters), trained on diverse datasets, then *fine-tuned* or *instruction-tuned* for specific real-world tasks.

* **Foundation Models & Amazon Bedrock:**

  * Amazon Bedrock was introduced as a **platform to manage and access multiple foundation models from different providers** (such as Claude, Llama, Titan, …), allowing users to avoid managing infrastructure, scaling, or model security themselves.
  * Key point: through a single API, you can experiment with multiple models, compare quality and cost, and select the right model for each scenario (chatbot, summarization, text classification, RAG, …).

* **Prompt Engineering:**

  * Emphasized as a **core skill** when working with GenAI:

    * *Prompt engineering = the process of designing, experimenting with, and refining prompts* so that the model correctly understands the context and produces appropriate outputs.
  * Main techniques mentioned:

    * **Zero-shot prompting:** no examples provided, only a description of the requirement.
    * **Few-shot prompting:** provide a few sample examples so the model “learns how to respond” in the desired style.
    * **Chain-of-Thought (CoT):** instruct the model to *lay out its reasoning step by step*, which improves logical consistency, especially for tasks involving calculations and multi-step reasoning.

* **RAG (Retrieval-Augmented Generation):**

  * Introduced as an architecture that combines **knowledge retrieval** with GenAI: the model is mainly “good at language”, while specific knowledge is taken from the organization’s own data sources (documents, knowledge bases, …).
  * My notes emphasize: *“RAG: retrieving relevant info from a data source”* – the model will retrieve relevant text passages, then use a foundation model to synthesize and answer based on that data, helping to:

    * Reduce the risk of “hallucination”.
    * Make knowledge updates easier (just update the data store, without retraining the model).

---

#### 2. “AWS AI/ML Services Overview” & Embeddings/RAG in Action (9:00 – 10:30)

This part focused on the **overall picture of the AI service ecosystem on AWS** and how to leverage it for GenAI/RAG.

#### 2.1. Embeddings and Titan Embeddings

* In the slide “What are embeddings?”, the instructor explained:

  * Embeddings are a way to **represent text/images as numerical vectors** so that models can measure similarity, perform search, clustering, etc.
  * Embeddings are the “foundation” of RAG systems, semantic search, recommendation systems, …

* AWS introduced **Titan Embeddings** – an embedding option provided by AWS, optimized for:

  * Semantic search.
  * RAG over enterprise documents.
  * Tight integration with Amazon Bedrock and other services.

* Note: *“Embeddings. Some options supported by AWS. RAG in action.”* – I understood this as a demo describing the pipeline: data → chunking → generate embeddings → store in a vector store → query and combine with an LLM to answer.

#### 2.2. “Ready-made” AI services on AWS

Mr. **Hoàng Anh** provided details on managed AI services, where I captured both use cases and indicative pricing:

* **Amazon Rekognition** – Computer Vision:

  * Detects objects, faces, and text in images/videos.
  * Note: *“0.0013 USD/image (under 1 million images)”* → suitable for medium-scale image recognition use cases such as camera monitoring and content filtering.

* **Amazon Translate** – Neural Machine Translation:

  * Automatic multilingual translation.
  * Note: *“15 USD / 1 million characters”* → can be applied to automated translation of documents, emails, and web content.

* **Amazon Textract** – OCR & structured document extraction:

  * Not only recognizes text but also **preserves layout** of tables, forms, and fields.
  * Note: *“0.05 USD/page (under 1 million pages)”*, highly suitable for extracting data from contracts and invoices.

* **Amazon Transcribe** – Speech-to-Text:

  * Converts speech to text, supports captions and meeting transcripts.
  * Note: *“0.024 USD/minute (under 250k minutes)”*.

* **Amazon Polly** – Text-to-Speech:

  * Generates natural-sounding speech from text.
  * Note: *“4 USD / 1 million characters”* → used for voicebots, audio guides, and training videos.

* **Amazon Comprehend** – NLP service:

  * Analyzes sentiment, key phrases, entities, relationships, … from text.
  * Note: *“0.0001 USD / 100 characters or 3 USD/hour”* → suitable for customer feedback analysis systems and ticket classification.

* **Amazon Kendra** – Intelligent Search / RAG Support:

  * Semantic search, FAQ, semantic retrieval.
  * Note: *“30 USD/index/month + 0.35 USD/hour”* → acts as an internal “search engine” for enterprise documents, integrates well with RAG.

* **Amazon Personalize** – Recommendation:

  * Personalized recommendations: products, content, user segmentation, …
  * Note: *“0.24 USD/hour training + 0.05 USD/GB + 0.15 USD/1000 recommendations”*.

Listing **use cases along with cost** made it easier for me to envision designing solutions that are both technically appropriate and budget-conscious.

---

### 3. “Generative AI with Amazon Bedrock” – AgentCore & Pipecat (10:45 – 12:00)

After the overview, the program moved into **building practical GenAI systems**.

#### 3.1. Pipecat – Framework for voice/multimodal AI agents

* **Pipecat** was introduced as a **pipeline framework optimized for real-time voice/multimodal agents**:

  * Supports composing multiple components: speech-to-text, LLM, text-to-speech, external tools, … into a unified pipeline.
  * Optimized for low latency, suitable for voice assistants and callbot applications.

The key takeaway for me: instead of “manually wiring” every service, one can use a framework like Pipecat to standardize the processing flow, making it easier to scale and maintain.

#### 3.2. Amazon Bedrock AgentCore and the Agentic AI ecosystem

Speaker **Hiếu Nghị** presented **Bedrock AgentCore** and the broader picture of **agentic AI systems**:

* **From LLMs to Agentic Systems:**

  * A standalone LLM only “answers questions”.
  * An agentic system adds: goals, planning, tool calling capabilities, data access, and multi-step decision-making.
  * Bedrock AgentCore was introduced as an **orchestration layer** for building such agents on AWS infrastructure.

* **Agent-building frameworks mentioned:**

  * crew.ai, Google ADK, LlamaIndex, OpenAI Agents SDK, LangChain, LangGraph, Strands Agents SDK, …
  * Main point: the ecosystem is rich, but when running on AWS, AgentCore helps **optimize integration with AWS services, security, logging, monitoring, …**

* **Key capabilities of Bedrock AgentCore** (based on slides and notes):

  * Connects to multiple foundation models on Bedrock.
  * Manages multi-step workflows and tool calls (Lambda, internal APIs, data queries, …).
  * Supports RAG and integrates with Kendra/Knowledge Base.
  * Enables guardrails (content policies, domain restrictions for responses).
  * Provides observability & monitoring over agent behavior in production.

* **Challenges when putting agents into production:**

  * Stability and predictability of agent behavior.
  * Controlling inference costs when workflows become complex.
  * Data security and access control when agents call into multiple systems.
  * Detailed logging/monitoring for debugging and continuous improvement.

The session concluded with a **demo of building a GenAI chatbot on Bedrock** using RAG and basic guardrails, bridging theory with practical implementation.

---

### III. Knowledge and lessons learned

1. **Clearer understanding of the role of GenAI in modern system architecture**

   * GenAI does not stand alone; it must be combined with RAG, search, data pipelines, monitoring, …
   * Proper understanding of foundation models and prompt engineering helps avoid unrealistic expectations and leads to more practical solution design.

2. **Grasping the AI service ecosystem on AWS from a “build vs. buy” perspective**

   * Services like Rekognition, Textract, Comprehend, Personalize, … are well suited for standardized use cases that do not require deep customization.
   * When domain-specific data is involved (contracts, legal documents, internal logs, …), combining **Bedrock + Embeddings + Kendra/RAG** offers more flexibility.

3. **Pragmatic view on costs**

   * The concrete numbers in the notes make it clear that technical problems must always be considered alongside economic constraints.
   * Right from the design phase, it is necessary to estimate volume (number of images, characters, minutes of audio, requests) to choose appropriate services and models.

4. **“Agentic” mindset instead of just “chatbot”**

   * The concept of AgentCore and agentic AI systems shows that the next step is not just Q&A, but **process automation**: reading data, calling APIs, making decisions, writing logs, …
   * This opens many directions for personal projects:

     * An agent assisting with legal contract analysis.
     * An agent monitoring infrastructure logs and alerting on anomalies.
     * An agent assisting with financial analysis and suggesting actions based on real-time data.

### IV. Personal application roadmap

After this event, I plan to:

1. **Design a RAG pipeline on AWS** for my current problem domain (e.g., legal contract analysis, educational materials):

   * Use Textract to extract document content.
   * Use Titan Embeddings to generate vectors and store them in a vector store.
   * Connect Kendra or an equivalent search engine for retrieval.
   * Use Bedrock (Claude/Llama/Titan) to build a chatbot that answers based on internal documents.

2. **Experiment with a small Agent using Bedrock AgentCore**:

   * Initial step: the agent receives a question → queries the knowledge base → synthesizes → produces a short report.
   * Next step: extend so that the agent can call Lambda to execute actions (e.g., create tickets, send emails, update logs).

3. **Further develop prompt engineering skills**:

   * Practice different prompt types: zero-shot, few-shot, CoT on my own use cases (AI/ML, DevOps, Security).
   * Record effective “prompt patterns” into a reusable library for multiple projects.


### V. Images

![Foundation Model](/images/4-Event/4.4-AWS/1.jpeg)
![What are Embedding?](/images/4-Event/4.4-AWS/2.jpeg)
![Amazon Titan Embedding](/images/4-Event/4.4-AWS/3.jpeg)
![RAG in action](/images/4-Event/4.4-AWS/4.jpeg)
![Data ingestion workflow](/images/4-Event/4.4-AWS/5.jpeg)
![AWS AI Service](/images/4-Event/4.4-AWS/6.jpeg)
![Lookout Family](/images/4-Event/4.4-AWS/7.jpeg)
![Pipecat](/images/4-Event/4.4-AWS/8.jpeg)