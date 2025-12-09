---
title : "Building the Backend (Lambda)"
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

### Introduction

In this section, we will build the core processing component (Backend) for the **Smart Contract Assistant** application. The system utilizes a Serverless architecture with **AWS Lambda** to handle user requests and interact with AI (Amazon Bedrock).

### Key Components

We will proceed through the following steps:

1.  **[Create RAG Search Lambda](5.4.1-rag-search/)**: Build an intelligent search function that connects to vector data in S3.
2.  **[Create Auxiliary Lambdas](5.4.2-other-lambdas/)**: Build the contract generation function (`generate_contract`) and the general chat function (`CallLLM`).
3.  **[Configure API & Security](5.4.3-api-secrets/)**: Set up API Gateway to expose connection endpoints and Secrets Manager to store secret keys.
