---
title: "Worklog Tuần 10"
date: "2025-11-10"
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

- Cải tiến và tối ưu hóa mô hình OCR cho nhiều loại hóa đơn
- Nâng cao chất lượng xử lý Voice với số tiếng Việt và cụm từ ghép
- Triển khai hệ thống Confidence Scoring cho cả Voice và Bill
- Phát hiện danh mục thông minh và nhận dạng ngữ cảnh
- Xử lý lỗi toàn diện và tối ưu hiệu suất
- Kiểm thử đa chiều với các trường hợp edge cases

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu và ghi chú học tập                                                                       |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ------------- | ------------------------------------------------------------------------------------------------------- |
| 2   | - Tham gia Cloud Mastery Series #2<br><br>Cải tiến thêm đôi chút về OCR <br>- Phát hiện và trích xuất mục hàng đúng định dạng Json<br>- Trích xuất đa mục hàng hóa trong hóa đơn<br>- Tính số lượng các thành phần có trong hóa đơn đó<br>- Kiểm tra thử với nhiều dạng bill khác nhau. <br><br>Cải thiện về chất lượng của mô hình Voice<br>- Xử Lý Số Tiếng Việt như (hai mươi hai thành 22)<br>- Nhận dạng các cụm từ ghép<br>- Sửa lỗi chính tả và xử lý tiếng ồn<br>- Cải tiến định dạng phản hồi về file Json<br>- Kiểm thử                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | 10/11/2025   | 10/11/2025    | [Sprint 02 - Day 06](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-2/day-6.md)  |
| 3   | Kiểm tra điểm tin cậy của mô hình OCR<br>- Tính toán Độ tin cậy Cấp trường<br>- Tính điểm tin cậy cho từng trường được trích xuất:<br>- Độ tin cậy Số tiền/Tổng:<br>- Độ tin cậy ngày:<br>- Độ rõ nét của văn bản<br>- Phân tách dòng rõ ràng<br>- Căn chỉnh giá<br>- Phát hiện số lượng<br>- Thuật toán độ tin cậy tổng thể<br>- Tính Low Confidence Threshold<br>- Kiểm tra hơn 30 bills<br><br>Kiểm tra Confidence Scoring của Voice<br>- Kiểm thử điểm số tin cậy nhiều lớp<br>- Kiểm thử thuật toán độ tin cậy tổng thể<br>- Kiểm thử Low Confidence Threholds của Voice<br>- Kiểm tra hiệu suất (hơn 50 mẫu, <4 giây)<br><br>Kiểm tra toàn bộ và testing hệ thống Voice và Bill                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | 11/11/2025   | 11/11/2025    | [Sprint 02 - Day 07](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-2/day-7.md)  |
| 4   | Phát hiện danh mục thông minh và nhận dạng các ngữ cảnh trong Voice<br>- Phát hiện danh mục nâng cao như phân tích tên người bán, triết xuất keyword dựa vào các danh mục<br>- Xác định ngữ cảnh <br>- Kiểm thử<br><br>Triết xuất các loại hóa đơn mới<br>- Thử nghiệm hóa đơn siêu thị <br>- Thử nghiệm trên hóa đơn nhà hàng<br>- Thử nghiệm trên hóa đơn cà phê, các quán nước,...<br>- Quy tắc trích xuất theo từng loại cụ thể<br>- Cải thiện phần trả về endpoint Json của phần Bill<br><br>Tích hợp và chạy thử với Backend<br>- Tích hợp các chức năng giao dịch<br>- Xử lý lỗi <br>- Trả về giá trị Json đúng                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | 12/11/2025   | 12/11/2025    | [Sprint 02 - Day 08](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-2/day-8.md)  |
| 5   | Error Handling, Optimization & Monitoring<br>Tối ưu hóa việc xử lý Voice<br>- Tối ưu hóa hiệu suất của model Voice<br>Xử lý Lỗi & Khả năng Phục hồi<br>- Xử lý Âm thanh Hỏng:<br>- Xác thực định dạng âm thanh (WAV, MP3, M4A)<br>- Kiểm tra thời lượng âm thanh (tối thiểu 0,5 giây, tối đa 30 giây)<br>- Phát hiện tệp bị hỏng/không đầy đủ<br>- Trả về lỗi xóa: "Định dạng âm thanh không hợp lệ hoặc tệp bị hỏng"<br>- Xử lý Thời gian Chờ STT:<br>- Đặt thời gian chờ cho quá trình xử lý STT (tối đa 30 giây)<br>- Nếu hết thời gian chờ, trả về kết quả một phần kèm theo cảnh báo<br>- Ghi nhật ký sự kiện hết thời gian chờ để theo dõi<br><br>Logic Thử Lại:<br>- Thử lại STT khi gặp lỗi tạm thời (tối đa 3 lần thử lại)<br>- Thời gian chờ theo cấp số nhân: 1 giây, 2 giây, 4 giây<br>- Trả về lỗi sau số lần thử lại tối đa<br><br>Trường hợp Ngoại lệ:<br>- Âm thanh trống/im lặng → Lỗi: "Không phát hiện thấy giọng nói"<br>- Giọng nói không phải tiếng Việt → Cảnh báo độ tin cậy thấp<br>- Nhiều người nói → Cảnh báo + trích xuất nỗ lực tốt nhất<br>- Âm thanh rất dài (>30 giây) → Lỗi: "Âm thanh quá dài" "dài"<br><br>Giảm cấp duyên dáng:<br>- Nếu phát hiện danh mục không thành công → Trả về "Chưa phân loại"<br>- Nếu trích xuất số lượng không thành công → Trả về giá trị null kèm cảnh báo<br>- Nếu không phát hiện ngày → Sử dụng ngày hiện tại kèm cảnh báo<br>- Luôn trả về kết quả một phần khi có thể | 13/11/2025   | 13/11/2025    | [Sprint 02 - Day 09](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-2/day-9.md)  |
| 6   | Kiểm tra và tài liệu toàn diện<br>- Chuẩn bị các data cho cho việc kiểm tra hai mô hình Voice và Bill<br>- Kiểm tra API của Voice<br>- Kiểm tra API của Bill OCR<br><br>Kiểm tra các trường hợp của Voice<br>- Kiểm tra khi có tiếng ồn xung quanh<br>- Kiểm tra khi nói nhanh hoặc chậm<br>- Kiểm tra khi đầu vào không đúng giá trị, như người nói và nói tàm phào<br>- Kiểm tra đa giao dịch trong một lần ghi âm<br>- Kiểm tra đầu vào mơ hồ <br><br>Kiểm tra các trường hợp của xử lý Bill<br>- Kiểm tra anh xoay nhiều hướng có nhận diện được không<br>- Kiểm tra chất lượng ảnh<br>- Kiểm tra các input không đúng ảnh hóa đơn<br>- Kiểm tra với các hóa đơn có độ phức tạp cao<br>- Kiểm tra với các hóa đơn có nhiều mặt hàng                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | 14/11/2025   | 14/11/2025    | [Sprint 02 - Day 10](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-2/day-10.md) |

### Kết quả đạt được tuần 10:

#### 1. Cải Tiến Mô Hình OCR

- Phát hiện và trích xuất mục hàng đúng định dạng JSON
- Trích xuất đa mục hàng hóa trong một hóa đơn
- Tính toán số lượng các thành phần trong hóa đơn tự động
- Kiểm thử thành công với nhiều loại hóa đơn: siêu thị, nhà hàng, cà phê, quán nước
- Xây dựng quy tắc trích xuất theo từng loại hóa đơn cụ thể
- Cải thiện format JSON response cho endpoint Bill

#### 2. Nâng Cao Chất Lượng Voice Processing

- Xử lý số tiếng Việt (chuyển "hai mươi hai" → "22")
- Nhận dạng các cụm từ ghép tiếng Việt
- Sửa lỗi chính tả và xử lý nhiễu âm thanh
- Cải tiến định dạng phản hồi JSON
- Tối ưu hóa hiệu suất xử lý Voice

#### 3. Hệ Thống Confidence Scoring

**OCR Confidence:**

- Tính toán độ tin cậy cấp trường (Field-level Confidence)
- Độ tin cậy cho Số tiền/Tổng
- Độ tin cậy cho Ngày tháng
- Đánh giá độ rõ nét văn bản và phân tách dòng
- Phát hiện căn chỉnh giá và số lượng
- Xây dựng thuật toán độ tin cậy tổng thể
- Thiết lập Low Confidence Threshold
- Kiểm thử trên hơn 30 hóa đơn thực tế

**Voice Confidence:**

- Triển khai điểm số tin cậy nhiều lớp (Multi-layer Confidence Scoring)
- Thuật toán độ tin cậy tổng thể cho Voice
- Thiết lập Low Confidence Thresholds
- Kiểm tra hiệu suất trên hơn 50 mẫu (thời gian xử lý <4 giây)

#### 4. Phát Hiện Danh Mục Thông Minh

- Phân tích tên người bán/merchant
- Trích xuất keyword dựa vào danh mục
- Xác định ngữ cảnh giao dịch
- Phát hiện danh mục nâng cao (Advanced Category Detection)

#### 5. Error Handling & Resilience

**Xử lý Lỗi Âm Thanh:**

- Xác thực định dạng âm thanh (WAV, MP3, M4A)
- Kiểm tra thời lượng (min: 0.5s, max: 30s)
- Phát hiện tệp bị hỏng/không đầy đủ
- Xử lý timeout STT (max: 30s)
- Logic retry với exponential backoff (3 lần, 1s-2s-4s)

**Xử lý Trường Hợp Ngoại Lệ:**

- Âm thanh trống/im lặng → Error: "Không phát hiện giọng nói"
- Giọng nói không phải tiếng Việt → Cảnh báo độ tin cậy thấp
- Nhiều người nói → Cảnh báo + trích xuất nỗ lực tốt nhất
- Âm thanh quá dài (>30s) → Error: "Âm thanh quá dài"

**Graceful Degradation:**

- Danh mục không phát hiện được → Trả về "Chưa phân loại"
- Số lượng không trích xuất được → Trả về null + cảnh báo
- Ngày không phát hiện → Sử dụng ngày hiện tại + cảnh báo
- Luôn trả về kết quả partial khi có thể

#### 6. Kiểm Thử Toàn Diện

**Voice Testing:**

- Kiểm tra với tiếng ồn xung quanh
- Kiểm tra tốc độ nói (nhanh/chậm)
- Kiểm tra đầu vào không hợp lệ (nói tàm phào)
- Kiểm tra đa giao dịch trong một lần ghi âm
- Kiểm tra đầu vào mơ hồ

**Bill OCR Testing:**

- Kiểm tra ảnh xoay nhiều hướng
- Kiểm tra chất lượng ảnh đa dạng
- Kiểm tra input không đúng định dạng hóa đơn
- Kiểm tra hóa đơn có độ phức tạp cao
- Kiểm tra hóa đơn nhiều mặt hàng

#### 7. Tích Hợp Backend

- Tích hợp các chức năng giao dịch với Backend
- Xử lý lỗi toàn diện
- Trả về giá trị JSON chuẩn hóa

**Tổng kết:** Tuần 10 tập trung vào việc nâng cao chất lượng và độ tin cậy của cả hai mô hình Voice và OCR. Đã triển khai thành công hệ thống confidence scoring, xử lý lỗi toàn diện, và kiểm thử đa chiều với nhiều edge cases. Hệ thống đã sẵn sàng tích hợp với Backend và xử lý các tình huống thực tế phức tạp.
