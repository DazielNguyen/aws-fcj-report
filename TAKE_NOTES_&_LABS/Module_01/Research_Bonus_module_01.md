
# **NGHIÊN CỨU BỔ SUNG: AWS WELL ARCHITECTED FRAMEWORK**

## Các khái niệm, nguyên tắc thiết kế và biện pháp thực hành tốt nhất về kiến trúc để thiết kế và vận hành hệ thống của ta trong môi trường cloud
* **Góc nhìn chuyên sâu:** Không chỉ là việc "xây dựng thế nào", mà là việc **chuyển đổi tư duy** từ môi trường vật lý (On-premise) sang Cloud-native.
* **Nguyên tắc cốt lõi:**
    * **Ngừng đoán mò về dung lượng (Stop guessing capacity):** Thay vì mua server dư thừa cho đỉnh tải (peak), hãy thiết kế hệ thống có khả năng tự co giãn (Auto Scaling) theo nhu cầu thực tế.
    * **Kiến trúc hướng tới sự thay đổi (Design for evolution):** Yêu cầu kinh doanh thay đổi liên tục, kiến trúc "tĩnh" sẽ chết. Cần sử dụng các dịch vụ lỏng lẻo (Loosely coupled) để dễ dàng thay thế, nâng cấp từng phần mà không đập đi xây lại toàn bộ.

## Trả lời các câu hỏi qua đó ta sẽ biết được mức độ phù hợp giữa các kiến trúc
* **Góc nhìn chuyên sâu:** Đây thực chất là quy trình **Quản lý Rủi ro (Risk Management)**.
* **Logic:** Không có kiến trúc nào "hoàn hảo", chỉ có sự đánh đổi (Trade-offs). Việc trả lời câu hỏi giúp bạn phát hiện ra "Nợ kỹ thuật" (Technical Debt). Ví dụ: Bạn chấp nhận bảo mật lỏng hơn một chút ở môi trường Dev để đổi lấy tốc độ phát triển nhanh hơn (Speed to Market), nhưng ở Production thì không.

## Sử dụng AWS WAF tích hợp trên AWS Management Console -> cải thiện kiến trúc của mình
* **Thực tế:** Công cụ này (AWS Well-Architected Tool) cung cấp một **cơ chế đo lường nhất quán**. Nó tạo ra một "ngôn ngữ chung" giữa đội ngũ kỹ thuật (CTO/DevOps) và đội ngũ kinh doanh (CEO/Product Owner) để hiểu tại sao cần đầu tư thời gian vào việc refactor (tái cấu trúc) hệ thống thay vì chỉ ra tính năng mới.


### KHÁI NIỆM CỦA WELL-ARCHITECTED (WA):

- **Bản chất:** AWS Well Architected Framework không phải là một bài kiểm tra "Đậu/Rớt". Nó là một **hướng dẫn sinh tồn**. Nó giúp bạn trả lời câu hỏi: *"Hệ thống của tôi có đang đi đúng hướng để phát triển bền vững trong 3-5 năm tới không?"*

- **Workload (Khối lượng công việc):** Cần hiểu rộng hơn. Workload có thể là một website nhỏ, nhưng cũng có thể là một hệ thống thanh toán lõi (Core Banking). Việc xác định đúng phạm vi Workload cực kỳ quan trọng để áp dụng bộ câu hỏi phù hợp (Dùng dao mổ trâu để giết gà là lãng phí, dùng dao lam để mổ trâu là rủi ro).

---

### TỔNG CỘNG CÓ 6 TRỤ CỘT:

**1. Operational Excellence (Vận hành xuất sắc):**
- **Tư duy:** Chạy được code chỉ là bước đầu, vận hành nó ổn định mới là đích đến.
- **Thực hành sâu:**
    + **Operations as Code:** Biến toàn bộ hạ tầng thành code (IaC - Infrastructure as Code như Terraform/CloudFormation). Mọi thay đổi hạ tầng phải được review như review code.
    + **Make frequent, small, reversible changes:** Chia nhỏ bản update. Nếu sai, phải có khả năng quay lui (rollback) tức thì.
- **Ví dụ:** Không chỉ là CI/CD để deploy, mà là tích hợp **Automated Testing** trong pipeline. Nếu test fail, chặn deploy ngay lập tức.

**2. Security (Bảo mật):**
- **Tư duy:** Bảo mật ở mọi lớp (Defense in Depth) và Tự động hóa phản ứng.
- **Thực hành sâu:**
    + **Identity as the Perimeter:** Trong Cloud, tường lửa (Firewall) quan trọng, nhưng Định danh (IAM) mới là bức tường lửa mạnh nhất.
    + **Traceability (Khả năng truy vết):** Phải biết chính xác "Ai, làm gì, lúc nào, ở đâu" thông qua CloudTrail.
- **Chi tiết:** Không dùng Root Account. Áp dụng nguyên tắc **Least Privilege** (Quyền tối thiểu - chỉ cấp đúng quyền cần thiết, không dư một dòng).

**3. Reliability (Độ tin cậy):**
- **Tư duy:** Mọi thứ rồi sẽ hỏng (Everything fails all the time). Thiết kế để hệ thống **tự chữa lành**.
- **Thực hành sâu:**
    + **Decoupling (Phân tách):** Dùng hàng đợi (SQS) để nối các service. Nếu service xử lý chết, tin nhắn vẫn còn trong hàng đợi, không bị mất dữ liệu.
    + **Testing Recovery:** Đừng đợi sự cố thật mới sửa. Hãy chủ động tạo sự cố giả (Game Days) để tập trận.
- **Ví dụ:** Multi-AZ là cơ bản. Nâng cao là **Cross-Region Replication** (Sao lưu sang vùng địa lý khác) cho Disaster Recovery (DR).

**4. Performance Efficiency (Hiệu năng hoạt động) - *Trụ cột bạn thiếu trong danh sách*:**
- **Tư duy:** Sử dụng nguồn lực máy tính hiệu quả nhất để đáp ứng yêu cầu hệ thống khi nhu cầu thay đổi.
- **Thực hành sâu:**
    + **Democratize advanced technologies:** Đừng tự build lại cái gì AWS đã có. Dùng Managed Services (như DynamoDB, Lambda) để đỡ gánh nặng quản lý OS.
    + **Go Serverless:** Để AWS lo việc quản lý máy chủ, bạn chỉ lo logic code.

**5. Cost optimization (Tối ưu chi phí):**
- **Tư duy:** Chi phí cloud là chi phí biến đổi (OpEx), không phải cố định (CapEx). Tối ưu chi phí là tối ưu giá trị mang lại.
- **Thực hành sâu:**
    + **Expenditure Awareness (Nhận thức chi tiêu):** Dùng **Tagging** (gắn nhãn) cho mọi tài nguyên để biết team nào, dự án nào đang tiêu tiền.
    + **Matching supply with demand:** Tắt môi trường Dev/Test vào ban đêm và cuối tuần (tiết kiệm ~65% chi phí cho môi trường này).
- **Ví dụ:** Dùng Spot Instances cho các tác vụ xử lý nền (background jobs) để giảm tới 90% chi phí so với On-Demand.

**6. Sustainability (Bền vững):**
- **Tư duy:** Giảm dấu chân carbon là trách nhiệm chung. Tối ưu code = Tối ưu điện năng.
- **Thực hành sâu:**
    + **Maximize Utilization:** Một server chạy 80% công suất tốt hơn 2 server chạy 10% công suất.
    + **Hardware Selection:** Dùng chip **AWS Graviton (ARM)** - hiệu năng tốt hơn nhưng tốn ít điện hơn chip x86 truyền thống.

---

### HOẶC ĐƠN GIẢN HƠN TA CÓ THỂ DÙNG WELL ARCHITECTED TOOL

* **Logic thực tế:** Tool này giúp tạo ra một bản báo cáo rủi ro (Risk Report).
    * **High Risk Issues (HRI):** Những lỗi chí mạng (ví dụ: mở port database ra public internet). Cần khắc phục ngay.
    * **Medium Risk Issues (MRI):** Những điểm chưa tối ưu (ví dụ: chưa bật log đầy đủ). Đưa vào lộ trình (roadmap) để sửa sau.

---

### CÁC CÂU HỎI CƠ BẢN (Mở rộng theo tư duy Architect):

- **Security:** “Ai có quyền truy cập dữ liệu này?”
    * **Phân tích:** Nếu câu trả lời là "Admin" hoặc "Mọi người", hệ thống đang "Trần trụi".
    * **Giải pháp SA:** Phải trả lời được cụ thể Role nào (Role-Based Access Control). Cần áp dụng mã hóa (Encryption) để ngay cả khi trộm được ổ cứng cũng không đọc được dữ liệu.

- **Reliability:** “Nếu 1 server chết, hệ thống có tiếp tục hoạt động không?”
    * **Phân tích:** Đây là khái niệm **Single Point of Failure (Điểm chết duy nhất)**.
    * **Giải pháp SA:** Hệ thống phải trả lời là "Có, traffic sẽ tự động chuyển sang server khác nhờ Load Balancer và Auto Scaling Group mà người dùng không hề hay biết".

- **Cost:** “Có tài nguyên nào chạy 24/7 mà không cần không?”
    * **Phân tích:** Đây là sự lãng phí thầm lặng (Zombie resources).
    * **Giải pháp SA:** Thiết lập **AWS Budgets** để cảnh báo khi chi phí tăng đột biến. Sử dụng **Trusted Advisor** để quét và chỉ ra các IP tĩnh (Elastic IP) hoặc ổ cứng (EBS Volume) đang không được gắn vào đâu nhưng vẫn bị tính tiền.

