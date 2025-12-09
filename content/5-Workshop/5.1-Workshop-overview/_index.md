---
title : "Overview"
weight : 1 
chapter : false
pre : " <b> 5.1 </b> "
---
# Building a Smart Contract Assistant on AWS

#### Introduction

The AI Contract Intelligence platform is a web service designed for individuals and small teams (freelancers, small business owners, administrative/legal personnel) who work with contracts daily but lack deep legal expertise. The solution utilizes Amazon Bedrock and a fully serverless AWS architecture to analyze contracts, highlight risks, suggest clause revisions, and generate summaries as well as new contract templates.

Built on AWS Amplify, Lambda, API Gateway, DynamoDB, S3, Cognito, EventBridge, and CloudWatch, the platform provides AI-powered contract review capabilities with low latency, low cost, and high security. It is optimized for single users or small teams without the need for complex enterprise-grade features.

The primary goal of the application is to assist users (such as lawyers, compliance officers, or business owners) in performing complex tasks such as:
*   **Information Retrieval:** Q&A regarding legal clauses based on an available repository of legal texts.
*   **Automated Drafting:** Requesting the AI to generate contract drafts based on standard templates and provided information.
*   **Analysis:** Summarizing and auditing contract content.

#### Solution Architecture

The system is designed using an **Event-driven Serverless** architecture, optimizing costs (pay-per-use) and enabling automatic scalability. We will apply **RAG (Retrieval-Augmented Generation)** techniques to provide private data context (vector data) to the AI model, ensuring answers are more accurate and realistic.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.53.png)
The core AWS service components include:

1.  **Amazon Bedrock (Generative AI):**
    *   Acts as the brain for natural language processing.
    *   We will use Foundation Models such as **Claude 3 (Haiku/Sonnet)** via API to handle intent understanding, text generation, and legal logic processing.

2.  **AWS Lambda & Amazon API Gateway (Backend):**
    *   **AWS Lambda:** Runs Python functions to handle business logic, such as vector searches, calling Bedrock APIs, and data orchestration.
    *   **Amazon API Gateway:** Creates secure HTTP endpoints (RESTful APIs) for the Frontend to communicate with the Backend.

3.  **Amazon S3 (Storage):**
    *   Stores static files like sample contract documents (.docx, .pdf).
    *   Stores the vector database (embeddings) of legal texts to serve Semantic Search features.

4.  **Amazon DynamoDB (Database):**
    *   Stores user information (Users).
    *   Manages work sessions (Chat Sessions) and saves the entire chat history (Chat Messages) with minimal latency.

5.  **AWS Amplify & Amazon Cognito (Frontend & Auth):**
    *   **AWS Amplify:** Automates deployment (CI/CD) and hosting for the web application (React/Vue).
    *   **Amazon Cognito:** Manages user identity, allowing secure sign-up/sign-in and granting API access.

#### Learning Objectives

Upon completion of this workshop, you will achieve:
*   A clear understanding of the process for building a GenAI application from Backend to Frontend.
*   Hands-on experience working with **Amazon Bedrock** and RAG techniques.
*   The ability to set up and configure Serverless services: Lambda, DynamoDB, API Gateway.
*   Skills in deploying modern web applications using AWS Amplify.