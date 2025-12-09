---
title : "Create DynamoDB Tables"
weight : 2
chapter : false
pre : " <b> 5.3.2. </b> "
---

We need to create 3 tables in Amazon DynamoDB to store user information, chat sessions, and message content.

Access the **DynamoDB** service -> Select **Tables** on the left menu -> Click **Create table**.

#### 1. Create Users Table

This table is used to store logged-in user information.

*   **Table name**: Enter `Users`
*   **Partition key**: Enter `user_id` (Data type: **String**)
![alt text](/images/5-Workshop/5.3-Infrastructure/3.8.png)
*   **Table settings**: Select **Customize settings**.
*   **Table class**: Select **DynamoDB Standard**.
*   **Read/write capacity settings**: Select **On-demand**.
*   Click **Create table**.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.9.png)

#### 2. Create ChatSessions Table

This table stores the list of conversations.

*   Follow the same steps as for the Users table.
*   **Table name**: Enter `ChatSessions`
*   **Partition key**: Enter `session_id` (Data type: **String**)
*   **Table settings**: Select **Customize settings** -> **On-demand**.
*   Click **Create table**.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.10.png)

#### 3. Create ChatMessages Table

This table stores details of individual messages within a conversation.

*   **Table name**: Enter `ChatMessages`
*   **Partition key**: Enter `session_id` (Data type: **String**)
*   **Sort key**: Enter `timestamp` (Data type: **String**)
    *   *Note:* This table requires a Sort key to order messages chronologically.
*   **Table settings**: Select **Customize settings** -> **On-demand**.
*   Click **Create table**.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.11.png)

#### Result

After completion, double-check the Tables list. You should see 3 tables with **Active** status as shown below:
![alt text](/images/5-Workshop/5.3-Infrastructure/3.12.png)