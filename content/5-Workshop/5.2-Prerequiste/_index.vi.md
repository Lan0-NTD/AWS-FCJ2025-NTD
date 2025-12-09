---
title : "Các bước chuẩn bị"
weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---

#### 1. Yêu cầu hệ thống và Công cụ

Trước khi bắt đầu, hãy đảm bảo máy tính của bạn đã được cài đặt các công cụ sau:

1.  **AWS Account**: Một tài khoản AWS đang hoạt động.
2.  **AWS CLI**: Đã cài đặt và cấu hình ([Hướng dẫn cài đặt](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)).
3.  **Node.js & NPM**: Để chạy các lệnh deploy backend và frontend.
4.  **Git**: Để tải source code.
5.  **Text Editor**: VS Code (khuyên dùng).

#### 2. Tải Source Code

Mở terminal trên máy tính của bạn và clone repository chứa mã nguồn của dự án:

```bash
git clone https://gitlab.com/manh-25/contract-demo.git
cd contract-demo
```

#### 3. Thiết lập Region

⚠️ **Quan trọng:** Trong suốt quá trình workshop, hãy đảm bảo bạn luôn chọn Region là **Singapore (ap-southeast-1)**.

Điều này rất quan trọng vì các dịch vụ như Amazon Bedrock (mô hình Claude 3) và các cấu hình trong code mẫu đang được thiết lập cho Region này.

#### 4. Tạo IAM User và Access Keys

Để ứng dụng và AWS CLI có thể tương tác với AWS, chúng ta cần tạo một IAM User có quyền quản trị.

**Bước 1: Tạo User**
1.  Truy cập **IAM Console** -> Chọn **Users** -> **Create user**.
2.  **User name**: Nhập `contract-app-demo`.
3.  Bấm **Next**.

![create user](/images/5-Workshop/5.2-Prerequisite/0.png)


**Bước 2: Cấp quyền (Set permissions)**
1.  Chọn **Add user to group**.
2.  Bấm **Create group**.
3.  **User group name**: Đặt là `ADMIN`.
4.  Trong danh sách **Permission policies**, tìm kiếm và tích chọn `AdministratorAccess`.
5.  Bấm **Create user group**.
6.  Sau khi group được tạo, tích chọn vào group `ADMIN` và bấm **Next**.
![create group](/images/5-Workshop/5.2-Prerequisite/1.png)
7.  Bấm **Create user**.
![download key](/images/5-Workshop/5.2-Prerequisite/3.png)

**Bước 3: Tạo Access Key**
1.  Bấm vào User `contract-app-demo` vừa tạo.
2.  Chuyển sang tab **Security credentials**.
3.  Kéo xuống mục **Access keys**, bấm **Create access key**.
4.  Chọn Use case: **Local code**. Tích vào ô xác nhận "I understand...". Bấm **Next**.
![local-code](/images/5-Workshop/5.2-Prerequisite/4.png)
5.  Bấm **Create access key**.
6.  Bấm **Done**
![Create access key](/images/5-Workshop/5.2-Prerequisite/5.png)



⚠️ **Lưu ý:** Bấm **Download .csv file** để lưu key về máy tính. Bạn sẽ không thể xem lại Secret access key sau khi rời khỏi trang này.

#### 5. Cấu hình AWS CLI

Mở Terminal trên máy tính của bạn và chạy lệnh sau để kết nối với tài khoản AWS:

```bash
aws configure
```

Nhập các thông tin dựa trên file .csv bạn vừa tải về:
*   **AWS Access Key ID**: (Lấy từ file csv)
*   **AWS Secret Access Key**: (Lấy từ file csv)
*   **Default region name**: `ap-southeast-1`
*   **Default output format**: `json` (hoặc để trống)
