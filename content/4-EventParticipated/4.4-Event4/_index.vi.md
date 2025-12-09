---
title: "AWS Cloud Mastery Series #2"
weight: 4
chapter: false
pre: " <b> 4.4. </b> "
---

### DevOps on AWS
#### Thứ Hai, ngày 17/11/2025, từ 8:30 – 17:00 – AWS Vietnam Office

### I. Thông tin chung về sự kiện

* **Tên sự kiện:** AWS Cloud Mastery Series #2 – DevOps on AWS
* **Thời gian:** Thứ Hai, ngày 17/11/2025, từ 8h30 đến 17h00
* **Địa điểm:** Văn phòng AWS Việt Nam
* **Đối tượng tham dự:** Sinh viên, thực tập sinh và kỹ sư trẻ quan tâm đến DevOps, hạ tầng trên AWS và vận hành hệ thống theo hướng tự động hóa.
* **Mục tiêu chính của buổi học:**

  * Hiểu đúng về **DevOps mindset** và vai trò của DevOps/Platform Engineer trong tổ chức.
  * Nắm được hệ sinh thái **DevOps Services trên AWS** (CodeCommit, CodeBuild, CodeDeploy, CodePipeline) và cách xây dựng pipeline CI/CD hoàn chỉnh.
  * Làm quen với tư duy **Infrastructure as Code (IaC)** thông qua CloudFormation và AWS CDK, hiểu vì sao “ClickOps” không còn phù hợp ở quy mô lớn.
  * Hiểu các lựa chọn **dịch vụ container** trên AWS (ECR, ECS, EKS, App Runner) và các chiến lược triển khai.
  * Nắm các khái niệm và công cụ **Monitoring & Observability** (CloudWatch, X-Ray, Grafana, Prometheus) để vận hành hệ thống một cách chủ động. 

---

### II. Nội dung chi tiết chương trình trong ngày

#### 2.1. Phiên sáng – DevOps Mindset & CI/CD & IaC

**2.1.1. 8:30 – 9:00 | Welcome & DevOps Mindset (Quang Tịnh – Platform Engineer)**

* Mở đầu, diễn giả **Quang Tịnh** giới thiệu lại tổng quan buổi AI/ML trước đó và đặt vấn đề: DevOps xuất hiện để giải quyết khoảng cách giữa **Development (Dev)** và **Operations (Ops)** – “DevOps là cầu nối giữa Dev và Ops”, không chỉ là một vị trí, mà là **một mindset và một cách làm việc**. 
* Diễn giả nhấn mạnh một số đặc điểm của **DevOps culture**:

  * **Collaboration:** Dev và Ops làm việc như một đội, cùng chịu trách nhiệm về chất lượng và vận hành sản phẩm.
  * **Automation-first:** ưu tiên tự động hóa build, test, deploy thay vì thao tác thủ công.
  * **Measurement & Feedback:** luôn đo lường và phản hồi dựa trên dữ liệu, không dựa trên cảm tính.
* Về **DevOps metrics**, diễn giả gợi lại các nhóm chỉ số thường được dùng theo hướng DORA:

  * **Deployment Frequency** – tần suất triển khai.
  * **Lead Time for Changes** – thời gian từ lúc commit tới khi lên production.
  * **MTTR (Mean Time To Recovery)** – thời gian trung bình để khôi phục sau sự cố.
  * **Change Failure Rate** – tỉ lệ triển khai gây lỗi.
* Cuối phần này, diễn giả liên hệ vai trò **Platform Engineer**: xây dựng nền tảng, công cụ và quy trình chuẩn, giúp các team product có thể triển khai, giám sát và vận hành dịch vụ một cách nhất quán, ít ma sát. 

---

**2.1.2. 9:00 – 10:30 | AWS DevOps Services – CI/CD Pipeline (Kha – CI/CD Workflow)**

* Phần này tập trung vào **CI/CD pipeline trên AWS**, do anh **Kha** trình bày. 

* Pipeline cơ bản được mô tả với các khối chính:

  1. **Source Control – AWS CodeCommit & Git strategies**

     * Giới thiệu **CodeCommit** như một dịch vụ Git managed trên AWS, tương đương GitHub/GitLab nhưng tích hợp sâu với hệ sinh thái AWS.
     * Nhắc đến các chiến lược Git phổ biến:

       * **GitFlow:** phù hợp với quy trình có release lớn, nhiều nhánh feature.
       * **Trunk-based Development:** commit thường xuyên lên main/trunk, tối ưu cho CI/CD và deployment nhanh.

  2. **Build & Test – AWS CodeBuild**

     * Sử dụng **CodeBuild** để build mã nguồn, chạy unit test, integration test.
     * Buildspec file định nghĩa các bước cài dependency, build, test, xuất artifact.

  3. **Deployment – AWS CodeDeploy**

     * Giới thiệu các chiến lược deploy:

       * **Blue/Green:** chạy song song hai môi trường, switch traffic khi bản mới ổn định.
       * **Canary:** chuyển traffic từng phần nhỏ để giảm rủi ro.
       * **Rolling update:** cập nhật dần từng nhóm instance.

  4. **Orchestration – AWS CodePipeline**

     * **CodePipeline** đóng vai trò “xương sống” pipeline, kết nối CodeCommit → CodeBuild → CodeDeploy và các bước approval, test tự động.
     * Mô hình tổng thể của pipeline được trình bày trong slide và được minh họa qua demo walk-through (từ commit đến khi deploy thành công).

* Điểm nhấn ở phiên này là việc **kết hợp DevOps mindset với toolchain AWS**: mọi bước từ commit đến production đều phải được tự động hóa và theo dõi.

---

**2.1.3. 10:45 – 12:00 | Infrastructure as Code (IaC) – Thịnh Nguyễn & Hoàng Anh**

* Mở đầu phiên, hai diễn giả **Thịnh Nguyễn** và **Hoàng Anh** đặt câu hỏi:

  > “Why ClickOps isn’t ideal?” – Tại sao không nên quản lý hạ tầng bằng việc click tay trên console? 

* Từ đó, các lý do được liệt kê:

  * **Automation:** không thể tự động hóa khi mọi thao tác đều click tay.
  * **Scalability:** khi hệ thống lớn, số lượng tài nguyên nhiều, con người không thể quản lý nổi bằng tay.
  * **Reproducibility:** khó tái tạo lại môi trường giống nhau giữa dev, staging, production.
  * **Collaboration:** không có “source of truth”, khó review, khó audit, dễ sai sót.

* **AWS CloudFormation**

  * Được giới thiệu như **dịch vụ IaC chuẩn trên AWS**, dùng template (YAML/JSON) để mô tả tài nguyên. 
  * Các khái niệm chính:

    * **Template:** file định nghĩa tài nguyên cần tạo (VPC, EC2, S3, RDS, v.v.).
    * **Stack:** một lần triển khai template.
    * **Drift detection:** phát hiện sự sai khác giữa thực tế hạ tầng và template (khi ai đó “clickops” trên console).
  * Ưu điểm: có thể version control; rollback stack khi lỗi; dễ nhân bản môi trường.

* **AWS Cloud Development Kit (CDK – “CloudDevKit”)**

  * Được nhắc đến như một lựa chọn **IaC hiện đại**, dùng **ngôn ngữ lập trình** (TypeScript, Python, Java, v.v.) để định nghĩa hạ tầng. 
  * CDK sinh ra CloudFormation template, cho phép:

    * Tái sử dụng **constructs** (thành phần hạ tầng đóng gói).
    * Áp dụng best practices, pattern chuẩn của AWS.
  * Phần “Choosing between IaC tools” kết luận:

    * CloudFormation: phù hợp khi muốn gần “native AWS”, đơn giản, dễ kiểm soát.
    * CDK: phù hợp khi dự án lớn, cần abstraction cao, tái sử dụng nhiều, đội dev đã quen code.

---

#### 2.2. Phiên chiều – Container Services & Monitoring/Observability

**2.2.1. 13:00 – 14:30 | Container Services on AWS (Trần Vĩ)**

* Diễn giả **Trần Vĩ** giới thiệu từ khái niệm cơ bản:

  * **Container**: ứng dụng được “đóng gói” cùng mọi dependency để khi di chuyển giữa các môi trường khác nhau vẫn chạy ổn định.
  * Phân biệt **Container vs Virtual Machine (VM)**: container dùng chung kernel, nhẹ hơn, khởi động nhanh hơn; VM cô lập mạnh hơn nhưng nặng và tốn tài nguyên hơn (phần so sánh chi tiết đã có trong slide, không ghi lại toàn bộ). 

* **Docker & Docker Workflow**

  * **Container engine:** Docker.
  * **Dockerfile:** mô tả cách build image, môi trường runtime.
  * **Image:** “blueprint” đóng gói code + runtime.
  * Workflow cơ bản: viết Dockerfile → build image → push lên registry → run container.

* **Amazon ECR (Elastic Container Registry)**

  * Được giới thiệu là **fully-managed container registry**, mặc định private.
  * Các tính năng chính theo ghi chú:

    * **Image scanning**
    * **Immutable tags**
    * **Lifecycle policies**
    * **Encryption & IAM** để kiểm soát truy cập images. 

* **Amazon ECS (Elastic Container Service)**

  * Dịch vụ **orchestration** cho containers.
  * Chức năng: đảm bảo container tự khởi động lại khi fail, scale up/down, phân phối traffic giữa các service, quản lý containers trên nhiều server.
  * Hỗ trợ 2 mode:

    * **EC2 mode:** chạy containers trên cụm EC2 – chi phí thấp cho workload chạy lâu dài nhưng phải tự quản lý server.
    * **Fargate mode:** serverless, không quản lý hạ tầng, trả tiền theo tài nguyên sử dụng.
  * Thành phần chính: **ECS cluster, task definition, task, service** – sơ đồ kiến trúc được minh họa trong slide. 

* **Amazon EKS (Elastic Kubernetes Service)**

  * Managed service cho **Kubernetes**, dùng khi cần kiến trúc linh hoạt, phức tạp.
  * Thành phần: **Control plane (master), worker node, pod, service**, sơ đồ minh họa kiến trúc Kubernetes.
  * So sánh ECS vs EKS: ECS đơn giản, gắn chặt AWS; EKS linh hoạt, phù hợp khi đã có kinh nghiệm Kubernetes hoặc cần portability cao.

* **AWS App Runner**

  * Được ghi chú là:

    * “Nhanh, đơn giản, cost effective”
    * “Directly from source code, no management required”
  * App Runner phù hợp cho trường hợp muốn đưa code web/service chạy nhanh nhất có thể, không muốn quản lý cluster, node, v.v. 

---

**2.2.2. 14:45 – 16:00 | Monitoring & Observability (Anh Nghiêm, Anh Long, Anh Quý)**

* **Khái niệm Monitoring & Observability** – anh **Nghiêm**

  * **Monitoring:** theo dõi các chỉ số, log, cảnh báo trong hệ thống.
  * **Observability:** khả năng suy luận nguyên nhân sự cố dựa trên các dữ liệu thu thập được từ hệ thống (metrics, logs, traces). 
  * Các dịch vụ AWS liên quan:

    * **Amazon CloudWatch**
    * **Amazon Managed Grafana**
    * **AWS X-Ray**
    * **Amazon Managed Service for Prometheus**

* **Amazon CloudWatch**

  * Monitor tài nguyên AWS **real-time**, cung cấp metrics và logs cho cả dịch vụ AWS và on-premises.
  * **Metrics:** dữ liệu hiệu năng của hệ thống; có thể là default metrics hoặc custom metrics.
  * **Logs:** thu thập log từ nhiều dịch vụ AWS, lưu trữ và cho phép query để phân tích.
  * **Alarms:** thiết lập ngưỡng, tự động gửi thông báo (SNS, email, v.v.) hoặc kích hoạt action (Auto Scaling, EventBridge).
  * **Dashboards:** giao diện trực quan để kết hợp metrics và logs, hỗ trợ tối ưu vận hành và chi phí. 

* **AWS X-Ray – anh Long**

  * Tập trung vào hệ thống **microservices**, giúp:

    * Phân tích **performance bottlenecks**.
    * Thực hiện **distributed tracing**: theo dõi request end-to-end, hiển thị service map, gán trace IDs qua các service.
    * Hỗ trợ **root cause analysis** và real user monitoring (RUM) khi kết hợp với CloudWatch. 

* **Observability Best Practices – anh Quý**

  * Nội dung chi tiết ở slide, trong ghi chú chỉ lưu lại tiêu đề.
  * Tập trung vào việc chuẩn hóa cách **log, metric, trace**, thiết lập **alert hợp lý**, tránh “alert noise” và gắn với **DevOps/SRE workflow**.

---

**2.2.3. 16:00 – 17:00 | DevOps Best Practices, Career & Q&A**

* Phần cuối ngày chủ yếu tổng kết:

  * Ôn lại pipeline chuẩn: từ **DevOps mindset → IaC → CI/CD → Containers → Observability**.
  * Nhắc tới các **DevOps best practices**: deployment an toàn (feature flags, canary, blue/green), tự động hóa test, postmortem không đổ lỗi cá nhân.
  * Thảo luận về **DevOps career pathway** và lộ trình **AWS Certifications** (Developer Associate, SysOps, DevOps Engineer Professional, v.v.).

---

### III. Kiến thức và bài học rút ra

1. **DevOps là một tư duy tổng thể, không chỉ là công cụ**

   * Việc nhấn mạnh DevOps là “cầu nối giữa Dev và Ops” giúp tôi nhìn rõ hơn vai trò DevOps/Platform Engineer: thiết kế nền tảng dùng chung cho các team, đảm bảo từ code tới production đi qua một đường ống chuẩn, có đo lường và tự động hóa.

2. **Tầm quan trọng của CI/CD và Git strategy rõ ràng**

   * Sử dụng **CodeCommit + CodeBuild + CodeDeploy + CodePipeline** cho phép chuẩn hóa quy trình build–test–deploy.
   * Việc chọn **GitFlow** hay **trunk-based** không chỉ là “cách đặt nhánh” mà ảnh hưởng trực tiếp đến tần suất release, cách xử lý hotfix, rollback.

3. **Infrastructure as Code giải quyết triệt để nhược điểm của ClickOps**

   * Các lý do “Automation – Scalability – Reproducibility – Collaboration” khiến tôi đánh giá lại thói quen click trên console.
   * **CloudFormation** thích hợp khi cần kiểm soát hạ tầng sát với AWS, trong khi **CDK** phù hợp khi muốn tái sử dụng và tổ chức hạ tầng bằng code.

4. **Hiểu rõ hơn bức tranh container trên AWS**

   * Từ Docker, ECR, ECS, EKS đến App Runner, mỗi dịch vụ phù hợp với một mức độ phức tạp khác nhau:

     * App Runner cho “chạy nhanh, ít quản lý hạ tầng”.
     * ECS (EC2/Fargate) cho microservices vừa phải, “thuần AWS”.
     * EKS khi cần đầy đủ sức mạnh Kubernetes.

5. **Monitoring & Observability là bắt buộc, không phải “nice-to-have”**

   * CloudWatch không chỉ là nơi xem log mà là trung tâm metrics, logs, alarms, dashboards.
   * X-Ray mở rộng khả năng quan sát sang chiều “trace”, giúp hiểu rõ hành trình của từng request trong hệ thống microservices.

Nhìn chung, sự kiện ngày 17/11 đã giúp tôi **khớp nối các mảnh ghép DevOps rời rạc** thành một bức tranh hoàn chỉnh trên nền tảng AWS.

---

### IV. Định hướng áp dụng vào học tập và dự án cá nhân

1. **Chuẩn hóa workflow DevOps cho các dự án hiện tại**

   * Áp dụng **trunk-based development** cho các repo cá nhân/thực tập.
   * Thiết lập một pipeline mẫu với **CodeCommit → CodeBuild → CodeDeploy → CodePipeline**, trong đó:

     * Tự động chạy unit test.
     * Tự động build image Docker và push lên ECR.

2. **Loại bỏ dần ClickOps, chuyển sang IaC**

   * Với các môi trường sandbox/lab hiện tại, tôi sẽ thử mô tả hạ tầng bằng **CloudFormation** trước (VPC, EC2, S3, IAM Role).
   * Sau khi quen, chuyển sang **AWS CDK** cho những dự án lớn hơn, tái sử dụng construct cho VPC, cluster, RDS, v.v.

3. **Đưa container vào pipeline học tập và sản phẩm**

   * Đóng gói các ứng dụng AI/ML và các dự án web cá nhân vào Docker image.
   * Thử triển khai một service trên **ECS Fargate** và một service đơn giản trên **App Runner** để so sánh chi phí, độ phức tạp vận hành.

4. **Thiết lập Monitoring & Observability tối thiểu cho mọi workload**

   * Bật **CloudWatch metrics & logs** cho EC2, Lambda, ECS task.
   * Tạo ít nhất một **dashboard** và một **alarm** cơ bản (CPU, lỗi 5xx).
   * Đối với các API quan trọng, tích hợp **X-Ray** để tập làm quen với distributed tracing.

5. **Định hướng nghề nghiệp và chứng chỉ**

   * Dựa trên nội dung sự kiện, tôi đánh giá DevOps/Platform Engineer là một hướng đi phù hợp nếu muốn kết hợp kiến thức hạ tầng và lập trình.
   * Trung hạn, tôi đặt mục tiêu chuẩn bị cho **AWS Certified Developer – Associate**, sau đó hướng tới **AWS DevOps Engineer – Professional** khi đã có đủ trải nghiệm thực tế.

Bài thu hoạch này là cơ sở để tôi hệ thống lại kiến thức về DevOps trên AWS, đồng thời làm guideline cụ thể cho việc thiết kế và tối ưu các hệ thống, dự án cá nhân trong giai đoạn tiếp theo.


### V. Một số hình ảnh trong sự kiện

![Why does DevOps Role exist?](/images/4-Event/4.5-AWS/1.jpeg)
![DevOps culture elements](/images/4-Event/4.5-AWS/2.jpeg)
![Next-generation DevOps](/images/4-Event/4.5-AWS/3.jpeg)
![4](/images/4-Event/4.5-AWS/4.jpeg)
![Why ClickOps isn't ideal](/images/4-Event/4.5-AWS/5.jpeg)