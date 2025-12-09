---
title : "Infrastructure Setup"
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

### Introduction

In this module, we will start building the foundation for the **Smart Contract Assistant** application. Before deploying the logic processing code (Lambda) or the user interface (Frontend), we need to prepare a location to store data.

We will set up two critical AWS services:

1.  **Amazon S3 (Simple Storage Service):**
    *   Acts as a "Data Lake".
    *   Stores contract templates.
    *   Stores encoded legal text data (Embeddings) to serve the intelligent search feature (RAG).

2.  **Amazon DynamoDB:**
    *   Acts as a high-performance NoSQL Database.
    *   Stores user profiles and manages login sessions.
    *   Stores real-time chat history with low latency.

### List of Steps

We will proceed through the following steps:

1.  **[Create Amazon S3 Bucket](5.3.1-Amazon-S3-Bucket/)**: Create a bucket and folder structure, and upload sample data.
2.  **[Create DynamoDB Tables](5.3.2-DynamoDB/)**: Initialize the 3 necessary data tables (Users, ChatSessions, ChatMessages).

{{% notice note %}}
**Important Note:** Please ensure you have selected the **Asia Pacific (Singapore) ap-southeast-1** Region before starting to create any of the resources below.
{{% /notice %}}