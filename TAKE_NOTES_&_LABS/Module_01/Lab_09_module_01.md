# **Module 01 - Lab 09**

https://000009.awsstudygroup.com/vi/

## 1. Các gói hỗ trợ của AWS:
- Chia ra 4 gói hỗ trợ khác nhau: 
    + Basic
    + Developer
    + Business
    + Enterprise
### 1.1 Gói Basic (Free) 
- Hỗ trợ 1-1 chat liên quan đến vấn đề tài khoản, vấn đề thanh toán khi gặp lỗi. 
- Giúp kiểm tra tài khoản và các vấn đề về dịch vụ. 
- Diễn đàn hỗ trợ
### 1.2 Gói Developer (Có tính phí)
- Cung cấp được những chức năng mở rộng hơn. 
    + Các chỉ dẫn về best practice
    + **Hỗ trợ xây dựng kiến trúc khối**: Chỉ dẫn cách sử dụng và kết hợp các sản phẩm, tính năng và dịch vụ của AWS. 
    + **Hỗ trợ không giới hạn các yêu cầu hỗ trợ**: được tạo bởi tài khoản gốc (Root User)
### 1.3 Gói Business (Có tính phí)
- Sẽ được nâng cấp hỗ trợ thêm các chức năng cao hơn. 
    + **Chỉ dẫn theo Use-case cụ thể:** Lời khuyên về sự lựa chọn các sản phẩm, tính năng, và dịch vụ của AWS, hỗ trợ tốt nhất cho nhu cầu của bạn. 
    + **AWS Trusted Advisor:** Truy cập đầy đủ vào công cụ tự động khảo sát môi trường AWS của bạn và xác định cơ hội tiết kiệm chi phí, giảm thiểu rủi ro an ninh và tăng cường độ tin cậy và hiệu suất của hệ thống
    + **Hỗ trợ sử dụng AWS Support API:** Tương tác với Support Center và Trusted Advisor qua API để tự động quản lý yêu cầu hỗ trợ và vận hành AWS Trusted Advisor
    + **Hỗ trợ về phần mềm bên thứ ba:** Hỗ trợ hệ điều hành và cấu hình máy ảo Amazon EC2, cùng với hiệu suất của các ứng dụng phổ biến trên nền tảng AWS
    + **Hỗ trợ không giới hạn các yêu cầu hỗ** trợ được tạo bởi tất cả các IAM User
- **Tip**:  Gói Business là lựa chọn phổ biến cho các doanh nghiệp vừa và nhỏ đang vận hành workload sản xuất trên AWS, cung cấp sự cân bằng tốt giữa chi phí và mức độ hỗ trợ.

### 1.4 Gói Enterprise (Có tính phí)
- với khách hàng sử dụng gói **AWS Support Enterprise** sẽ có thêm các đặc quyền về tính năng như sau:
    + **Chỉ dẫn về kiến trúc phần mềm:** Lời khuyên chuyên sâu về cách phối hợp dịch vụ AWS để giải quyết vấn đề về ứng dụng hoặc tải trọng công việc
    + **Quản lý sự kiện hạ tầng:** Phân tích chuyên sâu về use-case của bạn và cung cấp hướng dẫn về quy mô và kiến trúc phù hợp cho sự kiện cụ thể
    + **Technical Account Manager (TAM):** Sự hỗ trợ thường trực từ Technical Account Manager giải quyết các vấn đề liên quan đến tình huống và ứng dụng của bạn
    + **Ưu tiên và chăm sóc đặc biệt cho các yêu cầu hỗ trợ**
    + **Đánh giá Quản lý Doanh nghiệp:** Hỗ trợ đánh giá toàn diện về chiến lược cloud và tối ưu hóa chi phí
- **Security Note**: Gói Enterprise cung cấp quyền truy cập vào các chuyên gia bảo mật AWS, giúp đảm bảo môi trường cloud của bạn tuân thủ các tiêu chuẩn bảo mật và quy định nghiêm ngặt nhất.
## 2. Truy cập AWS Support: 
- Hỗ trợ Tài khoản và Thanh toán (Account and Billing Support)
    + Loại hỗ trợ này được cung cấp cho tất cả người dùng AWS, bao gồm cả gói hỗ trợ Basic. Bạn có thể nhận được hỗ trợ cho các vấn đề liên quan đến:

        + Câu hỏi về hóa đơn và thanh toán
        + minh tài khoản
        + Thay đổi thông tin tài khoản
        + Các vấn đề về thuế

- Hỗ trợ nâng hạn mức dịch vụ (Service limit increase)
    + Loại yêu cầu này được hỗ trợ cho tất cả người dùng AWS và cho phép bạn yêu cầu tăng giới hạn mặc định của các dịch vụ AWS.

- Hỗ trợ Kỹ thuật (Technical support)
    + Các yêu cầu kỹ thuật giúp giải quyết các vấn đề liên quan đến dịch vụ AWS hoặc ứng dụng bên thứ ba chạy trên AWS. Tùy thuộc vào gói hỗ trợ của bạn:
        + **Gói Developer:** Hỗ trợ qua email hoặc web portal của AWS Support Center
        + **Gói Business/Enterprise:** Hỗ trợ qua email, web portal, chat trực tuyến và điện thoại 24/7 
## 3. Quản lý Yêu cầu Hỗ trợ: 
 3.1. Khởi tạo Yêu cầu Hỗ trợ: 
 - Hướng dẫn chi tiết về cách tạo yêu cầu hỗ trợ mới, bao gồm cách điền thông tin liên quan và mô tả vấn đề một cách hiệu quả để nhận được hỗ trợ nhanh chóng.

 3.2. Lựa chọn mức độ nghiêm trọng (Severity) khi gửi yêu cầu: 
 - Giải thích về các mức độ nghiêm trọng khác nhau và cách chọn mức độ phù hợp với tình huống cụ thể, giúp đảm bảo vấn đề được xử lý theo đúng mức độ ưu tiên.

