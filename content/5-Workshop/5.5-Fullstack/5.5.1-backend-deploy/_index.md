---
title : "Deploy Serverless Backend"
weight : 1
chapter : false
pre : " <b> 5.5.1. </b> "
---

In this step, we will configure and deploy the entire Backend (including Lambda, API Gateway, Cognito...) automatically using the Serverless Framework.

#### 1. Configure Serverless File

1.  Open the project source code folder in VS Code.
2.  Navigate to the `backend` directory.
3.  Open the **`serverless.yml`** file.
4.  Locate and modify the following lines (replace `<your-bucket-name>` with the S3 Bucket name you created in section 5.3):

    *   At the `S3_BUCKET_RAW` environment variable line:
        ```yaml
        S3_BUCKET_RAW: contract-app-demo-yourname
        ```
    *   In the `iam` -> `statements` -> `Resource` section (S3 access permissions):
        ```yaml
        Resource:
          - "arn:aws:s3:::contract-app-demo-yourname"
          - "arn:aws:s3:::contract-app-demo-yourname/*"
        ```

![alt text](/images/5-Workshop/5.3-Infrastructure/3.29.png)

![alt text](/images/5-Workshop/5.3-Infrastructure/3.30.png)


#### 2. Configure API Endpoint for Frontend

Before deploying, let's update the API address for the frontend code (even though this file is located in the backend folder, it serves the client).

1.  Access AWS Console -> **Lambda** -> Select the **`ragsearch`** function.
2.  In the **Function overview** -> **Triggers** section, copy the **API Endpoint** URL.
3.  Return to VS Code, open the file at: `backend/src/services/ragService.ts` (or a similar path in your source code).
4.  Find the `RAG_API_URL` declaration line and paste the copied link:

    ```typescript
    const RAG_API_URL = "https://example.execute-api.ap-southeast-1.amazonaws.com";
    ```
5.  Save the file (Ctrl + S).
![alt text](/images/5-Workshop/5.3-Infrastructure/3.31.png)

#### 3. Configure AWS CLI

If you haven't configured it yet or want to be sure, run the following commands in the Terminal (CMD/PowerShell) at the project root directory:

1.  Run the command:
    ```bash
    aws configure
    ```
2.  Enter the information from the Access Key `.csv` file you downloaded:
    *   **AWS Access Key ID**: `<Enter Access Key ID>`
    *   **AWS Secret Access Key**: `<Enter Secret Access Key>`
    *   **Default region name**: `ap-southeast-1`
    *   **Default output format**: (Press Enter to skip)

#### 4. Deploy Backend

1.  Still in the Terminal, navigate into the backend folder:
    ```bash
    cd backend
    ```
2.  Run the deploy command:
    ```bash
    npx serverless deploy
    ```

⏳ **Wait:** This process will take about 3-5 minutes. The Serverless Framework will package the code, create a CloudFormation stack, and push it to AWS.

#### 5. Check Result

If the deployment is successful, the Terminal will display a green message with information about **Service Information**, **endpoints**, and **functions**.

![alt text](/images/5-Workshop/5.3-Infrastructure/3.32.png)

Now, return to the AWS Console, and you will see new resources such as the **Amazon Cognito User Pool** and the new Lambda functions created.