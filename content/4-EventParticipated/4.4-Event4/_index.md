---
title: "AWS Cloud Mastery Series #2"
weight: 4
chapter: false
pre: " <b> 4.4. </b> "
---

### DevOps on AWS
#### Monday, 17/11/2025, from 8:30 – 17:00 – AWS Vietnam Office

### I. General information about the event

* **Event name:** AWS Cloud Mastery Series #2 – DevOps on AWS
* **Time:** Monday, 17/11/2025, from 8:30 to 17:00
* **Venue:** AWS Vietnam Office
* **Participants:** Students, interns, and junior engineers interested in DevOps, AWS infrastructure, and operating systems with an automation-first approach.
* **Main objectives of the session:**

  * Gain a proper understanding of the **DevOps mindset** and the role of DevOps/Platform Engineers within an organization.
  * Understand the **DevOps Services ecosystem on AWS** (CodeCommit, CodeBuild, CodeDeploy, CodePipeline) and how to build a complete CI/CD pipeline.
  * Get familiar with the **Infrastructure as Code (IaC)** mindset through CloudFormation and AWS CDK, and understand why “ClickOps” is no longer appropriate at scale.
  * Understand the different **container service** options on AWS (ECR, ECS, EKS, App Runner) and deployment strategies.
  * Grasp the concepts and tools of **Monitoring & Observability** (CloudWatch, X-Ray, Grafana, Prometheus) to operate systems proactively.

---

### II. Detailed agenda for the day

#### 2.1. Morning session – DevOps Mindset & CI/CD & IaC

**2.1.1. 8:30 – 9:00 | Welcome & DevOps Mindset (Quang Tịnh – Platform Engineer)**

* At the beginning, speaker **Quang Tịnh** briefly revisited the previous AI/ML session and raised the core question: DevOps emerged to address the gap between **Development (Dev)** and **Operations (Ops)** – “DevOps is the bridge between Dev and Ops”, not just a job title but **a mindset and a way of working**.
* The speaker emphasized several characteristics of **DevOps culture**:

  * **Collaboration:** Dev and Ops work as one team, jointly responsible for product quality and operations.
  * **Automation-first:** prioritize automated build, test, and deployment instead of manual operations.
  * **Measurement & Feedback:** always measure and respond based on data, not intuition.
* Regarding **DevOps metrics**, the speaker revisited the common DORA-oriented metrics:

  * **Deployment Frequency** – how often deployments occur.
  * **Lead Time for Changes** – time from commit to production.
  * **MTTR (Mean Time To Recovery)** – average time to recover after an incident.
  * **Change Failure Rate** – percentage of deployments that result in failures.
* At the end of this part, the speaker linked to the role of the **Platform Engineer**: building the platform, tools, and standard processes that enable product teams to deploy, monitor, and operate services consistently with minimal friction.

---

**2.1.2. 9:00 – 10:30 | AWS DevOps Services – CI/CD Pipeline (Kha – CI/CD Workflow)**

* This section focused on the **CI/CD pipeline on AWS**, presented by **Kha**.

* The basic pipeline was described with the following main components:

  1. **Source Control – AWS CodeCommit & Git strategies**

     * **CodeCommit** was introduced as a managed Git service on AWS, equivalent to GitHub/GitLab but with deep integration into the AWS ecosystem.
     * Popular Git strategies were mentioned:

       * **GitFlow:** suitable for workflows with large releases and multiple feature branches.
       * **Trunk-based Development:** frequent commits to main/trunk, optimized for CI/CD and fast deployments.

  2. **Build & Test – AWS CodeBuild**

     * Use **CodeBuild** to build source code and run unit tests and integration tests.
     * The buildspec file defines steps to install dependencies, build, test, and output artifacts.

  3. **Deployment – AWS CodeDeploy**

     * Deployment strategies introduced:

       * **Blue/Green:** run two environments in parallel and switch traffic once the new version is stable.
       * **Canary:** shift traffic in small increments to reduce risk.
       * **Rolling update:** gradually update groups of instances.

  4. **Orchestration – AWS CodePipeline**

     * **CodePipeline** acts as the “backbone” of the pipeline, connecting CodeCommit → CodeBuild → CodeDeploy and additional steps for approvals and automated tests.
     * The overall pipeline model was presented on slides and illustrated via a demo walk-through (from commit to successful deployment).

* The key highlight was **combining the DevOps mindset with the AWS toolchain**: every step from commit to production should be automated and monitored.

---

**2.1.3. 10:45 – 12:00 | Infrastructure as Code (IaC) – Thịnh Nguyễn & Hoàng Anh**

* At the beginning of the session, speakers **Thịnh Nguyễn** and **Hoàng Anh** posed the question:

  > “Why ClickOps isn’t ideal?” – Why should we not manage infrastructure by manually clicking on the console?

* From there, the reasons were listed:

  * **Automation:** you cannot automate when every operation is a manual click.
  * **Scalability:** as systems grow and resources multiply, humans cannot manage everything manually.
  * **Reproducibility:** difficult to recreate identical environments across dev, staging, and production.
  * **Collaboration:** there is no single “source of truth”, making review, audit, and error prevention difficult.

* **AWS CloudFormation**

  * Introduced as the **standard IaC service on AWS**, using templates (YAML/JSON) to define resources.
  * Key concepts:

    * **Template:** a file defining the resources to be created (VPC, EC2, S3, RDS, etc.).
    * **Stack:** one deployment of a template.
    * **Drift detection:** detects differences between actual infrastructure and the template (when someone does “ClickOps” in the console).
  * Advantages: can be version-controlled; supports stack rollback on failure; makes environment replication easier.

* **AWS Cloud Development Kit (CDK – “CloudDevKit”)**

  * Mentioned as a **modern IaC option**, using **programming languages** (TypeScript, Python, Java, etc.) to define infrastructure.
  * CDK generates CloudFormation templates and enables:

    * Reusing **constructs** (packaged infrastructure components).
    * Applying AWS best practices and standard patterns.
  * The “Choosing between IaC tools” section concluded:

    * CloudFormation: suitable when you want to stay close to “native AWS”, simple and easy to control.
    * CDK: suitable for larger projects requiring higher abstraction, heavy reuse, and development teams already comfortable with coding.

---

#### 2.2. Afternoon session – Container Services & Monitoring/Observability

**2.2.1. 13:00 – 14:30 | Container Services on AWS (Trần Vĩ)**

* Speaker **Trần Vĩ** started with basic concepts:

  * **Container**: an application “packaged” with all its dependencies so it can run consistently across different environments.
  * Distinguishing **Container vs Virtual Machine (VM)**: containers share the kernel, are lighter, and start faster; VMs provide stronger isolation but are heavier and consume more resources (detailed comparison was on the slides; not fully captured in notes).

* **Docker & Docker Workflow**

  * **Container engine:** Docker.
  * **Dockerfile:** defines how to build the image and the runtime environment.
  * **Image:** a “blueprint” packaging code and runtime.
  * Basic workflow: write Dockerfile → build image → push to registry → run container.

* **Amazon ECR (Elastic Container Registry)**

  * Introduced as a **fully managed container registry**, private by default.
  * Key features from the notes:

    * **Image scanning**
    * **Immutable tags**
    * **Lifecycle policies**
    * **Encryption & IAM** to control access to images.

* **Amazon ECS (Elastic Container Service)**

  * A container **orchestration** service.
  * Functions: ensures containers automatically restart on failure, scales up/down, distributes traffic across services, and manages containers across multiple servers.
  * Supports two modes:

    * **EC2 mode:** run containers on an EC2 cluster – cost-effective for long-running workloads but requires managing servers.
    * **Fargate mode:** serverless, no infrastructure management, pay only for resources used.
  * Main components: **ECS cluster, task definition, task, service** – architectural diagrams were shown on the slides.

* **Amazon EKS (Elastic Kubernetes Service)**

  * Managed **Kubernetes** service, used when a flexible and complex architecture is required.
  * Components: **Control plane (master), worker node, pod, service**, with diagrams illustrating Kubernetes architecture.
  * ECS vs EKS comparison: ECS is simpler and tightly integrated with AWS; EKS is more flexible and suitable when teams already have Kubernetes experience or require higher portability.

* **AWS App Runner**

  * Notes recorded:

    * “Fast, simple, cost effective”
    * “Directly from source code, no management required”
  * App Runner is suitable when you want to get web/services running as quickly as possible without managing clusters, nodes, etc.

---

**2.2.2. 14:45 – 16:00 | Monitoring & Observability (Nghiêm, Long, Quý)**

* **Concepts of Monitoring & Observability** – by **Nghiêm**

  * **Monitoring:** tracking system metrics, logs, and alerts.
  * **Observability:** the ability to infer the root cause of incidents based on data collected from the system (metrics, logs, traces).
  * Related AWS services:

    * **Amazon CloudWatch**
    * **Amazon Managed Grafana**
    * **AWS X-Ray**
    * **Amazon Managed Service for Prometheus**

* **Amazon CloudWatch**

  * Monitors AWS resources in **real time**, providing metrics and logs for both AWS services and on-premises resources.
  * **Metrics:** performance data of the system; can be default or custom metrics.
  * **Logs:** collects logs from multiple AWS services, stores them, and allows queries for analysis.
  * **Alarms:** configure thresholds to automatically send notifications (SNS, email, etc.) or trigger actions (Auto Scaling, EventBridge).
  * **Dashboards:** visual interfaces combining metrics and logs, supporting operational and cost optimization.

* **AWS X-Ray – by Long**

  * Focuses on **microservices** systems and helps:

    * Analyze **performance bottlenecks**.
    * Perform **distributed tracing**: track requests end-to-end, visualize service maps, and propagate trace IDs across services.
    * Support **root cause analysis** and real user monitoring (RUM) when combined with CloudWatch.

* **Observability Best Practices – by Quý**

  * Detailed content was on the slides; only the headings were noted.
  * Focused on standardizing how to **log, measure metrics, and trace**, setting **reasonable alerts**, avoiding “alert noise”, and integrating with **DevOps/SRE workflows**.

---

**2.2.3. 16:00 – 17:00 | DevOps Best Practices, Career & Q&A**

* The final session of the day mainly summarized:

  * Recap of the standard pipeline: from **DevOps mindset → IaC → CI/CD → Containers → Observability**.
  * Reminder of **DevOps best practices**: safe deployments (feature flags, canary, blue/green), automated testing, and blameless postmortems.
  * Discussion on **DevOps career pathways** and the **AWS Certifications** roadmap (Developer Associate, SysOps, DevOps Engineer Professional, etc.).

---

### III. Knowledge and lessons learned

1. **DevOps is a holistic mindset, not just a set of tools**

   * Emphasizing that DevOps is “the bridge between Dev and Ops” helped me better understand the role of DevOps/Platform Engineers: designing shared platforms for teams, ensuring that code-to-production flows through a standardized, measurable, and automated pipeline.

2. **The importance of CI/CD and a clear Git strategy**

   * Using **CodeCommit + CodeBuild + CodeDeploy + CodePipeline** allows standardization of the build–test–deploy process.
   * Choosing between **GitFlow** and **trunk-based** is not just about branch naming; it directly affects release frequency, hotfix handling, and rollback strategies.

3. **Infrastructure as Code thoroughly addresses ClickOps drawbacks**

   * The reasons “Automation – Scalability – Reproducibility – Collaboration” make me reassess the habit of clicking through the console.
   * **CloudFormation** is suitable when infrastructure needs to be tightly controlled in an AWS-native manner, while **CDK** is appropriate when seeking reuse and code-based organization of infrastructure.

4. **A clearer picture of containers on AWS**

   * From Docker, ECR, ECS, EKS to App Runner, each service fits a different level of complexity:

     * App Runner for “fast deployment with minimal infrastructure management”.
     * ECS (EC2/Fargate) for moderate microservices that are “AWS-native”.
     * EKS when full Kubernetes capabilities are required.

5. **Monitoring & Observability are mandatory, not “nice-to-have”**

   * CloudWatch is not just a log viewer; it is the central hub for metrics, logs, alarms, and dashboards.
   * X-Ray expands observability into the “trace” dimension, providing insight into the journey of each request in a microservices environment.

Overall, the event on 17/11 helped me **connect previously scattered DevOps pieces** into a complete picture on the AWS platform.

---

### IV. Application roadmap for studies and personal projects

1. **Standardize the DevOps workflow for current projects**

   * Apply **trunk-based development** to personal/internship repositories.
   * Set up a sample pipeline with **CodeCommit → CodeBuild → CodeDeploy → CodePipeline**, in which:

     * Unit tests run automatically.
     * Docker images are automatically built and pushed to ECR.

2. **Gradually phase out ClickOps and move to IaC**

   * For current sandbox/lab environments, I will start by describing infrastructure with **CloudFormation** (VPC, EC2, S3, IAM Role).
   * Once familiar, I will move to **AWS CDK** for larger projects and reuse constructs for VPC, clusters, RDS, etc.

3. **Incorporate containers into my learning pipeline and products**

   * Package AI/ML applications and personal web projects into Docker images.
   * Try deploying one service on **ECS Fargate** and another simple service on **App Runner** to compare cost and operational complexity.

4. **Set up minimal Monitoring & Observability for every workload**

   * Enable **CloudWatch metrics & logs** for EC2, Lambda, and ECS tasks.
   * Create at least one basic **dashboard** and **alarm** (CPU, 5xx errors).
   * For critical APIs, integrate **X-Ray** to practice distributed tracing.

5. **Career and certification orientation**

   * Based on the event content, I consider DevOps/Platform Engineer a suitable path to combine infrastructure knowledge and programming skills.
   * In the medium term, I aim to prepare for **AWS Certified Developer – Associate**, and then move towards **AWS DevOps Engineer – Professional** once I have sufficient hands-on experience.

This reflection serves as a foundation for systematizing my knowledge of DevOps on AWS and as a concrete guideline for designing and optimizing systems and personal projects in the upcoming period.

### V. Some photos from the event

![Why does DevOps Role exist?](/images/4-Event/4.5-AWS/1.jpeg)
![DevOps culture elements](/images/4-Event/4.5-AWS/2.jpeg)
![Next-generation DevOps](/images/4-Event/4.5-AWS/3.jpeg)
![4](/images/4-Event/4.5-AWS/4.jpeg)
![Why ClickOps isn't ideal](/images/4-Event/4.5-AWS/5.jpeg)