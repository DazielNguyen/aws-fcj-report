---
title: "Chuẩn bị dữ liệu nguồn"
date: "2025-09-09"
weight: 2
chapter: false
pre: " <b> 5.2.2 </b> "
---

#### Tổng quan

Khởi tạo một kho lưu trữ đối tượng (S3 Bucket) để chứa các tài liệu gốc (PDF, Word, Text). Đây đóng vai trò là "nguồn sự thật" (Source of Truth) mà Knowledge Base sẽ truy cập để đọc hiểu, phân tích và đồng bộ hóa kiến thức cho AI.

#### Chuẩn bị dữ liệu

Chúng ta sẽ tạo một S3 Bucket để lưu trữ tài liệu gốc, đóng vai trò là nguồn tri thức cho Chatbot.

**Bước 1. Tạo S3 Bucket**

- Truy cập dịch vụ **S3** từ thanh tìm kiếm.
- Click **Create bucket**.
- Cấu hình thông tin Bucket:
  - **Bucket name:** Nhập `rag-workshop-<tên-bạn>` (Lưu ý: Viết thường, không dấu, không khoảng trắng. Ví dụ: `rag-workshop-nam-2024`).
  - **AWS Region:** Chọn `N. Virginia us-east-1`.
  - **Object Ownership:** Giữ mặc định `ACLs disabled`.
  - **Block Public Access settings:** Giữ mặc định (Đã chọn `Block all public access`).
- Kéo xuống cuối trang, Click **Create bucket**.

> ![Ảnh minh họa giao diện tạo S3 Bucket và chọn Region](link_anh_create_bucket_o_day)

**Bước 2. Tải lên tài liệu mẫu**

- Tại danh sách Buckets, Click vào **tên bucket** bạn vừa tạo.
- Click **Upload**.
- Tại giao diện Upload:
  - Click **Add files**.
  - Chọn file tài liệu mẫu từ máy tính của bạn (Khuyên dùng file PDF hoặc Word có nhiều nội dung văn bản).
- Kéo xuống cuối trang, Click **Upload**.
- Khi thấy thông báo màu xanh "Upload succeeded", Click **Close**.

> ![Ảnh minh họa giao diện upload file thành công](link_anh_upload_file_o_day)