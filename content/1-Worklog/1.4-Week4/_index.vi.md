---
title: "Worklog Tuần 4"
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* Học cách chuyển dịch lên AWS liền mạch và tối ưu hệ thống trên AWS 

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Tìm hiểu về dịch vụ AWS VM Import/Export                                                                                             | 09/29/2025   | 09/29/2025      | <https://000014.awsstudygroup.com/vi/>  |
| 3   | - Tìm hiểu về dịch vụ AWS Database Migration Service (DMS) và AWS Schema Conversion Tool (SCT)                    | 09/30/2025   | 09/30/2025      | <https://000043.awsstudygroup.com/vi/> |
| 4   | - Làm quen với AWS Lambda, bật tắt máy chủ tự động va nhắn tin qua Slack | 10/01/2025   | 10/01/2025      | <https://000022.awsstudygroup.com/vi/> |
| 5   | - Tạo bảng theo dõi hệ thống với Amazon Cloudwatch và Grafana                  | 10/02/2025   | 10/02/2025      | <https://000029.awsstudygroup.com/vi/> |
| 6   | - Quản lý tài nguyên theo nhóm bằng Tag và Resource Groups <br> - Quản lý truy cập dịch vụ EC2 bằng Tag thông qua IAM <br> - Quản lý dịch vụ và tự động hóa tác vụ sử dụng AWS System Manager                                                                                 | 10/02/2025   | 10/03/2025      | <https://000027.awsstudygroup.com/vi/> <br> <https://000028.awsstudygroup.com/vi/> <br> <https://000031.awsstudygroup.com/vi/>|


### Kết quả đạt được trong tuần 4:

* Hiểu được mục đích, kiến trúc tổng quan và kịch bản sử dụng của **AWS VM Import/Export** trong việc chuyển đổi máy ảo on-premise hoặc từ môi trường khác lên AWS một cách liền mạch.

* Nắm được quy trình và vai trò của:

  * **AWS Database Migration Service (DMS)** trong việc migrate dữ liệu giữa các hệ quản trị CSDL khác nhau, hạn chế downtime.
  * **AWS Schema Conversion Tool (SCT)** trong việc chuyển đổi schema khi migrate cơ sở dữ liệu không đồng nhất (heterogeneous migration).

* Làm quen với **AWS Lambda** và cơ chế serverless, đồng thời:

  * Thiết lập logic bật/tắt máy chủ tự động (EC2) thông qua Lambda.
  * Tìm hiểu cách tích hợp gửi thông báo qua **Slack** khi thực hiện các tác vụ tự động.

* Biết cách **tạo bảng, dashboard theo dõi hệ thống** với:

  * **Amazon CloudWatch** để thu thập metric, log, và tạo alarm.
  * **Grafana** để trực quan hóa dữ liệu giám sát từ CloudWatch một cách rõ ràng, dễ theo dõi.

* Nắm được cách **quản lý tài nguyên theo nhóm bằng Tag và Resource Groups**, bao gồm:

  * Gán thẻ (tag) có cấu trúc cho tài nguyên để tiện lọc, quản lý và tính chi phí.
  * Tạo và sử dụng **Resource Groups** để làm việc theo nhóm tài nguyên có chung đặc điểm.

* Hiểu cơ chế **quản lý truy cập dịch vụ EC2 bằng Tag thông qua IAM**, từ đó:

  * Xây dựng được chính sách IAM dựa trên điều kiện Tag (tag-based access control).
  * Hạn chế hoặc cấp quyền chi tiết hơn đến từng nhóm tài nguyên.

* Làm quen với **AWS Systems Manager** và vai trò của nó trong:

  * Quản lý cấu hình và trạng thái tài nguyên.
  * Tự động hóa một số tác vụ vận hành (operations) trên hệ thống chạy trên EC2 và môi trường hybrid.