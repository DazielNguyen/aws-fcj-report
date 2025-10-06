# **Module 2 - Các dịch vụ mạng trên AWS**
## **II. VPC Peering & Transit Gateway**
### 1. VPC Peering
- Khi tạo 2 VPC trong thực tế thì 2 VPC này không liên quan gì đến với nhau, thì nếu bạn có nhu cầu kết nối giữa 2 VPC này, hoặc 1 máy chủ trong VPC và kết nối được 5 máy chủ trong VPC 2 thì phải làm như thế nào? -> Dùng **VPC Peering**.
- **VPC Peering** là tính năng giúp kết nối **hai hay nhiều VPC** đề các tài nguyên bên trong hai VPC đó có thể liên lạc **trực tiếp** với nhau không cần thông qua Internet, góp phần gia tăng tính bảo mật cho VPC. 

- **VPC Peering** là kết nối cần tạo 1:1 giữa hai VPC thành viên, không hỗ trợ Transitive Routing.

- **VPC Peering** không hỗ trợ khi 2 VPC bị overlap IP address space.

***Kiến trúc VPC Peering***
![2.1 VPC Peering](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_02_VPC%20Peering%20%26%20Transit%20Gate%20/Image_module_02_02/2.1%20VPC%20Peering.png)

***Lưu ý:***
- Khi tạo Peering Connection trong kiến trúc bạn đã thấy, đã được chấp thuận bởi VPC có Peering Connection, nhưng chúng vẫn không thể nào kết nối được với nhau, thì phải làm sao? 
- Giải pháp: Mình phải tự tay cấu hình cái bảng định tuyến Custom Route Table mà được associate và gán được vào cái Subnet có máy chủ EC2. 
- Muốn đi tới đâu phải set up ID của VPC này đến IP của VCP mình muốn đến và ngược lại. 

***Kiến trúc VPC Peering_Real_time***

![2.2 VPC Peering Real_time](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_02_VPC%20Peering%20%26%20Transit%20Gate%20/Image_module_02_02/2.2%20VPC%20Peering%20Real_time.png)

***Lưu ý:***

- Tuy nhiên trong thực tế chúng ta có rất nhiều VPC, và tính năng **Peering** có thể hỗ trợ chúng ta tạo ra các Peering giữa các VPC trong điều kiện như: 
    + Nằm trong các Region khác nhau. 
    + Nằm trong các Account khác nhau. 
- Trong một doanh nghiệp thực tế họ có cả ngàn Account khác nhau, nên việc Peering hỗ trợ giữa các Account rất giúp ích cho doanh nghiệp, có thể kết nối nhiều máy chủ khác nhau ở các VPC khác nhau mượt mà, nhưng chúng ta phải ra rất nhiều VPC Connection

***Chuyện gì sẽ xảy ra nếu chúng ta kết nối 30 VPC?***

- **30 VPC Peering** => **435 Peering connections!!!** 
Ngồi cấu hình từng cái thôi cũng đù người=))))) Vấn đề giải quyết ở dưới.....

### 2. Transit Gateway
- Kiến trúc Transit Gateway không giống như VPC Peering là quan hệ 1:1, và chúng ta có thể hiểu rằng Transit Gateway như 1 cái hub trung tâm mạng.

- **Transit Gateway** được dùng kết nối các VPC và mạng on-premises thông qua một hub trung tâm. Điều này đơn giản hóa mạng và kết thúc các mối quan hệ định tuyến phức tạp 

- **Transit Gateway Attachment** là một công cụ để gán các subnet từng VPC cần kết nối với nhau vào một TGW đã được khởi tạo. Transit Gateway Attachment hoạt động ở quy mô Availability Zone *(AZ-level)*.

- Trong VPC, khi một subnet ở một AZ sẽ gán Transit Gateway Attachment với một TGW, các subnet khác trong cùng AZ đều có thể kết nối tới TGW đó.   

    + Giả sử VPC của mình có các Subnet rãi đều ở 3 AZ khác nhau, mình có thể cần đến 3 Transit Gateway Attachment.

- Các tập đoàn lớn thường ưa chuộng việc sử dụng 
**Transit Gateway**.

***Kiến trúc Transit Gateway***

![2.3 Transit Gateway](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_02_VPC%20Peering%20%26%20Transit%20Gate%20/Image_module_02_02/2.3%20Transit%20Gateway.png)

***Lưu ý***:

- Chúng ta có 4 cái VPC, như ảnh cấu trúc VPC Peering thì chúng ta cần phải tạo 6 cái Peering Connection.

- Nhưng trong cấu trúc này chỉ cần tạo 1 cái Transit Gateway thôi.

- Khi tạo Transit Gateway xong, thì mình tạo các Transit Gateway Attachment trong từng VPC khác nhau sẽ kết nối với nhau. 

- Nhưng nó vẫn giống VPC Peering ở chỗ là mình phải cấu hình cái Route table cho từng cái Transit Gateway Attachment đó.
