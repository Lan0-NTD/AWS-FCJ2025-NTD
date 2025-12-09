---
title : "Thiết lập cơ sở hạ tầng"
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

### Giới thiệu

Trong mô-đun này, chúng ta sẽ bắt đầu xây dựng nền móng (Foundation) cho ứng dụng **Smart Contract Assistant**. Trước khi triển khai các đoạn mã xử lý logic (Lambda) hay giao diện người dùng (Frontend), chúng ta cần chuẩn bị nơi để lưu trữ dữ liệu.

Chúng ta sẽ thiết lập hai dịch vụ quan trọng của AWS:

1.  **Amazon S3 (Simple Storage Service):**
    *   Đóng vai trò là "Data Lake".
    *   Nơi chứa các tài liệu hợp đồng mẫu (Templates).
    *   Nơi chứa dữ liệu văn bản luật đã được mã hóa (Embeddings) để phục vụ cho tính năng tìm kiếm thông minh (RAG).

2.  **Amazon DynamoDB:**
    *   Đóng vai trò là Cơ sở dữ liệu NoSQL hiệu năng cao.
    *   Lưu trữ hồ sơ người dùng, quản lý phiên đăng nhập.
    *   Lưu trữ lịch sử chat thời gian thực với độ trễ thấp.

### Danh sách các bước thực hiện

Chúng ta sẽ lần lượt đi qua các nội dung sau:

1.  **[Tạo Amazon S3 Bucket](5.3.1-Amazon-S3-Bucket/)**: Tạo bucket và cấu trúc thư mục, upload dữ liệu mẫu.
2.  **[Tạo bảng DynamoDB](5.3.2-DynamoDB/)**: Khởi tạo 3 bảng dữ liệu cần thiết (Users, ChatSessions, ChatMessages).

{{% notice note %}}
**Lưu ý quan trọng:** Hãy đảm bảo bạn đang chọn Region **Asia Pacific (Singapore) ap-southeast-1** trước khi bắt đầu tạo bất kỳ tài nguyên nào dưới đây.
{{% /notice %}}