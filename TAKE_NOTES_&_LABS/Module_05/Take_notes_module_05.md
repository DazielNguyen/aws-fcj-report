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

## **III. Amazon Cognito**


## **IV. AWS Organization & AWS Identify Center (SSO)**


## **V. AWS KMS**


## **VI. Thực hành và nghiên cứu bổ sung**
