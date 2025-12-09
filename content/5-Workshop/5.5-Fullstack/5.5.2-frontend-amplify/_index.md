---
title : "Deploy Frontend (Amplify)"
weight : 2
chapter : false
pre : " <b> 5.5.2. </b> "
---

#### 1. Prepare GitLab Repository

You need to push the frontend source code to your personal GitLab so Amplify can retrieve the code for building. There are 2 ways to do this:

**Method 1: Create new Repo and Push code (Recommended)**
1.  Log in to your personal GitLab and create a **New project/repository** (blank).
2.  Open Terminal on your computer, navigate to the `frontend` folder:
    ```bash
    cd frontend
    ```
3.  Remove old git configuration (if any):
    *   **Windows (PowerShell)**: `Remove-Item -Recurse -Force .git`
    *   **Mac/Linux**: `rm -rf .git`
4.  Initialize new git and push the code:
    ```bash
    git init
    git add .
    git commit -m "Initial deploy"
    git remote add origin <Your-GitLab-Repo-URL>
    git branch -M main
    git push -uf origin main
    ```

**Method 2: Fork from Sample Repo**
*   Access: [https://gitlab.com/manh-25/contract-demo](https://gitlab.com/manh-25/contract-demo)
*   Click the **Fork** button to copy it to your account.

#### 2. Create App on AWS Amplify
1.  Access the **AWS Amplify** service on the Console.
2.  Scroll to the bottom of the page, select **Create new app**.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.33.png)
3.  On the "Start building with Amplify" screen, select **GitLab** -> Click **Next**.
4.  Connect your GitLab account and select the Repository you just pushed (`main` branch).
![alt text](/images/5-Workshop/5.3-Infrastructure/3.34.png)

#### 3. Configure Build Settings
1.  Enter the **App name**.
2.  In the **Build settings** section, click the **Edit YML file** button.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.35.png)

3.  Delete all default content and **Overwrite (Paste)** the following code (to use `bun` for faster build speed):
```yaml
version: 1
frontend:
  phases:
    preBuild:
      commands:
        - curl -fsSL https://bun.sh/install | bash
        - export BUN_INSTALL="$HOME/.bun"
        - export PATH="$BUN_INSTALL/bin:$PATH"
        - bun install
    build:
      commands:
        - export BUN_INSTALL="$HOME/.bun"
        - export PATH="$BUN_INSTALL/bin:$PATH"
        - bun run build
  artifacts:
    baseDirectory: dist
    files:
      - "**/*"
  cache:
    paths:
      - node_modules/**/*
```

#### 4. Configure Environment Variables
1.  Click on **Advanced settings** -> Scroll down to the **Environment variables** section.
2.  Click **Add new variable** to add the following 4 variables one by one.
3.  **Where to get the Values?** -> Open another browser tab to retrieve the information:

    *   **Go to Amazon Cognito service:** Select the User Pool named `ai-contract-backend-user-pool-dev`.
        *   `VITE_COGNITO_REGION` = `ap-southeast-1`
        *   `VITE_COGNITO_USER_POOL_ID` = Copy **User pool ID**.
        *   `VITE_COGNITO_CLIENT_ID` = Go to the **App integration** tab, scroll to the bottom, and copy the **Client ID**.
  
    ![alt text](/images/5-Workshop/5.3-Infrastructure/3.36.png)

    *   **Go to Lambda service:** Select the function `ai-contract-backend-dev-api`.
        *   `VITE_API_URL` = Copy the **API Endpoint** (in the Configuration -> Triggers or API Gateway section).

    ![alt text](/images/5-Workshop/5.3-Infrastructure/3.37.png) 
    ![alt text](/images/5-Workshop/5.3-Infrastructure/3.38.png)


4.  After filling in all 4 variables, click **Next**.

#### 5. Deploy and Verify
1.  At the Review screen, double-check the information and click **Save and deploy**.
2.  Wait about 3-5 minutes for Amplify to perform the steps: Provision -> Build -> Deploy.
3.  When all 3 steps turn green, the application access link will appear in the **Domain** section (e.g., `https://main.d123...amplifyapp.com`).

👉 **Click the link to experience your Smart Contract Assistant application!**

 ![alt text](/images/5-Workshop/5.3-Infrastructure/3.39.png)