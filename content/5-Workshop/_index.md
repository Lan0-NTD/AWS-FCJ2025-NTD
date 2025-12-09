---
title : "Workshop"
weight: 5
chapter: false
pre: " <b> 5. </b> "
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

The solution is built entirely on AWS **Serverless** architecture, helping optimize operational costs and scalability. A highlight of the architecture is the application of the **RAG (Retrieval-Augmented Generation)** technique, allowing AI to retrieve accurate information from your own data repository instead of relying solely on pre-trained knowledge.

The key components of the system include:

1.  **AI & LLM (Amazon Bedrock):**
    *   This is the "heart" of the application. We use Amazon Bedrock to access advanced Large Language Models (LLMs) such as Claude 3 (Haiku/Sonnet) via API.
    *   Bedrock is responsible for understanding the context of questions, synthesizing information from documents, and generating natural responses.

2.  **Backend & Computing (AWS Lambda & API Gateway):**
    *   Uses **AWS Lambda** to run Python code snippets to handle business logic (vector search, calling Bedrock API, processing input data) without managing servers.
    *   **Amazon API Gateway** acts as the gateway, receiving requests from the user side (Frontend) and routing them to the corresponding Lambda functions.

3.  **Database & Storage (Amazon S3 & DynamoDB):**
    *   **Amazon S3:** Acts as the storage repository ("Data Lake") containing sample contract files (.docx, .pdf), metadata files, and embedded vector data to serve semantic search.
    *   **Amazon DynamoDB:** A high-performance NoSQL database used to store user information, manage work sessions, and chat message history, ensuring the lowest latency for retrieval.

4.  **Frontend & Authentication (AWS Amplify & Cognito):**
    *   The user interface is built using React/VueJS and is automatically deployed via **AWS Amplify**.
    *   **Amazon Cognito** provides sign-up, sign-in, and security mechanisms, ensuring only authorized users can access the application.

#### Learning Objectives

After completing this workshop, you will master:
*   How to deploy a **Full-stack** application on AWS from scratch.
*   Understanding and applying the **RAG** model to combine enterprise data with the power of LLMs.
*   Skills in working with **Infrastructure as Code** via the Serverless Framework.
*   Configuring and integrating core AWS services: S3, DynamoDB, Lambda, API Gateway, and Bedrock.

#### Practice Content

1. [Workshop Overview](5.1-Workshop-overview/)
2. [Prerequisites](5.2-Prerequiste/)
3. [Infrastructure Setup (S3, DynamoDB)](5.3-Infrastructure/)
4. [Building Backend (Lambda, IAM)](5.4-Backend/)
5. [Fullstack Deployment (Amplify)](5.5-Fullstack/)
6. [Clean Up Resources](5.6-Cleanup/)