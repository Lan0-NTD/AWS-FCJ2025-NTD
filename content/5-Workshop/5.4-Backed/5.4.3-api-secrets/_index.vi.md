---
title : "API Gateway & Secrets"
weight : 3
chapter : false
pre : " <b> 5.4.3. </b> "
---

Bước cuối cùng của phần Backend là mở cổng kết nối (API Gateway) và cấu hình bảo mật.

#### 1. Tạo API Gateway Trigger

1.  Mở lại Lambda Function **`ragsearch`**.
2.  Ở phần Function overview, bấm **Add trigger**.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.26.png)

3.  Chọn nguồn: **API Gateway**.
    *   Intent: **Create a new API**.
    *   API type: **HTTP API**.
    *   Security: **IAM**.
4.  Bấm **Add**.

![alt text](/images/5-Workshop/5.3-Infrastructure/3.27.png)

👉 **Quan trọng:** Sau khi tạo xong, hãy copy đường dẫn **API Endpoint** (có dạng `https://...amazonaws.com`) và lưu lại vào Notepad.

#### 2. Tạo Secrets Manager

1.  Tìm kiếm dịch vụ **Secrets Manager** -> Chọn **Store a new secret**.
2.  Secret type: Chọn **Other type of secret**.
3.  **Key/value pairs**:
    *   Key: `JWT_SECRET`
    *   Value: `(Nhập một mật khẩu tự chọn bất kỳ)`
4.  Bấm **Next** -> Đặt tên Secret (tùy ý) -> **Next** -> **Store**.


#### 3. Cập nhật ARN cho Lambda

Các Lambda function cần biết địa chỉ (ARN) của nhau để gọi lẫn nhau.

1.  Mở 3 tab trình duyệt tương ứng với 3 Lambda functions (`ragsearch`, `generate_contract`, `CallLLM`).
2.  Copy **Function ARN** của từng hàm (Nằm ở góc trên bên phải phần Function overview).
3.  Quay lại tab cấu hình **Environment variables** của hàm **`ragsearch`**.
4.  Bấm **Edit** và thêm các biến sau:
    *   `LAMBDA_RETRIEVAL_ARN`: Dán ARN của hàm `ragsearch`.
    *   `LAMBDA_REVIEW_ARN`: Dán ARN của hàm `CallLLM`.
    *   `LAMBDA_GENERATE_ARN`: Dán ARN của hàm `generate_contract`.
5.  Bấm **Save**.

![alt text](/images/5-Workshop/5.3-Infrastructure/3.28.png)

