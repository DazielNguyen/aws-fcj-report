---
title: "Worklog Tuần 9"
date: "2025-11-03"
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:

- Dự án FastAPI với MongoDB
- Thư viện STT tiếng Việt được lựa chọn và tích hợp
- Thư viện OCR tiếng Việt được lựa chọn và thử nghiệm
- Trích xuất NLP: số lượng, danh mục, ngày tháng, phát hiện jar (REQ-027)
- Phát hiện nhiều giao dịch (REQ-027)
- Xuất bản sự kiện lên RabbitMQ

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu và ghi chú học tập                                                                      |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ------------- | ------------------------------------------------------------------------------------------------------ |
| 2   | Thiết lập dự án <br>- Tạo cấu trúc dự án FastAPI (/app, /models, /services, /utils, /routers, /schemas, /ai-models)<br>- Thiết lập môi trường ảo (Python 3.11 trở lên)<br>- Cài đặt FastAPI, Uvicorn, Pydantic<br>- Cài đặt MongoDB cục bộ (Docker)<br>- Tạo cơ sở dữ liệu: ai_service_db (được cấu hình trong docker-compose.yml)<br>- Thu thập bộ dữ liệu: Bills, Voices (sử dụng mô hình MongoEngine)<br>- Thiết lập kết nối MongoDB với MongoEngine<br>- Kiểm tra kết nối (quản lý vòng đời trong database.py)<br>Nghiên cứu công nghệ <br>- Về phần Bill: Thử các loại mô hình OCR giải quyết được vấn đề triết xuất tiếng Việt tốt nhất. <br>- Về phần Voice: Tìm kiếm các loại mô hình Speech-to-Text, bằng ngôn ngữ Tiếng Việt.                                                                                                             | 03/11/2025   | 03/11/2025    | [Sprint 01 - Day 01](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-1/day-1.md) |
| 3   | Cấu trúc API cốt lõi và điểm cuối<br>- Cơ sở hạ tầng API dùng chung<br>- Thiết lập các API của Voice và Bill<br>- Tạo cấu trúc điểm cuối API cơ bản<br>- Thiết lập mô hình Pydantic cho yêu cầu/phản hồi<br>- Thêm phần mềm trung gian CORS<br>- Thêm phần mềm trung gian xử lý lỗi<br>- Tạo điểm cuối kiểm tra tình trạng (GET /health)<br>- Thiết lập ghi nhật ký (structlog)                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | 04/11/2025   | 04/11/2025    | [Sprint 01 - Day 02](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-1/day-2.md) |
| 4   | Quy trình Xử lý Giọng nói<br>- Cài đặt Thư viện STT tiếng Việt<br>- Tiền xử lý âm thanh<br>- Tích hợp Giọng nói thành Văn bản<br>- Triển khai chức năng STT<br>- Kiểm tra Voice Model<br><br>Chuẩn bị OCR cho extract Bill<br>- Cài đặt thư viện OCR đã chọn từ Ngày 1<br>- Nghiên cứu các kỹ thuật tiền xử lý ảnh<br>- Tạo quy trình tiền xử lý mẫu<br>- Thử nghiệm với hình ảnh bill                                                                                                                                                                                                                                                                                                                                                                                                                                                              | 05/11/2025   | 05/11/2025    | [Sprint 01 - Day 03](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-1/day-3.md) |
| 5   | Xử lý Text cho ngôn ngữ Tiếng Việt<br>- Test độ chính xác của mô hình, và chọn mô hình phù hợp, và nhóm dùng mô hình PhoWhisper của VinAI<br>- Kiểm tra detect của mô hình, có nhận được giọng nói và trả về Text hay không. <br>- Chỉnh sửa Endpoint của kết quả cuối có trả về đúng các category mà nhóm đưa ra hay không. <br>- Thử nghiệm xử lý nhiều giao dịch cùng lúc, mô hình có nhận được không. <br>- Thiết lập detect được thời gian của người nói về giao dịch<br>- Tạo đối tượng giao dịch<br><br>Tiền xử lý OCR<br>- Xử lý ảnh khi người dùng nhập vào và xử lý hóa đơn đó. Tạo cho ảnh đó đạt chất lượng tốt nhất trước khi đưa cho mô hình OCR xử lý. <br>- Thu thập các hóa đơn ở Việt Nam như ( hóa đơn điện, hóa đơn các trung tâm thương mại, hóa đơn các quán ăn, hóa đơn các cửa hàng tiện lợi, hóa đơn các quán cà phê, ...) | 06/11/2025   | 06/11/2025    | [Sprint 01 - Day 04](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-1/day-4.md) |
| 6   | Tích hợp và Kiểm thử<br>- Xử lý các công việc nền của Voice và Bill<br>- Thiết lập xuất bản sự kiện<br>Speech to Text<br>- Kiểm thử đầu cuối của Voice<br>- Các quy trình chạy như Ghi âm -> Xử lý -> Trả Endpoint, kiểm tra và cải thiện độ chính xác của xử lý Voice đã ổn chưa<br>Bill Detection<br>- Triển khai nghiệm thử các mô hình OCR, teseract, easyOCR,...                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | 07/11/2025   | 07/11/2025    | [Sprint 01 - Day 05](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-1/day-5.md) |

### Kết quả đạt được tuần 9:

#### 1. Thiết lập Dự án và Hạ tầng

- Hoàn thành cấu trúc dự án FastAPI với các thư mục chuẩn (/app, /models, /services, /utils, /routers, /schemas, /ai-models)
- Thiết lập môi trường Python 3.11+ với môi trường ảo
- Cài đặt và cấu hình MongoDB cục bộ sử dụng Docker
- Tạo cơ sở dữ liệu `ai_service_db` và thu thập bộ dữ liệu Bills và Voices
- Thiết lập kết nối MongoDB với MongoEngine và quản lý vòng đời kết nối

#### 2. Cấu trúc API và Middleware

- Thiết lập các API endpoint cho Voice và Bill processing
- Tạo mô hình Pydantic cho request/response validation
- Cấu hình CORS middleware và error handling middleware
- Triển khai health check endpoint (GET /health)
- Tích hợp structlog cho logging system

#### 3. Xử lý Giọng nói (Speech-to-Text)

- Nghiên cứu và lựa chọn mô hình **PhoWhisper của VinAI** cho STT tiếng Việt
- Triển khai tiền xử lý âm thanh và tích hợp Voice-to-Text
- Kiểm tra độ chính xác của mô hình và khả năng detect giọng nói
- Cấu hình endpoint trả về đúng các category đã định nghĩa
- Thử nghiệm xử lý nhiều giao dịch cùng lúc
- Thiết lập phát hiện thời gian giao dịch từ giọng nói
- Tạo đối tượng giao dịch từ dữ liệu voice

#### 4. Xử lý Hóa đơn (OCR)

- Nghiên cứu và lựa chọn thư viện OCR phù hợp (Tesseract, EasyOCR)
- Triển khai tiền xử lý ảnh để tối ưu chất lượng trước khi OCR
- Thu thập bộ dữ liệu hóa đơn Việt Nam đa dạng (điện, siêu thị, quán ăn, cửa hàng tiện lợi, cà phê)
- Thử nghiệm các mô hình OCR với hóa đơn thực tế

#### 5. Trích xuất NLP và Xử lý Dữ liệu

- Triển khai trích xuất thông tin: số lượng, danh mục, ngày tháng (REQ-027)
- Phát hiện jar detection
- Xử lý phát hiện nhiều giao dịch trong một request

#### 6. Tích hợp RabbitMQ

- Thiết lập xuất bản sự kiện lên RabbitMQ
- Xử lý các công việc nền (background tasks) cho Voice và Bill

#### 7. Testing và Quality Assurance

- Kiểm thử end-to-end cho Voice processing pipeline (Ghi âm → Xử lý → Trả Endpoint)
- Đánh giá và cải thiện độ chính xác của xử lý Voice
- Kiểm thử các mô hình OCR với dataset thực tế

**Tổng kết:** Tuần 9 đã hoàn thành đầy đủ các mục tiêu đề ra, bao gồm thiết lập hạ tầng dự án FastAPI-MongoDB, tích hợp mô hình PhoWhisper cho STT tiếng Việt, triển khai OCR cho xử lý hóa đơn, và thiết lập hệ thống event publishing với RabbitMQ. Các chức năng NLP cho trích xuất thông tin giao dịch đã được triển khai và kiểm thử thành công.
