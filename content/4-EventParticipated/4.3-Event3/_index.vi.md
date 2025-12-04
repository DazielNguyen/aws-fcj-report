---
title: "Event 3"
date: "2025-10-16"
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Bài thu hoạch: WORKSHOP “KHOA HỌC DỮ LIỆU TRÊN NỀN TẢNG AWS”

### Mục Đích Của Sự Kiện

- Giới thiệu tổng quan hệ sinh thái các dịch vụ trí tuệ nhân tạo (AI) hiện có trên AWS.
- Hướng dẫn quy trình thực tế để xây dựng và huấn luyện mô hình AI sử dụng Amazon SageMaker.
- Minh họa cách thức đưa mô hình AI từ phòng thí nghiệm ra thực tế (deployment) và tích hợp vào ứng dụng thông qua API.

### Danh Sách Diễn Giả

- **Anh Văn Hoàng Kha** - Cloud Solutions Architect, Leader của AWS User Group (Chia sẻ góc nhìn kiến trúc giải pháp).
- **Anh Bạch Doãn Vương** - Cloud DevOps Engineer, AWS Community Builder (Chia sẻ góc nhìn vận hành và triển khai).

### Nội Dung Chuyên Sâu

#### **Tầm Quan Trọng Của Điện Toán Đám Mây Trong Data Science**

- Phân tích vai trò cốt lõi của **Cloud Computing**: Không chỉ là nơi lưu trữ, Cloud cung cấp sức mạnh tính toán vô hạn để xử lý dữ liệu lớn (Big Data) và huấn luyện các mô hình AI phức tạp mà máy tính cá nhân khó đáp ứng.
- So sánh hiệu quả giữa **Cloud và On-premise (Máy chủ vật lý)**:

  - **Cloud:** Điểm mạnh nằm ở tính đàn hồi (Elasticity) — có thể tăng/giảm tài nguyên tức thì, triển khai cực nhanh, chuyển đổi chi phí đầu tư (CAPEX) thành chi phí vận hành (OPEX), và dễ dàng tích hợp các công nghệ mới.
  - **On-premise:** Gặp rào cản lớn về chi phí phần cứng ban đầu, khó khăn trong việc mở rộng hạ tầng khi dữ liệu tăng đột biến và tốn kém nhân lực bảo trì.

- **AWS** đóng vai trò là xương sống cho toàn bộ **Data Science pipeline**: Cung cấp một quy trình khép kín từ lúc thu thập dữ liệu thô, làm sạch, huấn luyện đến khi mô hình được đưa vào sử dụng thực tế.

#### **Phân Tầng Kiến Trúc AI Trên AWS**

AWS phân loại các dịch vụ AI thành **3 tầng (layers)** riêng biệt, được thiết kế để phù hợp với từng đối tượng người dùng có trình độ kỹ thuật và nhu cầu kiểm soát khác nhau:

**1. AI Services (Tầng Dịch Vụ Được Quản Lý Hoàn Toàn)**

> _Giải pháp "Mì ăn liền" dành cho Developer muốn tích hợp trí thông minh vào ứng dụng mà không cần am hiểu sâu về thuật toán ML._

- Đây là các mô hình đã được AWS huấn luyện sẵn (Pre-trained models) với hàng tỷ điểm dữ liệu.
- Người dùng chỉ cần gửi dữ liệu qua API và nhận lại kết quả phân tích.
- **Các dịch vụ tiêu biểu:**

  - **Amazon Comprehend:** Hiểu và phân tích ý nghĩa văn bản, cảm xúc người dùng (NLP).
  - **Amazon Translate:** Xóa bỏ rào cản ngôn ngữ với khả năng dịch thuật tự động.
  - **Amazon Textract:** "Đọc" tài liệu, bóc tách chữ viết và bảng biểu từ file scan/ảnh.
  - **Amazon Rekognition:** Thị giác máy tính, nhận diện vật thể, khuôn mặt trong ảnh/video.
  - **Amazon Polly:** Giọng đọc nhân tạo tự nhiên (Text-to-Speech).
  - **Amazon Bedrock:** Cổng kết nối đến các mô hình ngôn ngữ lớn (LLMs) hàng đầu hiện nay.

**Lợi ích:** Tốc độ đưa sản phẩm ra thị trường (Time-to-market) cực nhanh, không tốn công sức xây dựng mô hình từ số 0.

**2. ML Services (Tầng Bán Quản Lý)**

> _Công cụ đắc lực cho Data Scientist & ML Engineer cần môi trường chuyên nghiệp để tự xây dựng mô hình._

- **Amazon SageMaker** là trái tim của tầng này, cung cấp một nền tảng thống nhất để quản lý vòng đời của mô hình ML (ML Ops).
- Các module quan trọng:

  - **Data Wrangler:** Giảm thiểu thời gian chuẩn bị và làm sạch dữ liệu (vốn chiếm 80% thời gian dự án).
  - **Feature Store:** Kho lưu trữ các đặc trưng dữ liệu để tái sử dụng, tránh lãng phí tài nguyên tính toán.
  - **AutoML (SageMaker Autopilot):** Tự động thử nghiệm nhiều thuật toán để tìm ra mô hình tốt nhất mà không cần can thiệp thủ công.
  - **Model Registry & Monitoring:** Quản lý phiên bản mô hình và giám sát độ chính xác của mô hình theo thời gian thực (tránh hiện tượng model drift).

**Lợi ích:** Cân bằng hoàn hảo giữa tính tiện lợi và khả năng tùy biến sâu vào quy trình huấn luyện.

**3. AI Infrastructure (Tầng Hạ Tầng Tự Quản Lý)**

> _Dành cho các chuyên gia nghiên cứu (Researchers) cần can thiệp sâu vào phần cứng và tối ưu hóa ở mức thấp nhất._

- Cung cấp "gạch nền" để tự xây dựng hệ thống AI tùy chỉnh:

  - **Amazon EC2 P5/G6/Inferentia:** Các máy ảo gắn chip chuyên dụng (GPU/ASIC) cho hiệu suất tính toán cực cao.
  - **Amazon EKS / ECS:** Quản lý container cho các ứng dụng ML quy mô lớn.
  - **AWS Lambda:** Chạy code suy luận (inference) dạng serverless, tiết kiệm chi phí cho các tác vụ nhỏ.
  - **Amazon S3 / EFS:** Hệ thống lưu trữ "hồ dữ liệu" (Data Lake) khổng lồ.

**Lợi ích:** Không bị giới hạn bởi khuôn mẫu, tối ưu hóa chi phí triệt để cho các hệ thống siêu lớn, nhưng đòi hỏi kỹ năng DevOps cao.

#### Các Dịch Vụ AI Phổ Biến Hỗ Trợ Sinh Viên & Nhà Nghiên Cứu

**1. Amazon SageMaker**

- Là một IDE (Môi trường phát triển tích hợp) dành riêng cho ML trên mây:

  - Tích hợp mọi công đoạn từ xử lý dữ liệu thô đến tinh chỉnh tham số (hyperparameter tuning).
  - Cung cấp khả năng CI/CD cho Machine Learning, giúp tự động hóa quy trình train và deploy.
  - Hỗ trợ Notebooks (Jupyter) quen thuộc với sinh viên.

**2. Amazon Comprehend**

- Mang lại khả năng "đọc hiểu" cho ứng dụng:

  - **Phân tích cảm xúc:** Biết khách hàng đang vui, giận hay hài lòng qua email/comment.
  - **Nhận dạng thực thể:** Tự động phát hiện tên người, địa điểm, tổ chức trong văn bản.
  - **Bảo mật:** Tự động tìm và che giấu thông tin cá nhân (PII) trong dữ liệu.

**3. Amazon Translate**

- Dịch thuật chất lượng cao dựa trên Deep Learning (Neural Network).
- Khả năng tùy chỉnh từ vựng chuyên ngành (ví dụ: dịch đúng các thuật ngữ y khoa hoặc kỹ thuật).
- Giúp mở rộng phạm vi người dùng cho ứng dụng ra toàn cầu.

**4. Amazon Textract**

- Vượt xa công nghệ OCR truyền thống nhờ khả năng hiểu cấu trúc tài liệu.
- Giữ nguyên định dạng bảng biểu, form mẫu khi trích xuất, giúp số hóa giấy tờ hành chính nhanh chóng và chính xác.

#### Quy Trình Data Science Tiêu Chuẩn Trên AWS

1. **Ingest & Store:** Thu thập dữ liệu từ nhiều nguồn vào "kho chứa" Amazon S3.
2. **Prepare:** Làm sạch và chuẩn hóa dữ liệu bằng AWS Glue hoặc Lambda.
3. **Train & Tune:** Sử dụng SageMaker để huấn luyện và tối ưu hóa thuật toán.
4. **Deploy:** Đóng gói mô hình thành API Endpoint hoặc tích hợp vào ứng dụng.
5. **Monitor:** Sử dụng CloudWatch để theo dõi sức khỏe hệ thống và chất lượng dự đoán của mô hình.

#### **Demo 1: Tối Ưu Hóa Workflow Với Low-Code/No-Code**

- **Mục tiêu:** Chứng minh rằng rào cản kỹ thuật trong AI đang dần được xóa bỏ nhờ các công cụ trực quan.
- **Công cụ:** Amazon SageMaker Canvas (Giao diện kéo thả).
- **Quy trình thực hiện:**

  1. Upload bộ dữ liệu thô lên S3.
  2. Sử dụng giao diện đồ họa để định nghĩa luồng xử lý: Input -> Xử lý thiếu dữ liệu -> Chọn target column -> Train.
  3. Hệ thống tự động chạy thử nghiệm và trả về các chỉ số đánh giá (Accuracy, F1-score...) dưới dạng biểu đồ dễ hiểu.

- **Ý nghĩa:** Giúp sinh viên và Business Analyst có thể tạo ra giá trị từ dữ liệu ngay lập tức mà không cần viết hàng ngàn dòng code Python.

#### **Demo 2: Từ Mô Hình Đến Ứng Dụng Thực Tế (Deployment)**

- **Mục tiêu:** Minh họa "cây cầu" nối giữa mô hình toán học và người dùng cuối.
- **Công cụ:** SageMaker Endpoint kết hợp với API Gateway và Lambda.
- **Quy trình thực hiện:**

  1. Biến mô hình đã train thành một HTTP Endpoint (địa chỉ mạng).
  2. Thiết lập API Gateway để nhận yêu cầu từ bên ngoài (ví dụ: từ mobile app).
  3. Xử lý logic trung gian bằng AWS Lambda (serverless) để gọi model và trả kết quả về cho người dùng.

- **Ý nghĩa:** Cho thấy bức tranh toàn cảnh của việc làm sản phẩm AI: Model chỉ là một phần, việc tích hợp và phục vụ (serving) model mới tạo ra sản phẩm hoàn chỉnh.

#### Bảng So Sánh: Cloud vs. On-premise (Góc nhìn Hiệu Năng & Kinh Tế)

| Tiêu chí | Cloud (AWS) | On-premise (Máy chủ riêng) |
| :--- | :--- | :--- |
| **Khả năng mở rộng** | **Vô hạn & Tức thì:** Tự động scale theo lượng traffic thực tế. | **Cứng nhắc:** Bị giới hạn bởi số lượng phần cứng hiện có. |
| **Mô hình chi phí** | **OPEX (Chi phí vận hành):** Dùng bao nhiêu trả bấy nhiêu, không lãng phí. | **CAPEX (Chi phí vốn):** Phải bỏ tiền cục lớn mua máy móc, rủi ro khấu hao. |
| **Tốc độ triển khai** | **Phút:** Chỉ cần vài click chuột để có server. | **Tuần/Tháng:** Phải đặt hàng, lắp đặt, cài đặt OS. |
| **Bảo trì hệ thống** | **AWS lo:** Tập trung hoàn toàn vào phát triển ứng dụng. | **Tự làm:** Tốn nhân sự IT để vận hành điện, lạnh, phần cứng. |
| **Phù hợp với sinh viên** | **Cao:** Tận dụng gói Free Tier để học tập miễn phí. | **Thấp:** Yêu cầu máy cấu hình cao đắt tiền. |

#### Kết Luận Chung

- AWS cung cấp một **hệ sinh thái toàn diện và liền mạch**, xóa nhòa khoảng cách giữa việc học thuật và ứng dụng thực tế. Dù là người mới bắt đầu hay doanh nghiệp lớn, AWS đều có bộ công cụ (Layer) phù hợp để giải quyết bài toán dữ liệu.

### Cảm Nhận Cá Nhân Sau Sự Kiện

Buổi workshop **“AI Services on AWS for Data Science”** không chỉ cung cấp kiến thức lý thuyết mà còn mở ra tư duy mới về cách tiếp cận công nghệ, giúp tôi định hình rõ hơn con đường từ **nghiên cứu dữ liệu** đến **xây dựng sản phẩm**.

#### Mở rộng tư duy nhờ các chuyên gia

- Hiểu rõ lý do tại sao thế giới đang dịch chuyển lên Cloud: Đó là sự giải phóng khỏi gánh nặng hạ tầng để tập trung vào giá trị cốt lõi là dữ liệu.
- Nắm bắt được bức tranh tổng thể về **3 tầng AI**, từ đó biết cách lựa chọn dịch vụ phù hợp cho từng giai đoạn của dự án cá nhân.

#### Trực quan hóa kiến thức qua Demo

- **Demo 1 (Canvas):** Ấn tượng với khả năng "bình dân hóa" AI. Việc train model giờ đây trực quan như lắp ghép lego, giúp kiểm chứng ý tưởng cực nhanh.
- **Demo 2 (Deployment):** Đây là mảnh ghép tôi thường thiếu sót. Hiểu được cách tạo ra một API để người khác có thể dùng model của mình là bước ngoặt từ việc "làm bài tập" sang "làm sản phẩm".

#### Tiếp cận công nghệ tiên tiến

- Các dịch vụ như **Comprehend** hay **Textract** cho thấy sức mạnh của Pre-trained models. Chúng giúp giải quyết các bài toán khó (như đọc hóa đơn, phân tích sentiment) chỉ trong tích tắc mà không cần tự build model phức tạp.

#### Giá trị kết nối

- Cơ hội thảo luận về bài toán chi phí (Cost optimization) là rất thực tế, giúp sinh viên như tôi biết cách dùng Cloud mà không "cháy túi".
- Mạng lưới networking với các anh chị trong ngành giúp tôi có thêm động lực và định hướng nghề nghiệp rõ ràng hơn.

#### Bài học cốt lõi

- **Cloud First:** Tư duy đưa mọi thứ lên mây là xu hướng tất yếu của Data Science hiện đại.
- **Tính thực tiễn:** Một mô hình AI chỉ có giá trị khi nó được deploy và giải quyết vấn đề cho người dùng cuối.
- **Hệ sinh thái AWS:** Là kho công cụ khổng lồ mà tôi cần tiếp tục khai phá để nâng cao năng lực bản thân.

#### Một số hình ảnh ghi lại tại sự kiện

<img src="/images/4-EventParticipated/4.3-Event3/Event_03_IMG_7059.jpeg" alt="Event_03" width="2000"/>

> **Hình ảnh sự truyền đạt kiến thức từ 2 anh đến từ AWS**

<img src="/images/4-EventParticipated/4.3-Event3/Event_03.JPG" alt="Event_03" width="2000"/>

> **Hình ảnh đội FPTers check-in sau sự kiện**

> Đây là khoảnh khắc check-in của toàn bộ các bạn đang thực tập tại AWS sau khi kết thúc workshop.
