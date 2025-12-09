---
title : "Xây dựng Backend (Lambda)"
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

### Giới thiệu

Trong phần này, chúng ta sẽ xây dựng phần lõi xử lý (Backend) cho ứng dụng **Smart Contract Assistant**. Hệ thống sử dụng kiến trúc Serverless với **AWS Lambda** để xử lý các yêu cầu từ người dùng và tương tác với AI (Amazon Bedrock).

### Các thành phần chính

Chúng ta sẽ lần lượt thực hiện các bước sau:

1.  **[Tạo Lambda RAG Search](5.4.1-rag-search/)**: Xây dựng hàm tìm kiếm thông minh, kết nối với dữ liệu vector trong S3.
2.  **[Tạo các Lambda phụ trợ](5.4.2-other-lambdas/)**: Xây dựng hàm tạo hợp đồng (`generate_contract`) và hàm chat tổng quát (`CallLLM`).
3.  **[Cấu hình API & Bảo mật](5.4.3-api-secrets/)**: Thiết lập API Gateway để mở cổng kết nối và Secrets Manager để lưu trữ khóa bí mật.
