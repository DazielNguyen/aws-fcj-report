---
title: "Worklog Tuần 5"
date: "2025-10-06"
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

- Tìm hiểu kiến thức nền tảng và các dịch vụ cốt lõi về bảo mật trên AWS, xoay quanh triết lý "Security is job zero".
- Bắt đầu với khái niệm cơ bản nhất là **Mô hình chia sẻ trách nhiệm (Share Responsibility Model)**. 
- Tập trung sâu vào việc quản lý định danh và quyền truy cập (**Identify and Access Management - IAM**), bao gồm các thành phần: **User**, **Group**, **Policy**, và **Role**. 
- Mở rộng tìm hiểu thêm các dịch vụ quản lý định danh ở quy mô lớn hơn như **AWS Organizations** (quản lý nhiều tài khoản), **AWS Identity Center (SSO)** (đăng nhập một lần), và **Amazon Cognito** (quản lý người dùng cho ứng dụng web/di động).
- Nắm rõ kiến thức về bảo vệ dữ liệu thông qua mã hóa với **AWS KMS** và giám sát, kiểm tra tuân thủ với **AWS Security Hub**.


### Các công việc cần triển khai trong tuần này:

| Thứ 	| Công việc 	| Ngày bắt đầu 	| Ngày kết thúc 	| Nguồn tài liệu và ghi chú học tập 	|
|---	|---	|---	|---	|---	|
| 2 	| **Share Responsibility Model**<br><br>- Học về **Mô hình chia sẻ trách nhiệm**, trong đó AWS chịu trách nhiệm bảo mật *của* đám mây (hạ tầng vật lý, software nền tảng) và khách hàng chịu trách nhiệm bảo mật *trong* đám mây (cấu hình, dữ liệu, ứng dụng).<br>- Tìm hiểu về sự thay đổi trách nhiệm bảo mật tùy thuộc vào loại hình dịch vụ (hạ tầng, quản lý kết hợp, hay quản lý hoàn toàn).<br><br>**AWS Identify and Access Management (IAM)**<br><br>- Tìm hiểu về **Root Account**, tài khoản có toàn quyền tuyệt đối, và các best practice để bảo vệ nó (tạo IAM Admin User để dùng thay thế, khóa root credentials).<br>- Học về **IAM User**, một thực thể (principal) dùng để tương tác với AWS, khi mới tạo mặc định không có bất cứ quyền gì.<br>- Tìm hiểu về kĩ thuật quản lý user hiệu quả bằng cách gom nhiều IAM User vào chung một **IAM Group**.<br>- Học về **IAM Policy**, một văn bản JSON định nghĩa quyền hạn, bao gồm 2 loại:<br>  + **Identity-based Policy**: Gán trực tiếp cho một IAM Principal (User, Group, Role).<br>  + **Resource-based Policy**: Gán trực tiếp vào một tài nguyên (ví dụ: S3 Bucket Policy).<br>- Tìm hiểu về kĩ thuật đánh giá quyền của IAM, trong đó một **Deny tường minh (explicit deny)** luôn luôn được ưu tiên, bất kể có policy Allow nào khác.<br>- Học về kiến trúc của **IAM Role**, một tập hợp quyền (policy) mà không đi kèm credentials (mật khẩu/access key) vĩnh viễn.<br>- Tìm hiểu về kĩ thuật **Assume Role**: Một IAM User (hoặc Service) sử dụng dịch vụ **AWS STS (Security Token Service)** để tạm thời "đảm nhận" quyền của IAM Role và nhận về thông tin chứng thực tạm thời.<br>- Tìm hiểu về ứng dụng thực tế của IAM Role, ví dụ cấp quyền cho dịch vụ **EC2** truy cập vào S3 mà không cần lưu trữ access key trên máy chủ. 	| 06/10/2025 	| 06/10/2025 	| [Module 05](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Take_notes_module_05.md)	|
| 3 	| **Amazon Cognito**<br><br>- Học về **Amazon Cognito**, dịch vụ quản lý xác thực (đăng nhập, đăng ký) và cấp phép cho *người dùng cuối* của các ứng dụng web và di động (khác với IAM User là người quản trị AWS).<br>- Tìm hiểu về hai thành phần chính của Cognito:<br>  + **User Pool**: Thư mục quản lý người dùng, hỗ trợ đăng nhập trực tiếp hoặc qua các bên thứ ba (Facebook, Google).<br>  + **Identity Pool**: Cấp cho người dùng ứng dụng quyền truy cập (thường là tạm thời) vào các dịch vụ AWS khác.<br><br>**AWS Organization**<br><br>- Học về **AWS Organizations**, dịch vụ giúp quản lý và điều hành tập trung nhiều tài khoản AWS.<br>- Tìm hiểu về kĩ thuật **Consolidated Billing** (thanh toán tập trung) cho tất cả tài khoản.<br>- Tìm hiểu về kĩ thuật gom các tài khoản vào **OU (Organization Unit)** và áp dụng **Service Control Policies (SCP)** để *giới hạn* quyền tối đa mà các IAM User/Role trong tài khoản đó có thể thực hiện (kể cả deny-based).<br><br>**AWS Identify Center (SSO)**<br><br>- Học về **AWS Identity Center (SSO)**, dịch vụ giúp quản lý quyền truy cập tập trung (đăng nhập một lần) vào tất cả các tài khoản AWS trong Organization và các ứng dụng bên ngoài.<br>- Tìm hiểu về kĩ thuật sử dụng **Permission Set** (một bộ quyền được lưu trữ trong Identity Center) để gán cho User/Group. Khi user truy cập 1 tài khoản, Permission Set sẽ được cấp dưới dạng một IAM Role trong tài khoản đó. 	| 07/10/2025 	| 07/10/2025 	| [Module 05](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Take_notes_module_05.md) 	|
| 4 	| **AWS Key Management Service (KMS)**<br><br>- Học về **AWS KMS**, dịch vụ tạo và quản lý các khóa mã hóa (**encryption key**) để bảo vệ dữ liệu ở trạng thái nghỉ (**Encryption at rest**).<br>- Tìm hiểu về... **CMK (Customer Managed Key)** (khóa chính nằm trong KMS) và **Data Key** (khóa dùng để mã hóa/giải mã dữ liệu thực tế, được tạo ra bởi CMK).<br><br>**AWS Security Hub**<br><br>- Học về **AWS Security Hub**, dịch vụ kiểm tra bảo mật liên tục, dựa trên các best practices của AWS và tiêu chuẩn ngành (như **PCIDSS**).<br>- Tìm hiểu về cách Security Hub cung cấp kết quả dưới dạng *điểm số* và xác định các tài nguyên cần chú ý.<br><br>**Lab: 000002 - Bắt đầu với IAM và IAM Role**<br>- IAM Group và IAM User<br>- Tạo IAM Role<br>- Assume Role<br><br>**Lab: 000044 - IAM Role và Condition**<br>- Giới thiệu về IAM<br>- Tạo User quản trị EC2<br>- Tạo User quản trị RDS<br>- Tạo Group quản trị-Cấu hình IAM Role Condition<br>- Tạo IAM Role có quyền Admin 5.2 Tạo IAM User 5.3 Cấu hình Switch role 5.4 Giới hạn IP 5.5 Giới hạn theo thời gian.<br> 	| 08/10/2025 	| 08/10/2025 	| [Module 05](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Take_notes_module_05.md) 	|
| 5 	| **Lab: 000048 - IAM Role và Application**<br>- Sử dụng access key<br>- IAM Role trên EC2<br><br>**Lab: 000030 - IAM Permission Boundary**<br>- Giới thiệu IAM Permission Boundary<br>- Tạo Policy giới hạn<br>- Tạo IAM User giới hạn quyền<br>- Kiểm tra User bị giới hạn<br><br>**Lab: 000027 - Tag và Resource Groups**<br>- Sử dụng thẻ<br>- Sử dụng thẻ bằng Console<br>- Hiển thị các thẻ<br>- Thêm hoặc xóa thẻ<br>- Gắn thẻ cho một máy ảo<br>- Lọc tài nguyên theo thẻ<br>- Sử dụng thẻ bằng CLI<br>- Resource Group<br><br>**Lab: 000028 - Quản lý EC2 qua Resource Tag**<br>- Tạo IAM Policy<br>- Tạo IAM Role<br>- Kiểm tra IAM Role 	| 09/10/2025 	| 09/10/2025 	| [Module 05](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Take_notes_module_05.md) 	|
| 6 	| **Lab: 000018 - Sử dụng AWS Security Hub**<br>- Các tiêu chuẩn bảo mật<br>- Kích hoạt Security HUb<br>- Điểm từng bộ tiêu chuẩn<br><br>**Lab: 000012 - Sử dụng AWS SSO**<br>- Các bước chuẩn bị<br>- Tạo AWS Account trong AWS Organizations<br>- Thiết lập Organization Unit<br>- Thiết lập AWS SSO<br>- Kiểm tra<br><br>**Lab: 000033 - KMS Workshop**<br>- Thiết lập môi trường<br>- Bắt đầu với AWS KMS<br>- Mã hóa với AWS KMS<br>- Key Policy và các best practices<br>- Giám sát việc sử dụng AWS KMS.<br><br>[Nghiên cứu bổ sung] - AWS Certified Security Special All-in-One-Exam Guide (Exam SCS-C01)<br>- Tài liệu học để thi chúng chỉ Security Specialty 	| 10/10/2025 	| 10/10/2025 	| [Module 05](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Take_notes_module_05.md)<br> [Research Link](https://www.amazon.com/Certified-Security-Specialty-Guide-SCS-C01/dp/1260461726) 	|

### Kết quả đạt được tuần 5:

- **Bài học Nền tảng:** Nắm vững **Mô hình chia sẻ trách nhiệm (Share Responsibility Model)**, hiểu rõ đâu là trách nhiệm của AWS và đâu là của khách hàng.
- **Dịch vụ IAM (Cốt lõi):**
  + Phân biệt rõ ràng **Root Account** (toàn quyền, cần khóa lại) và **IAM User** (dùng hàng ngày, mặc định không có quyền).
  + Nắm vững 3 thành phần chính để cấp quyền: **IAM User** (đối tượng), **IAM Policy** (giấy phép - viết bằng JSON), và **IAM Group** (nhóm các đối tượng).
  + Hiểu rõ **IAM Role**: một cơ chế cấp quyền tạm thời (không có credentials vĩnh viễn) cho cả User và Service (như EC2).
- **Kĩ thuật IAM (Quan trọng):**
  + Biết cách một User/Service "nhận" quyền của Role thông qua kĩ thuật **Assume Role** (sử dụng dịch vụ **STS**).
  + Hiểu quy tắc đánh giá quyền: **Explicit Deny** (Deny tường minh) luôn thắng mọi quyền Allow.
- **Dịch vụ Quản lý Định danh (Identity Services):**
  + Phân biệt rõ **IAM** (quản lý người quản trị AWS) và **Amazon Cognito** (quản lý người dùng cuối của ứng dụng web/mobile).
  + Biết **Cognito User Pool** là thư mục người dùng (có thể login bằng Facebook, Google) và **Identity Pool** là nơi cấp quyền cho user đó truy cập tài nguyên AWS.
- **Dịch vụ Quản lý Đa tài khoản (Multi-Account):**
  + Hiểu **AWS Organizations** dùng để quản lý tập trung nhiều tài khoản, cho phép **Consolidated Billing** (thanh toán gộp).
  + Biết dùng **Service Control Policies (SCP)** trong Organization để *giới hạn* quyền tối đa của các tài khoản con.
  + Nắm được **AWS Identity Center (SSO)** là giải pháp đăng nhập một lần, sử dụng **Permission Set** để cấp quyền vào các tài khoản trong Organization.
- **Dịch vụ Mã hóa (Encryption):**
  + Biết **AWS KMS** là dịch vụ để tạo và quản lý khóa mã hóa.
  + Hiểu cơ chế mã hóa **Encryption at rest** và phân biệt được **CMK** (khóa chính trong KMS) với **Data Key** (khóa dùng để mã hóa dữ liệu thực tế).
- **Dịch vụ Giám sát Bảo mật (Monitoring):**
  + Biết **AWS Security Hub** là dịch vụ quét và chấm điểm bảo mật, giúp kiểm tra tuân thủ (compliance) theo các tiêu chuẩn (như **PCIDSS**).
- **Thực hành:**
  + Thực hành tạo và quản lý User, Group, Policy, Role.
  + Thực hành triển khai SSO và KMS.
  + Thực hành sử dụng các tính năng nâng cao của IAM như **Conditions** và **Permission Boundary**.