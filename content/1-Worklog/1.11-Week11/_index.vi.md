---
title: "Worklog Tuần 11"
date: "2025-11-17"
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

- Phát hiện và xử lý nhiều giao dịch phức tạp
- Tích hợp hỗ trợ file PDF cho Bill OCR
- Triển khai hệ thống feedback và fine-tuning models
- Nâng cao chất lượng xử lý hình ảnh và âm thanh
- Tích hợp Backend và lưu trữ MongoDB
- Automated testing và deployment Docker
- Làm quen với AWS và các công cụ quản lý

### Các công việc cần triển khai trong tuần này:

| Thứ 	| Công việc 	| Ngày bắt đầu 	| Ngày kết thúc 	| Nguồn tài liệu và ghi chú học tập 	|
|---	|---	|---	|---	|---	|
| 2 	| Phát hiện nhiều giao dịch và hỗ trợ PDF<br>- Phân tích cú pháp đa giao dịch phức tạp<br>- Tinh chỉnh thuật toán phát hiện đa giao dịch:<br>- Phát hiện phân công jar trong cụm từ<br>- Xử lý các loại giao dịch hỗn hợp:<br><br>Kiểm tra các cụm từ phức tạp<br>- Kiểm tra 1 giao dịch với 1 hủ<br>- Kiểm tra nhiều giao dịch<br>- Kiểm thử chuyển đổi giữa các hủ<br>- Kiểm thử các ngữ cảnh hỗn hợp<br><br>Cải thiện thêm hỗ trợ file PDF cho phần Bill<br>- Cài đặt các thư viện<br>- Kiểm thử giao dịch với file PDF 	| 17/11/2025 	| 17/11/2025 	| [Sprint 03 - Day 11](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-3/day-11.md) 	|
| 3 	| Hệ thống phản hồi và học tập của người dùng<br>- Xử lý hệ thống feedback từ user của phần Voice<br>- Xử lý hệ thống feedback từ user của phần Bill<br>- Fine-tuning các model dựa trên các feedback<br>- Cải thiện các cú pháp khi nhập vào sai<br>Kiểm tra độ cải thiện của 2 mô hình Voice và Test 	| 18/11/2025 	| 18/11/2025 	| [Sprint 03 - Day 12](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-3/day-12.md) 	|
| 4 	| Xử lý hình ảnh/âm thanh nâng cao <br>- Phát hiện và nâng cao chất lượng Bill<br>- Detect chất lượng ảnh<br>- Tự động xoay và nghiên ảnh<br>- Phát hiện ROI (Vùng quan tâm)<br>- Tích hợp với OCR Pipeline<br>- Kiểm thử<br><br>Xử lý tiếng ồn nền của Voice<br>- Triển khai giảm noise<br>- Phát hiện hoạt động giọng nói<br>- Cắt phần im lặng<br>- Giảm thời gian xử lý<br>- Tích hợp với Voice Pipeline<br>- Kiểm thử 	| 19/11/2025 	| 19/11/2025 	| [Sprint 03 - Day 13](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-3/day-13.md) 	|
| 5 	| Tích hợp Backend & Lưu trữ Tệp<br>Tích hợp dịch vụ giao dịch phụ trợ<br>- Review về Backend API<br>- Test AI và Backend flow<br>- Xác minh mức tiêu thụ sự kiện<br>- Kiểm tra việc tạo giao dịch tự động<br>- Khắc phục sự cố tích hợp<br><br>Tích hợp lưu trữ trên MongoDB<br>- Thiết lập Database cho Voice và Bill<br>- Chuẩn bị cho việc tích hợp cùng với S3 của Amazon<br><br> 	| 20/11/2025 	| 20/11/2025 	| [Sprint 03 - Day 14](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-3/day-14.md) 	|
| 6 	| Tạo thử nghiệm tự động<br>- Tạo test cho Voice và Bill<br>- Nghiệm thu và kiểm tra tất các cá kiểm tra<br>- Sửa lỗi<br>- Kiểm tra hồi quy đầy đủ<br><br>Setup và Deploy lên Docker 	| 21/11/2025 	| 21/11/2025 	| [Sprint 03 - Day 15](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-3/day-15.md) 	|

### Kết quả đạt được tuần 11:

#### 1. Phát Hiện Nhiều Giao Dịch và Hỗ Trợ PDF
- Phân tích cú pháp đa giao dịch phức tạp
- Tinh chỉnh thuật toán phát hiện đa giao dịch
- Phát hiện phân công jar trong cụm từ
- Xử lý các loại giao dịch hỗn hợp

**Kiểm Tra Cụm Từ Phức Tạp:**
- Kiểm tra 1 giao dịch với 1 hủ
- Kiểm tra nhiều giao dịch
- Kiểm thử chuyển đổi giữa các hủ
- Kiểm thử các ngữ cảnh hỗn hợp

**Hỗ Trợ PDF:**
- Cài đặt các thư viện xử lý PDF
- Kiểm thử giao dịch với file PDF
- Tích hợp PDF vào OCR Pipeline

#### 2. Hệ Thống Phản Hồi và Học Tập
- Xử lý hệ thống feedback từ user của phần Voice
- Xử lý hệ thống feedback từ user của phần Bill
- Fine-tuning các model dựa trên feedback
- Cải thiện xử lý các cú pháp nhập vào sai
- Kiểm tra độ cải thiện của 2 mô hình Voice và Bill

#### 3. Xử Lý Hình Ảnh/Âm Thanh Nâng Cao
**Nâng Cao Chất Lượng Bill:**
- Phát hiện và đánh giá chất lượng ảnh
- Tự động xoay và nghiêng ảnh
- Phát hiện ROI (Region of Interest/Vùng quan tâm)
- Tích hợp với OCR Pipeline
- Kiểm thử với nhiều điều kiện ảnh khác nhau

**Xử Lý Tiếng Ồn Nền Voice:**
- Triển khai giảm noise (Noise Reduction)
- Phát hiện hoạt động giọng nói (Voice Activity Detection)
- Cắt phần im lặng (Silence Trimming)
- Giảm thời gian xử lý
- Tích hợp với Voice Pipeline
- Kiểm thử với nhiều môi trường âm thanh

#### 4. Tích Hợp Backend & Lưu Trữ
**Tích Hợp Backend:**
- Review Backend API endpoints
- Test AI và Backend workflow
- Xác minh mức tiêu thụ sự kiện (Event Consumption)
- Kiểm tra việc tạo giao dịch tự động
- Khắc phục sự cố tích hợp

**Tích Hợp MongoDB:**
- Thiết lập Database cho Voice và Bill
- Chuẩn bị schema cho tích hợp với S3 của Amazon
- Triển khai storage strategy

#### 5. Testing Tự Động và Deployment
- Tạo automated tests cho Voice và Bill
- Nghiệm thu và kiểm tra tất cả test cases
- Sửa lỗi phát hiện từ testing
- Kiểm tra hồi quy đầy đủ (Full Regression Testing)
- Setup Docker environment
- Deploy lên Docker container

#### 6. AWS Learning
- Hiểu AWS và các nhóm dịch vụ cơ bản (Compute, Storage, Networking, Database)
- Tạo và cấu hình AWS Free Tier account
- Làm quen với AWS Management Console
- Cài đặt và cấu hình AWS CLI (Access Key, Secret Key, Region)
- Thực hiện các thao tác cơ bản với AWS CLI
- Kết nối và làm quen với cộng đồng First Cloud Journey

**Tổng kết:** Tuần 11 đã hoàn thành việc nâng cao khả năng xử lý đa giao dịch, tích hợp hỗ trợ PDF, triển khai hệ thống feedback và fine-tuning models. Đã cải thiện đáng kể chất lượng xử lý ảnh/âm thanh với các kỹ thuật nâng cao (ROI detection, noise reduction, VAD), tích hợp thành công với Backend và MongoDB, đồng thời hoàn tất automated testing và deployment lên Docker. Bên cạnh đó, đã làm quen với AWS ecosystem và các công cụ quản lý cơ bản, chuẩn bị cho việc triển khai cloud infrastructure.

