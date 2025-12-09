---
title: "Week 5 Worklog"
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---



### Week 5 Objectives:

* Continue learning how to optimize AWS systems.

### Tasks to be implemented this week:

| Day | Task                                                                                                                | Start Date | Completion Date | Reference Materials                                                                                                                                |
| --- | ------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2   | - Implement a system backup plan using AWS Backup                                                                   | 10/06/2025 | 10/06/2025      | [https://000013.awsstudygroup.com/](https://000013.awsstudygroup.com/)                                                                             |
| 3   | - Deploy an application using Docker <br> - Deploy the application on Amazon Elastic Container Service (Amazon ECS) | 10/07/2025 | 10/07/2025      | [https://000015.awsstudygroup.com/](https://000015.awsstudygroup.com/) <br> [https://000016.awsstudygroup.com/](https://000016.awsstudygroup.com/) |
| 4   | - Deploy the application with AWS CodePipeline <br> - Automate application deployment using AWS CodePipeline        | 10/08/2025 | 10/08/2025      | [https://000017.awsstudygroup.com/](https://000017.awsstudygroup.com/) <br> [https://000023.awsstudygroup.com/](https://000023.awsstudygroup.com/) |
| 5   | - Learn how to configure Single Sign-On (Amazon SSO)                                                                | 10/09/2025 | 10/09/2025      | [https://000012.awsstudygroup.com/](https://000012.awsstudygroup.com/)                                                                             |
| 6   | - Learn about IAM Permission Boundary                                                                               | 10/10/2025 | 10/10/2025      | [https://000030.awsstudygroup.com/](https://000030.awsstudygroup.com/)                                                                             |

### Week 5 Achievements:

* Understood the role and overall architecture of **AWS Backup**, including how to define backup plans, configure backup vaults, and schedule automated backups for resources.

* Understood the workflow of **packaging applications with Docker** at a fundamental level.

* Became familiar with **Amazon ECS** for container deployment:

  * Understood the concepts of **Task Definition**, **Service**, and **Cluster**.
  * Successfully deployed a containerized application to ECS following the documentation.

* Learned the process of **application deployment using AWS CodePipeline**, including:

  * Understanding the main stages: Source – Build – Deploy.
  * Setting up a CI/CD pipeline to automate deployment so that application updates are automatically built and deployed when source code changes.

* Explored the mechanism and benefits of **AWS Single Sign-On (SSO)**:

  * Understood the goal of centralized login management for multiple accounts and applications.
  * Understood user/group authorization flows within the SSO system.

* Understood the concept of **IAM Permission Boundary**:

  * Distinguished between a Permission Boundary and a standard IAM Policy.
  * Learned how Permission Boundaries limit the maximum permissions that a user or role can receive, enabling stronger access control.
