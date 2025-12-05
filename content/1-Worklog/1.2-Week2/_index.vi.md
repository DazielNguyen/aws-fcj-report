---
title: "Worklog Tuần 2"
date: "2025-09-15"
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

- **Hiểu rõ AWS VPC:** Nắm vững khái niệm cơ bản về VPC (Virtual Private Cloud) như một môi trường mạng logic cô lập, bao gồm các thành phần chính như Subnets (Public và Private), Route Tables, và ENI.

- **Kiểm soát lưu lượng và bảo mật:** Học cách cấu hình các lớp bảo mật (Security Groups và NACLs) và kiểm soát đường đi của lưu lượng mạng ra/vào Internet (Internet Gateway và NAT Gateway).

- **Kết nối mạng phức tạp:** Phân biệt và biết cách sử dụng các phương thức kết nối giữa các VPC (VPC Peering) và mô hình kết nối trung tâm (Transit Gateway).

- **Xây dựng môi trường Hybrid Cloud:** Tìm hiểu các giải pháp kết nối mạng tại chỗ (on-premises) với AWS, bao gồm VPN (Site-to-Site) và kết nối riêng tư (AWS Direct Connect).

- **Phân phối tải ứng dụng:** Hiểu chức năng của Elastic Load Balancing (ELB) và phân biệt được các loại bộ cân bằng tải khác nhau (ALB, NLB, CLB, GLB) để đảm bảo tính sẵn sàng cao và khả năng mở rộng cho ứng dụng.

### Các công việc cần triển khai trong tuần này:

| Thứ 	| Công việc 	| Ngày bắt đầu 	| Ngày kết thúc 	| Nguồn tài liệu và ghi chú học tập 	|
|---	|---	|---	|---	|---	|
| 2 	| - Tìm hiểu về AWS Virtual Private Cloud (VPC)<br>   + VPC là gì?<br>   + Cấu trúc của VPC được hoạt động như thế nào?<br>- Tìm hiểu về VPC-Subnets và kiến trúc của Subnet?<br>- Tìm hiểu về VPC-Route Table?<br>- Tìm hiểu về VPC-ENI và kiến trúc của VPC-ENI?<br>- Tìm hiểu về VPC-Endpoint và kiến trúc của VPC-Endpoint?<br>- Tìm hiểu về VPC-Internet Gateway và kiến trúc của VPC-Internet Gateway?<br>- Tìm hiểu về VPC-NAT Gateway và kiến trúc của VPC-NAT Gateway?<br>- Tìm hiểu về VPC-Security Group và kiến trúc của VPC-Security Group?<br>- Tìm hiểu về VPC-NACL và kiên trúc của VPC-NACL?<br>- Tìm hiểu về VPC-Flow Logs 	| 15/09/2025 	| 15/09/2025 	| [Module 02](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_02/Take_notes_module_02.md)	|
| 3 	| - Tìm hiểu về các dịch vụ mạng trên AWS?<br>- Tìm hiểu về VPC Peering và kiến trúc của VPC Peering?<br>- Tìm hiểu về Transit Gateway và kiến trúc của Transit Gateway?<br>- Nắm rõ các khái niệm về dịch vụ VPN & Direct Connect?<br>- VPN Site to Site là gì? Việc thiết lập nó như thế nào?<br>- Tìm hiểu về VPN Client to Site?<br>- AWS Direct Connect là gì? 	| 16/09/2025 	| 16/09/2025 	| [Module 02](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_02/Take_notes_module_02.md)	|
| 4 	| - Tìm hiểu về các khái niệm và tổng quan về Elastic Load Balancing? Và các loại ELB hiện nay?<br>- Tìm hiểu về ELB - Application Load Balancer và kiến trúc của nó?<br>- Tìm hiểu về ELB - Network Load Balancer và nắm rõ khái niệm?<br>- Tìm hiểu về ELB - Classic Load Balancer và nắm rõ khái niệm?<br>- Tìm hiểu về ELB - ELB - Gateway Load Balancer và kiến trúc của nó? 	| 17/09/2025 	| 17/09/2025 	| [Module 02](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_02/Take_notes_module_02.md) 	|
| 5 	| - **Lab 03** - Khởi tạo VPC<br>   1. Cấu hình tường lửa VPC<br>   2.Thực hành tạo 1 VPC<br>   3. Cấu hình Site to Site VPN<br>- **Lab 58** - System Manage - Session Manage<br>  1. Tạo kết nối đến máy chủ EC2<br>  2. Quản lí sessioin logs<br>  3. Sử tính năng Port Forwarding<br>- **Lab 19** - Thiết lập VPC Peering<br>  1. Cập nhật Network ACL<br>  2. Tạo kết nối Peering<br>  3. Cấu hình Route tables<br>  4. Kích hoạt Cross-Peer DNS 	| 18/09/2025 	| 18/09/2025 	| [Module 02](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_02/Take_notes_module_02.md)  	|
| 6 	| - **Lab 20** - Thiết lập Transit Gateway<br>  1. Thiết lập hạ tầng<br>  2. Tạo Transit Gateway -> Nối nhiều VPC lại với nhau<br>  3. Transit Gateway Attachments<br>  4. Tạo Route Table cho TGW<br>  5. Thêm Gateway vào Route Tables & Kiểm tra kết quả<br>- **Lab 10** - Hybrid DNS<br>  1. Thiết lập Hybrid DNS<br>  2. Tạo Outbound Endpoint<br>  3. Tạo Route 53 Resolver Rule<br>  4. Tạo Inbound Endpoint.<br>- Nghiên cứu bổ sung về **AWS Advanced Networking - Specialty Study Guid** 	| 19/09/2025 	| 19/09/2025 	| [Module 02](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_02/Take_notes_module_02.md) <br> [Research Link](https://www.amazon.com/Certified-Advanced-Networking-Official-Study/dp/1119439833)   	|

### Kết quả đạt được tuần 2:

- **Giải thích** được VPC là gì, vai trò của nó trong AWS, và các thành phần cốt lõi của nó (Subnet, Route Table, ENI).
- **Phân biệt** rõ ràng giữa Public Subnet (có Internet Gateway) và Private Subnet (sử dụng NAT Gateway để truy cập Internet).
- **So sánh và đối chiếu** hai cơ chế tường lửa chính: Security Group (stateful, áp dụng cho ENI) và NACL (stateless, áp dụng cho Subnet).
- **Trình bày** được cách thức kết nối riêng tư từ VPC đến các dịch vụ AWS (như S3) mà không cần qua Internet bằng VPC Endpoint.
- **Đánh giá** được ưu nhược điểm giữa hai giải pháp kết nối VPC: VPC Peering (kết nối 1:1, không hỗ trợ bắc cầu) và Transit Gateway (mô hình hub-and-spoke, đơn giản hóa quản lý).
- **Mô tả** được các phương thức thiết lập kết nối hybrid cloud, bao gồm VPN Site-to-Site (qua Internet) và AWS Direct Connect (kết nối vật lý riêng).
- **Phân loại** và **lựa chọn** được loại Elastic Load Balancer phù hợp cho từng kịch bản cụ thể:
   + **Application Load Balancer (ALB):** Cho lưu lượng HTTP/HTTPS (Layer 7), hỗ trợ path-based routing.
   + **Network Load Balancer (NLB):** Cho lưu lượng TCP/TLS (Layer 4), cần hiệu suất cực cao và IP tĩnh.
   + **Gateway Load Balancer (GLB):** Dùng để tích hợp các thiết bị mạng ảo (virtual appliances).
- **Xác định** được các bài thực hành (Lab) cần thiết để củng cố kiến thức đã học về VPC, Peering, Transit Gateway và các dịch vụ liên quan.