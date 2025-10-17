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

![Module_05_2_IAM_User](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_2_IAM_User.png)

### **3. IAM Policy**
- Được viết dưới dạng JSON. 
- IAM Policy có 2 loại: 
    + **Identity based Policy** gán với một IAM Principal(User)
    + **Resource based Policy** gán với một AWS Resource
- Cách thức tính quyền của IAM luôn ưu tiên Deny Accessment so với Allow, nếu đã có Deny tường minh (explicit) thì dù cho có Allow ở trên một IAM Policy khác thì cũng vẫn luôn là Deny. 

> IAM Plolicy JSON Example 

![Module_05_3_IAM_Policy](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_3_IAM_Policy.png)

- Ví dụ này cho thấy cách bạn có thể IAM Policy giới hạn việc quản lý S3 bằng cách: 
    + Cho phép tất cả các hành động của S3 trên bucket cụ thể
    + Deny tường minh (explicit deny) quyền truy cập vào mọi dịch vụ AWS ngoại trừ Amazon S3. 

### **4. IAM Role**
- **IAM Role** cho phép xác định một tập hợp quyền truy cập vào các tài nguyên (thông qua việc gán **IAM Policy vào IAM role**). IAM Role không có thông tin chứng thực **(credentials)** để truy cập vào management console hay AWS CLI/SDK.
- Khi một **IAM User** muốn sử dụng IAM Role , **IAM User sẽ cần assume** (đảm nhận) 1 IAM Role, ngay sau khi assume role, quyền hiện tại của user sẽ được thay bằng quyền đang được cấp cho IAM Role. Ngoài ra, thông tin xác thực bảo mật tạm thời sẽ được cấp cho IAM User hoặc một AWS Service để có thể truy cập tới các dich vụ của AWS. Việc assume role sẽ làm việc với dịch vụ **AWS STS - Security Token Service** giúp tạo ra các thông tin chứng thực tạm (tương tự như access key). 
- IAM Role có thể được sử dụng bởi: 
    + IAM User trong cùng một AWS Account
    + IAM User trong một AWS Account khác (cross-account access)
    + AWS Service (ví dụ: EC2, Lambda, ECS task)
    + Ứng dụng bên ngoài (federated user)

- Để một user có thể sử dụng IAM Role, IAM Role sẽ được gán một resource base IAM policy, 
hay còm gọi là IAM Role trust policy, quy định xem ai có thể sử dụng IAM Role. 
- IAM Role thường được dùng trong các thức tế để đảm bảo nguyên tác cấp quyền tối thiểu và dùng trong các trường hợp cấp quyền cho các AWS account khác truy cập tài nguyên của AWS account hiện tại. 
> IAM Role Example

![Module_05_4_IAM_Role](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_4_IAM_Role.png)

- IAM Role thường được dụng trong thực tế để đảm bảo **nguyên tắc cấp quyền tối thiểu** và dùng trong trường hợp **cấp quyền cho các AWS Account khác truy cập tài nguyên của AWS account hiện tại**. 
- Ngoài được sử dụng cho IAM User, IAM Role còn được sử dụng để cấp quyền truy cập các resource của AWS cho chính các AWS Service. 

- Trường hợp sử dụng thường thấy nhất là dùng IAM Role cấp quyền cho các ứng dụng chạy bên trong dịch vụ tính toán (EC2). 

> IAM Role for EC2 Example

![Module_05_5_IAM_Role_for_EC2](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_5_IAM_Role_for_EC2.png)

- Ngoài được sử dụng cho IAM User, IAM Role còn được sử dụng để cấp **quyền truy cấp các resource của AWS** cho chính **các AWS Service**. 

## **III. Amazon Cognito**
- **CLoud Native**: Khái niệm Cloud Native thường dùng để nói đến những ứng dụng được thiết kế để làm sao phát huy được tối đa sức mạnh của nền tảng Cloud, ví dụ như tính năng Auto-scale tận dụng những dịch vụ mà những nhà cung cấp dịch vụ cung cấp và quản lý, làm sao để ra được các sản phẩm chạy nhanh có thể cập những tính năng mới nhanh, giảm bớt công việc và quản lý hạ tầng, thì người ta gọi đó là ứng dụng Cloud Native, những ứng dụng sinh ra để chạy trên Cloud. 

- **Amazon Cognito** là dịch vụ được quản lý bởi AWS có chức năng xác thực, cấp phép và quản lý người dùng cho các ứng dụng web và di động. Người dùng có thể đăng nhập trực tiếp bằng tên người dùng và mật khẩu hoặc thông qua một bên thứ ba như Facebook, Amazon hoặc Google.
- Hai thành phần chính của Amazon Cognito là *User Pool và Identity Pool*
    + **User Pool** là thư mục người dùng cung cấp các tùy chọn đăng ký và đăng nhập cho người dùng ứng dụng.
    + **Identity Pool** cấp cho người dùng quyền truy cập vào các dịch vụ AWS khác.
> Ví dụ Amazon Cognito - User Pool 1

![Module_05_6_Amazon_Cognito_User_Pool_1](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_6_Amazon_Cognito_User_Pool_1.png)

- **User Pool**: Người dùng có thể đăng nhập trực tiếp bằng tên người dùng và mật khẩu hoặc thông qua một bên thứ ba như Facebook, Amazon hoặc Google. 

> Ví dụ Amazon Cognito - User Pool 2

![Module_05_7_Amazon_Cognito_User_Pool_2](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_7_Amazon_Cognito_User_Pool_2.png)

- **User Pool**: Sau khi đăng nhập với user pool, người dùng ứng dụng có thể truy cập các tài nguyên mà ứng dụng cho phép. 

> Ví dụ Amazon Cognito - User Pool 3

![Module_05_8_Amazon_Cognito_User_Pool_3](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_8_Amazon_Cognito_User_Pool_3.png)

- **User Pool**: Sau khi đăng nhập với user pool, người dùng ứng dụng có thể gọi đến API Endpoint (Backend) mà ứng dụng cho phép.

> Kiến trúc Amazon Cognito - User Pool kết hợp với Identity Pool

![Module_05_9_Amazon_Cognito_User_Pool_and_Identity_Pool](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_9_Amazon_Cognito_User_Pool_and_Identity_Pool.png)

- **User Pool** kết hợp với **Identity Pool** để truy cập trực tiếp vào các dịch vụ của AWS. 

## **IV. AWS Organization**
- **AWS Organizations** giúp quản lý và điều hành tập trung môi trường của mình bao gồm nhiều AWS account.
- **AWS Organizations** có thể tạo các tài khoản AWS mới và phân bổ tài nguyên, sắp xếp các AWS account theo **OU (Organization Unit)**, đồng thời đơn giản việc thanh toán với thanh toán tập trung (**consolidated billing**).
- **AWS Organization** có thể áp các chính sách kiểm soát dịch vụ (**Service Control Policies**) lên các **OU hoặc các AWS account**, SCP chỉ thiết lập giới hạn quyền tối đa cho các IAM User hoặc IAM role trong OU hoặc AWS account được gán.
- **SCP cũng cho phép thiết lập deny-based policy**.

> Kiến trúc AWS Organization

![Module_05_10_AWS_Organization](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_10_AWS_Organization.png)

## **V. AWS Identify Center (SSO)**
- **AWS Identity Center** giúp quản lý quyền truy cập tới AWS account và cả các ứng dụng bên ngoài.
    + **Identity source** có thể nằm trong AWS Identity Center hoặc được liên kết với Active Directory. (AWS Managed Microsoft AD, On-premises Microsoft AD thông qua Two way trust hoặc AD Connector).
- **Permission Set** xác định khả năng truy cập mà User và Group có đối với các tài khoản AWS trong AWS Organization. Các bộ quyền được lưu trữ trong AWS Identity Center và được cung cấp cho tài khoản AWS dưới dạng IAM roles. Bạn có thể gán nhiều quyền cho một User.

> Kiến trúc AWS Identify Center (SSO)

![Module_05_11_AWS_Identify_Center_SSO](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_11_AWS_Identify_Center_SSO.png)

## **VI. AWS Key Management Service - KMS**

- **AWS Key Management Service** giúp tạo và quản lý các encryption key, phục vụ cho mục đích encrypt/decrypt dữ liệu trên AWS. (**Encryption at rest**)
- **Encryption key** luôn nằm trong AWS KMS, đảm bảo tiêu chuẩn FIPS 140-2.
- **CMK (Customer Managed Key)** đóng vai trò là tài nguyên chính trong AWS KMS. CMK có thể có kích thước tới 4KB. Tuy nhiên thông thường, chúng ta chỉ sử dụng CMK cho mục đích tạo, mã hóa và giải mã **Data Key** - loại khóa được dùng bên ngoài AWS KMS để mã hóa dữ liệu.

> Kiến trúc AWS KMS

![Module_05_12_AWS_KMS](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_12_AWS_KMS.png)

- AWS Key Managenment Service giúp tạo và quản lý các encryption key, phục vụ cho mục đích encrypt/decrypt dữ liệu trên AWS. 

## **VII. AWS Security Hub**
- **AWS Security Hub** là dịch vụ cho phép chúng ta thực hiện kiểm tra bảo mật dựa trên các tiêu chuẩn và best practices.
- **Security Hub** chạy liên tục, kiểm tra cấu hình các dịch vụ trong tài khoản AWS và kiểm tra bảo mật dựa trên các best practice của AWS và tiêu chuẩn ngành (VD: **PCIDSS**).
- **Security Hub** cung cấp kết quả kiểm tra dưới dạng điểm số và giúp chúng ta xác định các tài khoản và tài nguyên cụ thể cần được chú ý.
> Ví dụ dùng Security Hub

![Module_05_13_AWS_Security_Hub](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_13_AWS_Security_Hub.png)

- **Security Hub** chạy liên tục, kiểm tra cấu hình các dịch vụ trong tài khoản AWS và kiểm tra bảo mật dựa trên các best practice của AWS và tiêu chuẩn ngành (VD: **PCIDSS**)

> Giao diện khi Test Security Hub

![Module_05_14_AWS_Security_Hub_Test](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_14_AWS_Security_Hub_Test.png)

- Security Hub cung cấp kết quả kiểm tra dưới dạng điểm số và giúp chúng ta xác định các tài khoản và tài nguyên cụ thể cần được chú ý. 

## **VIII. Thực hành và nghiên cứu bổ sung**
