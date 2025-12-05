---
title: "Worklog Tuần 6"
date: "2025-10-13"
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

- Ôn tập các khái niệm cơ sở dữ liệu (CSDL) nền tảng, bao gồm RDBMS (khóa chính, khóa ngoại), các kỹ thuật tối ưu (Index, Partition), và các khái niệm về vận hành (Database Log, Buffer).
- Phân biệt rõ hai loại hệ thống CSDL chính: **OLTP** (Online Transaction Processing - xử lý giao dịch) và **OLAP** (Online Analytical Processing - xử lý phân tích hay Kho dữ liệu).
- Hiểu rõ dịch vụ CSDL quan hệ được quản lý **Amazon RDS**, bao gồm các tính năng cốt lõi như **Multi-AZ** (cho tính sẵn sàng cao) và **Read Replicas** (cho hiệu năng đọc).
- Tìm hiểu về **Amazon Aurora**, dịch vụ CSDL cloud-native của AWS, với kiến trúc lưu trữ chia sẻ độc đáo, hiệu năng cao và các tính năng vượt trội như **Zero Replication Lag**.
- Tìm hiểu về **Amazon Redshift**, dịch vụ kho dữ liệu (Data Warehouse) quy mô petabyte, được thiết kế cho OLAP, và hiểu rõ kiến trúc **MPP** cùng kỹ thuật **Columnar Storage**.
- Hiểu về vai trò của **Amazon ElastiCache** (Redis, Memcached) như một lớp bộ nhớ đệm (caching) tốc độ cao để giảm tải cho CSDL chính.


### Các công việc cần triển khai trong tuần này:

| Thứ 	| Công việc 	| Ngày bắt đầu 	| Ngày kết thúc 	| Nguồn tài liệu và ghi chú học tập 	|
|---	|---	|---	|---	|---	|
| 2 	| **Database Concepts**<br><br>- **Bài học:** Ôn tập các khái niệm CSDL căn bản như **Database** (hệ thống thông tin có cấu trúc) và **Session** (phiên làm việc).<br>- **Học về kiến trúc:** CSDL Quan hệ (RDBMS), bao gồm **Primary Key (Khóa chính)** để xác định duy nhất một hàng và **Foreign Key (Khóa ngoại)** để tạo liên kết giữa các bảng.<br>- **Tìm hiểu về kĩ thuật:** **Normalization (Chuẩn hóa)**, là kỹ thuật chia dữ liệu ra nhiều bảng (sử dụng khóa) để chống trùng lặp dữ liệu.<br>- **Tìm hiểu về kĩ thuật:** Tối ưu hiệu năng:<br>  + **Index (Chỉ mục):** Một cấu trúc dữ liệu giúp tăng tốc độ truy xuất (đọc), nhưng làm tăng chi phí ghi.<br>  + **Partition (Phân vùng):** Chia một bảng lớn thành nhiều phần nhỏ để tăng tốc độ truy vấn.<br>  + **Execution Plan (Kế hoạch thực thi):** Là tập hợp các bước mà CSDL quyết định dùng để truy cập dữ liệu (ví dụ: có dùng Index hay không).<br>- **Tìm hiểu về kĩ thuật:** Đảm bảo toàn vẹn và tốc độ:<br>  + **Database Log (Nhật ký CSDL):** Ghi lại tất cả thay đổi, quan trọng cho việc khôi phục (recovery) và đồng bộ hóa (replication).<br>  + **Buffer (Bộ nhớ đệm):** Vùng lưu trữ tạm thời trong RAM, giúp tăng tốc độ đọc vì đọc từ RAM nhanh hơn đọc từ ổ cứng.<br>- **Bài học:** Phân loại CSDL:<br>  + **RDBMS (ACID):** Cấu trúc cố định (Schema), tối ưu lưu trữ (Normalization), mở rộng theo chiều dọc (Vertical Scaling).<br>  + **NoSQL (BASE):** Cấu trúc linh hoạt (Dynamic Schema), tối ưu hiệu năng (Denormalization), mở rộng theo chiều ngang (Horizontal Scaling).<br>- **Bài học:** Phân loại hệ thống:<br>  + **OLTP (Online Transaction Processing):** Hệ thống xử lý giao dịch (ngân hàng, đặt hàng), cần xử lý nhanh các thao tác đọc/ghi/cập nhật và đảm bảo toàn vẹn (roll back).<br>  + **OLAP (Online Analytical Processing):** Hệ thống kho dữ liệu (Data Warehouse), lưu trữ dữ liệu lịch sử để phân tích phức tạp (báo cáo, tìm xu hướng). 	| 13/10/2025 	| 13/10/2025 	| [Module 06](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_06/Take_notes_module_06.md) 	|
| 3 	| **Amazon RDS**<br><br>- **Học về dịch vụ:** **Amazon RDS (Relational Database Service)**, một dịch vụ CSDL quan hệ được quản lý hoàn toàn (managed service), hỗ trợ các engine phổ biến (MySQL, PostgreSQL, Oracle, v.v.).<br>- **Bài học:** Mục tiêu của RDS là tự động hóa các tác vụ quản trị (cập nhật, sao lưu) để người dùng tập trung vào ứng dụng.<br>- **Tìm hiểu về kĩ thuật:** **Automated Backups** (Sao lưu tự động) CSDL và transaction log, cho phép **Point-in-Time Recovery** (phục hồi tại một thời điểm) trong vòng 35 ngày.<br>- **Học về kiến trúc:** **Multi-AZ (High Availability)**<br>  + Tự động tạo một bản sao *standby* (dự phòng) ở một AZ khác.<br>  + Sử dụng **Synchronous Replication** (sao chép đồng bộ).<br>  + Hỗ trợ **Automatic Failover** (tự động chuyển đổi) nếu CSDL chính gặp sự cố.<br>- **Học về kiến trúc:** **Read Replicas (Tối ưu Hiệu năng Đọc)**<br>  + Tạo ra các bản sao *chỉ đọc* để giảm tải cho CSDL chính (ví dụ: cho các tác vụ báo cáo).<br>  + Sử dụng **Asynchronous Replication** (sao chép bất đồng bộ), có thể gây ra "replication lag" (độ trễ).<br>- **Bài học:** RDS thường được sử dụng cho các ứng dụng **OLTP** và được bảo vệ bằng **Security Group**. 	| 14/10/2025 	| 14/10/2025 	| [Module 06](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_06/Take_notes_module_06.md) 	|
| 4 	| **Amazon Aurora**<br><br>- **Học về dịch vụ:** **Amazon Aurora**, một CSDL do AWS phát triển, tương thích MySQL/PostgreSQL, thuộc dịch vụ RDS nhưng có hiệu năng cao hơn (gấp 3-5 lần).<br>- **Học về kiến trúc:** Khác biệt lớn nhất của Aurora là **tái thiết kế lại tầng lưu trữ**.<br>- **Học về kiến trúc:** Một "Cluster" Aurora bao gồm 1 **Writer** (bản ghi) và tối đa 15 **Readers** (bản đọc), tất cả cùng **chia sẻ một phân vùng lưu trữ (Cluster Volume) duy nhất**.<br>- **Tìm hiểu về kĩ thuật:** Dữ liệu trên Cluster Volume được **nhân bản 6 lần qua 3 AZ** để đảm bảo độ bền.<br>- **Bài học:** Ưu điểm vượt trội của Aurora là **Zero Replication Lag** (không có độ trễ sao chép) vì các bản Readers đọc chung volume với Writer.<br>- **Tìm hiểu về kĩ thuật:** Các tính năng doanh nghiệp như **Backtrack** (tua ngược CSDL mà không cần restore) và **Global Database** (tạo bản sao chỉ đọc ở các Region khác nhau). 	| 15/10/2025 	| 15/10/2025 	| [Module 06](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_06/Take_notes_module_06.md) 	|
| 5 	| **Amazon Redshift**<br><br>- **Học về dịch vụ:** **Amazon Redshift**, một dịch vụ **Data Warehouse (Kho dữ liệu)** quy mô petabyte, được tối ưu cho **OLAP**.<br>- **Học về kiến trúc:** **Massively Parallel Processing (MPP)** (Xử lý song song hàng loạt).<br>  + **Leader Node (Nút Lãnh đạo):** Tiếp nhận, phân tích và điều phối truy vấn.<br>  + **Compute Nodes (Nút Tính toán):** Lưu trữ và thực thi các phần công việc song song.<br>- **Tìm hiểu về kĩ thuật:** **Columnar Storage (Lưu trữ dạng Cột)**.<br>  + Khác với OLTP (lưu theo hàng), Redshift lưu dữ liệu của *cùng một cột* gần nhau.<br>  + Kỹ thuật này cực kỳ hiệu quả cho các truy vấn phân tích (OLAP) (ví dụ: `Tính tuổi trung bình` chỉ cần đọc cột `Tuổi`).<br>- **Tìm hiểu về kĩ thuật:** **Redshift Spectrum**, cho phép chạy truy vấn SQL **trực tiếp trên dữ liệu nằm trong Amazon S3** mà không cần tải về.<br><br>**Amazon ElastiCache**<br><br>- **Học về dịch vụ:** **Amazon ElastiCache**, một dịch vụ bộ nhớ đệm (caching) trong bộ nhớ RAM tốc độ cao.<br>- **Mục tiêu:** Tăng tốc độ ứng dụng và **giảm tải cho cơ sở dữ liệu chính** (như RDS).<br>- **Tìm hiểu về** các engine hỗ trợ: **Redis** (hỗ trợ nhiều kiểu dữ liệu, thường được ưu tiên) và **Memcached**.<br>- **Bài học:** Trách nhiệm của người dùng là phải tự viết và quản lý **Caching Logic** (logic quyết định *cái gì* và *khi nào* cần cache) trong ứng dụng của mình. 	| 16/10/2025 	| 16/10/2025 	| [Module 06](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_06/Take_notes_module_06.md) 	|
| 6 	| **Lab: 000005 - Bắt đầu với Amazon RDS**<br><br>1. Tạo cơ sở dữ liệu (database) trên Amazon RDS<br>2. Kết nối ứng dụng vào CSDL<br>3. Sao lưu và Phục hồi<br><br>**Lab: 000043 - Dịch chuyển CSDL với DMS và SCT**<br><br>1. Các bước chuẩn bị<br>2. Oracle sang Amazon Aurora (PostgreSQL)<br>    2.1 Chuyển dổi Schema<br>    2.2 Dịch chuyển cơ sở dữ liệu. <br>**[Nghiên cứu bổ sung] - Database Internals**<br><br>- Tài liệu tìm hiểu cách thức vận hành bên trong của cơ sở dữ liệu. <br> [Database Internals Deep Distributed Systems](https://www.amazon.com/Database-Internals-Deep-Distributed-Systems/dp/1492040347)<br>**[Nghiên cứu bổ sung] - The Data Warehouse Toolkit**<br>- Tài liệu tìm hiểu cách thức thiết kế và các kỹ thuật được sử dụng trong việc xây dựng Data-warehouse<br>[Data Warehouse Toolkit Definitive Dimensional](https://www.amazon.com/Data-Warehouse-Toolkit-Definitive-Dimensional/dp/1118530802)	| 17/10/2025 	| 17/10/2025 	| [Module 06](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_06/Take_notes_module_06.md) 	|

### Kết quả đạt được tuần 6:

- **Bài học (Nền tảng):**
  + Phân biệt rõ ràng hai mô hình hệ thống: **OLTP** (Online Transaction Processing - xử lý giao dịch) và **OLAP** (Online Analytical Processing - xử lý phân tích, kho dữ liệu).
  + Nắm vững các kỹ thuật tối ưu CSDL cơ bản: **Index** (tăng tốc độ đọc) và **Partition** (chia nhỏ bảng).
  + Hiểu vai trò của **Database Log** (để khôi phục/đồng bộ) và **Buffer** (dùng RAM để tăng tốc).
- **Dịch vụ (RDS):**
  + Biết **Amazon RDS** là dịch vụ CSDL quan hệ (OLTP) được quản lý.
  + Phân biệt rõ 2 tính năng chính của RDS: **Multi-AZ** (dùng cho tính Sẵn sàng cao - HA) và **Read Replicas** (dùng để tăng hiệu năng đọc).
- **Kĩ thuật (Replication):**
  + Phân biệt **Synchronous Replication** (Sao chép đồng bộ - dùng cho RDS Multi-AZ) và **Asynchronous Replication** (Sao chép bất đồng bộ - dùng cho RDS Read Replicas, có thể bị trễ).
- **Dịch vụ (Aurora):**
  + Biết **Amazon Aurora** là CSDL hiệu năng cao, cloud-native.
  + Hiểu kiến trúc **lưu trữ chia sẻ (Cluster Volume)** của Aurora và lợi ích vượt trội là **Zero Replication Lag** (không có độ trễ).
  + Nắm được các tính năng cao cấp như **Backtrack** và **Global Database**.
- **Dịch vụ (Redshift):**
  + Biết **Amazon Redshift** là dịch vụ kho dữ liệu (OLAP).
  + Hiểu kiến trúc **MPP (Massively Parallel Processing)** (gồm Leader Node và Compute Nodes).
  + Nắm vững kỹ thuật cốt lõi của OLAP: **Columnar Storage (Lưu trữ dạng Cột)**, giúp tăng tốc các truy vấn phân tích.
- **Dịch vụ (ElastiCache):**
  + Biết **Amazon ElastiCache** (Redis/Memcached) là dịch vụ caching trong RAM.
  + Hiểu vai trò của caching là giảm tải cho CSDL chính.
  + Nhận thức được trách nhiệm phải tự viết **Caching Logic** trong ứng dụng.
- **Thực hành:**
  + Biết cách tạo và vận hành (backup/restore) một CSDL **RDS**.
  + Biết cách sử dụng dịch vụ DMS và SCT để **dịch chuyển (migrate)** CSDL từ Oracle sang Aurora.