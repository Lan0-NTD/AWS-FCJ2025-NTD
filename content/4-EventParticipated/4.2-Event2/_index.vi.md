---
title: "AI-Driven Development Life Cycle"
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---
# **Reimagining Software Engineering**

**Địa điểm**: AWS Event Hall, L26 Bitexco Tower, HCMC  
**Thời gian**: 2PM – 4:30PM Thứ Sáu, ngày 03 tháng 10 năm 2025

## **Mục Đích Của Sự Kiện**

* Khám phá sự chuyển đổi của Software Development Lifecycle (SDLC) trong kỷ nguyên GenAI.  
* Giới thiệu mô hình AI-Driven Development Lifecycle (AI-DLC) và cách áp dụng trong các dự án thực tế.  
* Trình diễn công cụ Amazon Q Developer và KIRO – AI IDE hỗ trợ từ prototype đến production.  
* Chia sẻ best practices để developers và doanh nghiệp kiểm soát chất lượng khi ứng dụng AI vào toàn bộ quy trình phát triển phần mềm.

## **Danh Sách Diễn Giả**

* **Toan Huynh** – Senior Specialist Solutions Architect, AWS  
* **My Nguyen** – Senior Prototyping Architect, AWS

## **Nội Dung Nổi Bật**

### **1\. AI-Driven Development Life Cycle & Amazon Q Developer \- Toan Huynh**

#### **Sự phát triển của AI và tác động đến SDLC**

* Tiến hóa của AI: **auto-complete → assistant → agents**.  
* Mỗi giai đoạn đều thay đổi cách developers học, viết code, test, triển khai và vận hành phần mềm.  
* Dù AI hỗ trợ sâu, **developer vẫn phải là owner** của sản phẩm: quyết định, phê duyệt chất lượng, chịu trách nhiệm chuyên môn.

#### **Hai phương pháp developers sử dụng AI**

* **AI-assisted:** dùng AI cho các tác vụ hẹp → vẫn hạn chế, không đủ bao quát cả quy trình.  
* **AI-managed:** AI tham gia toàn bộ quá trình, phối hợp nhiều agents đảm nhiệm nhiều vai trò khác nhau → mô hình tương lai.

#### **7 vấn đề khi dùng AI → sự ra đời của AI-DLC**

* AI-DLC nằm **giữa AI-Assisted và AI-Managed**.  
* Trong AI-DLC, AI hỗ trợ nhiều task hơn:  
  * Planning  
  * Architecture suggestions  
  * Clarifying requirements  
  * Generating scaffolding  
  * Refactoring  
  * Testing flows

**Nhưng:** developers vẫn phải đảm bảo:

* Expertise  
* Decisions  
* Judgment  
* Validation

#### **Core Concepts of AI-DLC**

1. **Mob development**:  
   * Mob Elaboration  
   * Mob Construction  
2. **Spec-driven development**: hiệu quả nhưng khó tùy biến khi bài toán phức tạp.  
3. **Mỗi stage cần rõ ràng** về context – input – output.  
4. Khi làm việc với AI cần yêu cầu **ghi log quá trình** (không chỉ output cuối).  
5. Cần mô tả rõ ràng cho AI:  
   * Nêu rõ bạn cần gì  
   * Cung cấp tài liệu liên quan  
   * Không nên prompt kiểu “đừng làm ABC”  
6. AI hoạt động tốt trong các tác vụ cần tính chuẩn chỉnh, cấu trúc rõ → nên tận dụng vào những phần này.

#### **Ghi chú quan trọng từ diễn giả**

* Luôn yêu cầu AI tạo **plan**, sau đó review–refine–repeat liên tục.  
* Chia nhỏ yêu cầu trước khi giao cho AI.  
* Tạo **nhiều session tách biệt** cho từng task để tránh nhiễu context.

### **2\. KIRO – AI IDE for Prototype to Production \- My Nguyen**

#### **Giới thiệu KIRO**

* AI IDE được thiết kế cho luồng **spec → prototype → production**.  
* Hỗ trợ spec-driven development **tích hợp ngay trong IDE**.  
* UI trực quan, dễ quan sát toàn bộ workflow của dự án.

#### **Tính năng nổi bật**

* Agent hooks  
* Advanced context management  
* Tracking workflow  
* Tối ưu cho dự án nhỏ (ít tài liệu hơn so với AI-DLC truyền thống)

#### **Tích hợp AI-DLC trong KIRO**

* Có thể áp dụng methodology AI-DLC bằng cách:  
  * Tạo thư mục *steering*  
  * Đặt workflow AI-DLC (file .md) hoặc *rules* của công ty  
* Tương thích VSCode, Claude models và nhiều công nghệ mới.

#### **Điểm chung của hai phương pháp**

Cả AI-DLC và KIRO đều **dựa trên domain-driven design (DDD)** để đảm bảo rõ ràng về boundary, context và logic nghiệp vụ.

## **Những Gì Học Được**

#### **Tư duy thiết kế AI-driven**

* AI có thể tự động hóa phần lớn tác vụ SDLC, nhưng con người chịu trách nhiệm cuối cùng.  
* Cần thiết kế quy trình rõ ràng: context → inputs → outputs → validation.

#### **Quy trình kỹ thuật**

* AI-DLC giúp tự động hóa từ planning đến testing.  
* Mob development \+ spec-driven giúp củng cố sự minh bạch và kiểm soát chất lượng.  
* Nên lưu lại toàn bộ quá trình AI reasoning để tiện kiểm chứng.

#### **Cách làm việc hiệu quả với AI**

* Yêu cầu AI lập kế hoạch chi tiết trước khi làm.  
* Chia nhỏ vấn đề.  
* Tránh nhồi nhét quá nhiều vào một phiên làm việc.  
* Tận dụng thế mạnh AI ở các phần có cấu trúc, yêu cầu tính nhất quán.

#### **Công cụ**

* Amazon Q Developer hỗ trợ automation xuyên suốt SDLC.  
* KIRO phù hợp cho các sản phẩm nhỏ và yêu cầu nhanh về prototype–to–production.

## **Ứng Dụng Vào Công Việc**

* Áp dụng AI-DLC vào quy trình hiện tại để giảm thời gian lập kế hoạch, thiết kế và review.  
* Sử dụng Amazon Q Developer để tăng tốc coding, kiến trúc và test.  
* Dùng KIRO cho các dự án yêu cầu xây nhanh prototype hoặc tính trực quan cao.  
* Thiết lập workflow rõ ràng \+ ghi lại reasoning để đảm bảo kiểm soát chất lượng khi AI tham gia sâu vào SDLC.

## **Trải Nghiệm Trong Sự Kiện**

Buổi học đem lại góc nhìn rõ ràng về cách GenAI đang thay đổi software engineering.  
Các diễn giả cung cấp phương pháp thực tế, công cụ hiện đại, và hướng triển khai phù hợp cho mọi quy mô dự án.  
Việc kết hợp Amazon Q Developer và KIRO tạo nên bức tranh trọn vẹn về AI-driven development – từ enterprise workflows đến prototype builds.

### **Một số hình ảnh khi tham gia sự kiện**

![1](/images/4-Event/4.3-AWS/1.jpeg)
![2](/images/4-Event/4.3-AWS/2.jpeg)
![3](/images/4-Event/4.3-AWS/3.jpeg)
![4](/images/4-Event/4.3-AWS/4.jpeg)
![5](/images/4-Event/4.3-AWS/5.jpeg)
