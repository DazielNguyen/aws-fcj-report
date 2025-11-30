---
title: "Kiểm tra truy cập Model"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 5.2.1 </b> "
---

#### Tổng quan

Theo chính sách mới của AWS, các mô hình nền tảng (Foundation Models) thường được tự động kích hoạt. Tuy nhiên, đối với các mô hình của đối tác thứ ba như **Anthropic (Claude)**, người dùng lần đầu tiên sử dụng tại một Region mới bắt buộc phải khai báo thông tin sử dụng (Use Case) mới có thể gọi được mô hình.

Đảm bảo tài khoản AWS của bạn có quyền truy cập và sử dụng mô hình **Anthropic Claude 3 Sonnet**. Đây là bước bắt buộc để tránh lỗi `AccessDenied` khi Chatbot hoạt động sau này. Nếu đây là lần đầu tiên bạn sử dụng model này tại Region mới, bạn cần thực hiện khai báo mục đích sử dụng (Use Case).

#### Kiểm tra truy cập

Chúng ta sẽ thực hiện một bài kiểm tra nhanh (Test Run) để đảm bảo tài khoản của bạn đã sẵn sàng.

**Bước 1. Truy cập Chat Playground**

- Tại menu bên trái Bedrock Console, tìm mục **Playgrounds**.
- Click **Chat**.

> ![Ảnh minh họa menu Playgrounds bên trái](link_anh_menu_playgrounds_o_day)

**Bước 2. Chọn Model kiểm thử**

- Click **Select model** (phía trên khung chat).
- Category: Chọn **Anthropic**.
- Model: Chọn **Claude 3 Sonnet** (hoặc Claude 3.5 Sonnet).
- Throughput: Chọn **On-demand**.
- Click **Apply**.

> ![Ảnh minh họa bảng chọn Model Claude 3](link_anh_chon_model_o_day)

**Bước 3. Gửi tin nhắn kích hoạt**

- Trong khung chat: Nhập `Hello`.
- Click **Run**.
- **Quan sát kết quả:**
  - Nếu AI trả lời: **Thành công** (Chuyển ngay sang phần 2.3).
  - Nếu hiện lỗi màu đỏ hoặc popup "Submit use case details": **Cần khai báo thông tin** (Làm tiếp bước 4 bên dưới).

> ![Ảnh minh họa giao diện chat và thông báo lỗi nếu có](link_anh_chat_test_o_day)

**Bước 4. Khai báo Use Case (Chỉ thực hiện nếu gặp lỗi ở bước 3)**

- Click **Submit use case details** (trong thông báo lỗi).
- Điền biểu mẫu:
  - Company Name: Nhập `Personal Learning`.
  - Industry: Chọn `Technology`.
  - Intended Use: Chọn `Research & Development`.
- Click **Submit**.
- Đợi 1 phút, quay lại khung chat, Click **Run** lại tin nhắn `Hello` để xác nhận thành công.

> ![Ảnh minh họa form điền thông tin Use Case](link_anh_form_use_case_o_day)