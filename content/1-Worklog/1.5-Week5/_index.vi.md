---
title: "Worklog Tuần 5"
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---


### Mục tiêu tuần 5:

* Tiếp tục học cách tối ưu hóa hệ thống AWS 

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Triển khai kế hoạch sao lưu hệ thống với AWS Backup                                                                                            | 10/06/2025   | 10/06/2025      | <https://000013.awsstudygroup.com/vi/> |
| 3   | - Triển khai ứng dụng với Docker <br> - Triển khai ứng dụng lên Amazon Elastic Container Service (Amazon ECS)                                     | 10/07/2025   | 10/07/2025      | <https://000015.awsstudygroup.com/vi/> <br> <https://000016.awsstudygroup.com/vi/> |
| 4   | - Triển khai ứng dụng với AWS CodePipeline <br> - Tự động hóa triển khai ứng dụng với AWS CodePipeline | 10/08/2025   | 10/08/2025      | <https://000017.awsstudygroup.com/vi/> <br> <https://000023.awsstudygroup.com/vi/> |
| 5   | - Tìm hiểu về cách thiết lập Single Sign-On (Amazon SSO)          | 10/09/2025   | 10/09/2025      | <https://000012.awsstudygroup.com/vi/> |
| 6   | - Tìm hiểu về IAM Permission Boudary                                                                                      | 10/10/2025   | 10/10/2025      | <https://000030.awsstudygroup.com/vi/> |


### Kết quả đạt được trong tuần 5:

* Hiểu được vai trò và kiến trúc tổng quan của **AWS Backup**, bao gồm cách định nghĩa backup plan, cấu hình backup vault và thiết lập lịch sao lưu tự động cho tài nguyên.

* Nắm được quy trình **đóng gói ứng dụng với Docker** cơ bản

* Làm quen với **Amazon ECS** trong việc triển khai container:

  * Hiểu khái niệm **Task Definition**, **Service**, **Cluster**.
  * Triển khai ứng dụng container hóa lên ECS theo tài liệu hướng dẫn.

* Nắm được quy trình **triển khai ứng dụng với AWS CodePipeline**, bao gồm:

  * Hiểu các stage chính: Source – Build – Deploy.
  * Thiết lập pipeline tự động hoá quy trình triển khai (CI/CD) để khi cập nhật mã nguồn thì ứng dụng được build và deploy tự động.

* Tìm hiểu cơ chế và lợi ích của **AWS Single Sign-On (SSO)**:

  * Nắm được mục tiêu tập trung quản lý đăng nhập cho nhiều tài khoản và ứng dụng.
  * Hiểu luồng đăng nhập và phân quyền người dùng/nhóm.

* Hiểu khái niệm **IAM Permission Boundary**:

  * Phân biệt giữa Permission Boundary và Policy thông thường.
  * Nắm được cách sử dụng Permission Boundary để giới hạn quyền tối đa mà user/role có thể được cấp, hỗ trợ kiểm soát truy cập chặt chẽ hơn.