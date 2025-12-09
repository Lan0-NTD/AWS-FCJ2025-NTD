---
title : "Tạo bảng DynamoDB"
weight : 2
chapter : false
pre : " <b> 5.3.2. </b> "
---

Chúng ta cần tạo 3 bảng (Tables) trong Amazon DynamoDB để lưu trữ thông tin người dùng, các phiên chat và nội dung tin nhắn.

Truy cập dịch vụ **DynamoDB** -> Chọn **Tables** ở menu trái -> Bấm **Create table**.

#### 1. Tạo bảng Users

Bảng này dùng để lưu thông tin người dùng đăng nhập.

*   **Table name**: Nhập `Users`
*   **Partition key**: Nhập `user_id` (Kiểu dữ liệu: **String**)
![alt text](/images/5-Workshop/5.3-Infrastructure/3.8.png)
*   **Table settings**: Chọn **Customize settings**.
*   **Table class**: Chọn **DynamoDB Standard**.
*   **Read/write capacity settings**: Chọn **On-demand**.
*   Bấm **Create table**.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.9.png)

#### 2. Tạo bảng ChatSessions

Bảng này lưu trữ danh sách các cuộc hội thoại.

*   Thực hiện tương tự như bảng Users.
*   **Table name**: Nhập `ChatSessions`
*   **Partition key**: Nhập `session_id` (Kiểu dữ liệu: **String**)
*   **Table settings**: Chọn **Customize settings** -> **On-demand**.
*   Bấm **Create table**.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.10.png)

#### 3. Tạo bảng ChatMessages

Bảng này lưu chi tiết từng tin nhắn trong cuộc hội thoại.

*   **Table name**: Nhập `ChatMessages`
*   **Partition key**: Nhập `session_id` (Kiểu dữ liệu: **String**)
*   **Sort key**: Nhập `timestamp` (Kiểu dữ liệu: **String**)
    *   *Lưu ý:* Bảng này bắt buộc phải có Sort key để sắp xếp tin nhắn theo thời gian.
*   **Table settings**: Chọn **Customize settings** -> **On-demand**.
*   Bấm **Create table**.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.11.png)

#### Kết quả

Sau khi hoàn thành, hãy kiểm tra lại danh sách Tables. Bạn cần thấy 3 bảng với trạng thái **Active** như hình dưới đây:
![alt text](/images/5-Workshop/5.3-Infrastructure/3.12.png)