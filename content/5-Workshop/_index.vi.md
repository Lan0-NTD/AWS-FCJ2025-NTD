---
title : "Workshop"
weight: 5
chapter: false
pre: " <b> 5. </b> "
---
# Xây dựng Trợ lý Hợp đồng Thông minh (Smart Contract Assistant) trên AWS

#### Giới thiệu

Nền tảng AI Contract Intelligence là một dịch vụ web dành cho cá nhân và các nhóm người dùng nhỏ (freelancer, chủ doanh nghiệp nhỏ, nhân sự hành chính/pháp lý) làm việc với hợp đồng hằng ngày nhưng không có chuyên môn pháp lý sâu. Giải pháp sử dụng Amazon Bedrock và kiến trúc AWS serverless hoàn toàn để phân tích hợp đồng, làm nổi bật rủi ro, gợi ý chỉnh sửa điều khoản, và tạo tóm tắt cũng như mẫu hợp đồng mới.

Được xây dựng trên AWS Amplify, Lambda, API Gateway, DynamoDB, S3, Cognito, EventBridge và CloudWatch, nền tảng cung cấp khả năng rà soát hợp đồng bằng AI với độ trễ thấp, chi phí thấp và bảo mật cao, được tối ưu cho người dùng đơn lẻ hoặc các nhóm nhỏ mà không cần tính năng phức tạp như hệ thống doanh nghiệp.

Mục tiêu chính của ứng dụng là hỗ trợ người dùng (như luật sư, nhân viên pháp chế hoặc chủ doanh nghiệp) thực hiện các tác vụ phức tạp như:
*   **Tra cứu thông tin:** Hỏi đáp về các điều khoản luật dựa trên kho dữ liệu văn bản pháp lý có sẵn.
*   **Soạn thảo tự động:** Yêu cầu AI tạo ra các bản nháp hợp đồng dựa trên các template mẫu và thông tin cung cấp.
*   **Phân tích:** Tóm tắt và kiểm tra nội dung hợp đồng.
#### Kiến trúc giải pháp

Giải pháp được xây dựng hoàn toàn trên kiến trúc **Serverless** (Không máy chủ) của AWS, giúp tối ưu hóa chi phí vận hành và khả năng mở rộng. Điểm nhấn của kiến trúc là việc áp dụng kỹ thuật **RAG (Retrieval-Augmented Generation)**, cho phép AI truy xuất thông tin chính xác từ kho dữ liệu riêng của bạn thay vì chỉ dựa vào kiến thức đã được huấn luyện trước.

Các thành phần chính của hệ thống bao gồm:

1.  **AI & LLM (Amazon Bedrock):**
    *   Đây là "trái tim" của ứng dụng. Chúng ta sử dụng Amazon Bedrock để truy cập các mô hình ngôn ngữ lớn (LLM) tiên tiến như Claude 3 (Haiku/Sonnet) thông qua API.
    *   Bedrock chịu trách nhiệm hiểu ngữ cảnh câu hỏi, tổng hợp thông tin từ tài liệu và sinh ra câu trả lời tự nhiên.

2.  **Backend & Computing (AWS Lambda & API Gateway):**
    *   Sử dụng **AWS Lambda** để chạy các đoạn code Python xử lý logic nghiệp vụ (tìm kiếm vector, gọi API Bedrock, xử lý dữ liệu đầu vào) mà không cần quản lý máy chủ.
    *   **Amazon API Gateway** đóng vai trò là cửa ngõ, tiếp nhận các yêu cầu từ phía người dùng (Frontend) và định tuyến chúng đến các hàm Lambda tương ứng.

3.  **Database & Storage (Amazon S3 & DynamoDB):**
    *   **Amazon S3:** Đóng vai trò là kho lưu trữ ("Data Lake") chứa các file hợp đồng mẫu (.docx, .pdf), các file metadata và dữ liệu vector đã được nhúng (embeddings) phục vụ cho việc tìm kiếm ngữ nghĩa.
    *   **Amazon DynamoDB:** Cơ sở dữ liệu NoSQL hiệu năng cao dùng để lưu trữ thông tin người dùng, quản lý phiên làm việc (Sessions) và lịch sử tin nhắn chat, đảm bảo độ trễ thấp nhất khi truy xuất.

4.  **Frontend & Authentication (AWS Amplify & Cognito):**
    *   Giao diện người dùng được xây dựng bằng React/VueJS và được deploy tự động thông qua **AWS Amplify**.
    *   **Amazon Cognito** cung cấp cơ chế đăng ký, đăng nhập và bảo mật, đảm bảo chỉ những người dùng được ủy quyền mới có thể truy cập ứng dụng.

#### Mục tiêu học tập

Sau khi hoàn thành workshop này, bạn sẽ nắm vững:
*   Cách triển khai một ứng dụng **Full-stack** trên AWS từ con số 0.
*   Hiểu và ứng dụng mô hình **RAG** để kết hợp dữ liệu doanh nghiệp với sức mạnh của LLM.
*   Kỹ năng làm việc với **Infrastructure as Code** thông qua Serverless Framework.
*   Cấu hình và tích hợp các dịch vụ AWS cốt lõi: S3, DynamoDB, Lambda, API Gateway và Bedrock.

#### Nội dung thực hành

1. [Tổng quan về workshop](5.1-Workshop-overview/)
2. [Các bước chuẩn bị](5.2-Prerequiste/)
3. [Thiết lập cơ sở hạ tầng (S3, DynamoDB)](5.3-Infrastructure/)
4. [Xây dựng Backend (Lambda, IAM)](5.4-Backend/)
5. [Triển khai Fullstack (Amplify)](5.5-Fullstack/)
6. [Dọn dẹp tài nguyên](5.6-Cleanup/)