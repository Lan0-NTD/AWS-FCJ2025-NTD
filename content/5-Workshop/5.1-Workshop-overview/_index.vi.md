---
title : "Tổng quan"
weight : 1 
chapter : false
pre : " <b> 5.1 </b> "
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

Hệ thống được thiết kế theo kiến trúc **Event-driven Serverless**, giúp tối ưu hóa chi phí (chỉ trả tiền khi sử dụng) và khả năng mở rộng tự động. Chúng ta sẽ áp dụng kỹ thuật **RAG (Retrieval-Augmented Generation)** để cung cấp ngữ cảnh dữ liệu riêng (vector data) cho mô hình AI, giúp câu trả lời chính xác và thực tế hơn.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.53.png)

Các thành phần dịch vụ AWS cốt lõi bao gồm:

1.  **Amazon Bedrock (Generative AI):**
    *   Đóng vai trò là bộ não xử lý ngôn ngữ tự nhiên.
    *   Chúng ta sẽ sử dụng các mô hình nền tảng (Foundation Models) như **Claude 3 (Haiku/Sonnet)** thông qua API để thực hiện việc hiểu câu hỏi, sinh văn bản và xử lý logic pháp lý.

2.  **AWS Lambda & Amazon API Gateway (Backend):**
    *   **AWS Lambda:** Chạy các function Python để xử lý logic nghiệp vụ, như: tìm kiếm vector (search vectors), gọi Bedrock API, và ghép nối dữ liệu.
    *   **Amazon API Gateway:** Tạo các điểm cuối HTTP (RESTful API) an toàn để Frontend có thể giao tiếp với Backend.

3.  **Amazon S3 (Lưu trữ):**
    *   Lưu trữ các file tĩnh như tài liệu hợp đồng mẫu (.docx, .pdf).
    *   Lưu trữ cơ sở dữ liệu vector (embeddings) của các văn bản luật để phục vụ cho tính năng tìm kiếm ngữ nghĩa (Semantic Search).

4.  **Amazon DynamoDB (Cơ sở dữ liệu):**
    *   Lưu trữ thông tin người dùng (Users).
    *   Quản lý các phiên làm việc (Chat Sessions) và lưu lại toàn bộ lịch sử đoạn chat (Chat Messages) với độ trễ thấp nhất.

5.  **AWS Amplify & Amazon Cognito (Frontend & Auth):**
    *   **AWS Amplify:** Tự động hóa việc triển khai (CI/CD) và hosting cho ứng dụng web (React/Vue).
    *   **Amazon Cognito:** Quản lý định danh người dùng, cho phép đăng ký/đăng nhập an toàn và cấp quyền truy cập vào API.

#### Mục tiêu học tập

Sau khi hoàn thành workshop, bạn sẽ đạt được:
*   Hiểu rõ quy trình xây dựng ứng dụng GenAI từ Backend đến Frontend.
*   Kinh nghiệm thực tế khi làm việc với **Amazon Bedrock** và kỹ thuật RAG.
*   Khả năng thiết lập và cấu hình các dịch vụ Serverless: Lambda, DynamoDB, API Gateway.
*   Kỹ năng triển khai ứng dụng web hiện đại với AWS Amplify.

