---
title : "Triển khai Fullstack"
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

### Giới thiệu

Chúng ta đã có các thành phần rời rạc: S3, DynamoDB, Lambda Functions. Bây giờ là lúc "lắp ráp" chúng lại thành một ứng dụng hoàn chỉnh.

Trong phần này, chúng ta sẽ thực hiện:

1.  **[Deploy Backend Code](5.5.1-backend-deploy/)**: Sử dụng Serverless Framework để tự động cấu hình các kết nối, tạo User Pool (Cognito) để quản lý đăng nhập và cập nhật code backend.
2.  **[Deploy Frontend (Amplify)](5.5.2-frontend-amplify/)**: Đưa mã nguồn giao diện web lên GitLab, kết nối với AWS Amplify để build và hosting website.

Sau khi hoàn thành phần này, bạn sẽ có một đường link website hoạt động thực tế.