# **Module 01 - Lab 07**
https://000007.awsstudygroup.com/vi/

## 1. Tạo Budget: 
- **AWS Budget** là một dịch vụ cung cấp khả năng thiết lập ngân sách để gửi cảnh báo cho mình khi mình dùng vượt quá chi phí của mình.
- Quản lí chi phí là một việc quan trọng hàng đầu trong việc vận hành hệ thống của mình trên Cloud 
- Nó gồm 4 loại: 
    + **Cost Budget:** 
    + **Usage Budget:** 
    + **RI Budget(Reservation Instance Budget):**  
    + **Saving Plans Budget:**
- Nó sẽ có template để set up phần Budget này. 
## 2. Tạo Cost Budget:
- **Cost Budget:** 
    + Gửi cảnh báo khi tổng chi phí vượt quá ngưỡng chi phí trong ngân sách. Có thể thông qua email. 
    + Vd: Khi ngân sách của mình chỉ có $25 nhưng mức dịch vụ mình sử dụng gần mức $25 đó, chẳng hạn như $20 thì nó sẽ gửi email cảnh báo mình.  
- **Hướng dẫn sử dụng**: 
    + Bước 1: Tìm **Billing and Cost Management** tại thanh tìm kiếm.
    + Bước 2: Chọn **Budgets** từ menu bên trái: 
    + Bước 3: Nhấn **Create Budgets**
- **Thiết lập cấu hình Budgets:**
    + Bước 1: Phần **Budget Setup**, chọn **Customize**
    + Bước 2: Phần **Budget Types**, chọn **Cost budget**
    + Bước 3: Phần **Detail**, tại **Budget name**, nhập "Monthly"
    + Bước 4: Phần **Set budget amount** -> Chọn **Recuring Budget**
        + **Recuring Buget**: Nếu bạn muốn Budget được lặp lại định kỳ
        + **Expiring Budget**: Nếu bạn chỉ muốn Budget được áp dụng một lần duy nhất
    + Bước 5: Chọn **Fixed**, rồi nhập Budget mong muốn 
    + Bước 6: Phần **Configure alerts**, chọn **Add an alert threshold** để thiết lập ngưỡng cảnh báo. Nhấn **Next**.
    + Bước 7: Qua phần set up **Alert #1**, Nhập **Email recipt** để nhận cảnh báo nếu dùng quá mức dịch vụ 
## 3. Tạo Usage Budget: 
- **Usage Budget:** 
    + Gửi cảnh báo khi tổng mức sử dụng **theo từng dịch vụ** bạn lựa chọn vượt qua ngưỡng mức độ sử dụng trong ngân sách. 
    + Vd: Mức độ sử dụng theo số giờ chạy của dịch cụ EC2. Cụ thể như tôi chỉ đặt mức thời gian cho dịch vụ EC2 chỉ được chạy trong 30 giờ thì dịch vụ đó chỉ được chạy trong khoảng thời gian được đặt ra và không được quá cái thời gian đặt ra đó. 
- **Hướng dẫn sử dụng**
    + Thì nó sẽ set up tương tự như **Cost Budget**.
    + Điểm khác biệt thì nó sẽ cảnh báo trên mức tài nguyên mà mình sử dụng thay vì tiền. 
## 4. Tạo RI Budget: 
+ **RI Budget(Reservation Instance Budget):** 
        + Gửi cảnh báo dựa trên mức sử dụng các dịch vụ trả trước *(reservation instance)* của bạn. 
        + Để hiểu rõ hơn đó là một phương pháp giảm chi phí sử dụng instance bằng cách cho phép bạn trả trước hoặc cam kết mức sử dụng của instance theo thời hạn 1 - 3 năm. 
## 5. Tạo Saving Plan Budget:
- **Saving Plans Budget:**
    + Gửi cảnh báo dựa trên mức sử dụng các dịch vụ đã được quy định ở trong saving plans. 
    + Nó cũng gần giống như **Ri Budget** cho phép bạn trả trước hoặc cam kết dài hạn từ 1 - 3 năm mức sử dụng của instance đó
    + **Savings plans instance** là mô hình được ra đời sau và có tính **linh hoạt** hơn **Reserve Instance** với mức giảm giá tương đương. 
    + Khuyến khích sử dụng **Saving Instance** với EC2 Intance
## 6. Clean tài nguyên: 
- Khi cần xóa Budget thì nên cần làm gì? 
- Các bước xóa Bugget 
    + Bước 1: Đăng nhập vào **AWS Management Console** và tìm dịch vụ **AWS Billing and Cost Management** tại thanh tìm kiếm.
    + Bước 2: Tại trang quản trị, chọn **Budgets** từ menu bên trái.
    + Bước 3: Thực hiện xóa budget: Chọn Budget cần xóa
    + Bước 4: Nhấn vào nút **Delete**
- Việc xóa **AWS Budgets** không ảnh hưởng đến tài nguyên đang chạy trong tài khoản AWS của bạn. Các budget chỉ là công cụ giám sát và cảnh báo, không kiểm soát trực tiếp việc sử dụng tài nguyên.

