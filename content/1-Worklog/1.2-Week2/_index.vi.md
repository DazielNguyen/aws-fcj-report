---
title: "Worklog Tuần 2"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

- Học và thực hành dịch vụ Compute của AWS (EC2, AMI, EBS, Auto Scaling, ELB).
- Nắm vững kỹ năng giám sát và sao lưu với CloudWatch và AWS Backup.
- Tìm hiểu dịch vụ lưu trữ: S3, Storage Gateway, FSx.
- Thực hành triển khai, mở rộng và host website tĩnh.

### Các công việc cần triển khai trong tuần này:

| Thứ 	| Công việc 	| Ngày bắt đầu 	| Ngày kết thúc 	| Nguồn tài liệu và ghi chú học tập 	|
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------ |
| 2 	| - Tìm hiểu về AWS Virtual Private Cloud (VPC)<br>   + VPC là gì? <br>   + Cấu trúc của VPC được hoạt động như thế nào?<br>- Tìm hiểu về VPC-Subnets và kiến trúc của Subnet?<br>- Tìm hiểu về VPC-Route Table?<br>- Tìm hiểu về VPC-ENI và kiến trúc của VPC-ENI?<br>- Tìm hiểu về VPC-Endpoint và kiến trúc của VPC-Endpoint?<br>- Tìm hiểu về VPC-Internet Gateway và kiến trúc của VPC-Internet Gateway?<br>- Tìm hiểu về VPC-NAT Gateway và kiến trúc của VPC-NAT Gateway?<br>- Tìm hiểu về VPC-Security Group và kiến trúc của VPC-Security Group?<br>- Tìm hiểu về VPC-NACL và kiên trúc của VPC-NACL?<br>- Tìm hiểu về VPC-Flow Logs 	| 15/09/2025 	| 15/09 	| - Tài liệu: https://cloudjourney.awsstudygroup.com/<br>- Youtube: https://youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&si=W80Cdf_fSc6sjOV_<br>- Ghi chú: https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_01_VPC/Take_notes_module_02_01.md 	|
| 3 	| - Tìm hiểu về các dịch vụ mạng trên AWS?<br>- Tìm hiểu về VPC Peering và kiến trúc của VPC Peering?<br>- Tìm hiểu về Transit Gateway và kiến trúc của Transit Gateway?<br>- Nắm rõ các khái niệm về dịch vụ VPN & Direct Connect?<br>- VPN Site to Site là gì? Việc thiết lập nó như thế nào?<br>- Tìm hiểu về VPN Client to Site?<br>- AWS Direct Connect là gì? 	| 16/09/2025 	| 16/09/2025 	| - Tài liệu: https://cloudjourney.awsstudygroup.com/<br>- Youtube: https://youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&si=W80Cdf_fSc6sjOV_<br>- Ghi chú: https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_02_VPC%20Peering%20%26%20Transit%20Gate%20/Take_notes_module_02_02.md<br><br>https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_03_VPN_DirectConnect_LoadBalancer_ExtraResources/Take_notes_module_02_03.md 	|
| 4 	| - Tìm hiểu về các khái niệm và tổng quan về Elastic Load Balancing? Và các loại ELB hiện nay?<br>- Tìm hiểu về ELB - Application Load Balancer và kiến trúc của nó?<br>- Tìm hiểu về ELB - Network Load Balancer và nắm rõ khái niệm?<br>- Tìm hiểu về ELB - Classic Load Balancer và nắm rõ khái niệm?<br>- Tìm hiểu về ELB - ELB - Gateway Load Balancer và kiến trúc của nó? 	| 17/09/2025 	| 17/09/2025 	| - Tài liệu: https://cloudjourney.awsstudygroup.com/<br>- Youtube: https://youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&si=W80Cdf_fSc6sjOV_<br>- Ghi chú: https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_03_VPN_DirectConnect_LoadBalancer_ExtraResources/Take_notes_module_02_03.md 	|
| 5 	| - Thực hành Lab 03<br>- Thực hành Lab 58<br>- Thực hành Lab 19 	| 18/09/2025 	| 18/09/2025 	| - Tài liệu: https://cloudjourney.awsstudygroup.com/<br>- Youtube: https://youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&si=W80Cdf_fSc6sjOV_<br>- Ghi chú: https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/All_Lab_Practice_Module_02.md 	|
| 6 	| - Thực hành Lab 20<br>- Thực hành Lab 10<br>- Nghiên cứu bổ sung về AWS Advanced Networking - Specialty Study Guide 	| 19/09/2025 	| 19/09/2025 	| - Tài liệu: https://cloudjourney.awsstudygroup.com/<br>- Youtube: https://youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&si=W80Cdf_fSc6sjOV_<br>- Ghi chú: https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/All_Lab_Practice_Module_02.md 	|

### Kết quả đạt được tuần 2:

1. **Tính toán & Triển khai**

   - Hiểu rõ kiến thức về **Amazon EC2**, kiến trúc và các thành phần liên quan (AMI, Snapshot, Key Pair, EBS).
   - Triển khai và quản lý thành công EC2 cho cả Linux và Windows.
   - Thực hành triển khai ứng dụng thực tế **Node.js CRUD** trên EC2.
   - Nắm được các kỹ thuật tự động hóa với **User Data, Meta Data, AWS Systems Manager**.

2. **Khả năng mở rộng & Tính sẵn sàng cao**

   - Triển khai **EC2 Auto Scaling Group** để tự động điều chỉnh năng lực theo nhu cầu.
   - Cấu hình **Elastic Load Balancer (ELB)** để phân phối lưu lượng.
   - Tích hợp Auto Scaling với Load Balancer nhằm đảm bảo **high availability** và tối ưu chi phí.

3. **Giám sát & Quan sát hệ thống**

   - Sử dụng **Amazon CloudWatch** để giám sát hạ tầng và ứng dụng.
   - Tạo **metrics, dashboards, alarms** để theo dõi tình trạng hệ thống theo thời gian thực.
   - Quản lý log tập trung với **CloudWatch Logs**, thiết lập chính sách lưu trữ và phát hiện bất thường.
   - Thực hành thiết lập giám sát tự động qua **CloudFormation**.

4. **Bảo vệ & Sao lưu dữ liệu**

   - Thiết kế **AWS Backup Plans** cho nhiều dịch vụ (EBS, RDS, DynamoDB, EFS).
   - Áp dụng các mục tiêu **RTO/RPO** trong chiến lược khôi phục dữ liệu.
   - Cấu hình **SNS notifications** để nhận thông báo trạng thái sao lưu và phục hồi.

5. **Lưu trữ & Quản lý dữ liệu**
   - Hiểu rõ **Amazon S3** là dịch vụ lưu trữ đối tượng với lifecycle policies và storage classes.
   - Thực hành các tính năng: **versioning, ACL, Bucket Policy, CORS**.
   - Cấu hình **S3 Static Website Hosting** và kiểm tra truy cập công khai.
   - Tích hợp với **CloudFront** để tăng tốc độ phân phối nội dung và bảo mật bằng OAI.
   - Tìm hiểu **Amazon FSx for Windows File Server**: kiến trúc, tích hợp Windows, và dịch vụ lưu trữ file được quản lý hoàn toàn.
