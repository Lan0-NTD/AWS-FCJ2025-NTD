---
title: "AWS Cloud Mastery Series #3"
weight: 5
chapter: false
pre: " <b> 4.5. </b> "
---

### AWS Well-Architected Security Pillar
#### Monday, 29/11/2025, from 8:30 – 17:00 – AWS Vietnam Office

### I. General information about the event

* **Event name:** AWS Well-Architected Security Pillar
* **Time:** 08:30 – 12:00, 29/11/2025 (morning only)
* **Venue:** AWS Vietnam Office
* **Main objectives:**

  * Clarify the role of the **Security Pillar** within the **AWS Well-Architected Framework** and the **Shared Responsibility** model.
  * Systematize the 5 security pillars: **Identity & Access Management, Detection, Infrastructure Protection, Data Protection, Incident Response**.
  * Clarify **best practices** and common “pitfalls” for enterprises, especially in the context of cloud environments in Vietnam.
  * Provide a practical perspective through small demos (IAM policy simulation, detection-as-code, network firewall, IR playbook).

---

### II. Detailed content by timeline

#### 2.1. Opening & Security Foundation (08:30 – 08:50)

The opening session focused on **the overall picture of security on AWS**:

* **Role of the Security Pillar in Well-Architected**

  * Security was presented as a **mandatory foundation**, not a “nice-to-have” add-on at the end. If you design an architecture while ignoring the Security Pillar, the system is highly likely to encounter situations such as:

    * **Security breach** (data leakage, exposure of sensitive information).
    * **System outages** caused by misconfiguration, DDoS attacks, or operational errors.
    * **Data corruption** or data loss due to lack of backup/encryption.
    * **Incidents under high traffic** without appropriate protection and monitoring mechanisms.

* **Core principles:**

  * **Least Privilege:** grant only the exact minimum permissions required.
  * **Zero Trust:** do not implicitly trust any component, even within the VPC.
  * **Defense in Depth:** protect at multiple layers (identity, network, application, data, etc.).

* **Shared Responsibility Model:**

  * AWS is responsible for **“security OF the cloud”** (physical infrastructure, availability zones, hypervisor, etc.).
  * Customers are responsible for **“security IN the cloud”** (IAM, service configuration, source code, data, logging, IR, etc.).

* **Top threats in the Vietnamese cloud environment:**

  * Emphasis on common risks:

    * Exposure/misuse of **long-lived credentials**.
    * Unintentionally public S3 buckets.
    * Workloads unnecessarily exposed to the public Internet.
    * Lack of logging/monitoring leading to late incident detection.

This section established the mindset that **security must be designed from the outset**, based on the 5 pillars and shared responsibility, not treated as a “firefighting” exercise after incidents occur.

---

#### 2.2. Pillar 1 – Identity & Access Management (08:50 – 09:30) – Modern IAM Architecture

This session focused on modernizing IAM towards **multi-account, SSO, centralized governance**:

* **IAM: Users, Roles, Policies – avoiding long-term credentials**

  * Emphasis: do not use long-lived access keys attached to IAM users for workloads; instead use **IAM Roles + temporary credentials**.
  * Apply the **principle of least privilege** in every policy; avoid overusing `"Action": "*"`, `"Resource": "*"`.

* **IAM Identity Center & AWS Organizations**

  * IAM Identity Center was introduced as an **SSO solution** to centrally manage access across multiple accounts and applications.
  * Enabling SSO typically goes together with **AWS Organizations**, so it is necessary to clearly design the **organizational structure + account structure** from the beginning (prod / non-prod / security / logging, etc.).

* **SCPs – Service Control Policies**

  * The speaker compared SCPs to **“prohibition signs”**, whereas IAM policies are the “driver’s license”:

    * IAM policies **grant permissions**.
    * SCPs define the **maximum ceiling** of permissions that can be granted within an account/OU.
  * Principle: SCPs do not grant permissions; they only **filter** what IAM is allowed to grant.

* **Permission Boundaries**

  * Described as an “advanced IAM” tool for handling complex delegation use cases:

    * Allow teams to create IAM roles/users themselves while still being constrained by a “maximum permission boundary”.

* **MFA, Credential Rotation, IAM Access Analyzer**

  * **MFA:** comparison between **TOTP** and **FIDO2**, with a recommendation to enable MFA for the root account and critical identities.
  * **Credential rotation:** use **AWS Secrets Manager** to automatically rotate secrets, avoiding static secrets.
  * **IAM Access Analyzer:** analyzes policies/conditions to detect unintended access (public, cross-account, etc.) and sends alerts when risks are found.

* **Mini Demo: Validate IAM Policy + simulate access**

  * Demo illustrated using tools to **validate IAM policies** and “simulate” what an identity is effectively allowed to do on a resource, helping avoid misconfiguration before going to production.

---

#### 2.3. Pillar 2 – Detection & Continuous Monitoring (09:30 – 09:55)

This section, presented by **Đức Anh, Tuấn Thịnh, Thanh Đạt**, focused on **detection & continuous monitoring**:

* **AWS CloudTrail (Đức Anh)**

  * Described as the “backbone” of detection on AWS:

    * Logs and centrally monitors **all API calls** across all accounts.
    * Provides **multi-layer security visibility**:

      * **Management events** (configuration changes).
      * **Data events** (S3 object access, Lambda invoke, etc.).
      * **Network activity events**.
      * **Organization-wide coverage** when enabled at the organization level.
  * Integrated with **EventBridge** to:

    * Receive real-time events.
    * Automatically send notifications or trigger workflows (Lambda, SNS, SQS, Step Functions).
    * Support the **detection-as-code** concept: detection rules are also managed as code.

* **Amazon GuardDuty (Tuấn Thịnh)**

  * Focused on **threat detection** based on:

    * VPC Flow Logs, CloudTrail, DNS logs, and various other sources.
  * Notes mentioned **Advanced Protection Plans**:

    * Additional protection for S3, EKS, RDS, Lambda, runtime monitoring.
  * GuardDuty can integrate with EventBridge to **automate response** (send notifications, isolate instances, etc.) and also fits the **detection-as-code** model.

* **AWS Security Hub CSPM (Thanh Đạt)**

  * Addresses the challenge: **many services, many accounts, many compliance standards** → difficult to manage manually.
  * Key points:

    * Standardizes outputs into **ASFF** (AWS Security Finding Format).
    * Detects **misconfigurations**, assesses **security posture**.
    * Applies standards such as **AWS Foundational Security Best Practices**, **CIS Foundations Benchmark**.
    * Supports the **detection-as-code** model with centralized control for multi-account, multi-region environments.

---

#### 2.4. Pillar 3 – Infrastructure Protection (10:10 – 10:40) – Network & Workload Security

This section, presented by **Kha**, revolved around **network and workload security**:

* **Common Network Attack Vectors & Use Cases**

  * Analyzed common attack vectors: inbound, outbound, east–west (between VPCs/subnets/workloads).

* **AWS Layered Security & VPC Controls**

  * **Security Groups (SG):**

    * **Stateful:** when inbound is allowed, the corresponding outbound is automatically allowed.
    * No “deny” rules, only allow rules.
    * Supports **security group sharing** (RAM) and **security group referencing** across VPCs/accounts.
  * **Network ACLs (NACLs):**

    * Attached at the **subnet** layer, typically used for coarse-grained policies.
    * Supports both allow and deny rules.
    * Drawback: limited rule count and relatively simple inspection.

* **DNS & Perimeter Protection**

  * **Amazon Route 53:** mentioned in its role as DNS:

    * Private DNS, VPC DNS, Public DNS.
    * Supports **DNS filtering**, centralized rule and reporting management, suitable for both **cloud-only** and **hybrid network** models.

* **AWS Network Firewall**

  * Focus on:

    * **Egress filtering**, **environment segmentation**, **intrusion prevention**.
  * Supports both **stateless** and **stateful rules**, integrates with **Transit Gateway**, multi-VPC endpoints to control traffic across many VPCs.

In addition, the agenda emphasized **AWS WAF + AWS Shield** as the web application and DDoS protection layers, placed at the edge (ALB/CloudFront) in a defense-in-depth model.

---

#### 2.5. Pillar 4 – Data Protection (10:40 – 11:10) – Encryption, Keys & Secrets

This section, presented by **Thịnh Lâm and Việt Nguyễn**, focused on **encryption and key/secret management**:

* **AWS KMS (Key Management Service)**

  * Clarified the concepts of **master key** and **data key**, and how data keys are generated and encrypted by master keys.
  * **Key policy**: only principals explicitly defined in the policy can use the key; even administrators cannot use it if they are not included.
  * Distinguished between **managed keys** and **CMKs (customer-managed keys)**; CMKs can be configured for automatic or manual rotation.

* **Data Classification & Guardrails**

  * Notes mentioned **Amazon Macie** to scan S3 buckets and identify sensitive data (PII, critical documents).
  * Establish **guardrails**: for example, policies that deny access if S3 objects are not encrypted, enforcing encryption for sensitive data.

* **Encryption in Transit**

  * List of services to consider:

    * S3 & DynamoDB at the API level.
    * RDS (SSL), EBS & Nitro (encryption on the wire), ACM (issuing TLS certificates).

* **Secrets Manager & Rotation**

  * Use **Secrets Manager** to store credentials, connection strings, API keys, etc.
  * Supports automatic **rotation**, integrates with KMS to encrypt secrets.

---

#### 2.6. Pillar 5 – Incident Response (11:10 – 11:40) – IR Playbook & Automation

This section, shared by **Long and Tịnh Trương**, focused on **incident response (IR) processes**:

* **Context:**

  * Modern environments (multi-account, many services, hybrid) are too complex to “firefight manually”.
  * Types of incidents: security breaches, system outages, data corruption, high traffic, etc., require structured processes and a high degree of automation.

* **Security Responsibilities are Shared**

  * Revisited the **Shared Responsibility Model** and listed key foundational services that should be enabled for security:

    * AWS Organizations + SCP
    * CloudTrail
    * AWS Config
    * GuardDuty
    * Security Hub

* **Prevention Guidelines (prevention over cure)**

  * **Kill long-lived credentials** – eliminate long-term access keys.
  * **Never expose S3** – do not public S3 unless truly necessary and strictly controlled.
  * **No facing internet** for workloads that do not need public access.
  * **Everything through IaC** – all infrastructure changes should go through code.
  * **Double gate high-risk changes** – add extra approval layers for high-risk changes.

* **Incident Response Process (according to AWS)**

  * The standard IR process includes:

    1. **Prepare** – build playbooks, assign roles, prepare tools in advance.
    2. **Detection & Analysis** – detect via GuardDuty/Security Hub/CloudTrail, analyze impact.
    3. **Containment** – isolate the source of the incident (isolate instance, revoke keys, etc.).
    4. **Eradication & Recovery** – remove the root cause, restore systems from snapshots/backups.
    5. **Post-incident** – review, extract lessons learned, update playbooks.

* **Specific playbooks mentioned in the agenda:**

  * **Compromised IAM key.**
  * **S3 public exposure.**
  * **EC2 malware detection.**
  * Common steps include: snapshotting, isolation, evidence collection, and automation using **Lambda/Step Functions** for recurring scenarios.

---

#### 2.7. Wrap-Up & Q&A (11:40 – 12:00)

The wrap-up emphasized:

* The **5 Security Pillars** must be seen as a cohesive framework, not separate elements.
* **Common pitfalls** of Vietnamese enterprises:

  * Lack of standardized IAM (frequent use of root, long-lived credentials).
  * Not enabling CloudTrail/GuardDuty/Security Hub comprehensively.
  * Unintentionally public S3 or endpoints without guardrails.
* Suggested **learning roadmap**: AWS Certified Security – Specialty, then advanced Security topics within the Solutions Architect Professional track.

---

### III. Knowledge and lessons learned

1. **Security must be architected from day one, not patched after incidents**

   * The continuous reference to the Security Pillar in the Well-Architected Framework reinforced the idea that if the architecture does not enforce IAM, logging, network segmentation, encryption, etc. from the beginning, the cost of remediation later will be very high.

2. **Modern IAM = multi-account, SSO, SCP, permission boundaries, rotation, MFA**

   * IAM is not just “creating users and attaching policies”; it is a multi-layer architecture: Organizations, IAM Identity Center, SCPs, permission boundaries, Access Analyzer, etc., combined to deliver both flexibility and security.

3. **Detection-as-Code is essential in complex cloud environments**

   * Instead of manually inspecting logs, all detection rules (CloudTrail, GuardDuty, Security Hub) should be described as code, versioned, and deployed via pipelines – similar to how we manage IaC.

4. **Infrastructure security is not just “closing ports” but designing the network correctly**

   * Clearly distinguishing the roles of SGs vs NACLs, and the roles of Route 53, Network Firewall, etc., shows that security must be tightly coupled with multi-layer network architecture.

5. **Data Protection and IR are the final links but critically important**

   * It is not enough to encrypt data (KMS, encryption in transit); we must also classify data (Macie), enforce guardrails that deny non-encrypted resources, and manage secrets properly.
   * Without pre-prepared IR playbooks, teams will become “overwhelmed” when real incidents occur.

---

### IV. Application roadmap for studies and personal projects

1. **Standardize IAM & multi-account for lab/personal project environments**

   * Apply a minimal model of **AWS Organizations + IAM Identity Center + SCP**, avoiding putting everything into a single account.
   * Gradually remove long-lived credentials, replace them with roles + temporary credentials, and enable MFA for critical accounts.

2. **Establish a detection foundation for every workload**

   * Enable **CloudTrail at the org level**, activate **GuardDuty** and **Security Hub** across all personal lab accounts, at least at a baseline level.
   * Experiment with some **detection-as-code** rules (for example: S3 public access, security groups open to 0.0.0.0/0, credentials not rotated, etc.).

3. **Redesign VPC/network towards defense-in-depth**

   * Split VPCs into clear public/private subnets; minimize workloads directly exposed to the Internet.
   * Use security groups with meaningful semantics (by service role), NACLs at the subnet level, and consider experimenting with Network Firewall/Route 53 DNS filtering in advanced labs.

4. **Apply Data Protection & IR to projects with sensitive data**

   * For projects involving contracts and user data, plan to use **KMS, S3 encryption, RDS encryption**, Secrets Manager, and Macie.
   * Build a **simple IR playbook** for lab environments:

     * Scenario where an access key is exposed.
     * Scenario where an S3 bucket becomes public.
   * Experiment with Lambda/Step Functions to automatically isolate resources or revoke credentials in certain simulated scenarios.

5. **Plan to pursue Security Specialty**

   * The event reaffirmed that this is an area in which I need to invest seriously if I want to build AI/ML systems and enterprise applications on AWS in a secure and sustainable way. In my roadmap, I intend to:

     * Further consolidate knowledge of the Well-Architected Security Pillar and AWS SRA (Security Reference Architecture).
     * Then aim for **AWS Certified Security – Specialty** as a medium-term goal.

This reflection helps me synthesize the entire content of the 29/11 session according to the 5 Security Pillar components and clearly shape how to apply them to real-world systems that I am building or will build on AWS.

### V. Some photos from the event

![1](/images/4-Event/4.6-AWS/1.jpeg)
![2](/images/4-Event/4.6-AWS/2.jpeg)
![3](/images/4-Event/4.6-AWS/3.jpeg)
![4](/images/4-Event/4.6-AWS/4.jpeg)
![5](/images/4-Event/4.6-AWS/5.jpeg)
