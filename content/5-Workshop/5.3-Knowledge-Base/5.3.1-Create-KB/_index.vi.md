---
title: "Khởi tạo Knowledge Base"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 5.3.1 </b> "
---

#### Mục tiêu

Chúng ta sẽ sử dụng Amazon Bedrock Wizard để thiết lập toàn bộ kiến trúc RAG. Quá trình này sẽ kết nối nguồn dữ liệu S3, mô hình Embedding và tự động khởi tạo kho lưu trữ Vector (OpenSearch Serverless).

#### Các Bước Thực hiện

1.  Đăng nhập vào **AWS Management Console** và truy cập dịch vụ **Amazon Bedrock**.
2.  Trong menu bên trái, chọn **Knowledge bases**.
3.  Nhấp vào nút **Create knowledge base** ở góc trên bên phải của màn hình.

> ![Hình minh họa nút Create Knowledge Base trên giao diện Bedrock](link_anh_create_kb_button)

**Bước 1: Cấu hình Knowledge Base**

Trên màn hình cấu hình đầu tiên:

1.  **Knowledge base name:** Nhập tên cho knowledge base (Ví dụ: `kb-workshop-<ten-cua-ban>`).
2.  **IAM permissions:** Chọn tùy chọn **Create and use a new service role**.
3.  **Service role name:** Giữ giá trị mặc định do AWS đề xuất (bắt đầu bằng `AmazonBedrockExecutionRoleForKnowledgeBase_...`).
4.  Nhấp **Next**.

> ![Hình minh họa Bước 1: Nhập tên KB và chọn IAM Role](link_anh_step1_details)

**Bước 2: Cấu hình Nguồn Dữ liệu**

Kết nối đến S3 Bucket chứa các tài liệu:

1.  **Data source name:** Nhập tên nguồn dữ liệu (Ví dụ: `s3-datasource`).
2.  **S3 URI:**
    - Nhấp vào nút **Browse S3**.
    - Trong cửa sổ pop-up, chọn bucket `rag-workshop-<ten-cua-ban>` mà bạn đã tạo trong phần trước.
    - Nhấp **Choose**.
3.  Nhấp **Next**.

> ![Hình minh họa Bước 2: Chọn S3 Bucket làm nguồn dữ liệu](link_anh_step2_datasource)

**Bước 3: Lưu trữ & Xử lý**

Đây là bước quan trọng nhất để xác định mô hình AI và vị trí lưu trữ vector:

1.  **Embeddings model:**
    - Nhấp **Select model**.
    - Chọn model: **Titan Embeddings G1 - Text v2**.
2.  **Vector database:**
    - Chọn tùy chọn: **Quick create a new vector store - Recommended**.
    - _Lưu ý:_ Tùy chọn này cho phép AWS tự động tạo một cluster **Amazon OpenSearch Serverless** để lưu trữ dữ liệu, giúp bạn không phải quản lý cơ sở hạ tầng thủ công.
3.  Nhấp **Next**.

> ![Hình minh họa Bước 3: Chọn Titan Embeddings v2 và Quick Create Vector Store](link_anh_step3_storage)

**Bước 4: Xem xét và Tạo Knowledge Base**

1.  Xem xét tất cả thông tin cấu hình trên trang Review.
2.  Đảm bảo các mục S3 URI và Model đều chính xác.
3.  Cuộn xuống cuối trang và nhấp vào nút **Create knowledge base**.

> ![Hình minh họa Bước 4: Màn hình xem xét và nút Create](link_anh_step4_review)

**Bước 5: Chờ Khởi tạo**

Sau khi nhấp Create, hệ thống sẽ bắt đầu quá trình khởi tạo cơ sở hạ tầng nền cho Vector Store.

- **Thời gian chờ:** Khoảng **2 - 5 phút**.
- **Lưu ý:** Vui lòng không đóng trình duyệt trong thời gian này.
- **Thành công:** Khi màn hình hiển thị thông báo màu xanh **"Knowledge base created successfully"**, bạn đã hoàn thành bước này và sẵn sàng cho phần tiếp theo.

> ![Hình minh họa màn hình thông báo thành công màu xanh](link_anh_step5_success)
