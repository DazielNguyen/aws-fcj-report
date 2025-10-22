---
title: "Worklog Tuần 3"
date: "2025-09-22"
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

- Hiểu kiến thức toàn diện về các dịch vụ **máy chủ ảo (Compute VM)** trên AWS. 
- Tập trung vào dịch vụ cốt lõi là **Amazon EC2**, bao gồm cách lựa chọn cấu hình (**Instance Types**), các loại lưu trữ (**EBS, Instance Store**), và cách tự động hóa **(User data, Auto Scaling)**. 
- Tìm hiểu về các các dịch vụ liên quan như **Amazon Lightsail** (dịch vụ chi phí thấp), các giải pháp lưu trữ file chia sẻ **(EFS cho Linux và FSx cho Windows/Linux)**, và dịch vụ di dời ứng dụng **AWS MGN** để chuyển máy chủ lên AWS hoặc xây dựng **Disaster Recovery**.

### Các công việc cần triển khai trong tuần này:

| Thứ 	| Công việc 	| Ngày bắt đầu 	| Ngày kết thúc 	| Nguồn tài liệu và ghi chú học tập 	|
|---	|---	|---	|---	|---	|
| 2 	| **Amazon Elastic Compute Cloud (EC2)**<br>- Học về kiến trúc của Amazon EC2, một dịch vụ máy chủ ảo linh hoạt, có khả năng khởi tạo nhanh và co giãn tài nguyên mạnh mẽ.<br>- Tìm hiểu về kĩ thuật lựa chọn cấu hình máy chủ thông qua EC2 Instance Type, yếu tố quyết định các yếu tố như CPU, Memory, Network và Storage.<br>- Học về cách sử dụng AMI (Amazon Machine Image) để khởi tạo (provision) một hoặc nhiều EC2 Instances và dùng Key Pair (public và private key) để mã hóa thông tin đăng nhập.<br>- Tìm hiểu về kĩ thuật lưu trữ khối EBS (Elastic Block Store), vốn hoạt động độc lập, được replicate dữ liệu (nhân 3) để đảm bảo độ sẵn sàng và kết nối với EC2 qua mạng.<br>- Phân biệt EBS với Instance Store, là vùng đĩa NVME tốc độ cực cao nhưng dữ liệu sẽ bị xóa hết khi stop EC2.<br>- Học về kĩ thuật tự động hóa User Data, một đoạn script (bash shell hoặc powershell) chạy một lần khi khởi tạo EC2.<br>- Tìm hiểu về Meta Data, các thông tin liên quan đến EC2 (như IP, Hostname) có thể được truy cập từ chính máy chủ đó, thường dùng cho tự động hóa.<br>- Tìm hiểu về kĩ thuật EC2 Auto Scaling để tự động tăng (scale-out) hoặc giảm (scale-in) số lượng EC2 Instance dựa theo các điều kiện (scaling policy).<br>- Học về các EC2 Pricing Option (On-demand, Reserved Instance, Saving Plans, Spot Instance) để tối ưu chi phí. 	| 22/09/2025 	| 22/09/2025 	| **Documentation:** https://cloudjourney.awsstudygroup.com/<br>**Youtube:** https://youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&si=W80Cdf_fSc6sjOV<br>**Notes:** https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_03/Take_notes_module_03.md 	|
| 3 	| **Amazon Lightsail**<br>- Học về dịch vụ Amazon Lightsail, một giải pháp máy chủ ảo chi phí thấp (từ 3,5$/tháng) phù hợp cho các workload nhẹ, môi trường test/dev.<br>- Tìm hiểu về kĩ thuật kết nối Lightsail (nằm trong VPC đặc biệt) với VPC thông thường qua VPC Peering (chỉ bằng 1 click).<br><br>**Amazon EFS/FSX**<br>- Học về EFS (Elastic File System), dịch vụ lưu trữ file mạng (NFSv4) cho phép nhiều EC2 Instance (chỉ hỗ trợ Linux) mount vào cùng lúc, tính phí theo dung lượng sử dụng.<br>- Học về Amazon FSx, dịch vụ cho phép tạo NTFS volume (giao thức SMB) để gán vào nhiều EC2 Instance (hỗ trợ Windows và Linux).<br>- Tìm hiểu về kĩ thuật deduplication của FSx giúp giảm trùng lặp dữ liệu và giảm chi phí lưu trữ.<br><br>**AWS Application Migration Service (MGN)**<br>- Học về dịch vụ AWS MGN dùng để migrate (di dời) và replicate máy chủ (thật hoặc ảo) từ on-premise lên môi trường AWS.<br>- Tìm hiểu về kĩ thuật sao chép (replication) của MGN để phục vụ mục đích xây dựng Disaster Recovery Site với chi phí thấp (sử dụng các máy staging cấu hình nhỏ). 	| 23/09/2025 	| 23/09/2025 	| **Documentation:** https://cloudjourney.awsstudygroup.com/<br>**Youtube:** https://youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&si=W80Cdf_fSc6sjOV<br>**Notes:** https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_03/Take_notes_module_03.md 	|
| 4 	| **Lab: 000004 - Thao tác EC2 cơ bản.**<br>- Tạo máy chủ EC2<br>- Thực hiện snapshot EC2 Instance<br>- Cài đặt ứng dụng trên EC2<br><br>**Lab: 000027 - Quản lí tài nguyên bằng Tag và Resource Group**<br>- Sử dụng Tag<br>- Sử dụng Resource Group 	| 24/09/2025 	| 24/09/2025 	| **Documentation:** https://cloudjourney.awsstudygroup.com/<br>**Youtube:** https://youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&si=W80Cdf_fSc6sjOV<br>**Notes:** https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_03/Take_notes_module_03.md 	|
| 5 	| **Lab: 000008 - Quản lí tài nguyên với Amazon Cloud Watch**<br>- CloudWatch Agent<br>- Tạo CloudWatch Dashboard<br><br>**Lab: 000006 - Triển khai Autoscaling Group**<br>- Khởi tạo Launch Template<br>- Khởi tạo Target Group<br>- Khởi tạo Load Balancer<br>- Khởi tạo Auto Scaling Group<br>- Kiểm tra kết quả. 	| 25/09/2025 	| 25/09/2025 	| **Documentation:** https://cloudjourney.awsstudygroup.com/<br>**Youtube:** https://youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&si=W80Cdf_fSc6sjOV<br>**Notes:** https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_03/Take_notes_module_03.md 	|
| 6 	| **Lab: 000045 - Bắt đầu với Amazon Lightsail**<br><br>- Chuẩn bị<br>- Kiểm tra ứng dụng trên Lightsail<br>- Sử dụng Lightsail Loadbalancer<br>- Sử dụng RDS<br>- Dịch chuyển sang EC2.<br><br>**[Nghiên cứu bổ sung] - Microsoft Workloads on AWS**<br><br>- Series các bài thực hành bố sung dành cho việc chạy các máy chủ và ứng dụng của Microsoft trên AWS<br>- Bổ sung kiến thức về hệ điều hành<br>- Bổ sung các kiến thức về hệ điều hành Linux như LBI1, LBI2<br>- Bổ sung các kiến thức về hệ điều hành Window học thêm về hệ thống quản trị Bundo. Tham khảo các series thực hành 	| 26/09/2025 	| 26/09/2025 	| **Documentation:** https://cloudjourney.awsstudygroup.com/<br>**Youtube:** https://youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&si=W80Cdf_fSc6sjOV<br>**Notes:** https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_03/Take_notes_module_03.md<br>**Research Link:** [https://www.youtube.com/playlist?list=PLhr1KZpdzukdJ\|IxuIUM7pMB7aJ2_FfTP] 	|

### Kết quả đạt được tuần 3:


- **Dịch vụ EC2:** Hiểu rõ **EC2** là dịch vụ máy chủ ảo cốt lõi của AWS.
- **Kĩ thuật cấu hình EC2:** Biết cách lựa chọn **Instance Type** (cấu hình CPU, RAM, Network) và sử dụng **AMI** để khởi tạo hệ điều hành cho máy chủ.
- **Kĩ thuật bảo mật EC2:** Nắm được cách dùng **Key Pair** (public/private key) để mã hóa thông tin đăng nhập, thay vì dùng mật khẩu.
- **Dịch vụ lưu trữ (Storage):** Phân biệt rõ ràng 2 loại lưu trữ đĩa chính cho EC2:
    + **EBS (Elastic Block Store):** Là ổ đĩa mạng, hoạt động độc lập, dữ liệu được replicate x3 trong 1 AZ (độ sẵn sàng 99.999%), có thể backup bằng snapshot.
    + **Instance Store:** Là ổ đĩa vật lý (NVME) tốc độ cực cao, nhưng dữ liệu là tạm thời (sẽ bị xóa khi stop EC2), thường dùng cho cache/buffer hoặc swap.
- **Kĩ thuật tự động hóa (Automation):**
    + Biết cách dùng **User Data** để chạy script 1 lần khi máy chủ khởi động (ví dụ: cài đặt web server).
    + Hiểu **Meta Data** là gì và cách dùng nó để lấy thông tin (IP, hostname) của máy chủ từ bên trong chính nó, phục vụ cho các script tự động hóa.
- **Kĩ thuật co giãn (Scaling):** Nắm vững khái niệm **EC2 Auto Scaling** để tự động tăng (scale-out) hoặc giảm (scale-in) số lượng máy chủ theo tải (ví dụ: khi ActiveConnectionCount cao hoặc thấp).
- **Kĩ thuật tối ưu chi phí (Pricing):** Nhận biết 4 mô hình giá EC2: **On-demand** (theo giờ/giây, đắt nhất), **Reserved Instance** (cam kết 1-3 năm), **Saving Plans** (cam kết 1-3 năm, linh hoạt hơn), và **Spot Instance** (giá rẻ, tận dụng tài nguyên dư nhưng có thể bị đòi lại).
- **Dịch vụ Lightsail:** Hiểu **Amazon Lightsail** là dịch vụ VM chi phí thấp, đơn giản hóa, phù hợp cho workload nhẹ, và biết cách peering nó với VPC.
- **Dịch vụ lưu trữ file (File Storage):** Phân biệt 2 dịch vụ lưu trữ file chia sẻ cho nhiều máy chủ:
    + **EFS (Elastic File System):** Dùng cho **Linux** (giao thức NFSv4), tính phí theo dung lượng sử dụng.
    + **FSx:** Dùng cho **Windows/Linux** (giao thức SMB), hỗ trợ tính năng deduplication để giảm chi phí.
- **Dịch vụ di dời (Migration):** Hiểu **AWS MGN** là dịch vụ để di dời máy chủ từ on-premise lên AWS hoặc dùng để xây dựng hệ thống **Disaster Recovery (DR)** với chi phí thấp thông qua staging area.
- **Thực hành:** Nắm được các bước thực hành cơ bản với EC2 (tạo, snapshot), triển khai một cụm Auto Scaling Group hoàn chỉnh (với Load Balancer), và làm quen với Lightsail.
