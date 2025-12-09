---
title: "Các bài blogs đã dịch"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

### [Blog 1 - Getting started with healthcare data lakes: Using microservices](3.1-Blog1/)
Bài viết giới thiệu cách xây dựng một data lake hiện đại cho lĩnh vực y tế trên AWS bằng kiến trúc microservices. Nội dung tập trung vào nhu cầu hợp nhất nhiều nguồn dữ liệu khác nhau như hồ sơ sức khỏe điện tử (EHR), hệ thống xét nghiệm, chẩn đoán hình ảnh và thiết bị IoT y tế vào một nền tảng dữ liệu tập trung. Tác giả giải thích cách microservices — được triển khai qua API, container hoặc serverless — giúp tách biệt các bước ingest, xử lý, phân tích và quản trị dữ liệu, từ đó hệ thống linh hoạt, dễ mở rộng và dễ bảo trì hơn. Bài viết cũng mô tả các bước điển hình như đưa dữ liệu vào Amazon S3, lập catalog và chuyển đổi bằng các dịch vụ như AWS Glue, thiết lập bảo mật và quyền riêng tư (mã hóa, phân quyền chi tiết, ghi log), đồng thời đảm bảo tuân thủ các tiêu chuẩn như HIPAA.

---

### [Blog 2 - Streamline access to ISO-rating content changes with Verisk Rating Insights and Amazon Bedrock](3.2-Blog2/)
Bài viết trình bày cách Verisk nâng cấp sản phẩm ISO Electronic Rating Content (ERC) bằng một giao diện hội thoại sử dụng AI tạo sinh trên Amazon Bedrock. Từ các điểm đau của khách hàng — phải tải cả gói nội dung để lấy một phần thông tin nhỏ, việc so sánh các bản phát hành tốn hàng giờ hoặc nhiều ngày, đội hỗ trợ ERC phải xử lý nhiều truy vấn lặp lại — Verisk đã xây dựng một hệ thống RAG (Retrieval-Augmented Generation). Tài liệu được phân đoạn, nhúng bằng mô hình Amazon Titan và lưu trữ dưới dạng vector trong Amazon OpenSearch Serverless để truy xuất theo ngữ cảnh truy vấn. Mô hình Anthropic Claude 3.5 Sonnet trên Amazon Bedrock chịu trách nhiệm tạo câu trả lời, Amazon ElastiCache lưu lịch sử trò chuyện, và LlamaIndex điều phối các nguồn dữ liệu. Bài viết cũng mô tả vòng lặp đánh giá, cơ chế guardrail với Amazon Bedrock Guardrails, các chỉ số chất lượng do SME định nghĩa, cùng pipeline phân tích sử dụng Amazon S3 và Snowflake. Kết quả kinh doanh bao gồm rút ngắn thời gian phân tích từ hàng giờ/ngày xuống còn vài phút, giảm tải cho bộ phận hỗ trợ, tăng tốc onboarding khách hàng và cung cấp thông tin chi tiết chính xác, dễ hiểu về các thay đổi nội dung xếp hạng.

---

### [Blog 3 - How Poland’s Post Bank accelerated digital transformation while maintaining regulatory compliance on AWS](3.3-Blog3/)
Bài viết kể lại hành trình hiện đại hóa nền tảng ngân hàng số của Ngân hàng Bưu điện Ba Lan (Post Bank) trên AWS, đồng thời vẫn tuân thủ chặt chẽ các quy định tài chính. Bắt đầu từ năm 2019 với việc di chuyển thử một hệ thống không trọng yếu, ngân hàng dần xây dựng năng lực và niềm tin với đám mây, sau đó chọn ứng dụng ngân hàng điện tử và di động làm dự án di chuyển chủ lực. Sử dụng Terraform cho mô hình Infrastructure as Code, kiến trúc lai với các kết nối AWS Direct Connect dự phòng tới vùng châu Âu (Frankfurt) và vận dụng linh hoạt chiến lược 6R, Post Bank đạt được độ trễ ổn định, tính sẵn sàng cao với Amazon RDS Multi-AZ và giải pháp cache có thể tự động co giãn với Auto Scaling. Bài viết nhấn mạnh nền tảng quản trị mạnh dựa trên AWS Organizations, IAM Identity Center, SCPs, AWS Control Tower và kiến trúc mạng hub-and-spoke, phù hợp với AWS Well-Architected Framework và Security Reference Architecture. Kết quả định lượng gồm: giảm thời gian triển khai từ 2 giờ xuống 10 phút, giảm 40% mức sử dụng CPU, rút ngắn thời gian dựng môi trường từ 30 ngày xuống 30 phút và hạ tỷ lệ nghỉ việc nhân viên từ 30% xuống còn 5%. Ngân hàng tiếp tục mở rộng di chuyển lên đám mây và đã triển khai trợ lý AI nội bộ dùng Amazon Bedrock và Claude 3.5 để tra cứu kho tri thức nội bộ, thể hiện định hướng đổi mới liên tục trên nền tảng đám mây an toàn và tuân thủ.
