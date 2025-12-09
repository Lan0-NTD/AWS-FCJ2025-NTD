---
title: "AWS Cloud Mastery Series #3"
weight: 5
chapter: false
pre: " <b> 4.5. </b> "
---

### AWS Well-Architected Security Pillar
#### Thứ Hai, 29/11/2025, từ 8:30 – 17:00 – AWS Vietnam Office

### I. Thông tin chung về sự kiện

* **Tên sự kiện:** AWS Well-Architected Security Pillar
* **Thời gian:** 08:30 – 12:00, ngày 29/11/2025 (morning only)
* **Địa điểm:** AWS Vietnam Office
* **Mục tiêu chính:**

  * Làm rõ vai trò của **Security Pillar** trong khung **AWS Well-Architected Framework** và mô hình **Shared Responsibility**. 
  * Hệ thống hoá 5 trụ cột bảo mật: **Identity & Access Management, Detection, Infrastructure Protection, Data Protection, Incident Response**. 
  * Làm rõ các **best practices** và “bẫy thường gặp” của doanh nghiệp, đặc biệt trong bối cảnh môi trường cloud tại Việt Nam.
  * Cung cấp góc nhìn thực tế qua các demo nhỏ (IAM policy simulation, detection-as-code, network firewall, IR playbook).

---

### II. Nội dung chi tiết theo dòng thời gian

#### 2.1. Opening & Security Foundation (08:30 – 08:50)

Phần mở đầu tập trung vào **bức tranh tổng thể về bảo mật trên AWS**:

* **Vai trò Security Pillar trong Well-Architected**

  * Security được trình bày như **nền tảng bắt buộc**, không phải “tùy chọn” sau cùng. Nếu xây dựng kiến trúc mà bỏ qua Security Pillar, hệ thống rất dễ rơi vào các tình huống:

    * **Security breach** (rò rỉ dữ liệu, lộ thông tin nhạy cảm).
    * **System outages** do cấu hình sai, tấn công DDoS hoặc lỗi vận hành.
    * **Data corruption** hoặc mất dữ liệu do thiếu backup / encryption.
    * **Sự cố do lưu lượng cao** mà không có cơ chế bảo vệ và giám sát phù hợp. 

* **Nguyên tắc cốt lõi:**

  * **Least Privilege:** chỉ cấp đúng và đủ quyền cần thiết.
  * **Zero Trust:** không mặc định tin tưởng bất kỳ thành phần nào, kể cả trong nội bộ VPC.
  * **Defense in Depth:** bảo vệ nhiều lớp (identity, network, application, data…).

* **Shared Responsibility Model:**

  * AWS chịu trách nhiệm **“security OF the cloud”** (hạ tầng vật lý, vùng sẵn sàng, hypervisor…).
  * Khách hàng chịu trách nhiệm **“security IN the cloud”** (IAM, cấu hình dịch vụ, mã nguồn, dữ liệu, logging, IR…). 

* **Top threats trong môi trường cloud Việt Nam:**

  * Nhấn mạnh các rủi ro phổ biến:

    * Lộ/lạm dụng **long-lived credentials**. 
    * S3 bucket public ngoài ý muốn. 
    * Workload đặt Public Internet không cần thiết.
    * Thiếu logging/giám sát dẫn tới phát hiện muộn sự cố.

Phần này tạo nền tảng tư duy: **an ninh phải được thiết kế ngay từ đầu**, dựa trên 5 pillars và shared responsibility, không phải giải quyết “chữa cháy” khi đã có sự cố.

---

#### 2.2. Pillar 1 – Identity & Access Management (08:50 – 09:30) – Modern IAM Architecture

Phiên này tập trung vào hiện đại hóa IAM theo hướng **multi-account, SSO, quản trị tập trung**: 

* **IAM: Users, Roles, Policies – tránh long-term credentials**

  * Nhấn mạnh: không dùng access key dài hạn gắn với IAM user cho workload; thay bằng **IAM Role + temporary credentials**.
  * Áp dụng **principle of least privilege** trong mọi policy; tránh lạm dụng `"Action": "*"`, `"Resource": "*"`.

* **IAM Identity Center & AWS Organizations**

  * IAM Identity Center được giới thiệu là giải pháp **SSO** để quản lý truy cập cho nhiều tài khoản, nhiều ứng dụng cùng lúc. 
  * Khi bật SSO thường sẽ đi cùng với **AWS Organizations**, do đó cần thiết kế **organizational structure + account structure** rõ ràng từ đầu (prod / non-prod / security / logging…).

* **SCPs – Service Control Policies**

  * Được diễn giả ví như **“biển cấm”**, trong khi IAM policy là “bằng lái”:

    * IAM policy **cấp quyền**.
    * SCP **giới hạn trần tối đa** quyền có thể được cấp trong một account/OU. 
  * Nguyên tắc: SCP không cấp quyền, chỉ **filter** những gì IAM có thể cấp.

* **Permission Boundaries**

  * Được mô tả như công cụ “advanced IAM” để giải quyết bài toán phân quyền phức tạp:

    * Cho phép team tự tạo IAM role/user nhưng vẫn bị giới hạn bởi một “khung quyền tối đa” (boundary). 

* **MFA, Credential Rotation, IAM Access Analyzer**

  * **MFA:** so sánh **TOTP** và **FIDO2**, khuyến nghị dùng MFA cho root và tài khoản quan trọng. 
  * **Credential rotation:** sử dụng **AWS Secrets Manager** để xoay vòng secret tự động, tránh dùng secret cố định. 
  * **IAM Access Analyzer:** phân tích policy/condition để phát hiện quyền truy cập ngoài ý muốn (public, cross-account…), gửi cảnh báo khi phát hiện rủi ro. 

* **Mini Demo: Validate IAM Policy + simulate access**

  * Demo minh họa việc dùng công cụ để **validate IAM policy** và “simulate” xem một identity có thực sự được phép làm gì trên một resource, giúp tránh cấu hình sai trước khi đưa lên production.

---

#### 2.3. Pillar 2 – Detection & Continuous Monitoring (09:30 – 09:55)

Phần này do **Đức Anh, Tuấn Thịnh, Thanh Đạt** trình bày, tập trung vào **phát hiện & giám sát liên tục**: 

* **AWS CloudTrail (Đức Anh)**

  * Được mô tả là “xương sống” của detection trên AWS:

    * Ghi log và giám sát tập trung **mọi API call** trên tất cả tài khoản. 
    * Cung cấp **multi-layer security visibility**:

      * **Management events** (thay đổi cấu hình).
      * **Data events** (truy cập object S3, lambda invoke…).
      * **Network activity events**.
      * **Organization coverage** khi bật ở cấp tổ chức.
  * Tích hợp với **EventBridge** để:

    * Nhận real-time events.
    * Tự động thông báo hoặc kích hoạt workflow (Lambda, SNS, SQS, Step Functions).
    * Hỗ trợ khái niệm **detection-as-code**: rule detection cũng được quản lý như code. 

* **Amazon GuardDuty (Tuấn Thịnh)**

  * Tập trung vào **threat detection** dựa trên:

    * VPC Flow Logs, CloudTrail, DNS logs và nhiều nguồn khác. 
  * Ghi chú của anh có nêu các **Advanced Protection Plans**:

    * Bảo vệ thêm cho S3, EKS, RDS, Lambda, runtime monitoring. 
  * GuardDuty có thể tích hợp EventBridge để **tự động hoá phản ứng** (gửi thông báo, cô lập instance…) và cũng phù hợp mô hình **detection-as-code**. 

* **AWS Security Hub CSPM (Thanh Đạt)**

  * Giải quyết bài toán: **nhiều dịch vụ, nhiều tài khoản, nhiều tiêu chuẩn compliance** → khó quản lý thủ công. 
  * Các điểm chính:

    * Chuẩn hoá đầu ra thành **ASFF** (AWS Security Finding Format).
    * Phát hiện **cấu hình sai** (misconfiguration), đánh giá **security posture**.
    * Áp dụng chuẩn **AWS Foundational Security Best Practices**, **CIS Foundations Benchmark**. 
    * Hỗ trợ mô hình **detection-as-code**, kiểm soát tập trung multi-account, multi-region.

---

#### 2.4. Pillar 3 – Infrastructure Protection (10:10 – 10:40) – Network & Workload Security

Phần này do **anh Kha** trình bày, xoay quanh **bảo mật mạng và workload**: 

* **Common Network Attack Vectors & Use Cases**

  * Phân tích các hướng tấn công thường gặp: inbound, outbound, east–west (giữa các VPC/ subnet/ workload). 

* **AWS Layered Security & VPC Controls**

  * **Security Groups (SG):**

    * **Stateful:** cho phép chiều vào thì chiều ra tương ứng được tự động cho phép.
    * Không có rule “deny”, chỉ allow.
    * Hỗ trợ **security group sharing** (RAM) và **security group referencing** giữa các VPC/tài khoản. 
  * **Network ACLs (NACLs):**

    * Gắn ở lớp **subnet**, thường dùng cho chính sách coarse-grained.
    * Hỗ trợ cả allow và deny.
    * Nhược điểm: giới hạn số lượng rule, độ sâu kiểm tra đơn giản hơn. 

* **DNS & Perimeter Protection**

  * **Amazon Route 53:** được nhắc đến với vai trò DNS:

    * Private DNS, VPC DNS, Public DNS.
    * Hỗ trợ **DNS filter**, quản lý rule và reporting tập trung, dùng cho mô hình **cloud-only** hoặc **hybrid network**. 

* **AWS Network Firewall**

  * Tập trung vào:

    * **Egress filtering**, **environment segmentation**, **intrusion prevention**. 
  * Hỗ trợ cả **stateless** và **stateful rules**, tích hợp với **Transit Gateway**, multi-VPC endpoints để kiểm soát lưu lượng giữa nhiều VPC. 

Ngoài ra, trong sườn sự kiện còn nhấn mạnh **AWS WAF + AWS Shield** như lớp bảo vệ ứng dụng web và chống DDoS, được đặt ở biên (ALB/CloudFront) trong mô hình defense-in-depth.

---

#### 2.5. Pillar 4 – Data Protection (10:40 – 11:10) – Encryption, Keys & Secrets

Phần này do **Thịnh Lâm, Việt Nguyễn** trình bày, tập trung vào **mã hoá và quản lý khóa/bí mật**: 

* **AWS KMS (Key Management Service)**

  * Làm rõ khái niệm **master key** và **data key**, cách data key được sinh và mã hoá bởi master key. 
  * **Key policy**: chỉ các principal được chỉ định trong policy mới có thể sử dụng key, kể cả admin nếu không nằm trong policy cũng không được phép. 
  * Phân biệt **managed key** vs **CMK (customer-managed key)**; CMK có thể cấu hình rotation tự động hoặc thủ công.

* **Data Classification & Guardrails**

  * Ghi chú có nhắc đến **Amazon Macie** để quét S3 bucket, nhận diện dữ liệu nhạy cảm (PII, tài liệu quan trọng). 
  * Thiết lập **guardrails**: ví dụ policy deny nếu S3 object không được mã hoá, bắt buộc encryption cho dữ liệu nhạy cảm. 

* **Encryption in Transit**

  * Danh sách dịch vụ cần quan tâm:

    * S3 & DynamoDB ở mức API-based.
    * RDS (SSL), EBS & Nitro (mã hoá trên đường truyền), ACM (cấp chứng chỉ TLS). 

* **Secrets Manager & Rotation**

  * Dùng **Secrets Manager** để lưu credential, connection string, API key…
  * Hỗ trợ **rotation** tự động, tích hợp với KMS để mã hoá secrets. 

---

#### 2.6. Pillar 5 – Incident Response (11:10 – 11:40) – IR Playbook & Automation

Phần này do **anh Long, Tịnh Trương** chia sẻ, tập trung vào **quy trình ứng phó sự cố (IR)**: 

* **Bối cảnh:**

  * Môi trường hiện đại (multi-account, nhiều dịch vụ, hybrid) quá phức tạp để “chữa cháy bằng tay”.
  * Các loại sự cố: security breach, system outages, data corruption, high traffic,… đòi hỏi quy trình bài bản và mức độ automation cao. 

* **Security Responsibilities are Shared**

  * Nhắc lại **Shared Responsibility Model** và liệt kê một số dịch vụ nền tảng cần bật cho security foundation:

    * AWS Organizations + SCP
    * CloudTrail
    * AWS Config
    * GuardDuty
    * Security Hub 

* **Prevention Guidelines (phòng hơn chữa)** 

  * **Kill long-lived credentials** – loại bỏ access key dài hạn.
  * **Never expose S3** – không để S3 public trừ khi thực sự cần và được kiểm soát.
  * **No facing internet** cho workload không cần public.
  * **Everything through IaC** – mọi thay đổi hạ tầng đều nên qua code.
  * **Double gate high-risk changes** – thêm lớp phê duyệt cho thay đổi rủi ro cao.

* **Incident Response Process (theo AWS)** 

  * Quy trình IR chuẩn gồm:

    1. **Prepare** – xây dựng playbook, phân vai trò, chuẩn bị sẵn công cụ.
    2. **Detection & Analysis** – phát hiện từ GuardDuty/Security Hub/CloudTrail, phân tích mức độ.
    3. **Containment** – cô lập nguồn gây sự cố (isolate instance, revoke key…).
    4. **Eradication & Recovery** – loại bỏ nguyên nhân, khôi phục hệ thống từ snapshot/backup.
    5. **Post-incident** – review, rút kinh nghiệm, cập nhật playbook.

* **Các playbook cụ thể được đề cập trong sườn:**

  * **Compromised IAM key.**
  * **S3 public exposure.**
  * **EC2 malware detection.**
  * Các bước chung đều bao gồm: snapshot, isolation, thu thập bằng chứng, và automation bằng **Lambda/Step Functions** cho những trường hợp lặp lại.

---

#### 2.7. Wrap-Up & Q&A (11:40 – 12:00)

Phần tổng kết nhấn mạnh:

* **5 pillars Security** phải được nhìn như một “bộ khung” đồng bộ, không tách rời.
* Các **common pitfalls** của doanh nghiệp Việt Nam:

  * Thiếu IAM chuẩn hoá (root dùng thường xuyên, credential dài hạn).
  * Không bật đầy đủ CloudTrail/GuardDuty/Security Hub.
  * S3 hoặc endpoint public ngoài ý muốn, không có guardrails.
* Gợi ý **roadmap học tập**: AWS Certified Security – Specialty, sau đó Security nâng cao trong lộ trình Solutions Architect Professional. 

---

### III. Kiến thức và bài học rút ra

1. **Security phải được thiết kế từ kiến trúc, không phải xử lý sau khi có sự cố**

   * Việc liên tục nhắc tới Security Pillar trong Well-Architected giúp tôi nhận thức rõ: nếu kiến trúc không enforce IAM, logging, network segmentation, encryption… ngay từ đầu, chi phí khắc phục sau này sẽ rất lớn.

2. **IAM hiện đại = multi-account, SSO, SCP, permission boundaries, rotation, MFA**

   * IAM không chỉ là “tạo user và gán policy” mà là một kiến trúc đa lớp: Organizations, IAM Identity Center, SCP, permission boundaries, Access Analyzer… kết hợp để vừa linh hoạt vừa an toàn. 

3. **Detection-as-Code là hướng đi bắt buộc trong môi trường cloud phức tạp**

   * Thay vì xem log thủ công, mọi detection rule (CloudTrail, GuardDuty, Security Hub) cần được mô tả bằng code, có versioning, có pipeline triển khai – giống cách ta quản lý IaC. 

4. **Bảo mật hạ tầng không chỉ là “đóng port” mà là thiết kế network đúng nguyên tắc**

   * Phân biệt rõ vai trò của SG vs NACL, vai trò của Route 53, Network Firewall… cho thấy security phải gắn với kiến trúc mạng nhiều lớp. 

5. **Data Protection và IR là hai mắt xích cuối nhưng cực kỳ quan trọng**

   * Không chỉ mã hoá dữ liệu (KMS, encryption in transit) mà còn phải phân loại dữ liệu (Macie), thiết lập guardrails deny non-encrypted, quản lý secrets đúng cách. 
   * IR playbook, nếu không được chuẩn bị trước, sẽ khiến đội ngũ “rối loạn” khi xảy ra sự cố thực tế.

---

### IV. Định hướng áp dụng vào học tập và dự án cá nhân

1. **Chuẩn hoá IAM & multi-account cho các môi trường lab/dự án cá nhân**

   * Áp dụng mô hình **AWS Organizations + IAM Identity Center + SCP** tối thiểu, tránh dồn tất cả vào một account duy nhất.
   * Xoá dần long-lived credentials, thay bằng role + temporary credentials, bật MFA cho các tài khoản quan trọng.

2. **Thiết lập detection foundation cho mọi workload**

   * Bật **CloudTrail ở org-level**, kích hoạt **GuardDuty** và **Security Hub** trên toàn bộ tài khoản lab của bản thân, ít nhất ở mức baseline.
   * Thử triển khai một số rule **detection-as-code** (ví dụ: S3 public, security group mở 0.0.0.0/0, credential không rotation…).

3. **Thiết kế lại VPC/network theo hướng defense-in-depth**

   * Chia VPC thành public/private subnet rõ ràng; hạn chế tối đa workload trực tiếp public Internet.
   * Dùng security group đúng ngữ nghĩa (theo role của service), NACL ở mức subnet, và xem xét thử nghiệm Network Firewall/Route 53 DNS filter trong các bài lab nâng cao.

4. **Áp dụng Data Protection & IR vào các dự án có dữ liệu nhạy cảm**

   * Với các dự án liên quan đến hợp đồng, dữ liệu người dùng, kế hoạch sử dụng **KMS, S3 encryption, RDS encryption**, Secrets Manager và Macie.
   * Xây dựng một **IR playbook đơn giản** cho lab:

     * Trường hợp access key bị lộ.
     * Trường hợp S3 bucket bị public.
   * Thử dùng Lambda/Step Functions để tự động cô lập tài nguyên hoặc revoke credential trong một số kịch bản mô phỏng.

5. **Định hướng học tiếp Security Specialty**

   * Sự kiện khẳng định đây là mảng kiến thức mà tôi cần đầu tư nghiêm túc nếu muốn xây dựng hệ thống AI/ML và ứng dụng enterprise trên AWS một cách an toàn, bền vững. Trong lộ trình, tôi dự kiến:

     * Củng cố thêm Well-Architected – Security Pillar và AWS SRA (Security Reference Architecture).
     * Sau đó hướng tới **AWS Certified Security – Specialty** như một mục tiêu trung hạn.

Bài thu hoạch này giúp tôi tổng hợp lại toàn bộ nội dung buổi 29/11 theo đúng 5 trụ cột Security Pillar và định hình rõ ràng cách áp dụng vào các hệ thống thực tế mà tôi đang và sẽ xây dựng trên AWS.

### V. Một số hình ảnh trong sự kiện

![1](/images/4-Event/4.6-AWS/1.jpeg)
![2](/images/4-Event/4.6-AWS/2.jpeg)
![3](/images/4-Event/4.6-AWS/3.jpeg)
![4](/images/4-Event/4.6-AWS/4.jpeg)
![5](/images/4-Event/4.6-AWS/5.jpeg)