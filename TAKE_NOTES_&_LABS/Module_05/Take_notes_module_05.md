# **Module 5 - Dịch vụ Bảo Mật trên AWS** - "Security is job zero"
## **I. Share Responsibility Model - Mô hình chia sẻ trách nhiệm**
- **Mô hình chia sẻ trách nhiệm**: khi sử dụng dịch vụ của nhà cung cấp dịch vụ điện toán đám mây, việc bảo mật của ứng dụng sẽ là trách nhiệm chia sẻ của cả khách hàng và nhà cung cấp dịch vụ. 

- Khách hàng sẽ chịu trách nhiệm cho việc cấu hình, áp dụng các best practices, sử dụng các dịch vụ để đảm bảo việc bảo mật từ mức Hypervisor tới mức dữ liệu/ứng dụng

> Mô hình chia sẻ trách nhiệm 

![Module_05_1_Share_Responsibility_Model](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_1_Share_Responsibility_Model.png)

- Trách nhiệm bảo mật sẽ thay đổi tùy vào từng loại hình dịch vụ: 
    + Các dịch vụ ở mức hạ tầng
    + Các dịch vụ quản lý ở mức kết hợp
    + Các dịch vụ quản lý hoàn toàn bởi AWS

> Các mức dịch vụ của AWS

![Module_05_1_AWS_Service_Levels](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_1_AWS_Service_Levels.png)

## **II. AWS Identify and Access Management - Quản trị định danh và quyền truy cập**
### **1. Root Account**
- Tài khoản này có **toàn** quyền truy cập vào **tất cả** các dịch vụ và tài nguyên AWS, và có thể gỡ bỏ các chính sách toàn quyền đã gán vào tài nguyên. 
    + Thông tin tính phí
    + Dữ liệu cá nhân (khi đăng ký account)
    + Không bị giới hạn quyền. 

***Best Pratices***
- Tạo và sử dụng IAM Administrator User. 
- Khóa thông tin xác thực của root user (chia hai người giữ)
- Đảm bảo renew thông tin domain và email của root user. 
### **2. IAM User**
- **IAM** là dịch vụ giúp bạn kiểm soát quyền truy cập vào các dịch vụ và tài nguyên trong AWS account của mình. IAM cho phép bạn tạo nhiều tài khoản người dùng (IAM user) với thông tin xác thực (credentials) và quyển hạn khác nhau.
- IAM Principal (chủ thể IAM) là một thực thể có thể thực hiện các hành động trên tài nguyên nhất định trong AWS account của bạn.
    + AWS account and root user
    + IAM users
    + Federated users ( sử dụng web identity hoặc SAML federation )
    + IAM roles
    + Assumed-role sessions
    + AWS services
    + Anonymous users (không khuyến nghị)
- Người dùng IAM (IAM User) không phải là tài khoản AWS riêng biệt, IAM Users có mật khẩu riêng để truy cập vào management console hoặc access key/secret key để thực hiện programmatic access (AWS CLI và AWS SDK).
    + IAM User khi được tạo ra mặc định không có bất cứ quyền gì.
    + IAM User không được dùng để quản lý truy cập vào ứng dụng hay hệ điều hành.
    + Để cấp quyền cho IAM User chúng ta phải gán IAM Policy vào IAM User.
    + Để quản lý dễ dàng hơn chúng ta có thể gom nhiều IAM User thành 1 IAM Group.
    + IAM Group không thể là thành viên của 1 IAM Group khác.

> Kiến trúc IAM User
![Module_05_2_IAM_User]()

### **3. IAM Policy**
- Được viết dưới dạng JSON. 
- IAM Policy có 2 loại: 
    + **Identity based Policy** gán với một IAM Principal(User)
    + **Resource based Policy** gán với một AWS Resource
- Cách thức tính quyền của IAM luôn ưu tiên Deny Accessment so với Allow, nếu đã có Deny tường minh (explicit) thì dù cho có Allow ở trên một IAM Policy khác thì cũng vẫn luôn là Deny. 

> IAM Plolicy JSON Example 

![Module_05_3_IAM_Policy]()

- Ví dụ này cho thấy cách bạn có thể IAM Policy giới hạn việc quản lý S3 bằng cách: 
    + Cho phép tất cả các hành động của S3 trên bucket cụ thể
    + Deny tường minh (explicit deny) quyền truy cập vào mọi dịch vụ AWS ngoại trừ Amazon S3. 


 

## **III. Amazon Cognito**


## **IV. AWS Organization & AWS Identify Center (SSO)**


## **V. AWS KMS**


## **VI. Thực hành và nghiên cứu bổ sung**
