---
title: "Chuẩn bị dữ liệu nguồn"
date: "2025-09-09"
weight: 2
chapter: false
pre: " <b> 5.2.2 </b> "
---

#### Tổng quan

Khởi tạo một kho lưu trữ đối tượng (S3 Bucket) để chứa các tài liệu gốc (PDF, Word, Text). Đây đóng vai trò là "nguồn sự thật" (Source of Truth) mà Knowledge Base sẽ truy cập để đọc hiểu, phân tích và đồng bộ hóa kiến thức cho AI. Bạn có thể lưu trữ kiến thức liên quan đến lĩnh vực của bạn sử dụng trong việc tạo trợ lý cá nhân hoặc Chatbot cho riêng bạn. 

#### Chuẩn bị dữ liệu

Chúng ta sẽ tạo một S3 Bucket để lưu trữ tài liệu gốc, đóng vai trò là nguồn tri thức cho Chatbot.

**Bước 1. Tạo S3 Bucket**

- Truy cập dịch vụ [S3](https://us-east-1.console.aws.amazon.com/s3/get-started?region=us-east-1) từ thanh tìm kiếm.
- **AWS Region:** Chọn `United States (N. Virginia us-east-1)`.

> ![Truy cập S3](/images/5-Workshop/5.2-Prerequisite/04_S3.jpg)

- Click **Create bucket**.

> ![Create S3 Bucket](/images/5-Workshop/5.2-Prerequisite/05_S3_Create_Bucket.jpg)


- Cấu hình thông tin Bucket:
    - **Bucket Type:** Chọn `General purpose`
    - **Bucket name:** Nhập `rag-workshop-demo`
    - **Object Ownership:** Giữ mặc định `ACLs disabled`.
    - **Block Public Access settings:** Giữ mặc định (Đã chọn `Block all public access`).

> ![Configure S3 Bucket](/images/5-Workshop/5.2-Prerequisite/06_Configure_S3_Bucket.jpg)

- Kéo xuống cuối trang, Click **Create bucket**.

> ![Ảnh minh họa giao diện tạo S3 Bucket và chọn Region](/images/5-Workshop/5.2-Prerequisite/07_Finished_Create_bucket.jpg)

- Kiểm tra tạo S3 Bucket thành công.

> ![Create S3 Bucket Successful](/images/5-Workshop/5.2-Prerequisite/08_Create_S3_Successful.jpg)

**Bước 2. Tải lên tài liệu mẫu**
- Tài liệu mẫu, liên quan để tổng quan về kiến thức điện toán đám mây của AWS. 

_📊 <a href="/files/2-Proposal/pricing.csv" download>Tệp định dạng CSV</a>_

- Tại danh sách Buckets, Click vào **tên bucket** bạn vừa tạo.
- Click **Upload**.
- Tại giao diện Upload:
  - Click **Add files**.
  - Chọn file tài liệu mẫu từ máy tính của bạn (Khuyên dùng file PDF hoặc Word có nhiều nội dung văn bản).
- Kéo xuống cuối trang, Click **Upload**.
- Khi thấy thông báo màu xanh "Upload succeeded", Click **Close**.

> ![Ảnh minh họa giao diện upload file thành công](link_anh_upload_file_o_day)