
#### **Dịch vụ AWS không quản lý hoàn toàn** (còn gọi là IaaS - Infrastructure as a Service) là nơi AWS quản lý cơ sở hạ tầng vật lý (máy chủ host, trung tâm dữ liệu) , nhưng **khách hàng** phải chịu trách nhiệm quản lý hệ điều hành khách (guest OS), bao gồm cả việc cập nhật và vá lỗi
#### **Dịch vụ được AWS quản lý hoàn toàn** (thường là PaaS, FaaS, hoặc SaaS) là nơi AWS xử lý việc quản lý cơ sở hạ tầng, hệ điều hành, vá lỗi và co giãn, cho phép bạn tập trung vào ứng dụng và dữ liệu của mình.

Dưới đây là danh sách các dịch vụ được phân loại theo tài liệu:

### 1. Dịch vụ AWS KHÔNG quản lý hoàn toàn (Khách hàng quản lý HĐH)

Trong các dịch vụ được liệt kê, **Amazon EC2** là ví dụ điển hình nhất về dịch vụ không được quản lý hoàn toàn.

* **Amazon EC2 (Amazon Elastic Compute Cloud)**: Khi sử dụng EC2, khách hàng "đảm nhận trách nhiệm và quản lý hệ điều hành khách (guest operating system), bao gồm cả việc cập nhật và vá lỗi bảo mật". Bạn cũng có thể cài đặt phần mềm của riêng mình, chẳng hạn như MS SQL Server, lên một phiên bản EC2.

### 2. Dịch vụ được AWS quản lý hoàn toàn

Đây là các dịch vụ mà AWS quản lý cơ sở hạ tầng cơ bản, hệ điều hành và việc bảo trì.

* **Amazon RDS (Relational Database Service)**: Dịch vụ này "Đơn giản hóa việc quản lý các tác vụ quản trị cơ sở dữ liệu tốn thời gian" và "Giúp dễ dàng thiết lập, vận hành và mở rộng cơ sở dữ liệu quan hệ".
* **Amazon DynamoDB**: Được mô tả rõ ràng là một "cơ sở dữ liệu được quản lý hoàn toàn (fully managed)".
* **AWS Lambda**: Được xác định là một "dịch vụ tính toán không máy chủ (serverless)" . Các dịch vụ không máy chủ "loại bỏ chi phí quản lý" (removes management overhead).
* **Amazon API Gateway**: Được liệt kê là một phần của nền tảng không máy chủ "không yêu cầu cung cấp, duy trì và quản trị máy chủ" 
* **Lambda@Edge**: Tương tự như API Gateway, đây là một phần của nền tảng không máy chủ, nơi AWS quản lý việc thực thi.

---

## 1. Quản lý Chi phí & Gói Hỗ trợ (Cost Management & Support)


* **Keyword:** "truy cập vào **toàn bộ** các kiểm tra của AWS Trusted Advisor" (access to the **full set** of... AWS Trusted Advisor) với chi phí hiệu quả nhất  tối thiểu.
    * **Đáp án:** Gói **Business**.
---
* **Keyword:** "theo dõi chi phí... bằng **hình ảnh hóa đồ họa**" (track the costs... with a **graphical visualization**)
    * **Đáp án:** **AWS Cost Explorer**
---    
* **Keyword:** "dự báo" (forecasting) chi phí trong tương lai.
    * **Đáp án:** **AWS Cost Explorer**.
---
* **Keyword:** "phát hiện các khoản chi tiêu **bất thường**" (detect **unusual** cloud expenditures).
    * **Đáp án:** **AWS Cost Anomaly Detection**
---
* **Keyword:** "ước tính chi phí" (estimate their costs) khi lập kế hoạch.
    * **Đáp án:** **AWS Pricing Calculator**
---
* **Keyword:** "lợi ích của... **Thanh toán hợp nhất** (Consolidated Billing)".
    * **Đáp án:** **Nhận một hóa đơn duy nhất** (You get one bill for multiple accounts) và **Chia sẻ giảm giá theo khối lượng/phiên bản Reserved** (Share the volume pricing and Reserved Instance discounts).
---
* **Keyword:** "dữ liệu **chi tiết nhất** (most granular) về chi phí"
    * **Đáp án:** **AWS Cost and Usage Reports**.
---    
* **Keyword:** Gói hỗ trợ "rẻ nhất" (MOST affordable / minimum) cung cấp quyền truy cập **API Hỗ trợ AWS** (AWS Support API).
    * **Đáp án:** **Business**.
---
* **Keyword:** Gói hỗ trợ **Developer**
    * **Đáp án:** **Không có quyền truy cập API** (No access to the AWS Support API) và **Giới hạn 7 kiểm tra cốt lõi** của Trusted Advisor (Limited access to the 7 Core Trusted Advisor checks).
----
* **Keyword:** Gói hỗ trợ nào bao gồm **Concierge Support Team** (hỗ trợ về thanh toán/tài khoản).
    * **Đáp án:** **Enterprise**.

---

## 2. Nhận dạng & Truy cập (IAM - Identity and Access Management)

IAM là cốt lõi của bảo mật AWS, quản lý "ai" (danh tính) có thể làm "gì" (quyền).

* **Keyword:** "truy cập **lâu dài qua lập trình**" (long-term programmatic access).
    * **Đáp án:** **IAM User** (Vì IAM User được liên kết với Access Keys).
---
* **Keyword:** "truy cập... thông qua **AWS CLI**".
    * **Đáp án:** **Access Keys**.
---
* **Keyword:** "cải thiện bảo mật cho... IAM users".
    * **Đáp án:** **Bật MFA** (Enable Multi-Factor Authentication) và **Cấu hình chính sách mật khẩu mạnh** (Configure a strong password policy).
---
* **Keyword:** "cung cấp quyền truy cập **tạm thời**... cho **ứng dụng**" (provide **temporary** access... for **applications**).
    * **Đáp án:** **Tạo IAM role** và để ứng dụng "assume" (đảm nhận) role đó.
---
* **Keyword:** "quản lý quyền chung cho... **số lượng lớn người dùng**" (manage... permissions to a **large number of... users**).
    * **Đáp án:** Gắn policy vào một **IAM Group** và thêm người dùng vào Group đó.
---
* **Keyword:** "Thực hành tốt nhất (best practices) để bảo mật IAM".
    * **Đáp án:** **Khóa access key của người dùng root** (Lock away... root user access keys) và **Cấp đặc quyền tối thiểu** (Grant least privilege).
---
* "thực thi các đặc quyền và kiểm soát truy cập" (enforcing privileges and access controls).
    * **Đáp án:** **IAM Policy**.

---

## 3. Điện toán (Compute - EC2, Auto Scaling, ELB, Lambda)


* **Keyword:** "công suất tính toán... **tự động co giãn** (automatically scale) dựa trên lưu lượng".
    * **Đáp án:** **AWS Auto Scaling**.
---
* **Keyword:** "dịch vụ **theo vùng**" (zonal service).
    * **Đáp án:** **Amazon EC2** và **Amazon EBS**.
---
* **Keyword:** "chạy... 3 tháng... **không thể bị gián đoạn**" (run... for 3 months... **uninterruptible**).
    * **Đáp án:** **On-Demand Instance**. (Reserved Instance yêu cầu cam kết 1 hoặc 3 năm).
---
* **Keyword:** "**phân phối lưu lượng** truy cập ứng dụng đến" (distributes incoming application traffic).
    * **Đáp án:** **Elastic Load Balancing (ELB)**
---
* **Keyword:** "định tuyến dựa trên **đường dẫn** (path-based)" hoặc "định tuyến dựa trên **máy chủ** (host-based)".
    * **Đáp án:** **Application Load Balancer**.
---
* **Keyword:** "chuyển tiếp yêu cầu đến... **Lambda function làm mục tiêu**" (forward the incoming request to... **Lambda function as a target**).
    * **Đáp án:** **Application Load Balancer**.
---
* "cân bằng tải lưu lượng **TCP, UDP, và TLS**... **độ trễ cực thấp**" (load balancing **TCP, UDP, and TLS**... **ultra-low latencies**).
    * **Đáp án:** **Network Load Balancer**.
---
* **Keyword:** "tận dụng công suất EC2 chưa sử dụng... **giảm giá đến 90%**" (take advantage of **unused EC2 capacity**... **90% discount**).
    * **Đáp án:** **Spot Instance**.
---
* **Keyword:** "dịch vụ tính toán **không máy chủ** (serverless)".
    * **Đáp án:** **AWS Lambda**.
---
* **Keyword:** "lợi ích chính... chuyển sang **serverless**" (main benefit... moving to **serverless**).
    * **Đáp án:** **Loại bỏ chi phí quản lý** (Serverless removes management overhead).

---

## 4. Lưu trữ (Storage - S3, EBS, EFS)

Các dịch vụ này xử lý việc lưu trữ dữ liệu, từ tệp đối tượng, ổ đĩa cho máy chủ, đến hệ thống tệp.

* **Keyword:** "đặc điểm... Amazon S3".
    * **Đáp án:** **Không gian lưu trữ gần như không giới hạn** (virtually unlimited space)  và **Cơ sở hạ tầng lưu trữ đối tượng có độ bền cao** (highly durable object storage infrastructure).
---
* **Keyword:** "cung cấp cho người dùng cụ thể quyền truy cập vào bucket".
    * **Đáp án:** **Bucket Policy**.
---
* **Keyword:** "ngăn chặn việc **xóa trái phép**... đối tượng S3" (prevent **unauthorized deletion**... S3 objects)
    * **Đáp án:** **Cấu hình MFA delete** (Configure MFA delete).
---
* **Keyword:** "tự động chuyển dữ liệu **ít truy cập**... sang lớp lưu trữ **tiết kiệm chi phí** hơn" (automatically transfer **infrequently accessed** data... **cost-effective** storage class).
    * **Đáp án:** **S3 Lifecycle Policy**.
---
* **Keyword:** "khôi phục... nếu... vô tình **ghi đè hoặc xóa**" (accidentally **overwritten or deleted**... recoverable).
    * **Đáp án:** **S3 Versioning**.
---
* **Keyword:** "lưu trữ... **lâu dài**... thời gian truy xuất **12 giờ hoặc ít hơn**" (archived... **long time**... retrieval time of **12 hours or less**) 
    * **Đáp án:** **Amazon S3 Glacier Deep Archive**
---
* "lưu trữ tệp **có thể mở rộng**, tập trung... hỗ trợ **truy cập song song lớn**" (centralized **scalable**... **file storage**... support **massive parallel access**)
    * **Đáp án:** **Amazon Elastic File System (EFS)**.

---

### 5. Mạng & Phân phối Nội dung (Networking - VPC, Route 53, CloudFront)

Cách bạn cách ly tài nguyên, kết nối mạng và tăng tốc độ phân phối nội dung.

* **Keyword:** "bảo mật một mạng VPC" (secure a VPC network)    
    + **Đáp án:** **Network ACL**  và **Security group**.
---    
* **Keyword:** "áp dụng các quy tắc bảo mật cho **subnet**" (apply security rules to **subnets**)
    * **Đáp án:** **Network Access Control Lists (NACLs)** (Security Group áp dụng cho EC2 instance).
---
* **Keyword:** "hoạt động như một **tường lửa** (firewall) cho... EC2".
    * **Đáp án:** **Security Group**.
---
* **Keyword:** "chuyển hướng lưu lượng... sang **khu vực khác** khi có **thảm họa**" (reroute traffic... to **another region** during **disaster recovery**)
    * **Đáp án:** **Amazon Route 53**
---
* "dịch vụ **DNS** (Domain Name System) trên đám mây"
    * **Đáp án:** **Amazon Route 53**
---
* **Keyword:** "cung cấp một **phần logic bị cô lập**" (provision a **logically isolated section**)
    * **Đáp án:** **Amazon VPC**
---
* **Keyword:** "kết nối **chuyên dụng** (dedicated connection)... trải nghiệm mạng **nhất quán** (consistent)" 
    * **Đáp án:** **AWS Direct Connect**.
---
* **Keyword:** "thiết lập kết nối an toàn... **ít thời gian nhất** (least time)"
    * **Đáp án:** **AWS Site-to-Site VPN** (Direct Connect mất vài tuần đến vài tháng).
---
* **Keyword:** "**tăng tốc độ phân phối nội dung**" (speed up content delivery) 
    * **Đáp án:** **Amazon CloudFront** 
---
* **Keyword:** "lợi ích của... **Edge locations**".
    * **Đáp án:** **Cải thiện hiệu suất** (Improves application performance) và **Cung cấp bộ đệm (caching)** (Provides caching)

---

### 6. Cơ sở dữ liệu (Database - RDS, DynamoDB, Redshift)

* **Keyword:** "di chuyển (migrate)... cơ sở dữ liệu MySQL... sang Amazon RDS"    
    * **Đáp án:** **AWS Database Migration Service (AWS DMS)**.
---
* **Keyword:** "lưu trữ kết quả của các truy vấn SQL **chuyên sâu I/O** (I/O-intensive)" (để cải thiện hiệu suất)
    * **Đáp án:** **Amazon ElastiCache**. (Đây là dịch vụ caching).
---
* **Keyword:** "cơ sở dữ liệu OLTP MySQL **có khả năng mở rộng cao**" (highly scalable MySQL OLTP database)
    * **Đáp án:** **Amazon Aurora**
---
* **Keyword:** "cơ sở dữ liệu **phi quan hệ** (non-relational) linh hoạt, nhanh, có thể mở rộng"
    * **Đáp án:** **Amazon DynamoDB**
---
* **Keyword:** "tạo một **kho dữ liệu** (data warehouse)" 
    * **Đáp án:** **Amazon Redshift**
---
* "đặc điểm... Amazon RDS".
    * **Đáp án:** **Đơn giản hóa các tác vụ quản trị** (Simplifies... administration tasks) và **Dễ dàng thiết lập, vận hành và mở rộng** (Makes it easy to set up, operate, and scale)

---

### 7. Giám sát, Bảo mật & Quản trị (Monitoring, Security & Governance)

* **Keyword:** "phân tích, điều tra... **nguyên nhân gốc rễ** (root cause) của các vấn đề bảo mật"
    * **Đáp án:** **Amazon Detective**
---
* **Keyword:** "tài liệu tuân thủ (compliance documents) như... **SOC 1, SOC 2**"
    * **Đáp án:** **AWS Artifact**
---
* **Keyword:** "thiết lập một **landing zone**... môi trường **đa tài khoản** (multi-account)"
    * **Đáp án:** **AWS Control Tower**
---
* **Keyword:** "kiểm tra... tài nguyên... tuân thủ các **thực hành tốt nhất** (best practices)"
    * **Đáp án:** **AWS Trusted Advisor**
---
* "**kho lưu trữ (repository) cho các chỉ số (metrics) và log**"
    * **Đáp án:** **Amazon CloudWatch**
---
* "**lịch sử sự kiện** (event history) của... hoạt động tài khoản" / "xác định người dùng nào đã **chấm dứt** (terminated) EC2" 
    * **Đáp án:** **AWS CloudTrail**
---
* "khám phá, phân loại và bảo vệ **dữ liệu nhạy cảm (PII)**".
    * **Đáp án:** **Amazon Macie**.
---
* "phân tích **lỗ hổng** (vulnerability analysis) trên... máy chủ" 
    * **Đáp án:** **Amazon Inspector**.
---
* "dịch vụ phát hiện **mối đe dọa** (threat detection)... giám sát **hoạt động độc hại**" 
    * **Đáp án:** **Amazon GuardDuty** 
---
* "bảo vệ... khỏi các cuộc tấn công **DDoS**".
    * **Đáp án:** **AWS Shield**.

---

### 8. Các Khái niệm Cloud (Cloud Concepts)

Đây là những nguyên tắc cơ bản của AWS, bao gồm Lợi ích, Mô hình Trách nhiệm chung, và Well-Architected.

* **Keyword:** "Auto-Scaling dựa trên nhu cầu" là một ví dụ của
    * **Đáp án:** **Thực thi tính đàn hồi** (Implement elasticity)
---
* **Keyword:** "Trách nhiệm... **vá lỗi hệ điều hành máy chủ** (patch the host operating system) của... EC2"
    * **Đáp án:** **AWS**. (Lưu ý: AWS chịu trách nhiệm cho HĐH *host*, khách hàng chịu trách nhiệm cho HĐH *khách* (guest OS)).
---
* **Keyword:** "lợi ích của việc di chuyển" (benefits of migrating)
    * **Đáp án:** **Cho phép khách hàng tập trung vào hoạt động kinh doanh** (Enables the customer to focus on business activities)
---
* **Keyword:** "triển khai... ở **nhiều khu vực** (multiple AWS regions) chỉ với vài cú nhấp chuột"
    * **Đáp án:** **Vươn ra toàn cầu trong vài phút** (Go global in minutes)
---
* **Keyword:** "lưu lượng truy cập **thay đổi** (varying levels)... không tiêu thụ hết công suất"
    * **Đáp án:** **Tính đàn hồi** (Elasticity)
---
* **Keyword:** "nguyên tắc thiết kế **thực hiện hoạt động dưới dạng mã** (performing operations as code)"
    * **Đáp án:** (Trụ cột) **Operational Excellence** (Vận hành xuất sắc)
---
* **Keyword:** "phát biểu đúng... về Cấu trúc hạ tầng toàn cầu"
    * **Đáp án:** **Một AWS Region chứa nhiều Availability Zones** (An AWS Region contains multiple Availability Zones)
---
* **Keyword:** "quyền kiểm soát **chia sẻ** (shared control) giữa AWS và khách hàng"
    * **Đáp án:** **Nhận thức và Đào tạo** (Awareness and training)
---
* **Keyword:** "trách nhiệm **duy nhất** của **khách hàng**" (solely the responsibility of the **customer**)
    * **Đáp án:** **Bảo vệ Dịch vụ và Truyền thông** (Service and Communications Protection)  (ví dụ: cấu hình Security Group, mã hóa dữ liệu).
---
* **Keyword:** "trách nhiệm **duy nhất** của **AWS**" (sole responsibility of **AWS**) 
    * **Đáp án:** **Kiểm soát vật lý và môi trường** (Physical and environmental controls).
---
* **Keyword:** "lợi ích tài chính chính" (key financial benefit).
    * **Đáp án:** **Thay thế chi phí vốn ban đầu (CAPEX) bằng chi phí biến đổi thấp (variable costs)**
---
* **Keyword:** "mô tả Mô hình Trách nhiệm Chung" (describes the AWS Shared Responsibility model) 
    * **Đáp án:** **AWS chịu trách nhiệm bảo mật cơ sở hạ tầng vật lý... khách hàng chịu trách nhiệm bảo mật ứng dụng và dữ liệu của họ** (AWS is responsible for securing the physical infrastructure... customers are responsible for securing their applications and data) 

---


---

## 1. 🏗️ Thiết kế kiến trúc bảo mật (Secure Architectures)

Lĩnh vực này tập trung vào việc bảo vệ tính toàn vẹn của dữ liệu và hệ thống, sử dụng các dịch vụ IAM, mã hóa, và bảo mật mạng.

* **IAM (Identity and Access Management)**
    * [cite_start]**Tình huống:** Cần cấp quyền truy cập **lâu dài qua lập trình** (ví dụ: cho AWS CLI)[cite: 371, 946, 973].
    * [cite_start]**Giải pháp:** Sử dụng **IAM User** và tạo **Access Keys**[cite: 375, 851, 854, 975, 979].
    * [cite_start]**Tình huống:** Cần cấp quyền truy cập **tạm thời** cho các ứng dụng, dịch vụ AWS, hoặc bên thứ ba[cite: 1349, 2132, 2135, 2138].
    * [cite_start]**Giải pháp:** Sử dụng **IAM Role** để ứng dụng có thể "assume" (đảm nhận) role đó[cite: 1354, 1356, 2135, 2138].
    * [cite_start]**Tình huống:** Quản lý quyền chung cho một **số lượng lớn người dùng**[cite: 1123].
    * [cite_start]**Giải pháp:** Gắn policy vào một **IAM Group** và thêm người dùng vào group đó[cite: 1124, 1128].
    * [cite_start]**Thực hành tốt nhất:** Luôn tuân thủ **nguyên tắc đặc quyền tối thiểu** (Grant least privilege) và **khóa access key của tài khoản root**[cite: 304, 306, 311, 1185, 1189, 1191, 1195].
* **MFA (Multi-Factor Authentication)**
    * [cite_start]**Tình huống:** Ngăn chặn việc **xóa trái phép** hoặc vô tình các đối tượng quan trọng trong S3[cite: 424, 426, 1388, 1390].
    * [cite_start]**Giải pháp:** Cấu hình **MFA Delete** trên S3 bucket[cite: 427, 432, 1394, 1401].
    * [cite_start]**Tình huống:** Tăng cường bảo mật cho IAM users[cite: 684, 685].
    * [cite_start]**Giải pháp:** **Bật MFA** và cấu hình chính sách mật khẩu mạnh (strong password policy)[cite: 686, 688].
* **Mã hóa (KMS & CloudHSM)**
    * [cite_start]**Tình huống:** Cần một mô-đun bảo mật phần cứng (HSM) **một bên thuê** (single-tenant) để quản lý khóa mã hóa[cite: 312, 313, 318].
    * [cite_start]**Giải pháp:** **AWS CloudHSM**[cite: 321]. (Lưu ý: KMS là dịch vụ multi-tenant).
* **Security Groups (SG) và NACLs**
    * [cite_start]**Nền tảng:** Cả hai đều được dùng để bảo mật VPC[cite: 63, 1077, 1078].
    * [cite_start]**Security Group:** Hoạt động như một tường lửa (firewall) **cấp độ instance** (cho EC2)[cite: 1940, 1941]. Nó là **stateful** (luôn tự động cho phép lưu lượng trả về).
    * [cite_start]**NACL (Network ACL):** Hoạt động như một tường lửa **cấp độ subnet**[cite: 612, 618, 1541, 1542]. Nó là **stateless** (bạn phải cấu hình cả quy tắc inbound và outbound).
    * [cite_start]**Quy tắc hợp lệ:** SG có thể lấy nguồn (source) là một **Security Group ID** khác hoặc một **dải địa chỉ IP** (address range)[cite: 21, 22, 26, 28, 1671, 1674, 1675].
* **GuardDuty, Shield, và WAF**
    * [cite_start]**Amazon GuardDuty:** Dịch vụ phát hiện mối đe dọa (threat detection) **sử dụng machine learning** để liên tục giám sát **hoạt động độc hại** hoặc trái phép[cite: 1534, 1535, 1538, 1540, 2022, 2026].
    * [cite_start]**AWS Shield:** Dịch vụ bảo vệ chống lại các cuộc tấn công **DDoS**[cite: 1756, 1759, 1760].
    * [cite_start]**Amazon Inspector:** Dịch vụ tự động đánh giá và phân tích **lỗ hổng bảo mật** (vulnerability) trên các ứng dụng đã triển khai[cite: 1445, 1446, 1447, 1448, 1452].

---

## 2. 🔄 Thiết kế kiến trúc linh hoạt và bền vững (Resilient Architectures)

Tập trung vào khả năng chịu lỗi (fault tolerance) và khôi phục sau thảm họa (disaster recovery) bằng cách sử dụng nhiều vùng và tự động hóa.

* **Multi-AZ và Multi-Region**
    * [cite_start]**Tình huống:** Cần tăng **tính sẵn sàng cao** (high-availability) hoặc **khả năng phục hồi** (resilience) cho ứng dụng quan trọng[cite: 87, 89, 585, 587, 896, 897].
    * [cite_start]**Giải pháp:** Triển khai các instance (ví dụ: EC2) ở **nhiều Availability Zones (AZ)**[cite: 93, 95, 588, 594, 900, 903, 1330, 1334].
    * [cite_start]**Nguyên tắc:** Các AZ được thiết kế cách xa nhau về mặt vật lý để phòng ngừa thảm họa cục bộ[cite: 264, 265, 275].
* **Disaster Recovery (DR)**
    * [cite_start]**Tình huống:** Cần chuyển hướng (reroute) lưu lượng truy cập sang một **khu vực (region) khác** trong trường hợp xảy ra thảm họa[cite: 102].
    * [cite_start]**Giải pháp:** **Amazon Route 53**[cite: 98, 105].
    * [cite_start]**Tình huống:** Cần một giải pháp DR để sao chép (replicate) máy chủ **on-premises** lên AWS[cite: 762, 763, 764].
    * [cite_start]**Giải pháp:** **AWS Elastic Disaster Recovery**[cite: 771].
* **Auto Scaling và Load Balancing (ELB)**
    * [cite_start]**AWS Auto Scaling:** Tự động điều chỉnh (co giãn) số lượng instance EC2 dựa trên nhu cầu hoặc lưu lượng truy cập[cite: 190, 191, 1001, 1007, 1612, 1616, 1620].
    * [cite_start]**ELB (Elastic Load Balancing):** **Phân phối lưu lượng** truy cập đến nhiều mục tiêu (như EC2) ở nhiều AZ để tăng tính sẵn sàng cao[cite: 353, 355, 730, 733, 735, 1509, 1511].
    * [cite_start]**Thiết kế HA:** Để đảm bảo tính sẵn sàng cao, một Application Load Balancer (ALB) cần được cấu hình với tối thiểu **2 Availability Zones**[cite: 830, 831, 835].
* **Backup & Restore**
    * [cite_start]**EBS:** Bạn có thể tạo **point-in-time backups** cho ổ đĩa EBS bằng cách tạo **EBS Snapshots**[cite: 1644, 1647, 1653]. [cite_start]Các snapshot này được lưu trữ bền bỉ trên **Amazon S3**[cite: 1652, 1653].
    * [cite_start]**AWS Backup:** Dịch vụ **trung tâm hóa và tự động hóa** việc sao lưu dữ liệu trên các dịch vụ AWS[cite: 1169, 1174, 1177].
    * [cite_start]**S3:** Để có thể khôi phục dữ liệu nếu bị vô tình **ghi đè hoặc xóa**, hãy bật **S3 Versioning**[cite: 1676, 1677, 1679].

---

## 3. ⚡ Thiết kế hệ thống hiệu năng cao (High-Performing Architectures)

Tập trung vào việc tối ưu hóa tốc độ, độ trễ và thông lượng bằng cách sử dụng các dịch vụ phù hợp và cơ chế caching.

* **Caching (Bộ nhớ đệm)**
    * [cite_start]**Amazon ElastiCache:** Được sử dụng để lưu vào bộ đệm (cache) kết quả của các truy vấn cơ sở dữ liệu (ví dụ: SQL) **chuyên sâu về I/O**, giúp cải thiện hiệu suất ứng dụng[cite: 214, 215, 219, 1101, 1102, 1103, 1105].
    * [cite_start]**Amazon CloudFront:** Cải thiện hiệu suất của trang web bằng cách **lưu vào bộ đệm (caching)** nội dung tại các **Edge Locations**, giảm tải cho máy chủ gốc[cite: 639, 641, 643, 646, 1911, 1914].
* **Phân phối nội dung (CloudFront & Global Accelerator)**
    * [cite_start]**Amazon CloudFront:** Dịch vụ CDN (Mạng phân phối nội dung) giúp **tăng tốc độ phân phối nội dung** (ví dụ: hình ảnh, video từ S3) cho người dùng toàn cầu với độ trễ thấp nhất[cite: 822, 823, 824, 826, 1515, 1518, 1521].
    * [cite_start]**AWS Global Accelerator:** Tối ưu hóa tốc độ truy cập ứng dụng bằng cách sử dụng mạng toàn cầu của AWS và cung cấp một địa chỉ **Anycast Static IP**[cite: 465, 466, 467, 472].
* **Lưu trữ (Storage) tối ưu hiệu năng**
    * **EBS (Elastic Block Store):**
        * [cite_start]**General Purpose SSD (gp2/gp3):** Được khuyến nghị cho hầu hết các workload, bao gồm cả **boot volumes** (ổ đĩa khởi động)[cite: 2112, 2114, 2116].
        * [cite_start]**Throughput Optimized HDD (st1):** Tốt nhất cho các workload **chuyên sâu về thông lượng** (throughput-intensive), truy cập thường xuyên[cite: 2065, 2066, 2067].
    * [cite_start]**EFS (Elastic File System):** Một hệ thống tệp (file storage) có thể mở rộng, hỗ trợ **truy cập song song lớn** (massive parallel access) từ nhiều instance[cite: 1856, 1857, 1858, 1863].
* **Tính toán (Compute) hiệu năng cao**
    * [cite_start]**AWS Lambda:** Một dịch vụ tính toán **không máy chủ (serverless)**, cho phép bạn chạy mã mà không cần quản lý máy chủ[cite: 1809, 1811]. [cite_start]Lợi ích chính là **loại bỏ chi phí quản lý** (removes management overhead)[cite: 1945, 1946, 1951, 1954].
    * [cite_start]**AWS Elastic Beanstalk:** Cho phép triển khai nhanh ứng dụng (ví dụ: PHP) mà không cần cấu hình cơ sở hạ tầng phức tạp[cite: 1780, 1781, 1782, 1783, 1785].

---

## 4. 💰 Thiết kế tối ưu chi phí (Cost-Optimized Architectures)

Tập trung vào việc hiểu rõ, kiểm soát và giảm thiểu chi phí đám mây mà không ảnh hưởng đến hiệu suất hoặc khả năng phục hồi.

* **Công cụ giám sát chi phí**
    * [cite_start]**AWS Cost Explorer:** Cung cấp **hình ảnh hóa đồ họa** (graphical visualization) để theo dõi và phân tích chi phí[cite: 115, 118]. [cite_start]Nó có thể lưu trữ dữ liệu lịch sử **12 tháng** [cite: 401, 403, 407] [cite_start]và đưa ra **đề xuất mua Reserved Instance (RI)**[cite: 431, 433, 437, 1958, 1960, 1963].
    * [cite_start]**AWS Budgets:** Cho phép bạn đặt ngân sách tùy chỉnh và **nhận cảnh báo (alerts)** khi chi tiêu vượt ngưỡng[cite: 788, 789, 792, 796].
    * [cite_start]**Cost Allocation Tags:** Dùng để **phân loại và theo dõi** chi phí ở mức độ chi tiết (ví dụ: theo dự án, theo phòng ban)[cite: 1063, 1064, 1067].
* **Mô hình định giá (Savings Plans & RIs)**
    * [cite_start]**Savings Plans:** Mô hình linh hoạt cung cấp mức giảm giá đáng kể khi cam kết sử dụng (tính bằng $/giờ) trong **1 hoặc 3 năm** cho EC2, Fargate và Lambda[cite: 579, 580, 583, 1739, 1740, 1745].
    * **Reserved Instances (RIs):**
        * [cite_start]Cung cấp giảm giá cho **EC2** và **RDS** khi cam kết 1 hoặc 3 năm[cite: 363, 364, 366, 369, 1837, 1838, 1839, 1840, 1844].
        * [cite_start]**Standard RI:** Dành cho workload ổn định, không thể thay đổi loại instance[cite: 1577, 1580, 1582].
        * [cite_start]**Convertible RI:** Cho phép **thay đổi** họ instance, hệ điều hành... miễn là giá trị bằng hoặc lớn hơn[cite: 655, 656, 659, 1205, 1207, 1209, 1210, 1211].
    * [cite_start]**Spot Instances:** Cung cấp mức **giảm giá sâu nhất (lên đến 90%)** bằng cách sử dụng công suất EC2 chưa dùng đến, nhưng có thể bị **gián đoạn**[cite: 1059, 1061, 1150, 1151].
* **Tối ưu hóa lưu trữ (Storage Tiering)**
    * [cite_start]**S3 Lifecycle Policies:** Dùng để **tự động di chuyển** các đối tượng sang các lớp lưu trữ rẻ hơn (ví dụ: S3 Standard-IA) khi chúng **ít được truy cập**[cite: 1139, 1140, 1141, 1147, 2170, 2174].
    * [cite_start]**S3 Glacier Deep Archive:** Lớp lưu trữ **rẻ nhất** dành cho việc lưu trữ **lâu dài** (archiving) với thời gian truy xuất chấp nhận được là **12 giờ hoặc ít hơn**[cite: 2005, 2006, 2009, 2013].
    * [cite_start]**S3 Glacier Flexible Retrieval:** Tùy chọn chi phí thấp cho lưu trữ, cho phép truy xuất dữ liệu trong **vài phút** (minutes) khi cần[cite: 983, 984, 988].