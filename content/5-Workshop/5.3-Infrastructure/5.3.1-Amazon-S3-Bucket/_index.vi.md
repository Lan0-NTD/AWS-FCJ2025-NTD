---
title : "Tạo Amazon S3 Bucket"
weight : 1
chapter : false
pre : " <b> 5.3.1. </b> "
---

Trong bước này, chúng ta sẽ tạo một S3 Bucket để lưu trữ tài liệu hợp đồng mẫu và các dữ liệu vector cần thiết cho AI.

#### 1. Tạo Bucket

1.  Truy cập dịch vụ **S3** trên AWS Console.
2.  Chọn nút màu cam **Create bucket**.
3.  **General configuration**:
    *   **Bucket type**: Chọn General purpose.
    *   **Bucket name**: Đặt một tên duy nhất toàn cầu (ví dụ: `contract-app-demo`).
    *   *Lưu ý: Tên bucket chỉ được dùng chữ thường, số và dấu gạch ngang, không dùng chữ hoa.*
4.  Kéo xuống dưới cùng, các thiết lập khác giữ nguyên mặc định.
5.  Bấm **Create bucket**.

![alt text](/images/5-Workshop/5.3-Infrastructure/3.1.png)
![alt text](/images/5-Workshop/5.3-Infrastructure/3.2.png)


#### 2. Tạo cấu trúc thư mục

Sau khi tạo xong, chúng ta cần tạo cấu trúc thư mục để tổ chức dữ liệu.

1.  Bấm vào tên **Bucket** bạn vừa tạo để truy cập vào bên trong.
2.  Bấm nút **Create folder**.
3.  Lần lượt tạo **4 thư mục** với tên chính xác như sau (bạn cần lặp lại thao tác tạo folder 4 lần):
    *   `contract-templates`
    *   `index`
    *   `legal-corpus`
    *   `user-data`

Sau khi tạo xong, cấu trúc bucket của bạn sẽ trông như sau:

![alt text](/images/5-Workshop/5.3-Infrastructure/3.3.png)

#### 3. Upload dữ liệu mẫu

Sử dụng các file trong thư mục source code `contract-demo` mà bạn đã tải về máy tính ở phần Chuẩn bị:

1.  Truy cập vào folder `contract-templates` trên S3 -> Bấm **Upload** -> Chọn các file mẫu hợp đồng (.docx/.pdf) từ máy tính -> Bấm **Upload**.
2.  Truy cập vào folder `index` trên S3 -> Bấm **Upload** -> Chọn file `template_metadata.jsonl`.
3.  Truy cập vào folder `legal-corpus` trên S3 -> Bấm **Upload** -> Chọn file dữ liệu luật (nếu có trong source code).

![alt text](/images/5-Workshop/5.3-Infrastructure/3.4.png)


Sử dụng các file trong thư mục source code `contract-demo` mà bạn đã tải về máy tính ở phần Chuẩn bị. Thực hiện upload theo cấu trúc sau:

1.  Truy cập vào folder `index` trên S3 -> Bấm **Upload** -> Chọn file `template_metadata.jsonl` -> Bấm **Upload**.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.5.png)
2.  Truy cập vào folder `legal-corpus` trên S3. Tại đây, hãy tạo thêm 2 thư mục con là `index` và `raw-documents`.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.6.png)
    *   Truy cập vào folder con `index` -> Bấm **Upload** -> Chọn file `legal_chunks_with_emb.jsonl` (hoặc `legal_metadata.json`).
![alt text](/images/5-Workshop/5.3-Infrastructure/3.7.png)
    *   Truy cập vào folder con `raw-documents` -> Bấm **Upload** -> Chọn các file tài liệu luật gốc (nếu có).
