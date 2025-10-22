# **Module 6 - Dịch vụ Cơ sở dữ liệu trên AWS** 
## **I. Database Concepts**
> Video "Module 06-01 - Database Concepts review" là một bài giảng ôn tập lại các khái niệm cơ sở dữ liệu (CSDL) nền tảng, chuẩn bị cho việc tìm hiểu các dịch vụ CSDL trên nền tảng AWS.

### 1. Giới thiệu và Mục tiêu

- **Mục tiêu:** Video ôn tập các khái niệm cơ bản về CSDL trước khi đi sâu vào các dịch vụ của AWS (như RDS, Aurora, ElasticCache, Redshift).
- **Mô hình chia sẻ trách nhiệm:** Khi dùng dịch vụ CSDL của AWS, AWS sẽ quản lý phần hạ tầng (như hệ điều hành, cập nhật bản vá). Người dùng sẽ tập trung hơn vào phần ứng dụng, như thiết kế dữ liệu và tối ưu truy vấn để tăng hiệu năng.

### 2. Các Khái niệm CSDL Căn bản

- **Database (Cơ sở dữ liệu):** Là một **hệ thống các thông tin** có cấu trúc / bán cấu trúc, được lưu trữ trên các thiết bị lưu trữ nhằm thõa mãn yêu cầu khai thác thông tin đồng thời của nhiều người sử dụng hay nhiều chương trình ứng dụng chạy cùng một lúc với những mục đích khác nhau.
- **Phiên làm việc (Session):** Là khoảng thời gian tính từ thời gian bắt đầu kết nối vào hệ thống CSDL (time start) và thời gian kết thúc (time end) là khoảng thời gian bạn ngắt kết nối. Khi ứng dụng kết nối tới CSDL, nó tạo ra một phiên làm việc. CSDL hỗ trợ một số lượng phiên nhất định, nếu vượt quá có thể gây tắc nghẽn.

### 3. CSDL Quan hệ (RDBMS)

> Đây là loại CSDL tổ chức dữ liệu dưới dạng bảng (gồm hàng và cột).

![01_RDBMS](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_06/Image_module_06/01_RDBMS.png)

- **Primary Key (Khóa chính):** Là một cột (hoặc nhóm cột) dùng để **xác định duy nhất** một hàng (bản ghi) trong bảng. Giá trị của khóa chính không được trùng lặp.
- **Foreign Key (Khóa ngoại):** Là một cột trong một bảng, dùng để **tạo liên kết** với khóa chính của một bảng khác. Nó hoạt động như một tham chiếu chéo giữa các bảng vì nó tham chiếu đến khóa chính của một bảng khác, do đó thiết lập liên kết giữa chúng. 
* **Mục đích của Khóa:** Việc sử dụng khóa chính/khóa ngoại và chia dữ liệu ra nhiều bảng (gọi là **chuẩn hóa - Normalization**) giúp **chống trùng lặp dữ liệu** và tiết kiệm dung lượng lưu trữ.

### 4. Các Kỹ thuật Tối ưu Hiệu năng

> Kỹ thuật Index

![02_Index](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_06/Image_module_06/02_Index.png)

- **Index (Chỉ mục):**
    + **Công dụng:** Là một cấu trúc dữ liệu giúp **tăng tốc độ truy xuất dữ liệu** (đọc). Nó hoạt động giống như mục lục của một cuốn sách, giúp tìm dữ liệu nhanh chóng mà không cần "dò quét" (scan) toàn bộ bảng. Các **chỉ mục được sử dụng để định vị dữ liệu một cách nhanh chóng mà không cần phải tìm kiếm mọi hàng trong bảng cơ sở dữ liệu mỗi khi truy cập bảng cơ sở dữ liệu.** Chỉ mục có thể được tạo bằng cách sử dụng một hoặc nhiều cột của bảng cơ sở dữ liệu.

    + **Nhược điểm:** Làm **tăng chi phí ghi** (vì vừa phải ghi vào bảng, vừa phải cập nhật Index) và tốn thêm không gian lưu trữ.

> Kỹ thuật Parition

![03_Partition](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_06/Image_module_06/03_Partition.png)

- **Partition (Phân vùng):**
    + **Công dụng:** Là kỹ thuật **chia một bảng lớn thành nhiều phần nhỏ hơn** (gọi là các phân vùng). Khi truy vấn, hệ thống chỉ cần tìm kiếm trên các phân vùng liên quan thay vì toàn bộ bảng, giúp tăng tốc độ.

- **Execution Plan (Kế hoạch thực thi):**
    + **Khái niệm:** Là một tập hợp các bước mà CSDL sẽ sử dụng để truy cập dữ liệu (ví dụ: quyết định có dùng Index hay không). Kế hoạch truy vấn là một chuỗi các bước được sử dụng để truy cập dữ liệu trong hệ quản trị cơ sở dữ liệu quan hệ SQL. ... Khi một truy vấn được gửi đến cơ sở dữ liệu, trình tối ưu hóa truy vấn sẽ đánh giá một số phương án có thể khác nhau, chính xác để thực hiện truy vấn và trả về những gì nó cho là tùy chọn tốt

    + **Tầm quan trọng:** Đọc hiểu được Execution Plan là kỹ năng quan trọng nhất để tối ưu hóa các câu truy vấn phức tạp.

### 5. Đảm bảo Tính Toàn vẹn và Tốc độ

> Kỹ thuật Database Log

![04_Database_Log](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_06/Image_module_06/04_Database_Log.png)

- **Database Log (Nhật ký CSDL):**
    + **Khái niệm:** Là một tệp ghi lại **tất cả các thay đổi** xảy ra với CSDL.
    + **Công dụng:** Rất quan trọng cho hai việc: 
        1) **Khôi phục sau sự cố** (ví dụ, phục hồi dữ liệu bị mất giữa 2 lần backup) và 
        2) **Đồng bộ hóa dữ liệu** giữa CSDL chính và phụ.
- **Buffer (Bộ nhớ đệm):**
    + **Khái niệm:** Là một vùng lưu trữ tạm thời trong bộ nhớ chính (RAM).
    + **Công dụng:** Dữ liệu thường xuyên truy cập sẽ được lưu tại đây. Việc đọc dữ liệu từ RAM nhanh hơn rất nhiều so với đọc từ ổ cứng, do đó giúp tăng tốc độ truy xuất.

### 6. Phân loại Hệ thống CSDL

- **CSDL Quan hệ (RDBMS) vs. Phi quan hệ (NoSQL):**

| Đặc điểm | **CSDL Quan hệ (RDBMS)** | **CSDL Phi quan hệ (NoSQL)** |
| :--- | :--- | :--- |
| **Cấu trúc** | Bảng (hàng và cột), có cấu trúc cố định (Schema). | Đa dạng (Document, Key-Value, Wide-column, Graph), cấu trúc linh hoạt (Dynamic Schema). |
| **Ngôn ngữ** | SQL (Ngôn ngữ truy vấn có cấu trúc). | Đa dạng, không chỉ SQL. |
| **Mở rộng** | Thường mở rộng theo chiều dọc (Vertical Scaling - tăng sức mạnh máy chủ). | Thiết kế để mở rộng theo chiều ngang (Horizontal Scaling - thêm máy chủ). |
| **Tối ưu** | Tối ưu lưu trữ (Chuẩn hóa - Normalization). | Tối ưu hiệu năng, tính toán chấp nhận trùng lặp dữ liệu (Phi chuẩn hóa - Denormalization). |
| **Mô hình** | **ACID**: Tập trung vào tính nhất quán (Consistency) của dữ liệu. | **BASE**: Tập trung vào tính sẵn sàng cao (Availability) và hiệu năng. |

- **OLTP (Online Transaction Processing):**
    + **Khái niệm:** Là các hệ thống xử lý giao dịch trực tuyến, ví dụ như hệ thống đặt hàng, ngân hàng.
    + **Đặc điểm:** Cần xử lý **nhanh** các thao tác đọc, ghi, cập nhật thường xuyên và phải đảm bảo tính toàn vẹn dữ liệu (ví dụ: có khả năng "roll back" - hoàn tác - nếu giao dịch lỗi).
- **OLAP (Online Analytical Processing):**
    + **Khái niệm:** Là các hệ thống xử lý phân tích trực tuyến, thường gọi là **Kho dữ liệu (Data Warehouse)**.
    + **Đặc điểm:** Lưu trữ một lượng lớn dữ liệu lịch sử. Mục tiêu là để **phân tích dữ liệu phức tạp** (ví dụ: chạy báo cáo, tìm kiếm xu hướng kinh doanh) chứ không phải để xử lý giao dịch. Dữ liệu từ hệ thống OLTP thường sẽ được chuyển sang hệ thống OLAP để phân tích.

## **II. Amazon RDS**
### 1. Amazon RDS (Relational Database Service)
**Amazon RDS** là một dịch vụ cơ sở dữ liệu quan hệ được quản lý hoàn toàn (managed service).
- **Khái niệm:** Thay vì tự cài đặt, quản lý và bảo trì cơ sở dữ liệu trên các máy chủ ảo (EC2), AWS sẽ làm hết các công việc quản trị hạ tầng này.
- **Hỗ trợ đa nền tảng:** RDS hỗ trợ các hệ quản trị CSDL phổ biến như:
    + MySQL
    + PostgreSQL
    + Oracle
    + Microsoft SQL Server
    + MariaDB
* **Mục tiêu:** Dịch vụ này giúp tự động hóa các tác vụ quản trị tốn thời gian như cập nhật phần mềm, sao lưu, và khôi phục. Điều này cho phép người dùng (như lập trình viên, quản trị CSDL) tập trung vào việc tối ưu ứng dụng thay vì lo lắng về hạ tầng.
* **Kiến trúc:** Về bản chất, RDS chạy trên các máy chủ EC2 đã được AWS tối ưu hóa, sử dụng ổ cứng EBS cho lưu trữ và được bảo mật bằng Security Group.

### 2. Các Tính năng Chính của Amazon RDS

- Tập trung vào 3 tính năng quan trọng giúp giải quyết các thách thức của việc vận hành CSDL truyền thống:
    
    1. Tự động Sao lưu (Automated Backups) - Cả log và database - max 35 ngày

    + RDS tự động sao lưu CSDL và cả các file "log" giao dịch.
    + Tính năng này cho phép **Phục hồi tại một thời điểm chỉ định (Point-in-Time Recovery)**, giúp lấy lại dữ liệu về chính xác bất kỳ thời điểm nào trong vòng 35 ngày qua.
    + Việc sao lưu được thực hiện tăng dần (incremental) để tiết kiệm chi phí lưu trữ.
    
    2. Multi-AZ (Đa Vùng Sẵn sàng) - Cho Tính Sẵn sàng Cao (HA)
    > Cơ chế tự động fail over, Primary / Standby, hay còn gọi là cơ chế **Multi-AZ**

    ![05_Multi_AZ](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_06/Image_module_06/05_Multi_AZ.png)

    + **Vấn đề:** Nếu máy chủ CSDL chính bị hỏng, ứng dụng sẽ ngừng hoạt động.
    + **Giải pháp Multi-AZ:** Khi được kích hoạt, RDS tự động tạo ra một bản sao (standby) đồng bộ hoàn toàn của CSDL chính và đặt ở một Vùng Sẵn sàng (Availability Zone - AZ) khác.
    + **Cơ chế:** Dữ liệu được sao chép **đồng bộ (Synchronous Replication)**. Điều này có nghĩa là khi ứng dụng ghi dữ liệu, nó phải được xác nhận ghi thành công ở cả CSDL chính và CSDL dự phòng.
    + **Tự động Chuyển đổi (Automatic Failover):** Nếu CSDL chính gặp sự cố, RDS sẽ tự động chuyển hướng kết nối của ứng dụng sang CSDL dự phòng mà không cần can thiệp thủ công.
    + **Chi phí:** Tính năng này làm tăng gấp đôi chi phí CSDL, nên thường chỉ dùng cho các môi trường production quan trọng.

    3. Read Replicas (Bản sao chỉ đọc) - Để Tối ưu Hiệu năng Đọc

    + **Vấn đề:** Các tác vụ báo cáo (reporting) hoặc truy vấn phức tạp có thể làm chậm CSDL chính, ảnh hưởng đến người dùng.
    + **Giải pháp Read Replica:** RDS cho phép tạo ra một hoặc nhiều bản sao chỉ đọc của CSDL chính.
    + **Cơ chế:** Dữ liệu được sao chép **bất đồng bộ (Asynchronous Replication)**. Điều này có nghĩa là bản sao chỉ đọc có thể có "độ trễ" (replication lag) vài giây so với bản chính.
    + **Ứng dụng:** Các ứng dụng báo cáo, phân tích sẽ được cấu hình để kết nối vào các bản sao chỉ đọc này, giúp giảm tải hoàn toàn cho CSDL chính.
    
    4. Chạy với cơ chế tự động fail over , Primary / Standby , hay còn gọi là cơ chế Multi-AZ
    5. RDS thường được sử dụng cho các ứng dụng OLTP.
    6. RDS cung cấp tính năng mã hóa dữ liệu at rest và in transit.
    7. RDS cũng được bảo vệ bởi tính năng tường lửa giống như EC2 ( Security Group và NACL )
    8. Thay đổi quy mô (Thay đổi instance size ).
    9. Tự động tăng dung lượng lưu trữ ( Storage Auto scaling ).
> Kiến trúc RDS

![06_AWS_RDS](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_06/Image_module_06/06_AWS_RDS.png)

## **III. Amazon Aurora**

**Amazon Aurora** là một hệ quản trị CSDL do chính AWS phát triển thuộc Amazon RDS nên thừa hưởng các tính năng của RDS, được thiết kế để tương thích với MySQL và PostgreSQL.

- **Sự khác biệt lớn nhất:** Aurora **tái thiết kế lại hoàn toàn kiến trúc tầng lưu trữ (storage layer) bên dưới**. Nó không sử dụng ổ đĩa EBS như RDS thông thường.
- **Hiệu năng:** Cung cấp hiệu suất cao hơn (được quảng cáo là gấp 3-5 lần) so với RDS MySQL/PostgreSQL tiêu chuẩn, đặc biệt là với các tác vụ có **độ song song (concurrency) cao**.
- Các tính năng Amazon Aurora cung cấp: 
    + **Back Track** - Phục hồi lại DB về thời điểm trước đó. 
    + **Clone** - Tạo bản sao
    + **Global Database** - 1 Master bà Multi Read nằm ở các Region khác nhau
    + **Multi Master** - Multi Master database. 

#### Kiến trúc và Tính năng Vượt trội của Aurora
> Kiến trúc của Aurora

![07_Aurora](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_06/Image_module_06/07_Aurora.png)

1.  **Mô hình Cluster và Lưu trữ Chia sẻ:**
    + Một CSDL Aurora là một "Cluster" bao gồm một phiên bản ghi (Writer) và có thể có nhiều phiên bản đọc (Reader - lên đến 15).
    + Tất cả các phiên bản này **cùng chia sẻ một phân vùng lưu trữ (Cluster Volume) duy nhất**.
    + Dữ liệu trên phân vùng này được AWS tự động nhân bản 6 lần qua 3 Vùng Sẵn sàng (AZ) để đảm bảo độ bền bỉ.

2.  **Không có Độ trễ Sao chép (Zero Replication Lag):**
    + Vì tất cả các phiên bản (cả Ghi và Đọc) đều đọc chung từ một volume, các bản sao chỉ đọc (Read Replicas) **không hề có độ trễ** so với bản chính. Đây là ưu điểm vượt trội so với Read Replica của RDS thông thường.

3.  **Tính sẵn sàng cao (HA) và Failover:**
    + Nếu phiên bản Ghi (Writer) bị lỗi, Aurora sẽ tự động "thăng cấp" (promote) một trong các phiên bản Đọc (Reader) lên làm Writer mới trong thời gian rất ngắn.

4.  **Các tính năng Doanh nghiệp (Enterprise):**
> Aurora Back Track

![08_Aurora_Back_track](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_06/Image_module_06/08_Aurora_Back_track.png)

    + **Backtrack:** Cho phép "tua ngược" CSDL về một thời điểm trong quá khứ mà không cần khôi phục từ backup.

> Aurora Global Database

![09_Aurora_Global_Database](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_06/Image_module_06/09_Aurora_Global_Database.png)

    + **Global Database:** Cho phép tạo các bản sao chỉ đọc ở các **Region (khu vực địa lý) khác nhau** trên toàn thế giới, phục vụ cho các ứng dụng toàn cầu.

### 4. So sánh RDS Multi-AZ và Aurora

| Tính năng | **RDS Multi-AZ (cho MySQL/PostgreSQL...)** | **Amazon Aurora** |
| :--- | :--- | :--- |
| **Mục đích** | Sẵn sàng cao (High Availability) | Sẵn sàng cao (HA) **VÀ** Hiệu năng cao |
| **Bản sao** | 1 bản chính (Primary), 1 bản dự phòng (Standby) | 1 bản ghi (Writer), tối đa 15 bản đọc (Reader) |
| **Bản dự phòng** | Không thể truy cập (chỉ để dự phòng) | Các bản đọc có thể truy cập để phục vụ truy vấn |
| **Sao chép (Replication)** | **Đồng bộ (Synchronous)** ở tầng CSDL | **Đồng bộ** ở tầng Lưu trữ (Storage Layer) |
| **Read Replica Lag** | Có độ trễ (Asynchronous Replication) | **Không có độ trễ (Zero Lag)** |
| **Tự động Failover** | Có (Tự động chuyển sang bản Standby) | Có (Tự động thăng cấp 1 bản Reader lên Writer) |

## **IV. Amazon ElastiCache**
## **V. Amazon Redshift**
