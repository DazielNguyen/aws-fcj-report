
---

### 1. Quản lý Chi phí & Gói Hỗ trợ (Cost Management & Support)

Lĩnh vực này tập trung vào cách AWS tính phí, các công cụ để theo dõi/tối ưu hóa chi phí và các gói hỗ trợ khác nhau.

* [cite_start]**Keyword:** "truy cập vào **toàn bộ** các kiểm tra của AWS Trusted Advisor" (access to the **full set** of... AWS Trusted Advisor) [cite: 71, 72] [cite_start]với chi phí hiệu quả nhất [cite: 73] [cite_start]/ tối thiểu[cite: 1919].
    * [cite_start]**Đáp án:** Gói **Business**[cite: 79, 1921].
* [cite_start]**Keyword:** "theo dõi chi phí... bằng **hình ảnh hóa đồ họa**" (track the costs... with a **graphical visualization**)[cite: 115].
    * [cite_start]**Đáp án:** **AWS Cost Explorer**[cite: 118].
* [cite_start]**Keyword:** "dự báo" (forecasting) chi phí trong tương lai[cite: 1251].
    * [cite_start]**Đáp án:** **AWS Cost Explorer**[cite: 1253].
* [cite_start]**Keyword:** "phát hiện các khoản chi tiêu **bất thường**" (detect **unusual** cloud expenditures)[cite: 544, 545].
    * [cite_start]**Đáp án:** **AWS Cost Anomaly Detection**[cite: 546].
* [cite_start]**Keyword:** "ước tính chi phí" (estimate their costs) khi lập kế hoạch[cite: 736, 737, 738].
    * [cite_start]**Đáp án:** **AWS Pricing Calculator**[cite: 742].
* [cite_start]**Keyword:** "lợi ích của... **Thanh toán hợp nhất** (Consolidated Billing)"[cite: 781, 782].
    * [cite_start]**Đáp án:** **Nhận một hóa đơn duy nhất** (You get one bill for multiple accounts) [cite: 787, 791] [cite_start]và **Chia sẻ giảm giá theo khối lượng/phiên bản Reserved** (Share the volume pricing and Reserved Instance discounts)[cite: 784, 791].
* [cite_start]**Keyword:** "dữ liệu **chi tiết nhất** (most granular) về chi phí"[cite: 868].
    * [cite_start]**Đáp án:** **AWS Cost and Usage Reports**[cite: 869, 870].
* [cite_start]**Keyword:** Gói hỗ trợ "rẻ nhất" (MOST affordable / minimum) cung cấp quyền truy cập **API Hỗ trợ AWS** (AWS Support API)[cite: 237, 1017].
    * [cite_start]**Đáp án:** **Business**[cite: 240, 1020].
* [cite_start]**Keyword:** Gói hỗ trợ **Developer**[cite: 714].
    * [cite_start]**Đáp án:** **Không có quyền truy cập API** (No access to the AWS Support API) [cite: 717, 719] [cite_start]và **Giới hạn 7 kiểm tra cốt lõi** của Trusted Advisor (Limited access to the 7 Core Trusted Advisor checks)[cite: 718, 720].
* [cite_start]**Keyword:** Gói hỗ trợ nào bao gồm **Concierge Support Team** (hỗ trợ về thanh toán/tài khoản)[cite: 2071, 2072].
    * [cite_start]**Đáp án:** **Enterprise**[cite: 2079].

---

### 2. Nhận dạng & Truy cập (IAM - Identity and Access Management)

IAM là cốt lõi của bảo mật AWS, quản lý "ai" (danh tính) có thể làm "gì" (quyền).

* [cite_start]**Keyword:** "truy cập **lâu dài qua lập trình**" (long-term programmatic access)[cite: 371, 372].
    * [cite_start]**Đáp án:** **IAM User**[cite: 375]. (Vì IAM User được liên kết với Access Keys).
* [cite_start]**Keyword:** "truy cập... thông qua **AWS CLI**"[cite: 242, 851].
    * [cite_start]**Đáp án:** **Access Keys**[cite: 246, 854].
* [cite_start]**Keyword:** "cải thiện bảo mật cho... IAM users"[cite: 684, 685].
    * [cite_start]**Đáp án:** **Bật MFA** (Enable Multi-Factor Authentication) [cite: 686, 687] [cite_start]và **Cấu hình chính sách mật khẩu mạnh** (Configure a strong password policy)[cite: 686, 688].
* [cite_start]**Keyword:** "cung cấp quyền truy cập **tạm thời**... cho **ứng dụng**" (provide **temporary** access... for **applications**)[cite: 1349].
    * [cite_start]**Đáp án:** **Tạo IAM role** và để ứng dụng "assume" (đảm nhận) role đó[cite: 1354, 1356].
* [cite_start]**Keyword:** "quản lý quyền chung cho... **số lượng lớn người dùng**" (manage... permissions to a **large number of... users**)[cite: 1123].
    * [cite_start]**Đáp án:** Gắn policy vào một **IAM Group** và thêm người dùng vào Group đó[cite: 1124, 1128].
* [cite_start]**Keyword:** "Thực hành tốt nhất (best practices) để bảo mật IAM"[cite: 1185, 1186, 1187].
    * [cite_start]**Đáp án:** **Khóa access key của người dùng root** (Lock away... root user access keys) [cite: 1189, 1193, 1194] [cite_start]và **Cấp đặc quyền tối thiểu** (Grant least privilege)[cite: 1191, 1195].
* [cite_start]"thực thi các đặc quyền và kiểm soát truy cập" (enforcing privileges and access controls)[cite: 1889, 1891, 1892].
    * [cite_start]**Đáp án:** **IAM Policy**[cite: 1896].

---

### 3. Điện toán (Compute - EC2, Auto Scaling, ELB, Lambda)

Đây là các dịch vụ chạy mã và ứng dụng của bạn.

* [cite_start]**Keyword:** "công suất tính toán... **tự động co giãn** (automatically scale) dựa trên lưu lượng"[cite: 190, 1001].
    * [cite_start]**Đáp án:** **AWS Auto Scaling**[cite: 191, 1007].
* [cite_start]**Keyword:** "dịch vụ **theo vùng**" (zonal service)[cite: 229, 230].
    * [cite_start]**Đáp án:** **Amazon EC2** [cite: 233] [cite_start]và **Amazon EBS**[cite: 235, 236].
* [cite_start]**Keyword:** "chạy... 3 tháng... **không thể bị gián đoạn**" (run... for 3 months... **uninterruptible**)[cite: 378, 379, 380, 1454, 1455].
    * [cite_start]**Đáp án:** **On-Demand Instance**[cite: 382, 1458]. (Reserved Instance yêu cầu cam kết 1 hoặc 3 năm).
* [cite_start]**Keyword:** "**phân phối lưu lượng** truy cập ứng dụng đến" (distributes incoming application traffic)[cite: 730, 733].
    * [cite_start]**Đáp án:** **Elastic Load Balancing (ELB)**[cite: 735].
* [cite_start]**Keyword:** "định tuyến dựa trên **đường dẫn** (path-based)" hoặc "định tuyến dựa trên **máy chủ** (host-based)"[cite: 456, 457, 925, 926].
    * [cite_start]**Đáp án:** **Application Load Balancer**[cite: 463, 932].
* [cite_start]**Keyword:** "chuyển tiếp yêu cầu đến... **Lambda function làm mục tiêu**" (forward the incoming request to... **Lambda function as a target**)[cite: 1830, 1831, 1832].
    * [cite_start]**Đáp án:** **Application Load Balancer**[cite: 1835].
* [cite_start]"cân bằng tải lưu lượng **TCP, UDP, và TLS**... **độ trễ cực thấp**" (load balancing **TCP, UDP, and TLS**... **ultra-low latencies**)[cite: 1589, 1590, 1591].
    * [cite_start]**Đáp án:** **Network Load Balancer**[cite: 1592].
* [cite_start]**Keyword:** "tận dụng công suất EC2 chưa sử dụng... **giảm giá đến 90%**" (take advantage of **unused EC2 capacity**... **90% discount**)[cite: 1059, 1060, 1061].
    * [cite_start]**Đáp án:** **Spot Instance**[cite: 1061].
* [cite_start]**Keyword:** "dịch vụ tính toán **không máy chủ** (serverless)"[cite: 1809].
    * [cite_start]**Đáp án:** **AWS Lambda**[cite: 1811].
* [cite_start]**Keyword:** "lợi ích chính... chuyển sang **serverless**" (main benefit... moving to **serverless**)[cite: 1945].
    * [cite_start]**Đáp án:** **Loại bỏ chi phí quản lý** (Serverless removes management overhead)[cite: 1946, 1951, 1954].

---

### 4. Lưu trữ (Storage - S3, EBS, EFS)

Các dịch vụ này xử lý việc lưu trữ dữ liệu, từ tệp đối tượng, ổ đĩa cho máy chủ, đến hệ thống tệp.

* [cite_start]**Keyword:** "đặc điểm... Amazon S3"[cite: 477, 1010].
    * [cite_start]**Đáp án:** **Không gian lưu trữ gần như không giới hạn** (virtually unlimited space) [cite: 478, 482, 1011, 1016] [cite_start]và **Cơ sở hạ tầng lưu trữ đối tượng có độ bền cao** (highly durable object storage infrastructure)[cite: 482, 486, 1013, 1016].
* [cite_start]**Keyword:** "cung cấp cho người dùng cụ thể quyền truy cập vào bucket"[cite: 487, 488, 1084, 1085].
    * [cite_start]**Đáp án:** **Bucket Policy**[cite: 492, 493, 1086, 1089].
* [cite_start]**Keyword:** "ngăn chặn việc **xóa trái phép**... đối tượng S3" (prevent **unauthorized deletion**... S3 objects)[cite: 424, 426, 1388, 1390, 1391].
    * [cite_start]**Đáp án:** **Cấu hình MFA delete** (Configure MFA delete)[cite: 427, 432, 1394, 1401].
* [cite_start]**Keyword:** "tự động chuyển dữ liệu **ít truy cập**... sang lớp lưu trữ **tiết kiệm chi phí** hơn" (automatically transfer **infrequently accessed** data... **cost-effective** storage class)[cite: 1139, 1140, 1141].
    * [cite_start]**Đáp án:** **S3 Lifecycle Policy**[cite: 1147].
* [cite_start]**Keyword:** "khôi phục... nếu... vô tình **ghi đè hoặc xóa**" (accidentally **overwritten or deleted**... recoverable)[cite: 1676, 1677].
    * [cite_start]**Đáp án:** **S3 Versioning**[cite: 1679].
* [cite_start]**Keyword:** "lưu trữ... **lâu dài**... thời gian truy xuất **12 giờ hoặc ít hơn**" (archived... **long time**... retrieval time of **12 hours or less**)[cite: 2005, 2006].
    * [cite_start]**Đáp án:** **Amazon S3 Glacier Deep Archive**[cite: 2009, 2013].
* [cite_start]"lưu trữ tệp **có thể mở rộng**, tập trung... hỗ trợ **truy cập song song lớn**" (centralized **scalable**... **file storage**... support **massive parallel access**)[cite: 1856, 1857, 1858].
    * [cite_start]**Đáp án:** **Amazon Elastic File System (EFS)**[cite: 1863].

---

### 5. Mạng & Phân phối Nội dung (Networking - VPC, Route 53, CloudFront)

Cách bạn cách ly tài nguyên, kết nối mạng và tăng tốc độ phân phối nội dung.

* [cite_start]**Keyword:** "bảo mật một mạng VPC" (secure a VPC network)[cite: 63].
    * [cite_start]**Đáp án:** **Network ACL** [cite: 65, 70] [cite_start]và **Security group**[cite: 66, 70].
* [cite_start]**Keyword:** "áp dụng các quy tắc bảo mật cho **subnet**" (apply security rules to **subnets**)[cite: 612].
    * [cite_start]**Đáp án:** **Network Access Control Lists (NACLs)**[cite: 618]. (Security Group áp dụng cho EC2 instance).
* [cite_start]**Keyword:** "hoạt động như một **tường lửa** (firewall) cho... EC2"[cite: 1940].
    * [cite_start]**Đáp án:** **Security Group**[cite: 1941].
* [cite_start]**Keyword:** "chuyển hướng lưu lượng... sang **khu vực khác** khi có **thảm họa**" (reroute traffic... to **another region** during **disaster recovery**)[cite: 102].
    * [cite_start]**Đáp án:** **Amazon Route 53**[cite: 98, 105].
* [cite_start]"dịch vụ **DNS** (Domain Name System) trên đám mây"[cite: 878, 879].
    * [cite_start]**Đáp án:** **Amazon Route 53**[cite: 886].
* [cite_start]**Keyword:** "cung cấp một **phần logic bị cô lập**" (provision a **logically isolated section**)[cite: 185, 473, 1178, 1180].
    * [cite_start]**Đáp án:** **Amazon VPC**[cite: 188, 481, 1184].
* [cite_start]**Keyword:** "kết nối **chuyên dụng** (dedicated connection)... trải nghiệm mạng **nhất quán** (consistent)"[cite: 1160, 1161, 1162].
    * [cite_start]**Đáp án:** **AWS Direct Connect**[cite: 1164].
* [cite_start]**Keyword:** "thiết lập kết nối an toàn... **ít thời gian nhất** (least time)"[cite: 619, 621, 627].
    * [cite_start]**Đáp án:** **AWS Site-to-Site VPN**[cite: 628]. (Direct Connect mất vài tuần đến vài tháng).
* [cite_start]**Keyword:** "**tăng tốc độ phân phối nội dung**" (speed up content delivery)[cite: 1515, 1912].
    * [cite_start]**Đáp án:** **Amazon CloudFront**[cite: 1518, 1521].
* [cite_start]**Keyword:** "lợi ích của... **Edge locations**"[cite: 639, 640].
    * [cite_start]**Đáp án:** **Cải thiện hiệu suất** (Improves application performance) [cite: 641, 644, 645] [cite_start]và **Cung cấp bộ đệm (caching)** (Provides caching)[cite: 643, 646].

---

### 6. Cơ sở dữ liệu (Database - RDS, DynamoDB, Redshift)

* [cite_start]**Keyword:** "di chuyển (migrate)... cơ sở dữ liệu MySQL... sang Amazon RDS"[cite: 30].
    * [cite_start]**Đáp án:** **AWS Database Migration Service (AWS DMS)**[cite: 31, 36].
* [cite_start]**Keyword:** "lưu trữ kết quả của các truy vấn SQL **chuyên sâu I/O** (I/O-intensive)" (để cải thiện hiệu suất)[cite: 214, 215, 1101, 1102, 1103].
    * [cite_start]**Đáp án:** **Amazon ElastiCache**[cite: 219, 1105]. (Đây là dịch vụ caching).
* [cite_start]**Keyword:** "cơ sở dữ liệu OLTP MySQL **có khả năng mở rộng cao**" (highly scalable MySQL OLTP database)[cite: 661].
    * [cite_start]**Đáp án:** **Amazon Aurora**[cite: 664].
* [cite_start]**Keyword:** "cơ sở dữ liệu **phi quan hệ** (non-relational) linh hoạt, nhanh, có thể mở rộng"[cite: 966, 967, 968].
    * [cite_start]**Đáp án:** **Amazon DynamoDB**[cite: 972].
* [cite_start]**Keyword:** "tạo một **kho dữ liệu** (data warehouse)"[cite: 1323, 1324].
    * [cite_start]**Đáp án:** **Amazon Redshift**[cite: 1326, 1329].
* [cite_start]"đặc điểm... Amazon RDS"[cite: 1067].
    * [cite_start]**Đáp án:** **Đơn giản hóa các tác vụ quản trị** (Simplifies... administration tasks) [cite: 1068, 1073, 1076] [cite_start]và **Dễ dàng thiết lập, vận hành và mở rộng** (Makes it easy to set up, operate, and scale)[cite: 1068, 1074, 1076].

---

### 7. Giám sát, Bảo mật & Quản trị (Monitoring, Security & Governance)

* [cite_start]**Keyword:** "phân tích, điều tra... **nguyên nhân gốc rễ** (root cause) của các vấn đề bảo mật"[cite: 12, 14, 15, 16].
    * [cite_start]**Đáp án:** **Amazon Detective**[cite: 20].
* [cite_start]"tài liệu tuân thủ (compliance documents) như... **SOC 1, SOC 2**"[cite: 145, 149, 1037, 1546, 1547, 1548].
    * [cite_start]**Đáp án:** **AWS Artifact**[cite: 151, 1041, 1042, 1552].
* [cite_start]**Keyword:** "thiết lập một **landing zone**... môi trường **đa tài khoản** (multi-account)"[cite: 250, 251, 252, 811, 812, 814].
    * [cite_start]**Đáp án:** **AWS Control Tower**[cite: 256, 816].
* [cite_start]**Keyword:** "kiểm tra... tài nguyên... tuân thủ các **thực hành tốt nhất** (best practices)"[cite: 340, 341, 743, 744, 745, 750].
    * [cite_start]**Đáp án:** **AWS Trusted Advisor**[cite: 345, 346, 751].
* [cite_start]"**kho lưu trữ (repository) cho các chỉ số (metrics) và log**"[cite: 872, 876].
    * [cite_start]**Đáp án:** **Amazon CloudWatch**[cite: 877].
* [cite_start]"**lịch sử sự kiện** (event history) của... hoạt động tài khoản" [cite: 888] [cite_start]/ "xác định người dùng nào đã **chấm dứt** (terminated) EC2"[cite: 1897, 1898].
    * [cite_start]**Đáp án:** **AWS CloudTrail**[cite: 890, 1905].
* [cite_start]"khám phá, phân loại và bảo vệ **dữ liệu nhạy cảm (PII)**"[cite: 1212].
    * [cite_start]**Đáp án:** **Amazon Macie**[cite: 1213].
* [cite_start]"phân tích **lỗ hổng** (vulnerability analysis) trên... máy chủ"[cite: 1445, 1446, 1447, 1448].
    * [cite_start]**Đáp án:** **Amazon Inspector**[cite: 1452].
* [cite_start]"dịch vụ phát hiện **mối đe dọa** (threat detection)... giám sát **hoạt động độc hại**"[cite: 1534, 1535].
    * [cite_start]**Đáp án:** **Amazon GuardDuty**[cite: 1538, 1540].
* [cite_start]"bảo vệ... khỏi các cuộc tấn công **DDoS**"[cite: 1759].
    * [cite_start]**Đáp án:** **AWS Shield**[cite: 1760].

---

### 8. Các Khái niệm Cloud (Cloud Concepts)

Đây là những nguyên tắc cơ bản của AWS, bao gồm Lợi ích, Mô hình Trách nhiệm chung, và Well-Architected.

* [cite_start]**Keyword:** "Auto-Scaling dựa trên nhu cầu" là một ví dụ của[cite: 160].
    * [cite_start]**Đáp án:** **Thực thi tính đàn hồi** (Implement elasticity)[cite: 162].
* [cite_start]**Keyword:** "Trách nhiệm... **vá lỗi hệ điều hành máy chủ** (patch the host operating system) của... EC2"[cite: 297, 299, 1396, 1397].
    * [cite_start]**Đáp án:** **AWS**[cite: 301, 1402]. (Lưu ý: AWS chịu trách nhiệm cho HĐH *host*, khách hàng chịu trách nhiệm cho HĐH *khách* (guest OS)).
* [cite_start]**Keyword:** "lợi ích của việc di chuyển" (benefits of migrating)[cite: 323, 1247].
    * [cite_start]**Đáp án:** **Cho phép khách hàng tập trung vào hoạt động kinh doanh** (Enables the customer to focus on business activities)[cite: 330, 331, 1249, 1251].
* [cite_start]**Keyword:** "triển khai... ở **nhiều khu vực** (multiple AWS regions) chỉ với vài cú nhấp chuột"[cite: 395, 396].
    * [cite_start]**Đáp án:** **Vươn ra toàn cầu trong vài phút** (Go global in minutes)[cite: 398].
* [cite_start]**Keyword:** "lưu lượng truy cập **thay đổi** (varying levels)... không tiêu thụ hết công suất"[cite: 449, 450, 1426, 1427, 1428].
    * [cite_start]**Đáp án:** **Tính đàn hồi** (Elasticity)[cite: 451, 455, 1430].
* [cite_start]**Keyword:** "nguyên tắc thiết kế **thực hiện hoạt động dưới dạng mã** (performing operations as code)"[cite: 521].
    * [cite_start]**Đáp án:** (Trụ cột) **Operational Excellence** (Vận hành xuất sắc)[cite: 523, 527].
* [cite_start]**Keyword:** "phát biểu đúng... về Cấu trúc hạ tầng toàn cầu"[cite: 632, 633].
    * [cite_start]**Đáp án:** **Một AWS Region chứa nhiều Availability Zones** (An AWS Region contains multiple Availability Zones)[cite: 637, 638].
* [cite_start]**Keyword:** "quyền kiểm soát **chia sẻ** (shared control) giữa AWS và khách hàng"[cite: 721, 722].
    * [cite_start]**Đáp án:** **Nhận thức và Đào tạo** (Awareness and training)[cite: 729].
* [cite_start]**Keyword:** "trách nhiệm **duy nhất** của **khách hàng**" (solely the responsibility of the **customer**)[cite: 915, 917].
    * [cite_start]**Đáp án:** **Bảo vệ Dịch vụ và Truyền thông** (Service and Communications Protection) [cite: 916, 919, 924] (ví dụ: cấu hình Security Group, mã hóa dữ liệu).
* [cite_start]**Keyword:** "trách nhiệm **duy nhất** của **AWS**" (sole responsibility of **AWS**)[cite: 1222, 1224, 1225].
    * [cite_start]**Đáp án:** **Kiểm soát vật lý và môi trường** (Physical and environmental controls)[cite: 1230].
* [cite_start]**Keyword:** "lợi ích tài chính chính" (key financial benefit)[cite: 1022].
    * [cite_start]**Đáp án:** **Thay thế chi phí vốn ban đầu (CAPEX) bằng chi phí biến đổi thấp (variable costs)**[cite: 1025, 1027, 1028].
* [cite_start]**Keyword:** "mô tả Mô hình Trách nhiệm Chung" (describes the AWS Shared Responsibility model)[cite: 1336, 1337].
    * [cite_start]**Đáp án:** **AWS chịu trách nhiệm bảo mật cơ sở hạ tầng vật lý... khách hàng chịu trách nhiệm bảo mật ứng dụng và dữ liệu của họ** (AWS is responsible for securing the physical infrastructure... customers are responsible for securing their applications and data)[cite: 1338, 1340, 1348, 1355].

---

Hy vọng phần phân tích theo nhóm này giúp bạn hệ thống hóa kiến thức và nhận diện các từ khóa quan trọng một cách hiệu quả.

Bạn có muốn tôi đi sâu vào một nhóm dịch vụ cụ thể nào (ví dụ: chỉ các dịch vụ Cơ sở dữ liệu hoặc chỉ các dịch vụ Bảo mật) không?