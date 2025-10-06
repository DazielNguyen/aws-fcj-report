# **Module 2 - Các dịch vụ mạng trên AWS**
## **III. VPN & Direct Connect**
### 1. Giới thiệu về VPN & và Direct Connet

- Đây là tính năng dùng để kết nối giữa môi trường on-premises và môi trường trên Cloud. Hay người ta thường hay gọi là môi trường Hybrid. 

- Hybrid ở đây là gì? Là có nghĩa rằng chúng ta chạy một phần dịch vụ ở local hay được gọi là on-premises và một phần dịch vụ trên chạy trên điện toán đám mây ở trên AWS. 
### 2. VPN Site to Site

- **VPN Site to Site** dùng trong mô hình hybrid để thiết lập kết nối liên tục giữa môi trường trung tâm dữ liệu truyền thống tới môi trường VPC của AWS. 

- Việc thiết lập kết nối sẽ cần 2 đầu endpoint ở phía AWS và phía khách hàng: 

    + **Virtual Private Gateway** Được quản lí hoàn toàn AWS (chia 2 endpoint ở 2 đầu 2 AZ)

    + **Customer Gateway**: Đầu endpoint phía khách hàng, có thể là thiết bị phần cứng hoặc software appliance. 

***Link hướng dẫn tất cả những thiết bị, software application...***: [https://docs.aws.amazon.com/vpn/latest/s2svpn/your-cgw.html]

### 3. VPN Client to Site
- **VPN Client to Site**: Cho phép một host truy cập tới tài nguyên trong VPC. 

- Chi phí dịch vụ khá cao, cho nên thường khi sử dụng Client to Site thì thường sẽ dùng qua dịch vụ **Third Party** của AWS cung cấp. 

- Khuyến khích sử dụng VPN Client to Site trong **AWS Market Place**.

### 4. AWS Direct Connect

- **AWS Direct Connect** là dịch vụ cho phép tạo kết nối riêng tư từ trung tâm dữ liệu truyền thống tới AWS.

- Độ trễ khoảng **20ms - 30ms**. 

- **AWS Direct Connect** ở Việt Nam hiện tại sẽ thông qua AWS Direct Connect partners và hoạt động dưới dạng ***Hosted Connections***. (Nếu trực tiếp tới AWS thì là ***Dedicated Connections***)

    + Băng thông Direct Connect có thể thay đổi lên/xuống tùy nhu cầu.   

- Trong thực tế khi đi làm Cloud Engineer thì mình không bao giờ được cấu hình **Direct Connect** này, hầu hết sẽ có đội ngũ Partner sẽ làm thay.

- **Direct Connect** là đường kết nối ở mức thấp không có thực hiện mã hóa dữ liệu, sau khi đấu nối thực hiện Direct Connect xong thì chúng ta phải sử dụng thêm VPN Site to Site.

## **IV. Elastic Load Balancing**

### 1. Tổng quan về Elastic Load Balancing.
- **Elastic Load Balancing** (ELB) là một dịch vụ cân bằng tải được quản lí bởi AWS, có chức năng phân phối lưu lượng cho nhiều EC2 Instance hoặc Container.

- Sử dụng giao thức **HTTP, HTTPS, TCP và SSL (TCP bảo mật).**

- Có thể nằm ở -> **Public** hoặc **Private** Subnet.

- Mỗi ELB sẽ được cấp tên DNS và kết nối thông qua DNS. Chỉ có Network Load Balancer hỗ trợ gán IP tĩnh. 

- ELB không kết nối qua địa chỉ IP, chỉ kết nối qua DNS trừ ELB - Network Load Balancer.

- ELB có tính năng **health check**, không gửi lưu lượng đến các Instance không đạt **health check**.

- Bao gồm 4 loại: 
    + **Application Load Balancer**
    + **Network Load Balancer** -> Hỗ trợ gán IP tĩnh
    + **Classic Load Balancer** -> Giá cao
    + **Gateway Load Balancer** -> Mới nhất

- **Sticky session (session affinity):** Tính năng cho phép các kết nối được gán vào một target nhất định. Việc này đảm bảo các requests từ một user trong một session sẽ được gửi tới cùng một target. 

- **Sticky session** là cần thiết trong trường hợp các máy chủ ứng dụng **lưu trữ thông tin trạng thái của người dùng** tại server. 

    + Hoạt động trên **Network Load Balancer, Application Load Balancer, Classic Load Balancer.**

- ELB cung cấp tính năng lưu trữ logs truy cập **(access logs)** chugns ta có thể sử dụng access logs để phân tích truy cập, trouble shoot. Logs truy cập sẽ được lưu trữ vào một dịch vụ lưu trữ đối tượng là **Amazon S3** (Simple Storage Service).


### 2. ELB - Application Load Balancer

- **Application Load Balancer** (ALB) là một dịch vụ cân bằng tải được quản lí bởi AWS, hoạt động ở **Layer 7**. 

- Sử dụng giao thức **HTTP, HTTPS**

- Hỗ trợ tính năng **path-based routing**. (/mobile /desktop sẽ được route tới 2 target group khác nhau) 
    
    + Application Load Balancer -> Hỗ trợ tính năng **path-based routing** -> Giả sử các ứng dụng mobile có nhóm máy chủ ứng dụng riêng -> Sẽ được Route tới 2 target group khác nhau. -> Target group (gồm nhiều target nhỏ khác nhau). 

- Cho phép **route traffic** tới cả target nằm ngoài VPC (IP address), EC2, Lambda, Container (ECS, EKS). 

***Kiến trúc ELB - Application Load Balancer***

![4.2 ELB - Application Load Balancer](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_03_VPN_DirectConnect_LoadBalancer_ExtraResources/Image_module_02_03/4.2%20ELB%20-%20Application%20Load%20Balancer.png)

### 3. ELB - Network Load Balancer

- **Network Load Balancer** (NLB) là một dịch vụ cân bằng tải được quản lí bởi AWS, protocol hoạt động ở Layer 4. 

    + ***Quản lí hoàn toàn bởi AWS hiểu sao cho đúng?*** 
    + Thì mình không cần phải lo về việc **auto-scale** cho nó.

- Sử dụng giao thức **TCP, TLS**. 

- Hỗ trợ tính năng **set IP tĩnh**. 

- Hỗ trợ **Hiệu năng cao nhất trong các loại Load Balancer** có khả năng xử lý đến hàng triệu request. 
    + **Performance:** Extreme Performance

- Cho phép route traffic tới cả target nằm ngoài VPC (IP address), EC2, Container (ECS, EKS).

### 4. ELB - Classic Load Balancer

- **Classic Load Balancer** (CLB) là một dịch vụ cân bằng tải được quản lý bởi AWS, hoạt động ở Layer 4 và Layer 7. 

- Sử dụng giao thức **HTTP, HTTPS, TCP, TLS.**

- Cost: Cao hơn ALB và NLB. 

- Tính năng: Ít tính năng cao cấp hơn ALB và NLB, hiện tại rất ít được sử dụng 
 
- Cho phép Route traffic tới EC2. 

### 5. ELB - Gateway Load Balancer

- **Gate Load Balancer** (GLB) là một dịch vụ cân bằng tải được quản lí bởi AWS, protocol hoạt động ở Layer 3.

- **Gate Load Balancer** lắng nghe toàn bộ IP packets và foward tới target group chỉ định. 

- Sử dụng GENEVE protocol trên Port 6081

- Cho phép route traffic tới các Virtual appliance được AWS hỗ trợ.

- Danh sách vendor hỗ trợ.

[https://aws.amazon.com/vi/elasticloadbalancing/partners/]

***Mô hình thường thấy khi sử dụng Gateway Load Balancer:***

![4.5 Model Gateway Load Balancer](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_03_VPN_DirectConnect_LoadBalancer_ExtraResources/Image_module_02_03/4.5%20Model%20Gateway%20Load%20Balancer.png)

***Giải thích:***
- Để ý chiều đi của mô hình từ 1 -> 5 gạch màu tím , còn đường về thì ngược lại.
- Ta thấy một lớp tường lửa nằm ở VPC khác nó là dịch vụ hỗ trở ở VPC của chúng ta.

_______________________________________________________________
## **V. Thực hành và nghiên cứu bổ sung.** 

### **Lab: 000003**
 - Khởi tạo VPC.
    + Cấu hình tường lửa VPC 
    + Thực hành tạo 1 VPC
    + Cấu hình Site to Site VPN

### **Lab: 000058**
 - System Manager - Session Manager 
    + Tạo kết nối đến máy chủ EC2
    + Quản lí sessioin logs
    + Sử tính năng Port Forwarding

### **Lab: 000019**
 - Thiết lập VPC Peering
    + Cập nhật Network ACL 
    + Tạo kết nối Peering 
    + Cấu hình Route tables 
    + Kích hoạt Cross-Peer DNS. 

### **Lab: 000020**
 - Thiết lập Transit Gateway
    + Thiết lập hạ tầng
    + Tạo Transit Gateway -> Nối nhiều VPC lại với nhau
    + Transit Gateway Attachments
    + Tạo Route Table cho TGW
    + Thêm Gateway vào Route Tables & Kiểm tra kết quả

### **Lab: 000010**
 - Hybrid DNS
    + Thiết lập Hybrid DNS
    + Tạo Outbound Endpoint
    + Tạo Route 53 Resolver Rule
    + Tạo Inbound Endpoint.

### **[Nghiên cứu bổ sung] - AWS Advanced Networking - Specialty Study Guide**

Link: [https://www.amazon.com/Certified-Advanced-Networking-Official-Study/dp/1119439833]

***Phần hướng dẫn của Tuần 2:***

- Tài liệu giúp chuẩn bị kiến thức cho bài thi AWS Advanced Networking - Specialty Study Guide

- Đánh giá của chuyên gia về các nguyên tác thiết kế của AWS phù hợp với mục tiêu thi và giải thích chi tiết về các chủ đề thi chính kết hợp với các kịch bản trong thực tế.

***Phần hướng dẫn của Tuần 1:***

- Tìm hiểu về các: 
	+ Khái nghiệm 
	+ Nguyên tắc thiết kế
	+ Biện pháp tốt nhất về kiến trúc để thiết kế và vận hành hệ thống của bạn trong môi trường điện toán đám mây. 

- Sử dụng Framework bằng cách trả lời các câu hỏi. 
	+ Cần biết được mức độ phù hợp giữa kiến trúc của mình với các phương pháp tốt nhất được khuyến nghị. 
- Khi sử dụng AWS WAF tích hợp trên AWS Management Console sẽ có hướng dẫn để cải thiện kiến trúc hiện tại của mình. 












