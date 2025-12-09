---
title: "Cách Ngân hàng Bưu điện Ba Lan tăng tốc chuyển đổi số trong khi vẫn duy trì tuân thủ quy định trên AWS"
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---


Tác giả: Waldemar Szczepański, Bartłomiej Rafał, Piotr Boetzel, và Dariusz Matczak | Ngày đăng: 16/09/2025 | Danh mục: [Cloud Adoption](https://aws.amazon.com/blogs/publicsector/category/migration-solutions/cloud-adoption/), [Customer Solutions](https://aws.amazon.com/blogs/publicsector/category/post-types/customer-solutions/), [Financial Services](https://aws.amazon.com/blogs/publicsector/category/industries/financial-services/), [Government](https://aws.amazon.com/blogs/publicsector/category/public-sector/government/), [Migration](https://aws.amazon.com/blogs/publicsector/category/enterprise-strategy/migration-enterprise-strategy/), [Public Sector](https://aws.amazon.com/blogs/publicsector/category/public-sector/), [Regions](https://aws.amazon.com/blogs/publicsector/category/regions/)

Trong thị trường dịch vụ tài chính cạnh tranh của Ba Lan, Ngân hàng Bưu điện (Post Bank) đối mặt với một thách thức quan trọng: làm thế nào để tăng tốc đổi mới và cải thiện trải nghiệm khách hàng trong khi vẫn tuân thủ các yêu cầu quy định nghiêm ngặt. Giải pháp đến từ chiến lược di chuyển lên đám mây, không chỉ thay đổi hạ tầng công nghệ mà còn toàn bộ cách tiếp cận ngân hàng số của họ. Bằng cách di chuyển hệ thống ngân hàng điện tử sang [Amazon Web Services (AWS)](https://aws.amazon.com/), Post Bank đã rút ngắn thời gian triển khai ứng dụng từ 2 giờ xuống chỉ còn 10 phút, giảm 40% mức sử dụng CPU và cải thiện đáng kể độ tin cậy hệ thống—tất cả trong khi vẫn đảm bảo tuân thủ đầy đủ các quy định tài chính khắt khe của Ba Lan.

Câu chuyện chuyển đổi này cho thấy cách các tổ chức tài chính có thể sử dụng công nghệ AWS Cloud để trở nên linh hoạt và hiệu quả hơn mà không làm giảm tính bảo mật hay tuân thủ. Với Post Bank, kết quả không chỉ ở các chỉ số kỹ thuật: tỷ lệ nghỉ việc của nhân viên giảm từ 30% xuống còn 5%, và ngân hàng có thể cung cấp môi trường phát triển mới trong 30 phút thay vì 30 ngày.

## **Xây dựng niềm tin thông qua áp dụng từng bước**

Hành trình lên đám mây của Post Bank bắt đầu thận trọng vào năm 2019, với việc di chuyển một hệ thống không trọng yếu.

“Chúng tôi cần học công nghệ đám mây và xây dựng niềm tin trong toàn tổ chức,”  
 — Waldemar Szczepański, Trưởng nhóm Trung tâm xuất sắc về điện toán đám mây (CCoE) tại Post Bank.

Cách tiếp cận có kiểm soát này cho phép đội ngũ CNTT phát triển kỹ năng về đám mây trong khi chứng minh giá trị thực tế với các bên liên quan.

Đại dịch COVID-19 đã thúc đẩy mạnh mẽ quá trình chuyển đổi số của ngân hàng.  
 Khả năng mở rộng nhanh chóng và triển khai tính năng mới liên tục trở thành yếu tố quyết định thành công trong kinh doanh.

Bên cạnh đó, xung đột tại Ukraine bổ sung thêm một yếu tố chiến lược quan trọng:  
 ban lãnh đạo cấp cao nhận thấy tầm quan trọng của tính dự phòng địa lý và việc lưu trữ hệ thống ngoài lãnh thổ Ba Lan.

Những yếu tố hội tụ này đã tạo ra thời điểm hoàn hảo cho sự thay đổi tổ chức.  
 Post Bank thành lập đội CCoE theo [AWS Cloud Adoption Framework (AWS CAF)](https://aws.amazon.com/cloud-adoption-framework/), đặt nền tảng cho chiến lược di chuyển toàn diện lên đám mây.

## **Chuyển đổi tổ chức**

Việc di chuyển một hệ thống kinh doanh quan trọng đòi hỏi nhiều hơn là chuyên môn kỹ thuật—nó cần sự đồng bộ trong tổ chức. Post Bank đã thay đổi toàn diện hoạt động CNTT: áp dụng công nghệ mới, thay đổi mô hình làm việc, quản lý chi phí đám mây và quy trình vận hành.

Nhóm CCoE phải điều phối nhiều bên liên quan nội bộ gồm: nhóm kiến trúc, bảo mật, kiểm toán và vận hành — mỗi nhóm có các yêu cầu và mối quan tâm riêng cần được giải quyết.

“Chúng tôi không thể làm điều này một mình,”  
 — Szczepański chia sẻ.  
 “Các kiến trúc sư AWS và đối tác AWS đã giúp chúng tôi xây dựng bản thử nghiệm (proof of concept), và chương trình [AWS Migration Acceleration Program (MAP)](https://aws.amazon.com/migration-acceleration-program/) cung cấp cả phương pháp luận lẫn một phần tài trợ cho quá trình di chuyển.”

Cách tiếp cận hợp tác này chứng minh là yếu tố then chốt.  
 Các kiến trúc sư AWS và chuyên gia từ đối tác AWS làm việc cùng với đội ngũ của Post Bank, vừa cung cấp chuyên môn, vừa chuyển giao kiến thức cho nhân sự nội bộ.

## **Kiến trúc cho môi trường lai**

Sau khi đánh giá kỹ lưỡng năng lực đội ngũ, độ phức tạp của ứng dụng và tác động đến người dùng, nhóm CCoE đã chọn ứng dụng ngân hàng điện tử và di động làm dự án di chuyển chủ lực.  
 Đây là hệ thống trọng yếu, thử thách khả năng duy trì hiệu năng và độ tin cậy trong môi trường kết hợp giữa on-premises và đám mây.

Họ sử dụng phương pháp [Infrastructure as Code (IaC)](https://aws.amazon.com/what-is/iac/) với Terraform, đặt nền tảng cho việc triển khai nhanh chóng và nhất quán.

Tuy nhiên, kiến trúc lai mang lại những thách thức riêng biệt.  
 Khoảng cách 750 km giữa trung tâm dữ liệu nội bộ và [vùng AWS](https://docs.aws.amazon.com/glossary/latest/reference/glos-chap.html#region) Châu Âu (Frankfurt) khiến quản lý độ trễ (latency) trở thành ưu tiên hàng đầu.

Post Bank đã triển khai các kết nối [AWS Direct Connect](https://aws.amazon.com/directconnect/) dự phòng trên những tuyến đường địa lý khác nhau, giúp đạt được độ trễ ổn định 30 mili-giây, đáp ứng yêu cầu vận hành của ứng dụng.

![](/images/3-Blog/Blog3/1.png) 
Hình minh họa 1: sơ đồ kết nối AWS Direct Connect

Nhóm dự án đã áp dụng linh hoạt [chiến lược 6Rs](https://aws.amazon.com/blogs/enterprise-strategy/6-strategies-for-migrating-applications-to-the-cloud/) gồm:  
 rehost, replatform, repurchase, re-architect, retire, và retain.

Khi mô hình kiểm soát truy cập mạng on-premises không thể chuyển trực tiếp lên đám mây, họ chọn chiến lược “repurchase”, sử dụng giải pháp của bên thứ ba từ [AWS Marketplace](https://aws.amazon.com/marketplace/).

Để đảm bảo tính sẵn sàng cao của cơ sở dữ liệu, họ tái nền tảng (replatform) sang [Amazon Relational Database Service (Amazon RDS](https://aws.amazon.com/rds/)) Multi-AZ.  
 Giải pháp bộ nhớ đệm trong bộ nhớ (in-memory cache) được di chuyển (rehost) và nâng cấp với plugin cộng đồng để hỗ trợ [AWS Auto Scaling](https://aws.amazon.com/autoscaling/).

## **Chứng minh giá trị thông qua thành công có thể đo lường**

Bản thử nghiệm (proof of concept) của Post Bank không chỉ là một bài kiểm tra kỹ thuật, mà là một cách tiếp cận dựa trên dữ liệu nhằm thuyết phục các bên liên quan.  
 Nhóm dự án đã xác định 10 chỉ số hiệu suất chính (KPI), trực tiếp giải quyết các mối lo ngại của các bên về chi phí, bảo mật và hiệu năng.

“Việc lựa chọn các chỉ số KPI là yếu tố then chốt,”  
 — chia sẻ Bartłomiej Rafał, Trưởng nhóm kỹ thuật CCoE.  
 “Chúng tôi cần những số liệu có thể phản biện lại các nghi ngờ bằng các con số cụ thể.”

Kết quả vượt ngoài mong đợi ở hầu hết các chỉ số, chỉ có một KPI chưa đạt mức mục tiêu đề ra, nhưng vẫn tốt hơn đáng kể so với mức hiệu suất trung bình của hệ thống on-premises trước đây.

Cách tiếp cận dựa trên bằng chứng thực nghiệm này đã biến những người hoài nghi thành người ủng hộ mạnh mẽ.Tính sẵn sàng của hệ thống (system availability) được cải thiện rõ rệt nhờ khả năng tự phục hồi tự động, có thể khắc phục sự cố trong vòng 10 giây, thay vì phải can thiệp thủ công như trước.Tốc độ phát triển (development velocity) tăng đáng kể, khi thời gian khởi tạo môi trường mới giảm từ 30 ngày xuống còn 30 phút.

## **Duy trì bảo mật và tuân thủ trên đám mây**

Đối với một tổ chức tài chính tại Ba Lan, vấn đề bảo mật và tuân thủ quy định là không thể thương lượng. Post Bank đã xây dựng nền tảng đám mây của mình dựa trên các thực tiễn tốt nhất của AWS, tuân theo [AWS Well-Architected Framework Security Pillar](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/welcome.html) và [AWS Security Reference Architecture](https://docs.aws.amazon.com/prescriptive-guidance/latest/security-reference-architecture/welcome.html).

Bằng cách sử dụng [AWS Organizations](https://aws.amazon.com/organizations/) kết hợp với [AWS IAM Identity Center](https://aws.amazon.com/iam/identity-center/) và [service control policies (SCPs)](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html), ngân hàng đã thực thi các cơ chế kiểm soát tuân thủ quan trọng như: phân tách môi trường (environment isolation), phân chia nhiệm vụ (separation of duties), nguyên tắc đặc quyền tối thiểu (least privilege access) và mã hóa bắt buộc (mandatory encryption).  
 [AWS Control Tower](https://aws.amazon.com/controltower/) giúp đơn giản hóa quản trị bảo mật, cho phép thiết lập các chính sách như giới hạn sử dụng dịch vụ trong phạm vi các vùng thuộc Khu vực Kinh tế châu Âu (EEA).

Nhóm kỹ thuật đã sử dụng [Account Factory for Terraform (AFT)](https://docs.aws.amazon.com/controltower/latest/userguide/aft-overview.html) để tạo mới tất cả tài khoản AWS với cấu hình và cài đặt bảo mật chuẩn. Đối với quản lý danh tính, họ liên kết (federate) IAM Identity Center với hệ thống quản lý danh tính sẵn có, giúp đơn giản hóa việc chứng nhận tuân thủ bằng cách điều chỉnh quy trình hiện có thay vì tạo quy trình mới. Sơ đồ dưới đây minh họa kiến trúc này:

![](/images/3-Blog/Blog3/2.png) 
Hình minh họa 2: sơ đồ phân quyền và bảo mật

Điều quan trọng đối với ngân hàng là chỉ thay đổi tối thiểu các quy trình hiện có trong khi vẫn đơn giản hóa việc tuân thủ. Kiến trúc bảo mật mạng hub-and-spoke, được thể hiện trong sơ đồ sau, cho phép mở rộng các quy trình bảo mật hiện có sang môi trường AWS Cloud thông qua đồng bộ hóa quản lý tường lửa (firewall management synchronization).

![](/images/3-Blog/Blog3/3.png)  
Hình minh họa 3: sơ đồ kiến trúc mạng

## **Bài học cho các tổ chức tài chính**

Thành công của Post Bank trong quá trình di chuyển lên đám mây mang lại những bài học giá trị cho các tổ chức tài chính khác đang cân nhắc chuyển đổi:

* **Bắt đầu nhỏ nhưng nghĩ lớn** – Bắt đầu với một hệ thống không trọng yếu giúp Post Bank xây dựng kỹ năng và sự tự tin, đồng thời giảm thiểu rủi ro.

* **Thiết lập quản trị mạnh mẽ từ sớm** – Nhóm CCoE đóng vai trò then chốt trong việc lãnh đạo và điều phối các nhóm liên quan.

* **Đầu tư vào kiến trúc** – Dành thời gian thiết kế hệ thống đúng cách, xem xét các chiến lược di chuyển 6Rs, sẽ mang lại lợi ích lớn trong giai đoạn triển khai.

* **Sử dụng PoC một cách chiến lược** – Bao gồm các chỉ số KPI trực tiếp phản ánh mối quan tâm của các bên liên quan và chứng minh rõ ràng lợi ích như cải thiện tính sẵn sàng và hiệu quả vận hành.

* **Tận dụng chuyên môn bên ngoài** – Hợp tác với các kiến trúc sư AWS và sử dụng các chương trình như MAP (Migration Acceleration Program) để tăng tốc quá trình di chuyển đồng thời nâng cao năng lực nội bộ.

## **Hướng tới đổi mới liên tục**

“AWS Cloud khiến đội ngũ quản trị viên và kiểm thử của chúng tôi hài lòng hơn, đồng thời nâng cao sự thỏa mãn của các bên liên quan trong kinh doanh vì chúng tôi có thể triển khai thay đổi và nâng cấp nhanh hơn,” – Szczepański chia sẻ. Sự chuyển đổi này đã thay đổi căn bản cách Post Bank tiếp cận công nghệ. Giám đốc Bộ phận Hệ thống CNTT của Post Bank, Artur Szatkowski, khẳng định đầy tự tin:  
 “Chúng tôi sẽ không quay lại với các giải pháp on-premises.”

Ngân hàng có kế hoạch di chuyển thêm nhiều hệ thống khác và đang khám phá các năng lực mới dựa trên đám mây.Gần đây, họ đã triển khai trợ lý AI nội bộ sử dụng [Amazon Bedrock](https://aws.amazon.com/bedrock/) và Claude 3.5 của Anthropic.  Nhờ đó, nhân viên có thể nhanh chóng tìm kiếm thông tin trong kho dữ liệu nội bộ khổng lồ của ngân hàng, bao gồm tài liệu, biểu mẫu, điều khoản dịch vụ và tài liệu quảng bá. Hành trình của Post Bank chứng minh rằng, với kế hoạch cẩn trọng, hợp tác chặt chẽ và cam kết tuân thủ các tiêu chuẩn tốt nhất, các tổ chức tài chính hoàn toàn có thể đạt được tính linh hoạt và khả năng đổi mới của điện toán đám mây trong khi vẫn duy trì bảo mật và tuân thủ nghiêm ngặt mà khách hàng và cơ quan quản lý yêu cầu.

## **Về Post Bank**

Post Bank là một ngân hàng tiêu dùng của Ba Lan với khoảng 700.000 khách hàng, đã hoạt động trên thị trường 35 năm. Đối tác chiến lược và cổ đông chính của ngân hàng là Bưu điện Quốc gia Ba Lan. Thông qua mối quan hệ này, các sản phẩm và dịch vụ của ngân hàng được cung cấp tại mọi bưu điện trên toàn quốc, tạo nên mạng lưới khoảng 4.700 chi nhánh — lớn gấp 5 lần so với các đối thủ. Điều này giúp Post Bank phục vụ cả những người dân chưa có khả năng tiếp cận dịch vụ số, góp phần thúc đẩy tài chính toàn diện tại Ba Lan.

| ![](/images/3-Blog/Blog3/4.jpg) | Waldemar Szczepański Waldemar là Trưởng nhóm Trung tâm Xuất sắc về Điện toán Đám mây (CCoE) tại Post Bank, phụ trách việc phát triển ngân hàng trong các lĩnh vực công nghệ đám mây và trí tuệ nhân tạo (AI). Ông có hơn 20 năm kinh nghiệm trong lĩnh vực tài chính. Tại Post Bank, ông đã lãnh đạo các dự án nhằm xây dựng môi trường làm việc hiện đại và ứng dụng các công nghệ mới, bao gồm AI và ngân hàng đám mây. |
| :---- | :---- |
| ![](/images/3-Blog/Blog3/5.jpg) | **Bartłomiej Rafał** Bartłomiej là Trưởng nhóm kỹ thuật CCoE tại Post Bank. Ông đam mê việc ứng dụng công nghệ để giải quyết các vấn đề kinh doanh và cải thiện quy trình hiện có. Là một chuyên gia công nghệ đa năng (tech generalist), ông có niềm quan tâm sâu rộng đến mọi khía cạnh của CNTT, từ hạ tầng, an ninh mạng, kiến trúc hệ thống cho đến quản lý — và luôn có nhiều ý tưởng hơn thời gian để thực hiện. |
| ![](/images/3-Blog/Blog3/6.jpg) | **Piotr Boetzel** Piotr là Kiến trúc sư Giải pháp Cấp cao (Senior Solution Architect) tại AWS, làm việc với khách hàng thuộc khu vực công (Public Sector) ở Trung và Đông Âu (CEE). Ông hỗ trợ khách hàng trong các dự án hiện đại hóa và chuyển đổi hệ thống, đặc biệt tập trung vào bảo mật và tuân thủ quy định. |
| ![](/images/3-Blog/Blog3/7.png) | **Dariusz Matczak** Dariusz là Quản lý tài khoản (Account Manager) tại AWS, phụ trách khu vực công ở Ba Lan. Ông có hơn 15 năm kinh nghiệm làm việc với khách hàng và đối tác trên nhiều ngành công nghiệp, hỗ trợ họ trong các dự án chuyển đổi số lên đám mây và triển khai nhiều dự án công nghệ khác nhau. |