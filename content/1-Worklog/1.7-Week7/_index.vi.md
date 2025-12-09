---
title: "Worklog Tuần 7"
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---


### Mục tiêu tuần 7:

*   Tìm hiểu về kiến trúc và các khái niệm cơ bản của Kubernetes.
*   Học cách triển khai và quản lý ứng dụng trên Amazon EKS.
*   Xây dựng một pipeline CI/CD hoàn chỉnh để tự động hóa việc triển khai lên EKS.

### Công việc đã thực hiện trong tuần:
| Day | Task | Start Date | Completion Date | Reference Material |
|---|---|---|---|---|
| 2 | Chỉnh sửa chi tiết kiến trúc.<br>Đọc lab 126:<br>- Cách khởi tạo cluster, worker node & kiến trúc quản lý. <br>- Hiểu các khái niệm cơ bản: Pod, Deployment, DaemonSet, … — cách thức Kubernetes tổ chức container. <br>- Cách deploy micro-services lên EKS. | 20/10/2025 | 21/10/2025 | <https://000126.awsstudygroup.com/vi/> |
| 4 | Họp team dự án:<br>- Thống nhất nguồn dữ liệu và định dạng dữ liệu.<br>- Kiểm tra tính năng, sửa lỗi.<br>- Lên luồng user. | 22/10/2025 | 22/10/2025 | |
| 5 | Hoàn thành lab 62:<br>- Thiết lập Amazon EKS — khởi tạo cluster Kubernetes.<br>- Dùng AWS CodePipeline + AWS CodeBuild + GitHub để tạo pipeline CI/CD: mỗi khi có commit mới, pipeline tự build container, push image, deploy lên EKS.<br>- Cấu hình RBAC để CodeBuild/CodePipeline có quyền deploy lên cluster. | 23/10/2025 | 23/10/2025 | <https://000062.awsstudygroup.com/vi/> |
| 6 | Meeting team báo cáo hằng tuần. | 24/10/2025 | 24/10/2025 | |
| 7 | Chuẩn bị tài liệu ôn tập giữa kì. | 24/10/2025 | 25/10/2025 | |

### Kết quả đạt được trong tuần 7:

*   **Kiến thức chuyên sâu về Kubernetes:** Đã nắm vững các khái niệm cốt lõi của Kubernetes và kiến trúc của Amazon EKS thông qua việc nghiên cứu lý thuyết (Lab 126).
*   **Kỹ năng triển khai CI/CD trên EKS:** Xây dựng thành công một pipeline CI/CD hoàn chỉnh, tự động hóa toàn bộ quy trình từ build, push image đến deploy ứng dụng lên EKS, tích hợp với GitHub, CodePipeline và CodeBuild (Lab 62).
*   **Dự án:** Đã thống nhất được các chi tiết quan trọng về dữ liệu và luồng người dùng, đồng thời tiến hành kiểm thử và sửa lỗi cho các tính năng đã phát triển.
*   **Chuẩn bị cho Ôn tập:** Bắt đầu hệ thống hóa kiến thức và chuẩn bị tài liệu cho kỳ ôn tập giữa kỳ.
