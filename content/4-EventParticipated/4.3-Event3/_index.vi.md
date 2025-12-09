---
title: "AWS Cloud Mastery Series #1"
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

### AI/ML/GenAI on AWS
#### Thứ Bảy, 15/11/2025 – AWS Vietnam Office


### I. Thông tin chung về sự kiện

* **Tên sự kiện:** AI/ML/GenAI on AWS
* **Thời gian:** 8:30 – 12:00, ngày 15/11/2025
* **Địa điểm:** AWS Vietnam Office
* **Mục tiêu:**

  * Giới thiệu tổng quan về AI/ML và GenAI trên nền tảng AWS.
  * Làm rõ khái niệm *foundation models* và các cách ứng dụng trong thực tế.
  * Trình bày hệ sinh thái dịch vụ AI/ML trên AWS, từ dịch vụ “ready-made” đến nền tảng xây dựng mô hình tùy chỉnh.
  * Minh họa cách xây dựng ứng dụng GenAI sử dụng Amazon Bedrock, RAG và AgentCore.


### II. Nội dung chính theo dòng thời gian

### 1. Phần mở đầu – Giới thiệu GenAI và Foundation Models (8:30 – 9:00)

Người trình bày **Lâm Tuấn Kiệt** tập trung vào việc đặt nền tảng về **Generative AI (GenAI)**:

* **GenAI là gì:**

  * Khác với các mô hình ML truyền thống chủ yếu “phân loại” hoặc “dự đoán”, GenAI có khả năng *tạo mới* nội dung: văn bản, hình ảnh, âm thanh, mã nguồn,…
  * GenAI được xây dựng dựa trên các **foundation models** có quy mô rất lớn (nhiều tỷ tham số), được huấn luyện trên tập dữ liệu đa dạng, sau đó *tinh chỉnh* hoặc *hướng dẫn* để phù hợp với từng bài toán thực tế.

* **Foundation Models & Amazon Bedrock:**

  * Amazon Bedrock được giới thiệu là **nền tảng quản lý và truy cập nhiều foundation models từ các nhà cung cấp khác nhau** (như Claude, Llama, Titan,…), giúp người dùng không phải tự quản lý hạ tầng, scaling hay bảo mật mô hình.
  * Điểm nhấn: cùng một API, có thể thử nghiệm nhiều mô hình, so sánh chất lượng và chi phí, lựa chọn mô hình phù hợp với từng kịch bản (chatbot, tóm tắt, phân loại văn bản, RAG,…).

* **Prompt Engineering:**

  * Được nhấn mạnh như **kỹ năng cốt lõi** khi làm việc với GenAI:

    * *Prompt engineering = quá trình thiết kế, thử nghiệm và tinh chỉnh prompt* để mô hình hiểu đúng bối cảnh và cho ra kết quả phù hợp.
  * Các kỹ thuật chính được nêu:

    * **Zero-shot prompting:** không cung cấp ví dụ, chỉ mô tả yêu cầu.
    * **Few-shot prompting:** đưa thêm một vài ví dụ mẫu để mô hình học “cách trả lời” đúng phong cách.
    * **Chain-of-Thought (CoT):** hướng dẫn mô hình *diễn giải từng bước suy luận*, giúp kết quả có tính logic, đặc biệt cho bài toán tính toán, lập luận nhiều bước.

* **RAG (Retrieval-Augmented Generation):**

  * Được giới thiệu như kiến trúc kết hợp **truy xuất tri thức** với GenAI: mô hình chỉ “giỏi ngôn ngữ”, còn kiến thức cụ thể thì lấy từ kho dữ liệu riêng của doanh nghiệp (document, knowledge base,…).
  * Ghi chú của tôi nhấn mạnh: *“RAG: retrieving relevant info from a data source”* – mô hình sẽ truy xuất đoạn văn bản liên quan, sau đó dùng foundation model để tổng hợp và trả lời dựa trên dữ liệu đó, giúp:

    * Giảm rủi ro “hallucination”.
    * Dễ cập nhật kiến thức (chỉ cần cập nhật kho dữ liệu, không cần retrain model).


### 2. Phiên “AWS AI/ML Services Overview” & Embeddings/RAG in Action (9:00 – 10:30)

Phần này tập trung vào **bức tranh hệ sinh thái dịch vụ AI trên AWS** và cách tận dụng cho GenAI/RAG.

#### 2.1. Embeddings và Titan Embeddings

* Trong phần slide “What are embeddings?” giảng viên giải thích:

  * Embedding là cách **biểu diễn văn bản/hình ảnh thành vector số** để mô hình có thể đo được mức độ tương đồng, tìm kiếm, phân cụm,…
  * Embeddings là “nền móng” của các hệ thống RAG, semantic search, recommendation,…

* AWS giới thiệu **Titan Embeddings** – một lựa chọn embedding do chính AWS cung cấp, tối ưu cho:

  * Tìm kiếm ngữ nghĩa (semantic search).
  * RAG trên tài liệu doanh nghiệp.
  * Khả năng tích hợp chặt với Amazon Bedrock và các dịch vụ khác.

* Ghi chú: *“Embeddings. Một vài options AWS hỗ trợ. RAG in action.”* – tôi hiểu đây là phần demo mô tả pipeline: dữ liệu → chia nhỏ → sinh embedding → lưu vào vector store → truy vấn và kết hợp với LLM để trả lời.

#### 2.2. Các dịch vụ AI “ready-made” trên AWS

Anh **Hoàng Anh** giới thiệu chi tiết các dịch vụ AI managed, trong đó tôi có ghi lại cả use case lẫn chi phí tham khảo:

* **Amazon Rekognition** – Computer Vision:

  * Nhận diện đối tượng, khuôn mặt, text trong ảnh/video.
  * Ghi chú: *“0.0013 USD/ảnh (dưới 1 triệu ảnh)”* → phù hợp các bài toán nhận diện ảnh ở quy mô vừa, như giám sát camera, lọc nội dung.

* **Amazon Translate** – Neural Machine Translation:

  * Dịch tự động đa ngôn ngữ.
  * Ghi chú: *“15 USD / 1 triệu ký tự”* → có thể áp dụng cho hệ thống dịch tự động tài liệu, email, nội dung web.

* **Amazon Textract** – OCR & trích xuất cấu trúc tài liệu:

  * Không chỉ nhận dạng text, mà còn **giữ bố cục** bảng, form, field.
  * Ghi chú: *“0.05 USD/trang (dưới 1 triệu trang)”*, rất phù hợp cho bài toán trích xuất hợp đồng, hóa đơn.

* **Amazon Transcribe** – Speech-to-Text:

  * Chuyển giọng nói thành văn bản, hỗ trợ caption, transcript cuộc họp.
  * Ghi chú: *“0.024 USD/phút (dưới 250k phút)”*.

* **Amazon Polly** – Text-to-Speech:

  * Tạo giọng nói tự nhiên từ văn bản.
  * Ghi chú: *“4 USD / 1 triệu ký tự”* → dùng cho voicebot, audio guide, video training.

* **Amazon Comprehend** – NLP service:

  * Phân tích sentiment, key phrase, entity, relationship,… từ văn bản.
  * Ghi chú: *“0.0001 USD / 100 ký tự hoặc 3 USD/giờ”* → thích hợp gắn với hệ thống phân tích ý kiến khách hàng, phân loại ticket.

* **Amazon Kendra** – Intelligent Search / RAG Support:

  * Tìm kiếm ngữ nghĩa, FAQ, semantic search.
  * Ghi chú: *“30 USD/index/tháng + 0.35 USD/giờ”* → đóng vai “search engine” nội bộ cho tài liệu doanh nghiệp, kết hợp tốt với RAG.

* **Amazon Personalize** – Recommendation:

  * Gợi ý cá nhân hóa: sản phẩm, nội dung, phân đoạn người dùng,…
  * Ghi chú: *“0.24 USD/giờ training + 0.05 USD/GB + 0.15 USD/1000 recommendation”*.

Việc nêu cụ thể **use case kèm chi phí** giúp tôi hình dung tốt hơn cách thiết kế giải pháp vừa “đúng bài toán”, vừa cân bằng được ngân sách.

### 3. Phiên “Generative AI with Amazon Bedrock” – AgentCore & Pipecat (10:45 – 12:00)

Sau phần overview, chương trình đi sâu vào **xây dựng hệ GenAI thực chiến**.

#### 3.1. Pipecat – Framework cho voice/multimodal AI agents

* **Pipecat** được giới thiệu là **pipeline framework tối ưu cho real-time voice/multimodal agents**:

  * Hỗ trợ ghép nhiều khối: speech-to-text, LLM, text-to-speech, các công cụ bên ngoài… thành một pipeline thống nhất.
  * Tối ưu cho độ trễ thấp, phù hợp các ứng dụng trợ lý giọng nói, callbot.

Điểm quan trọng tôi rút ra: thay vì “tự ráp” từng dịch vụ, có thể dùng framework như Pipecat để chuẩn hóa luồng xử lý, dễ mở rộng và maintain.

#### 3.2. Amazon Bedrock AgentCore và hệ sinh thái Agentic AI

Diễn giả **Hiếu Nghị** trình bày về **Bedrock AgentCore** và bức tranh **agentic AI systems**:

* **Từ LLM tới Agentic Systems:**

  * LLM đơn thuần chỉ “trả lời câu hỏi”.
  * Agentic system có thêm: mục tiêu, kế hoạch, khả năng gọi công cụ (tools), truy cập dữ liệu, ra quyết định nhiều bước.
  * Bedrock AgentCore được giới thiệu như **lớp điều phối** để xây dựng các agent kiểu này trên hạ tầng AWS.

* **Các framework build agents được nhắc đến:**

  * crew.ai, Google ADK, LlamaIndex, OpenAI Agents SDK, LangChain, LangGraph, Strands Agents SDK,…
  * Ý chính: hệ sinh thái rất phong phú, nhưng nếu chạy trên AWS thì AgentCore giúp **tối ưu việc tích hợp với dịch vụ AWS, bảo mật, logging, monitoring,…**

* **Các khả năng chính của Bedrock AgentCore** (dựa trên slide và ghi chú):

  * Kết nối với nhiều foundation model trên Bedrock.
  * Quản lý workflow nhiều bước, gọi tools (Lambda, API nội bộ, truy vấn dữ liệu…).
  * Hỗ trợ RAG, tích hợp với Kendra/Knowledge Base.
  * Xây dựng guardrails (chính sách nội dung, giới hạn miền trả lời).
  * Quan sát & giám sát hành vi agent khi đưa vào production.

* **Thách thức khi đưa agents vào production:**

  * Độ ổn định và khả năng dự đoán hành vi của agent.
  * Kiểm soát chi phí inference khi workflow quá phức tạp.
  * Bảo mật dữ liệu, giới hạn quyền truy cập khi agent gọi nhiều hệ thống khác nhau.
  * Logging/monitoring chi tiết để debug và cải tiến.

Phần cuối là **demo xây dựng chatbot GenAI trên Bedrock** sử dụng RAG và một số guardrails cơ bản, giúp kết nối lý thuyết với cách triển khai thực tế.

### III. Kiến thức và bài học rút ra

1. **Nhận thức rõ hơn về vai trò của GenAI trong kiến trúc hệ thống hiện đại**

   * GenAI không đứng một mình mà cần kết hợp với RAG, search, data pipeline, monitoring,…
   * Việc hiểu đúng về foundation model và prompt engineering giúp tránh kỳ vọng sai lệch và thiết kế giải pháp thực tế hơn.

2. **Nắm được hệ sinh thái dịch vụ AI trên AWS dưới góc độ “build vs. buy”**

   * Các dịch vụ như Rekognition, Textract, Comprehend, Personalize… rất phù hợp khi bài toán đã tương đối chuẩn, không cần custom quá sâu.
   * Khi cần đặc thù dữ liệu riêng (hợp đồng, tài liệu pháp lý, log nội bộ,…), thì kết hợp **Bedrock + Embeddings + Kendra/RAG** sẽ linh hoạt hơn.

3. **Quan điểm thực tế về chi phí**

   * Các con số cụ thể trong ghi chú giúp tôi hiểu rằng bài toán kỹ thuật luôn phải đi song song với bài toán kinh tế.
   * Ngay từ giai đoạn thiết kế, cần ước lượng volume (số ảnh, số ký tự, số phút audio, số request) để chọn dịch vụ và mô hình phù hợp.

4. **Tư duy “agentic” thay vì chỉ “chatbot”**

   * Khái niệm AgentCore và agentic AI systems cho thấy bước tiến tiếp theo không chỉ là hỏi–đáp, mà là **tự động hóa quy trình**: đọc dữ liệu, gọi API, ra quyết định, ghi log,…
   * Điều này mở ra nhiều hướng cho các dự án cá nhân:

     * Agent hỗ trợ phân tích hợp đồng pháp lý.
     * Agent theo dõi log hạ tầng và cảnh báo bất thường.
     * Agent hỗ trợ phân tích tài chính, gợi ý hành động dựa trên dữ liệu thời gian thực.


### IV. Định hướng áp dụng cá nhân

Sau sự kiện này, tôi định hướng:

1. **Thiết kế một pipeline RAG trên AWS** cho bài toán mình đang làm (ví dụ: phân tích hợp đồng pháp luật, tài liệu học tập):

   * Dùng Textract để trích xuất nội dung tài liệu.
   * Dùng Titan Embeddings để sinh vector và lưu vào vector store.
   * Kết nối Kendra hoặc search engine tương đương để truy xuất.
   * Sử dụng Bedrock (Claude/Llama/Titan) để xây dựng chatbot trả lời dựa trên tài liệu nội bộ.

2. **Thử nghiệm một Agent nhỏ với Bedrock AgentCore**:

   * Bước đầu: agent đọc một câu hỏi → truy vấn knowledge base → tổng hợp lại → tạo báo cáo ngắn.
   * Sau đó mở rộng: agent có thể gọi Lambda để thực hiện hành động (ví dụ tạo ticket, gửi email, cập nhật log).

3. **Rèn luyện thêm kỹ năng prompt engineering**:

   * Luyện tập các dạng prompt: zero-shot, few-shot, CoT trên chính các bài toán mình đang làm (AI/ML, DevOps, Security).
   * Ghi lại các “prompt pattern” hiệu quả thành một thư viện dùng lại cho nhiều dự án.

  
### V. Một số hình ảnh trong sự kiện

![Foundation Model](/images/4-Event/4.4-AWS/1.jpeg)
![What are Embedding?](/images/4-Event/4.4-AWS/2.jpeg)
![Amazon Titan Embedding](/images/4-Event/4.4-AWS/3.jpeg)
![RAG in action](/images/4-Event/4.4-AWS/4.jpeg)
![Data ingestion workflow](/images/4-Event/4.4-AWS/5.jpeg)
![AWS AI Service](/images/4-Event/4.4-AWS/6.jpeg)
![Lookout Family](/images/4-Event/4.4-AWS/7.jpeg)
![Pipecat](/images/4-Event/4.4-AWS/8.jpeg)