---
title : "Create Amazon S3 Bucket"
weight : 1
chapter : false
pre : " <b> 5.3.1. </b> "
---

In this step, we will create an S3 Bucket to store contract templates and the necessary vector data for the AI.

#### 1. Create Bucket

1.  Access the **S3** service on the AWS Console.
2.  Select the orange **Create bucket** button.
3.  **General configuration**:
    *   **Bucket type**: Select General purpose.
    *   **Bucket name**: Enter a globally unique name (e.g., `contract-app-demo`).
    *   *Note: Bucket names can only contain lowercase letters, numbers, and hyphens; do not use uppercase letters.*
4.  Scroll to the bottom, keeping other settings as default.
5.  Click **Create bucket**.

![alt text](/images/5-Workshop/5.3-Infrastructure/3.1.png)
![alt text](/images/5-Workshop/5.3-Infrastructure/3.2.png)


#### 2. Create Folder Structure

Once created, we need to create a folder structure to organize the data.

1.  Click on the **Bucket** name you just created to access it.
2.  Click the **Create folder** button.
3.  Create **4 folders** one by one with the exact names below (you need to repeat the folder creation process 4 times):
    *   `contract-templates`
    *   `index`
    *   `legal-corpus`
    *   `user-data`

After creating them, your bucket structure will look like this:

![alt text](/images/5-Workshop/5.3-Infrastructure/3.3.png)

#### 3. Upload Sample Data

Use the files in the `contract-demo` source code folder that you downloaded to your computer in the Preparation section:

1.  Access the `contract-templates` folder on S3 -> Click **Upload** -> Select sample contract files (.docx/.pdf) from your computer -> Click **Upload**.
2.  Access the `index` folder on S3 -> Click **Upload** -> Select the `template_metadata.jsonl` file.
3.  Access the `legal-corpus` folder on S3 -> Click **Upload** -> Select legal data files (if available in the source code).

![alt text](/images/5-Workshop/5.3-Infrastructure/3.4.png)


Use the files in the `contract-demo` source code folder that you downloaded to your computer in the Preparation section. Perform the upload according to the following structure:

1.  Access the `index` folder on S3 -> Click **Upload** -> Select the `template_metadata.jsonl` file -> Click **Upload**.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.5.png)
2.  Access the `legal-corpus` folder on S3. Here, create 2 additional subfolders named `index` and `raw-documents`.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.6.png)
    *   Access the `index` subfolder -> Click **Upload** -> Select the `legal_chunks_with_emb.jsonl` (or `legal_metadata.json`) file.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.7.png)
    *   Access the `raw-documents` subfolder -> Click **Upload** -> Select the raw legal document files (if available).