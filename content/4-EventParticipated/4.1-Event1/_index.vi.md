---
title: "Vietnam Cloud Day 2025"
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# **Vietnam Cloud Day 2025**
# **Ho Chi Minh City Connect Edition for Builders \- GenAI and Data Track**

**Địa điểm**: AWS Event Hall, L26 Bitexco Tower, HCMC

**Thời gian**: 1PM Thứ Năm, ngày 18 tháng 09 năm 2025

## **Mục Đích Của Sự Kiện**

* Giới thiệu tổng quan về xu hướng **Agentic AI** và tầm nhìn của AWS.  
* Khám phá chiến lược xây dựng nền tảng dữ liệu thống nhất phục vụ AI & Analytics trên AWS.  
* Phân tích lộ trình GenAI, các kiến trúc AI Agent và thách thức khi đưa vào production.  
* Tìm hiểu mô hình **AI-Driven Development Lifecycle (AI-DLC)**.  
* Nắm bắt các nguyên tắc bảo mật, quản trị rủi ro và Responsible AI trong Generative AI.  
* Giới thiệu các dịch vụ AWS mới hỗ trợ AI Agents và nâng cao năng suất doanh nghiệp.

## **Danh Sách Diễn Giả**

* **Jun Kai Loke** – AI/ML Specialist Solutions Architect, AWS  
* **Kien Nguyen** – Solutions Architect, AWS  
* **Tamelly Lim** – Storage Specialist Solutions Architect, AWS  
* **Binh Tran** – Senior Solutions Architect, AWS  
* **Taiki Dang** – Solutions Architect, AWS  
* **Christal Poon** – Specialist Solutions Architect, AWS

## **Nội Dung Nổi Bật**

### **Opening – Agentic AI Overview – Jun Kai Loke**

#### **Agentic AI và xu hướng phát triển**

* Agentic AI là xu hướng chiến lược hàng đầu, hướng đến hệ thống tự vận hành, giảm giám sát của con người, và tự động hóa sâu.  
* Các ví dụ thành công: Katalon, Apero, Techcom Securities.

#### **Amazon Bedrock – Nền tảng phát triển AI**

* Triển khai bảo mật ở quy mô lớn  
* Kết hợp tools và memory  
* Giám sát toàn diện end-to-end

### **Building a Unified Data Foundation on AWS – Kien Nguyen**

#### **Thách thức hiện tại**

* 89% CDOs đang triển khai GenAI nhưng chỉ 52% đánh giá nền tảng dữ liệu đã sẵn sàng (Harvard Business Review).  
* Nguyên nhân: data silos, people silos, business silos.

#### **Chiến lược dữ liệu End-to-End:** 

3 thành phần chính:

* **Producers**  
* **Foundations**  
* **Consumers**

#### **Các thành phần dữ liệu trọng yếu từ AWS**

* **Amazon Bedrock**  
* **Cơ sở dữ liệu** – RDS, database chuyên dụng hỗ trợ vector search  
* **Analytics & ML** – SageMaker, Unified Studio  
* **Data & AI Governance**  
* **Lake House Architecture** – S3, Redshift Managed Storage, Iceberg Open API  
* **Amazon DataZone**

### **GenAI Roadmap & AI Agents Architecture – Jun Kai Loke & Tamelly Lim**

Blueprint xây dựng AI Agents: Model & application capabilities, tool framework.

Amazon Bedrock

Amazon Nova – phát triển và tùy chỉnh mới

Strands Agents – mô hình Agents thế hệ mới

Khó khăn khi đưa Agents vào production

→ AWS giới thiệu Amazon Bedrock AgentCore để giải quyết.

#### **AgentCore gồm các thành phần**

* Agent Core Runtime  
* Agent Core Gateway  
* Memory  
* Agent Browser  
* Code Interpreter

→ Tăng cường bảo mật và khả năng mở rộng.

### **AI-Driven Development Lifecycle (AI-DLC) – Binh Tran**

#### **Hai mô hình phát triển phần mềm hiện tại**

* **AI Managed Pattern** – ít giám sát nhưng kém tin cậy

* **AI Assisted Pattern** – AI hỗ trợ tác vụ nhỏ, vẫn còn hạn chế

#### **AI-DLC – Chu trình phát triển phần mềm mới**

Gồm 3 giai đoạn:

#### **1\. Inception**

* Xây dựng context  
* Phác thảo user stories  
* Lập kế hoạch bằng work units

#### **2\. Construction**

* Code \+ test  
* Bổ sung kiến trúc  
* Triển khai IaC \+ kiểm thử

#### **3\. Operation**

* Deploy production bằng IaC  
* Quản lý sự cố

### **Securing Generative AI Applications – Taiki Dang**

#### **Các yếu tố bảo mật trọng yếu**

* Compliance & Governance  
* Legal & Privacy  
* Controls  
* Risk Management  
* Resilience

#### **Scoping matrix**

* Consumer App  
* Enterprise App  
* Pre-trained models  
* Fine-tuned models  
* Self-trained models

#### **Frameworks & Standards**

* AWS Well-Architected  
* MITRE ATLAS  
* OWASP Top 10 for LLM Apps  
* NIST AI 600-1  
* ISO 42001  
* EU AI Act

#### **Rủi ro theo từng lớp**

* Consumer: IP, Legal, Hallucination, Safety  
* Tuner: managed/hosted, data retention  
* Provider: training data, model construction

#### **Giảm thiểu rủi ro**

* Prompt engineering  
* Fine-tuning  
* RAG  
* Parameter tuning  
* Bedrock Guardrails  
* Bảo mật prompt

### **Beyond Automation: AI Agents as Productivity Multipliers – Christal Poon**

#### **Các dạng dịch vụ AI Agents**

* Specialized Agents  
* Fully-managed Agents  
* DIY Agents

#### **Dịch vụ hỗ trợ năng suất doanh nghiệp**

**Amazon QuickSight**

**Amazon Q**:

* Dashboards  
* Reports  
* Executive summaries  
* AI Agent Scenarios

#### **Sắp ra mắt tại Việt Nam**

**QuickSuite**:

* Quick Researcher  
* Quick Automate  
* Humans in the Loop

## **Những Gì Học Được**

* Hiểu rõ hệ sinh thái Agentic AI & Roadmap của AWS: Agentic AI là thế hệ tiếp theo của automation, hướng tới self-directed systems.  
* Kiến trúc dữ liệu vững chắc là nền tảng GenAI: S3, Iceberg, Redshift, Bedrock, SageMaker giữ vai trò trung tâm.  
* AI-DLC tạo ra phương pháp phát triển phần mềm hiện đại: Tự động hóa từ planning → coding → testing → deployment.  
* Bảo mật là yếu tố xuyên suốt mọi lớp AI stack: Cần tuân thủ chuẩn, bảo vệ dữ liệu, đánh giá rủi ro.  
* AWS đang mở rộng mạnh hệ sinh thái AI Agents & Enterprise AI.

## **Ứng Dụng Vào Công Việc**

* Tích hợp AI Agents vào các tác vụ nghiệp vụ.  
* Dùng Amazon Bedrock, Amazon Q, Guardrails để kiểm soát chất lượng.  
* Xây dựng nền tảng dữ liệu thống nhất trước GenAI.  
* Ứng dụng mô hình AI-DLC vào phát triển nội bộ.  
* Xây dashboard, insight với QuickSight & Amazon Q.

## **Trải Nghiệm Tại Sự Kiện**

Workshop mang lại góc nhìn rõ ràng về chuyển đổi từ automation truyền thống sang **Agentic AI**.  
Các diễn giả chia sẻ sâu sắc, thực tế và định hướng rõ ràng cho hành trình GenAI tại Việt Nam.  
Sự kết hợp của **AgentCore**, **Bedrock**, **AI-DLC** và **Amazon Q** tạo nên bức tranh toàn diện về thế hệ AI dành cho doanh nghiệp.

### **Một số hình ảnh tại sự kiện**
*(Bạn thêm hình tại đây)*
