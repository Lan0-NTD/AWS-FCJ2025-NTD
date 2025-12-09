---
title : "Preparation Steps"
weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---

#### 1. System Requirements and Tools

Before starting, please ensure your computer has the following tools installed:

1.  **AWS Account**: An active AWS account.
2.  **AWS CLI**: Installed and configured ([Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)).
3.  **Node.js & NPM**: To run backend and frontend deployment commands.
4.  **Git**: To download the source code.
5.  **Text Editor**: VS Code (recommended).

#### 2. Download Source Code

Open the terminal on your computer and clone the repository containing the project source code:

```bash
git clone https://gitlab.com/manh-25/contract-demo.git
cd contract-demo
```

#### 3. Region Setup

⚠️ **Important:** Throughout this workshop, please ensure you always select the Region as **Singapore (ap-southeast-1)**.

This is crucial because services like Amazon Bedrock (Claude 3 models) and configurations in the sample code are set up for this Region.

#### 4. Create IAM User and Access Keys

For the application and AWS CLI to interact with AWS, we need to create an IAM User with administrative permissions.

**Step 1: Create User**
1.  Go to **IAM Console** -> Select **Users** -> **Create user**.
2.  **User name**: Enter `contract-app-demo`.
3.  Click **Next**.

![create user](/images/5-Workshop/5.2-Prerequisite/0.png)

**Step 2: Set permissions**
1.  Select **Add user to group**.
2.  Click **Create group**.
3.  **User group name**: Name it `ADMIN`.
4.  In the **Permission policies** list, search for and check `AdministratorAccess`.
5.  Click **Create user group**.
6.  After the group is created, select the `ADMIN` group and click **Next**.
![create group](/images/5-Workshop/5.2-Prerequisite/1.png)
7.  Click **Create user**.
![download key](/images/5-Workshop/5.2-Prerequisite/3.png)

**Step 3: Create Access Key**
1.  Click on the newly created User `contract-app-demo`.
2.  Switch to the **Security credentials** tab.
3.  Scroll down to the **Access keys** section, click **Create access key**.
4.  Select Use case: **Local code**. Check the confirmation box "I understand...". Click **Next**.
![local-code](/images/5-Workshop/5.2-Prerequisite/4.png)
5.  Click **Create access key**.
6.  Click **Done**.
![Create access key](/images/5-Workshop/5.2-Prerequisite/5.png)

⚠️ **Note:** Click **Download .csv file** to save the keys to your computer. You will not be able to view the Secret access key again after leaving this page.

#### 5. Configure AWS CLI

Open the Terminal on your computer and run the following command to connect to your AWS account:

```bash
aws configure
```

Enter the information based on the .csv file you just downloaded:
*   **AWS Access Key ID**: (Get from csv file)
*   **AWS Secret Access Key**: (Get from csv file)
*   **Default region name**: `ap-southeast-1`
*   **Default output format**: `json` (or leave blank)