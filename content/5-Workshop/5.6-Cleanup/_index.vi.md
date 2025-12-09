---
title : "Dọn dẹp tài nguyên"
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

#### 0. Sao lưu dữ liệu (Tùy chọn)

Nếu bạn muốn giữ lại dữ liệu trước khi xóa, hãy thực hiện bước này. Nếu không, hãy bỏ qua và xuống bước 1.

*   **DynamoDB**: Vào từng bảng (`ChatMessages`, `ChatSessions`, `Users`) -> Tab **Explore items** -> Chọn **Scan** -> Chọn tất cả -> **Export to CSV**.
*   **S3**: Vào Bucket -> Chọn tất cả file -> **Actions** -> **Download**.

---

#### 1. Xóa API Gateway

*Tại sao phải xóa trước?* API Gateway đang kết nối với Lambda. Xóa nó trước giúp ngắt các kết nối phụ thuộc.

1.  Truy cập **API Gateway Console**.
2.  Tìm và xóa lần lượt 2 API sau:
    *   `ragsearch-API` (API tạo thủ công).
    *   `dev-ai-contract-backend` (API do Serverless tạo).
![alt text](/images/5-Workshop/5.3-Infrastructure/3.40.png)

3.  Chọn API -> Bấm **Delete** -> Xác nhận xóa.

![alt text](/images/5-Workshop/5.3-Infrastructure/3.41.png)

#### 2. Xóa Lambda Functions

Truy cập **Lambda Console**. Bạn sẽ thấy danh sách khoảng 6 hàm (3 hàm tạo tay và 3 hàm do Serverless tạo).

1.  Tích chọn ô checkbox bên cạnh **tất cả** các hàm sau:
    *   `ragsearch`
    *   `CallLLM`
    *   `generate_contract`
    *   `ai-contract-backend-dev-api`
    *   `ai-contract-backend-dev-postConfirmation`
    *   `ai-contract-backend-dev-custom-resource-existing-cup`
![alt text](/images/5-Workshop/5.3-Infrastructure/3.50.png)

2.  Bấm nút **Actions** -> Chọn **Delete**.
3.  Xác nhận xóa.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.52.png)



#### 3. Xóa Cognito User Pool

1.  Truy cập **Cognito Console** -> **User pools**.
2.  Bấm vào tên pool: `ai-contract-backend-user-pool-dev`.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.42.png)
3.  Bấm **Delete**.
4.  Chọn phương thức xác thực xóa (thường là gõ tên pool) và xác nhận.

#### 4. Xóa DynamoDB Tables

1.  Truy cập **DynamoDB Console** -> **Tables**.
2.  Tích chọn 3 bảng:
    *   `ChatMessages`
    *   `ChatSessions`
    *   `Users`
![alt text](/images/5-Workshop/5.3-Infrastructure/3.43.png)
3.  Bấm **Delete**.
4.  **Lưu ý:** Bỏ tích ô *Create a backup* (để tránh tốn thời gian và chi phí lưu backup) -> Gõ `confirm` để xác nhận xóa.


#### 5. Xóa S3 Buckets

{{% notice note %}}
**Lưu ý:** AWS yêu cầu Bucket phải **Trống (Empty)** thì mới cho phép **Xóa (Delete)**.
{{% /notice %}}

Thực hiện quy trình sau cho **cả 2 bucket** (Bucket chính `contract-app-demo...` và bucket deployment `ai-contract-backend-dev-serverless...`):

1.  **Làm trống Bucket:**
    *   Chọn Bucket -> Bấm **Empty**.
    *   Gõ `permanently delete` để xác nhận -> Bấm **Empty**.
    *   Bấm **Exit** để quay lại.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.44.png)

2.  **Xóa Bucket:**
    *   Khi bucket đã trống, tích chọn Bucket đó -> Bấm **Delete**.
    *   Gõ tên bucket để xác nhận -> Bấm **Delete bucket**.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.45.png)


#### 6. Xóa Secrets Manager

1.  Truy cập **Secrets Manager Console**.
2.  Bấm vào tên secret bạn đã tạo (ví dụ: `JWT_SECRET`...).
![alt text](/images/5-Workshop/5.3-Infrastructure/3.46.png)
3.  Bấm **Actions** -> **Delete secret**.
4.  Đặt thời gian chờ (Waiting period) là tối thiểu (7 ngày) -> Xác nhận xóa.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.47.png)

#### 7. Xóa Amplify App

1.  Truy cập **AWS Amplify**.
2.  Chọn App **SmartContractAssistant** (hoặc tên bạn đã đặt).
![alt text](/images/5-Workshop/5.3-Infrastructure/3.48.png)
3.  Ở menu bên trái, chọn **App settings** -> **General settings**.
4.  Bấm nút **Delete app** ở góc phải -> Xác nhận.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.49.png)


---

### Tổng kết

Xin chúc mừng! Bạn đã hoàn thành workshop và dọn dẹp sạch sẽ tài nguyên.

**Danh sách tài nguyên đã xóa:**
*   ✅ 2 API Gateway
*   ✅ 6 Lambda Functions
*   ✅ 1 Cognito User Pool
*   ✅ 3 DynamoDB Tables
*   ✅ 2 S3 Buckets
*   ✅ 1 Secrets Manager Secret
*   ✅ 1 Amplify App