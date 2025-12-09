---
title : "Deploy Backend Serverless"
weight : 1
chapter : false
pre : " <b> 5.5.1. </b> "
---

Trong bước này, chúng ta sẽ cấu hình và triển khai toàn bộ Backend (bao gồm Lambda, API Gateway, Cognito...) tự động thông qua Serverless Framework.

#### 1. Cấu hình file Serverless

1.  Mở thư mục source code dự án trên VS Code.
2.  Đi vào thư mục `backend`.
3.  Mở file **`serverless.yml`**.
4.  Tìm và chỉnh sửa các dòng sau (thay thế `<your-bucket-name>` bằng tên Bucket S3 bạn đã tạo ở bài 5.3):

    *   Tại dòng biến môi trường `S3_BUCKET_RAW`:
        ```yaml
        S3_BUCKET_RAW: contract-app-demo-tenban
        ```
    *   Tại phần `iam` -> `statements` -> `Resource` (Phân quyền truy cập S3):
        ```yaml
        Resource:
          - "arn:aws:s3:::contract-app-demo-tenban"
          - "arn:aws:s3:::contract-app-demo-tenban/*"
        ```

![alt text](/images/5-Workshop/5.3-Infrastructure/3.29.png)

![alt text](/images/5-Workshop/5.3-Infrastructure/3.30.png)


#### 2. Cấu hình API Endpoint cho Frontend

Trước khi deploy, chúng ta cập nhật luôn địa chỉ API cho code frontend (mặc dù file này nằm trong thư mục backend nhưng nó phục vụ cho client).

1.  Truy cập AWS Console -> **Lambda** -> Chọn hàm **`ragsearch`**.
2.  Trong phần **Function overview** -> **Triggers**, copy đường dẫn **API Endpoint**.
3.  Quay lại VS Code, mở file theo đường dẫn: `backend/src/services/ragService.ts` (hoặc đường dẫn tương tự trong source code của bạn).
4.  Tìm dòng khai báo `RAG_API_URL` và dán link vừa copy vào:

    ```typescript
    const RAG_API_URL = "https://example.execute-api.ap-southeast-1.amazonaws.com";
    ```
5.  Lưu file lại (Ctrl + S).
![alt text](/images/5-Workshop/5.3-Infrastructure/3.31.png)

#### 3. Cấu hình AWS CLI

Nếu bạn chưa cấu hình hoặc muốn đảm bảo chắc chắn, hãy chạy lại các lệnh sau trong Terminal (CMD/PowerShell) tại thư mục gốc của dự án:

1.  Chạy lệnh:
    ```bash
    aws configure
    ```
2.  Nhập thông tin từ file `.csv` Access Key bạn đã tải về:
    *   **AWS Access Key ID**: `<Nhập Access Key ID>`
    *   **AWS Secret Access Key**: `<Nhập Secret Access Key>`
    *   **Default region name**: `ap-southeast-1`
    *   **Default output format**: (Nhấn Enter để bỏ qua)

#### 4. Deploy Backend

1.  Vẫn trong Terminal, di chuyển vào thư mục backend:
    ```bash
    cd backend
    ```
2.  Chạy lệnh deploy:
    ```bash
    npx serverless deploy
    ```

⏳ **Chờ đợi:** Quá trình này sẽ mất khoảng 3-5 phút. Serverless Framework sẽ đóng gói code, tạo CloudFormation stack và đẩy lên AWS.

#### 5. Kiểm tra kết quả

Nếu deploy thành công, Terminal sẽ hiện thông báo màu xanh với các thông tin về **Service Information**, **endpoints**, và **functions**.

![alt text](/images/5-Workshop/5.3-Infrastructure/3.32.png)

Lúc này, quay lại AWS Console, bạn sẽ thấy các tài nguyên mới như **Amazon Cognito User Pool** và các Lambda functions mới đã được tạo ra.