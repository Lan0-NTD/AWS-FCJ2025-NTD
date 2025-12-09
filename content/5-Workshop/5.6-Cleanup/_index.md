---
title : "Clean Up Resources"
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

#### 0. Backup Data (Optional)

If you want to keep the data before deleting, perform this step. Otherwise, skip to step 1.

*   **DynamoDB**: Go to each table (`ChatMessages`, `ChatSessions`, `Users`) -> **Explore items** tab -> Select **Scan** -> Select all -> **Export to CSV**.
*   **S3**: Go to the Bucket -> Select all files -> **Actions** -> **Download**.

---

#### 1. Delete API Gateway

*Why delete first?* API Gateway is currently connected to Lambda. Deleting it first helps sever dependent connections.

1.  Access the **API Gateway Console**.
2.  Find and delete the following 2 APIs one by one:
    *   `ragsearch-API` (Manually created API).
    *   `dev-ai-contract-backend` (API created by Serverless).
![alt text](/images/5-Workshop/5.3-Infrastructure/3.40.png)

3.  Select the API -> Click **Delete** -> Confirm deletion.

![alt text](/images/5-Workshop/5.3-Infrastructure/3.41.png)

#### 2. Delete Lambda Functions

Access the **Lambda Console**. You will see a list of about 6 functions (3 manually created and 3 created by Serverless).

1.  Check the checkbox next to **all** of the following functions:
    *   `ragsearch`
    *   `CallLLM`
    *   `generate_contract`
    *   `ai-contract-backend-dev-api`
    *   `ai-contract-backend-dev-postConfirmation`
    *   `ai-contract-backend-dev-custom-resource-existing-cup`
![alt text](/images/5-Workshop/5.3-Infrastructure/3.50.png)

2.  Click the **Actions** button -> Select **Delete**.
3.  Confirm deletion.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.52.png)



#### 3. Delete Cognito User Pool

1.  Access **Cognito Console** -> **User pools**.
2.  Click on the pool name: `ai-contract-backend-user-pool-dev`.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.42.png)
3.  Click **Delete**.
4.  Select the deletion verification method (usually typing the pool name) and confirm.

#### 4. Delete DynamoDB Tables

1.  Access **DynamoDB Console** -> **Tables**.
2.  Check the 3 tables:
    *   `ChatMessages`
    *   `ChatSessions`
    *   `Users`
![alt text](/images/5-Workshop/5.3-Infrastructure/3.43.png)
3.  Click **Delete**.
4.  **Note:** Uncheck the *Create a backup* box (to avoid time and backup costs) -> Type `confirm` to confirm deletion.


#### 5. Delete S3 Buckets

{{% notice note %}}
**Note:** AWS requires the Bucket to be **Empty** before allowing it to be **Deleted**.
{{% /notice %}}

Perform the following process for **both buckets** (The main Bucket `contract-app-demo...` and the deployment bucket `ai-contract-backend-dev-serverless...`):

1.  **Empty the Bucket:**
    *   Select the Bucket -> Click **Empty**.
    *   Type `permanently delete` to confirm -> Click **Empty**.
    *   Click **Exit** to return.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.44.png)

2.  **Delete the Bucket:**
    *   Once the bucket is empty, select that Bucket -> Click **Delete**.
    *   Type the bucket name to confirm -> Click **Delete bucket**.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.45.png)


#### 6. Delete Secrets Manager

1.  Access **Secrets Manager Console**.
2.  Click on the secret name you created (e.g., `JWT_SECRET`...).
![alt text](/images/5-Workshop/5.3-Infrastructure/3.46.png)
3.  Click **Actions** -> **Delete secret**.
4.  Set the Waiting period to the minimum (7 days) -> Confirm deletion.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.47.png)

#### 7. Delete Amplify App

1.  Access **AWS Amplify**.
2.  Select the App **SmartContractAssistant** (or the name you assigned).
![alt text](/images/5-Workshop/5.3-Infrastructure/3.48.png)
3.  On the left menu, select **App settings** -> **General settings**.
4.  Click the **Delete app** button on the right corner -> Confirm.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.49.png)


---

### Conclusion

Congratulations! You have completed the workshop and cleaned up your resources.

**List of deleted resources:**
*   ✅ 2 API Gateways
*   ✅ 6 Lambda Functions
*   ✅ 1 Cognito User Pool
*   ✅ 3 DynamoDB Tables
*   ✅ 2 S3 Buckets
*   ✅ 1 Secrets Manager Secret
*   ✅ 1 Amplify App