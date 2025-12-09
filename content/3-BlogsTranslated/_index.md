---
title: "Translated Blogs"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---



### [Blog 1 - Getting started with healthcare data lakes: Using microservices](3.1-Blog1/)
This blog explains how to build a modern healthcare data lake on AWS using a microservices architecture. It discusses why healthcare organizations need a central data platform to consolidate diverse sources such as electronic health records (EHR), lab systems, imaging, and IoT medical devices. The article shows how microservices—exposed via APIs and deployed on containers or serverless—help decouple ingestion, transformation, analytics, and governance, making the platform easier to scale and evolve. It walks through typical patterns for landing data in Amazon S3, cataloging and transforming it with services like AWS Glue, enforcing security and privacy (for example, encryption, fine-grained access control, logging), and aligning the architecture with regulations such as HIPAA.

---

### [Blog 2 - Streamline access to ISO-rating content changes with Verisk Rating Insights and Amazon Bedrock](3.2-Blog2/)
This blog describes how Verisk enhanced its ISO Electronic Rating Content (ERC) with a generative AI–powered conversational interface using Amazon Bedrock. It starts from customer pain points—manual downloads of full rating packages, slow comparison of releases, and heavy load on the ERC support team—and shows how Verisk built a Retrieval-Augmented Generation (RAG) system. Documents are chunked and embedded with the Amazon Titan embedding model, stored in Amazon OpenSearch Serverless as vector embeddings, and retrieved dynamically based on user queries. Anthropic Claude 3.5 Sonnet on Amazon Bedrock generates responses, while Amazon ElastiCache stores chat history and LlamaIndex orchestrates data sources. The post also covers evaluation loops, guardrails with Amazon Bedrock Guardrails, SME-driven quality metrics, and an analytics pipeline using Amazon S3 and Snowflake. Business results include cutting analysis time from hours or days to minutes, reducing support workload, speeding onboarding, and giving customers more accurate, explainable insights into rating content changes.


---

### [Blog 3 - How Poland’s Post Bank accelerated digital transformation while maintaining regulatory compliance on AWS](3.3-Blog3/)
This blog tells the story of how Poland’s Post Bank modernized its digital banking platforms on AWS while staying compliant with strict financial regulations. Starting with a cautious migration of a noncritical system in 2019, the bank gradually built cloud skills and confidence, then selected its electronic and mobile banking application as the flagship migration project. Using Terraform-based Infrastructure as Code, a hybrid architecture with redundant AWS Direct Connect links to the Europe (Frankfurt) Region, and a mix of 6R migration strategies (rehost, replatform, repurchase, etc.), the bank achieved predictable latency, high availability on Amazon RDS Multi-AZ, and scalable caching with Auto Scaling. The article highlights strong governance based on AWS Organizations, IAM Identity Center, SCPs, AWS Control Tower, and a hub-and-spoke network security model aligned to the AWS Well-Architected Framework and Security Reference Architecture. Measurable outcomes include reducing deployment time from 2 hours to 10 minutes, cutting CPU usage by 40%, shrinking environment provisioning from 30 days to 30 minutes, and lowering employee turnover from 30% to 5%. The bank now plans further migrations and has already deployed an internal AI assistant using Amazon Bedrock and Anthropic Claude 3.5 to search internal knowledge, demonstrating continuous innovation on a secure, compliant cloud foundation.
