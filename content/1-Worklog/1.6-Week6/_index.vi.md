---
title: "Worklog Tuần 6"
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---


### Mục tiêu tuần 6:

* Tìm hiểu về cách hiện đại hóa ứng dụng, làm quen với cách xây dựng ứng dụng Serverless và trải nghiệm các dịch vụ AI trên AWS
* Trao đổi với các thành viên trong nhóm, lên ý tưởng sơ bộ, triển khai các dịch vụ cơ bản phục vụ cho dự án và học thêm các kiến thức liên quan

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Serverless: Lambda tương tác với S3 và DynamoDB                                                                                                                                           | 10/13/2025   | 10/13/2025      | <https://000078.awsstudygroup.com/vi/>    | 
| 3   | - Gọi API thông qua API Gateway                                                                                                                                                             | 10/14/2025   | 10/14/2025      | <https://000079.awsstudygroup.com/vi/>    |
| 4   | - Tìm hiểu về Amazon Cognito                                                                                                                                                                | 10/15/2025   | 10/15/2025      | <https://000081.awsstudygroup.com/vi/>    |
| 5   | - Tìm hiểu cách triển khai ứng dụng trên AWS Serverless Application Model (SAM)                                                                                                             | 10/16/2025   | 10/16/2025      | <https://000080.awsstudygroup.com/vi/>    |
| 6   | - **Thực hành:** <br>&emsp; + Triển khai Frontend <br>&emsp; + Triển khai Lambda Function <br>&emsp; + Cấu hình API Gateway <br>&emsp; + Kiểm tra API với Postman và Frontend               | 10/17/2025   | 10/17/2025      | <https://000078.awsstudygroup.com/vi/> <br> <https://000079.awsstudygroup.com/vi/> <br> <https://000080.awsstudygroup.com/vi/> |


### Kết quả đạt được tuần 6:

* Hiểu được mô hình **Serverless trên AWS** thông qua bài lab Lambda tương tác với **S3** và **DynamoDB**, bao gồm:

  * Cách Lambda đọc/ghi dữ liệu từ S3.
  * Cách Lambda thao tác dữ liệu trong DynamoDB ở mức cơ bản.

* Nắm được vai trò của **Amazon API Gateway** trong kiến trúc serverless:

  * Hiểu luồng request từ client → API Gateway → Lambda.
  * Biết cách cấu hình endpoint để chuyển tiếp request đến Lambda function.

* Tìm hiểu tổng quan về **Amazon Cognito**:

  * Nắm được khái niệm User Pool, Identity Pool.
  * Hiểu mục đích sử dụng Cognito trong việc xác thực và quản lý người dùng cho ứng dụng web/mobile.

* Làm quen với cách triển khai ứng dụng bằng **AWS Serverless Application Model (AWS SAM)**:

  * Hiểu ý nghĩa file template (hạ tầng dưới dạng mã – IaC).
  * Nắm được luồng build, deploy và update ứng dụng serverless qua SAM.

* Hoàn thành bài **thực hành triển khai ứng dụng đầu cuối**, bao gồm:

  * Triển khai **Frontend** kết nối với backend serverless.
  * Triển khai **Lambda Function** xử lý logic phía server.
  * Cấu hình **API Gateway** để kết nối frontend với Lambda.
  * Kiểm tra hoạt động của API thông qua **Postman** và kiểm thử từ giao diện frontend.

* Trao đổi với các thành viên trong nhóm để:

  * Thống nhất ý tưởng sơ bộ cho dự án sử dụng kiến trúc serverless.
  * Xác định và triển khai các dịch vụ AWS cơ bản cần thiết, đồng thời bổ sung thêm kiến thức liên quan phục vụ cho giai đoạn phát triển tiếp theo.



