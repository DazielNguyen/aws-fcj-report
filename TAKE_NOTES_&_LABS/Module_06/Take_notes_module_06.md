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

![01_RDBMS]()

- **Primary Key (Khóa chính):** Là một cột (hoặc nhóm cột) dùng để **xác định duy nhất** một hàng (bản ghi) trong bảng. Giá trị của khóa chính không được trùng lặp.
- **Foreign Key (Khóa ngoại):** Là một cột trong một bảng, dùng để **tạo liên kết** với khóa chính của một bảng khác. Nó hoạt động như một tham chiếu chéo giữa các bảng vì nó tham chiếu đến khóa chính của một bảng khác, do đó thiết lập liên kết giữa chúng. 
* **Mục đích của Khóa:** Việc sử dụng khóa chính/khóa ngoại và chia dữ liệu ra nhiều bảng (gọi là **chuẩn hóa - Normalization**) giúp **chống trùng lặp dữ liệu** và tiết kiệm dung lượng lưu trữ.

### 4. Các Kỹ thuật Tối ưu Hiệu năng

> Kỹ thuật Index

![02_Index]()

- **Index (Chỉ mục):**
    + **Công dụng:** Là một cấu trúc dữ liệu giúp **tăng tốc độ truy xuất dữ liệu** (đọc). Nó hoạt động giống như mục lục của một cuốn sách, giúp tìm dữ liệu nhanh chóng mà không cần "dò quét" (scan) toàn bộ bảng. Các **chỉ mục được sử dụng để định vị dữ liệu một cách nhanh chóng mà không cần phải tìm kiếm mọi hàng trong bảng cơ sở dữ liệu mỗi khi truy cập bảng cơ sở dữ liệu.** Chỉ mục có thể được tạo bằng cách sử dụng một hoặc nhiều cột của bảng cơ sở dữ liệu.

    + **Nhược điểm:** Làm **tăng chi phí ghi** (vì vừa phải ghi vào bảng, vừa phải cập nhật Index) và tốn thêm không gian lưu trữ.

> Kỹ thuật Parition

![03_Partition]()

- **Partition (Phân vùng):**
    + **Công dụng:** Là kỹ thuật **chia một bảng lớn thành nhiều phần nhỏ hơn** (gọi là các phân vùng). Khi truy vấn, hệ thống chỉ cần tìm kiếm trên các phân vùng liên quan thay vì toàn bộ bảng, giúp tăng tốc độ.

- **Execution Plan (Kế hoạch thực thi):**
    + **Khái niệm:** Là một tập hợp các bước mà CSDL sẽ sử dụng để truy cập dữ liệu (ví dụ: quyết định có dùng Index hay không). Kế hoạch truy vấn là một chuỗi các bước được sử dụng để truy cập dữ liệu trong hệ quản trị cơ sở dữ liệu quan hệ SQL. ... Khi một truy vấn được gửi đến cơ sở dữ liệu, trình tối ưu hóa truy vấn sẽ đánh giá một số phương án có thể khác nhau, chính xác để thực hiện truy vấn và trả về những gì nó cho là tùy chọn tốt

    + **Tầm quan trọng:** Đọc hiểu được Execution Plan là kỹ năng quan trọng nhất để tối ưu hóa các câu truy vấn phức tạp.

### 5. Đảm bảo Tính Toàn vẹn và Tốc độ

> Kỹ thuật Database Log

![04_Database_Log]()

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
## **III. Amazon Aurora**
## **IV. Amazon ElastiCache**
## **V. Amazon Redshift**
