---
title : "Fullstack Deployment"
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

### Introduction

We have the discrete components: S3, DynamoDB, Lambda Functions. Now it is time to "assemble" them into a complete application.

In this section, we will:

1.  **[Deploy Backend Code](5.5.1-backend-deploy/)**: Use the Serverless Framework to automatically configure connections, create a User Pool (Cognito) to manage logins, and update the backend code.
2.  **[Deploy Frontend (Amplify)](5.5.2-frontend-amplify/)**: Push the web interface source code to GitLab and connect to AWS Amplify to build and host the website.

After completing this section, you will have a live, functioning website link.