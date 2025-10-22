---
title: "Worklog Tuần 4"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---


### Mục tiêu tuần 4:

- Tìm hiểu kiến thức toàn diện về các dịch vụ lưu trữ đa dạng trên AWS. 
- Tập trung sâu vào dịch vụ cốt lõi là **Amazon S3** (Simple Storage Service), một dịch vụ lưu trữ đối tượng, bao gồm các đặc tính (như độ bền 11 số 9, nhân bản 3 AZ), các lớp lưu trữ (Storage Classes).
- Học về các tính năng quan trọng như quản lý vòng đời **(Lifecycle Management)**, **Versioning** (lập phiên bản), và **Static Website Hosting**.
- Các giải pháp di dời dữ liệu quy mô lớn (dòng **Snow Family**), giải pháp lưu trữ hybrid kết nối on-premise với cloud (Storage Gateway), dịch vụ quản lý sao lưu tập trung (**AWS Backup**), và các khái niệm, chiến lược cơ bản về **Disaster Recovery (DR)**.

### Các công việc cần triển khai trong tuần này:

| Thứ 	| Công việc 	| Ngày bắt đầu 	| Ngày kết thúc 	| Nguồn tài liệu và ghi chú học tập 	|
|---	|---	|---	|---	|---	|
| 2 	| **Amazon Simple Storage Service - S3**<br><br>- Học về kiến trúc của **Amazon S3**, một dịch vụ lưu trữ dạng **đối tượng (object)**, phù hợp với dữ liệu ghi một lần đọc nhiều lần (WORM).<br>- Tìm hiểu về kĩ thuật nhân bản dữ liệu tự động trên **3 AZ** trong 1 Region để đảm bảo độ sẵn sàng cao.<br>- Tìm hiểu về độ bền (**durability**) của S3 được thiết kế lên đến 99.999999999% (11 số 9).<br>- Tìm hiểu về kĩ thuật upload (HTTP PUT) và truy cập (HTTP GET) dữ liệu S3 thông qua **REST API**.<br>- Học về kiến trúc của các **lớp lưu trữ (Storage Class)**, bao gồm S3 Standard, S3 Standard IA, S3 Intelligent Tiering, S3 One Zone IA, và Amazon Glacier/Deep Archive.<br>- Tìm hiểu về kĩ thuật quản lý vòng đời **(Object Life Cycle Management)** để tự động di chuyển object giữa các lớp lưu trữ theo thời gian.<br>- Tìm hiểu về kĩ thuật host **Static Website** (phù hợp cho Single Page Application) và cấu hình **CORS** (Cross-origin resource sharing).<br>- Tìm hiểu về kĩ thuật kiểm soát truy cập (Control Access) bằng **S3 Access Control List (ACL)** (gắn vào bucket/object) và **S3 Bucket Policy** (dễ quản lý hơn).<br>- Học về kiến trúc của **S3 Endpoint**, cho phép truy cập S3 bucket thông qua mạng riêng của AWS mà không cần Internet.<br>- Tìm hiểu về kĩ thuật **Versioning** (lập phiên bản) để khôi phục đối tượng sau khi vô tình xóa hay ghi đè, và hỗ trợ chống ransomware.<br>- Tìm hiểu về kĩ thuật tối ưu hiệu năng (performance) S3 bằng cách dùng **random prefix** (tiền tố ngẫu nhiên) cho object key, giúp S3 lưu trữ object trên nhiều partition.<br>- Học về kiến trúc của **S3 Glacier**, dịch vụ lưu trữ chi phí thấp, dài hạn, yêu cầu phải **retrieve (truy xuất)** dữ liệu (Expedited, Standard, Bulk) về S3 Bucket trước khi sử dụng. 	| 29/09/2025 	| 29/09/2025 	| **Documentation:** https://cloudjourney.awsstudygroup.com/<br>**Youtube:** https://youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&si=W80Cdf_fSc6sjOV<br>**Notes:** https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_04/Take_notes_module_04.md 	|
| 3 	| **Snow Family**<br><br>- Học về các dịch vụ **Snow Family** (Snowball, Snowball Edge, Snowmobile) dùng để di dời (migrate) dữ liệu quy mô PetaByte (PB) đến Exabyte (EB) từ on-premise lên AWS (S3 hoặc Glacier).<br>- Tìm hiểu về kĩ thuật của **Snowball Edge** là thiết bị đặc biệt có sẵn tài nguyên tính toán (compute) để xử lý dữ liệu local.<br><br>**Amazon Storage Gateway**<br><br>- Học về kiến trúc của **AWS Storage Gateway**, một giải pháp lưu trữ **Hybrid** kết hợp dung lượng lưu trữ trên AWS với on-premise.<br>- Tìm hiểu về kĩ thuật của ba loại gateway:<br>    + **File Gateway:** Cho phép lưu trữ file lên S3 qua giao thức NFS và SMB.<br>    + **Volume Gateway:** Cung cấp lưu trữ dạng khối (block storage) qua iSCSI, dữ liệu được lưu trên S3.<br>    + **Tape Gateway:** Cung cấp thư viện băng từ ảo (VTL) iSCSI, lưu dữ liệu tape ảo vào S3 hoặc Glacier. 	| 30/09/2025 	| 30/09/2025 	| **Documentation:** https://cloudjourney.awsstudygroup.com/<br>**Youtube:** https://youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&si=W80Cdf_fSc6sjOV<br>**Notes:** https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_04/Take_notes_module_04.md 	|
| 4 	| **Disaster Recovery on AWS**<br><br>- Tìm hiểu về kĩ thuật... thiết kế Disaster Recovery (DR) dựa trên hai chỉ số chính:<br>    + **RTO (Recovery Time Objective):** Thời gian cần thiết để phục hồi dịch vụ.<br>    + **RPO (Recovery Point Objective):** Khoảng thời gian tối đa mà dữ liệu có thể bị mất.<br>- Học về 4 chiến lược DR trên AWS: Sao lưu và khôi phục, Pilot Light, Low Capacity Active-Active, và Full Capacity Active-Active.<br><br>**AWS Backup**<br>- Học về dịch vụ **AWS Backup**, một dịch vụ quản lý tập trung, cho phép cấu hình và lập lịch (schedule), chính sách lưu giữ (retention) cho việc sao lưu nhiều tài nguyên AWS (EBS, EC2, RDS, EFS, Storage Gateway...). 	| 01/10/2025 	| 01/10/2025 	| **Documentation:** https://cloudjourney.awsstudygroup.com/<br>**Youtube:** https://youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&si=W80Cdf_fSc6sjOV<br>**Notes:** https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_04/Take_notes_module_04.md 	|
| 5 	| **Lab: 000057 - Khởi đầu với Amazon S3**<br>- Tạo S3 Bucket<br>- Upload dữ liệu trên S3<br>- Host static website trên S3<br><br>**Lab: 000013 - AWS Backup**<br>- Chuẩn bị hạ tầng<br>- Khởi tạo Backup Plan<br>- Thiết lập Notification<br>- Kiểm tra hoạt động<br><br>**Lab: 000014 - AWS Import/Export**<br>- Chuẩn bị máy ảo<br>- Import máy ảo lên AWS<br>- Export máy ảo từ AWS 	| 02/10/2025 	| 02/10/2025 	| **Documentation:** https://cloudjourney.awsstudygroup.com/<br>**Youtube:** https://youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&si=W80Cdf_fSc6sjOV<br>**Notes:** https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_04/Take_notes_module_04.md 	|
| 6 	| **Lab: 000024 - Storage Gateway**<br>- Khởi tạo Storage Gateway<br>- Khởi tạo File Sharing<br>- Kết nối File Share với máy<br><br>**Lab: 000025 - FSX**<br>- AWS Managed MS AD<br>- Triển khai Instance<br>- Thiết lập và sử dụng FSx<br><br>**[Nghiên cứu bổ sung] - AWS Skill Builder**<br><br>- Series các bài lý thuyết chuyên sâu cho chuyên gia lưu trữ trên AWS.<br>- Storage Learning Plan: Block Storage<br>- Storage Learning Plan: Object Storage 	| 03/10/2025 	| 03/10/2025 	| **Documentation:** https://cloudjourney.awsstudygroup.com/<br>**Youtube:** https://youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&si=W80Cdf_fSc6sjOV<br>**Notes:** https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_04/Take_notes_module_04.md<br>**Research Link:** https://explore.skillbuilder.aws/ 	|

### Kết quả đạt được tuần 4:

- **Dịch vụ S3 (Cơ bản):** Hiểu rõ **Amazon S3** là dịch vụ lưu trữ đối tượng (object storage), không phải lưu trữ khối, hoạt động theo mô hình WORM (Ghi 1 lần, đọc nhiều lần).
- **Bài học về Độ bền (Durability):** Nắm được S3 được thiết kế cho độ bền 11 số 9 (99.999999999%) bằng cách tự động nhân bản dữ liệu trên 3 Availability Zone (AZ).
- **Kĩ thuật Tối ưu chi phí S3:** Phân biệt được các lớp lưu trữ (Storage Classes) như **S3 Standard** (truy cập thường xuyên), **S3 Standard IA** (không thường xuyên), và **S3 Glacier** (lưu trữ dài hạn, chi phí thấp, phải retrieve).
- **Kĩ thuật Tự động hóa S3:**
    + Biết cách dùng **Object Life Cycle Management** để tự động chuyển dữ liệu xuống các lớp rẻ hơn (ví dụ: từ Standard sang Glacier) theo thời gian.
    + Hiểu về **Trigger Event** (ví dụ: kích hoạt serverless function khi upload file).
- **Kĩ thuật Bảo mật S3:** Phân biệt hai cơ chế kiểm soát truy cập: **S3 ACL** (cơ chế cũ) và **S3 Bucket Policy** (dễ dàng xác định quyền truy cập hơn).
- **Bài học về Bảo vệ Dữ liệu (S3):** Hiểu rõ tính năng **Versioning** (lập phiên bản) cho phép khôi phục lại các phiên bản cũ của file, giúp chống xóa nhầm hoặc tấn công ransomware.
- **Kĩ thuật Mạng S3:**
    + Nắm được cách dùng **S3 Endpoint** để truy cập S3 từ trong VPC qua mạng riêng của AWS mà không cần Internet.
    + Biết cách host **Static Website** trên S3 và cấu hình **CORS**.
- **Dịch vụ Di dời Dữ liệu (Migration):** Nhận biết dòng **Snow Family** (Snowball, Snowmobile) là giải pháp di dời dữ liệu *vật lý* quy mô lớn (Petabyte, Exabyte) từ on-premise.
- **Dịch vụ Lưu trữ Hybrid:** Hiểu **Storage Gateway** là giải pháp lưu trữ lai, cho phép các ứng dụng on-premise sử dụng các giao thức (NFS, SMB, iSCSI) để lưu trữ dữ liệu lên S3/Glacier.
- **Bài học về Disaster Recovery (DR):** Nắm được 2 khái niệm cơ bản để thiết kế DR là **RTO** (thời gian phục hồi) và **RPO** (lượng dữ liệu chấp nhận mất).
- **Dịch vụ Sao lưu (Backup):** Biết **AWS Backup** là dịch vụ quản lý tập trung, giúp tự động hóa việc sao lưu (schedule, retention) cho nhiều tài nguyên AWS (EBS, RDS, EFS...).
- **Thực hành:** Nắm được các bước thực hành tạo S3 bucket, host website tĩnh, và cấu hình AWS Backup.



