---
title: "Bản đề xuất"
date: "2025-09-09"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Ứng dụng quản lý tài chính cá nhân

### 1. Tóm tắt điều hành

Dự án Personal Finance Management App hướng đến việc cung cấp một nền tảng quản lý tài chính cá nhân thông minh, hiện đại và mang tính tự động hóa cao. Ứng dụng cho phép người dùng ghi nhận thu chi, tạo và quản lý nhiều hũ tiền (money jars) theo mục đích khác nhau, lập kế hoạch chi tiêu, nhận cảnh báo thông minh và tạo báo cáo phân tích trực quan.

Ứng dụng được xây dựng với kiến trúc microservices trên nền tảng .NET và FastAPI, triển khai trên AWS Cloud, đảm bảo tính linh hoạt, khả năng mở rộng và an toàn dữ liệu. Quy trình phát triển tuân theo mô hình Agile/Scrum (2 tuần/sprint), với thời gian hoàn thành MVP trong 2 tháng.

### 2. Tuyên bố vấn đề

#### Vấn đề hiện tại

Trên thị trường đã có rất nhiều ứng dụng quản lý tài chính, tuy nhiên phần lớn vẫn yêu cầu người dùng nhập liệu thủ công — một công việc tốn thời gian, dễ sai sót và khiến người dùng nhanh chóng bỏ cuộc. Các ứng dụng hiện có chỉ tập trung vào thống kê chi tiêu mà chưa thực sự giúp người dùng tự động hóa quy trình quản lý tài chính cá nhân.

#### Giải pháp

Giải pháp sử dụng AWS Cloud kết hợp kiến trúc microservices để xây dựng một nền tảng quản lý tài chính cá nhân tự động hóa, tích hợp AI trong xử lý giọng nói và nhận diện hóa đơn. Hệ thống được triển khai trên AWS ECS Fargate cho các service backend (.NET), FastAPI cho xử lý AI, và Next.js cho frontend. So với các nền tảng tài chính phổ biến như Money Lover hay Misa Money Keeper, ứng dụng này tập trung vào tự động hóa hoàn toàn nhập liệu tài chính thông qua AI voice-to-text và bill scanning chi tiết tiếng Việt, giúp giảm thao tác thủ công và sai sót. Hệ thống phù hợp cho người dùng cá nhân và nhóm nhỏ, đồng thời có thể mở rộng khi cần cho quy mô doanh nghiệp hoặc ứng dụng ngân hàng số.

#### Lợi ích và hoàn vốn đầu tư (ROI)

Giải pháp mang lại nhiều lợi ích thiết thực cả về mặt kỹ thuật và giá trị kinh doanh:

- Tự động hóa nhập liệu: Giảm hơn 70% thao tác thủ công nhờ AI nhận diện giọng nói và hóa đơn.
- Tăng độ chính xác: Hạn chế sai sót nhập liệu, đảm bảo tính toàn vẹn của dữ liệu tài chính (>90% chính xác).
- Cải thiện hiệu suất người dùng: Ghi nhận và phân loại giao dịch chỉ trong vài giây, tối ưu trải nghiệm sử dụng.
- Tiết kiệm chi phí: Chi phí hạ tầng thấp nhờ tận dụng AWS Free Tier đến năm 2026; chỉ ước tính ~60 USD/tháng cho AWS và ~30 USD cho compute AI.
- Hoàn vốn nhanh: Dự kiến hoàn vốn trong 6–12 tháng, nhờ tiết kiệm thời gian nhập liệu và tăng hiệu suất vận hành.
- Khả năng mở rộng & tích hợp: Kiến trúc microservices trên AWS cho phép dễ dàng bổ sung tính năng (mobile app, phân tích nâng cao, tích hợp ngân hàng).

### 3. Kiến trúc giải pháp

Hệ thống được triển khai theo mô hình **microservices** trên nền tảng **AWS Cloud**, kết hợp các dịch vụ serverless, container, và cơ sở dữ liệu quản lý để đảm bảo hiệu năng và khả năng mở rộng.

![Ứng dụng quản lý tài chính cá nhân Sofware Architecture](/images/2-Proposal/development_architecture.drawio.png)

Người dùng truy cập ứng dụng web **Next.js** thông qua **Amazon CloudFront**, nội dung tĩnh được lưu trữ trong **Amazon S3** và phân phối qua **Amazon Route 53**.
Lớp bảo mật đầu tiên được cung cấp bởi **AWS WAF** nhằm ngăn chặn các tấn công phổ biến như SQL Injection hoặc XSS.

Khi người dùng đăng nhập, quá trình xác thực được xử lý bởi **Amazon Cognito**, cấp token truy cập để frontend gửi các yêu cầu API qua **Amazon API Gateway**.
API Gateway định tuyến yêu cầu đến **Application Load Balancer (ALB)** thông qua **AWS PrivateLink**, sau đó chuyển tiếp đến **Amazon ECS (Fargate)** — nơi triển khai các container backend bao gồm:

- **Backend Service (.NET)**: Xử lý nghiệp vụ chính của hệ thống.

- **AI Service (FastAPI)**: Xử lý hóa đơn, nhận dạng giọng nói và các tác vụ AI.

Khi người dùng tải hóa đơn hoặc ghi âm, file tạm thời được lưu trong **Amazon S3**.  
**AI Service** có thể truy cập tệp từ **Amazon S3** để thực hiện các xử lý dữ liệu, sau đó trả kết quả lại cho **Backend Service** thông qua message broker.

Hình ảnh container được lưu trữ trong **Amazon ECR**, và quá trình triển khai được tự động hóa qua **GitLab CI/CD Pipeline** — bao gồm các bước build image, push lên ECR, và cập nhật Task Definition trên ECS.

Tất cả logs, metrics và cảnh báo từ ECS, API Gateway, và ALB được gửi về **Amazon CloudWatch** để giám sát tập trung, đồng thời **Amazon SNS** được cấu hình để gửi cảnh báo tự động khi có sự cố.

![Ứng dụng quản lý tài chính cá nhân Cloud Architecture](/images/2-Proposal/cloud_architecture.drawio.png)

_Dịch vụ AWS sử dụng_

- _Amazon Route 53_: Quản lý DNS và tên miền truy cập.
- _AWS WAF_: Bảo vệ hệ thống khỏi các tấn công web phổ biến.
- _Amazon CloudFront_: Phân phối nội dung tĩnh toàn cầu và tăng tốc truy cập frontend.
- _Amazon S3_: Lưu trữ website tĩnh và file người dùng (hóa đơn, ghi âm).
- _Amazon Cognito_: Xác thực và quản lý người dùng.
- _Amazon API Gateway_: Cổng vào của hệ thống, định tuyến request từ frontend đến backend.
- _AWS PrivateLink_: Tạo kết nối riêng giữa API Gateway và ALB trong VPC để tăng cường bảo mật.
- _Application Load Balancer (ALB)_: Cân bằng tải giữa các container backend trên ECS.
- _Amazon ECS (Fargate)_: Chạy các microservices Backend và FastAPI (AI).
- _Amazon ECR_: Kho lưu trữ image container cho ECS.
- _Amazon CloudWatch_: Giám sát logs, hiệu năng và cảnh báo hệ thống.
- _Amazon SNS_: Gửi thông báo hoặc cảnh báo khi có sự cố.
- _GitLab CI/CD_: Tự động hóa pipeline build, push và deploy container lên ECS.

---

### 4. Triển khai kỹ thuật

#### Các giai đoạn triển khai

1. _Nghiên cứu và vẽ kiến trúc_: Nghiên cứu các mô hình microservices và thiết kế kiến trúc tổng thể trên AWS (bao gồm CloudFront, ECS Fargate, RDS, S3, API Gateway, Cognito) — (Tháng 1).
2. _Tính toán chi phí và điều chỉnh giải pháp_: Sử dụng AWS Pricing Calculator để ước tính chi phí, tối ưu lựa chọn dịch vụ nhằm đảm bảo chi phí thấp và dễ triển khai cho người mới học — (Tháng 1–2).
3. _Phát triển, kiểm thử, triển khai_: Xây dựng frontend (Next.js), backend (.NET), và AI service (FastAPI); kiểm thử tích hợp microservices, sau đó triển khai toàn bộ hệ thống lên AWS bằng ECS Fargate và thiết lập giám sát qua CloudWatch — (Tháng 2–3).

#### Yêu cầu kỹ thuật

- _Frontend_:
  Ứng dụng web **Next.js** được lưu trữ trong **Amazon S3** và phân phối qua **CloudFront**, giao tiếp với backend thông qua **API Gateway**.
  Người dùng đăng nhập qua **Amazon Cognito**, nhận token để gọi API bảo mật.
- _Backend_:
  Viết bằng **.NET** hoặc framework tương tự, triển khai trên **ECS Fargate**.
  Các service xử lý nghiệp vụ người dùng, giao dịch và các yêu cầu từ frontend.
  Container image được lưu trong **ECR**, được cập nhật qua pipeline CI/CD từ **GitLab**.
  **ALB** được dùng để cân bằng tải giữa các container backend.
- _AI Service_:
  Viết bằng **FastAPI**, xử lý hình ảnh hóa đơn và giọng nói, kết nối đến **S3** để đọc dữ liệu.
  Kết quả được trả về **Backend Service** thông qua API nội bộ.
- _Hạ tầng Cloud_:
  Sử dụng **Amazon VPC** (multi-AZ), **Application Load Balancer**, và **CloudWatch** để giám sát.
  Hình ảnh container được lưu trữ trên **ECR** và triển khai qua **ECS Fargate**.
  CI/CD được thực hiện qua **GitLab CI/CD** để tự động hóa build và deploy.
- _Bảo mật_:
  Quản lý quyền truy cập người dùng bằng **Amazon Cognito**.
  Sử dụng **IAM Roles** cho ECS, S3, CloudWatch, và API Gateway để giới hạn quyền truy cập.
  **Security Group** được cấu hình chặt chẽ giữa ECS, ALB và các dịch vụ khác để đảm bảo an toàn mạng.
  **AWS WAF** được cấu hình để bảo vệ tầng frontend khỏi các tấn công web phổ biến.

### 5. Lộ trình & Mốc triển khai

- _Trước thực tập (Tháng 0)_: 1 tháng lên kế hoạch.
- _Thực tập (Tháng 1–3)_:
  - Tháng 1: Học AWS và nâng cấp kỹ năng lập trình.
  - Tháng 2: Thiết kế và điều chỉnh kiến trúc.
  - Tháng 3: Triển khai, kiểm thử, đưa vào sử dụng.
- _Sau triển khai_: Nghiên cứu thêm về mobile và triển khai sau tháng thứ 4.

### 6. Ước tính ngân sách

_Có thể xem chi phí trên [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=2f4e6708ef12a3310b2d3955aaf1d4563932d165)_

| Dịch vụ              |                            Trong Free Tier |                        Sau khi hết Free Tier |
| -------------------- | -----------------------------------------: | -------------------------------------------: |
| Amazon ECS (Fargate) |                           0,00 USD / tháng |                             8,00 USD / tháng |
| Amazon API Gateway   |                           0,00 USD / tháng |                             2,00 USD / tháng |
| Amazon S3            |                           0,00 USD / tháng |                             1,00 USD / tháng |
| Amazon CloudWatch    |                           0,00 USD / tháng |                             2,00 USD / tháng |
| Amazon Cognito       |                           0,00 USD / tháng |                             0,00 USD / tháng |
| Amazon ECR           |                           0,00 USD / tháng |                             0,20 USD / tháng |
| Amazon Route 53      |                           1,00 USD / tháng |                             1,00 USD / tháng |
| AWS WAF              |                           0,00 USD / tháng |                             1,00 USD / tháng |
| Amazon SNS           |                           0,00 USD / tháng |                             0,50 USD / tháng |
| GitLab CI/CD         |                           0,00 USD / tháng |                             2,00 USD / tháng |
| **Tổng ước tính**    | **≈ 1,00 USD / tháng** (≈ 12,00 USD / năm) | **≈ 17,70 USD / tháng** (≈ 212,40 USD / năm) |

### 7. Đánh giá rủi ro

_Ma trận rủi ro_

- Mô hình AI nhận dạng sai (voice/bill): Ảnh hưởng trung bình, xác suất trung bình.
- Mất kết nối AWS hoặc lỗi dịch vụ vùng (region): Ảnh hưởng cao, xác suất thấp.
- Vượt ngân sách sử dụng AWS: Ảnh hưởng trung bình, xác suất thấp.
- Lỗi đồng bộ dữ liệu giữa các microservices: Ảnh hưởng trung bình, xác suất trung bình.
- Lộ thông tin người dùng (Cognito/Database): Ảnh hưởng cao, xác suất thấp.

_Chiến lược giảm thiểu_

- AI: Cải thiện mô hình OCR và voice-to-text qua huấn luyện thêm, kiểm thử định kỳ với dữ liệu thực tế.
- AWS Region: Thiết lập triển khai đa vùng (multi-AZ) và backup định kỳ cơ sở dữ liệu RDS.
- Chi phí: Cấu hình **AWS Budget Alert** và tối ưu ECS, S3 theo mức sử dụng thực tế.
- Microservices: Dùng **SQS/RabbitMQ** để đảm bảo xử lý bất đồng bộ và retry khi lỗi.
- Bảo mật: Mã hóa dữ liệu (AES-256, HTTPS), kiểm soát IAM theo nguyên tắc “Least Privilege”.

_Kế hoạch dự phòng_

- Nếu AWS gặp sự cố: Tạm thời chuyển sang lưu trữ dữ liệu giao dịch cục bộ và đồng bộ lại sau khi khôi phục.
- Khôi phục hạ tầng bằng **AWS CloudFormation** hoặc **IaC (Infrastructure as Code)** đã lưu sẵn.
- Giữ bản sao cơ sở dữ liệu định kỳ (RDS snapshot) để phục hồi trong tình huống mất dữ liệu.

### 8. Kết quả kỳ vọng của dự án

- **Tự động hóa nhập liệu tài chính:** Ứng dụng giúp người dùng không cần nhập thủ công, chỉ cần chụp hóa đơn hoặc ghi âm giọng nói để hệ thống tự phân loại chi tiêu.
- **Quản lý tài chính trực quan:** Người dùng có thể xem biểu đồ chi tiêu, báo cáo tháng, và nhận gợi ý tiết kiệm dựa trên hành vi tiêu dùng.
- **Trải nghiệm người dùng tối giản:** Giao diện web thân thiện, thiết kế hiện đại, tối ưu cho thiết bị di động và phù hợp với người mới quản lý tài chính.
- **Hệ thống ổn định, dễ mở rộng:** Kiến trúc microservices giúp dễ dàng bổ sung tính năng mới như nhắc nhở chi tiêu, phân tích dự báo AI, hoặc mở rộng sang mobile app.
- **Chi phí vận hành thấp:** Tận dụng Free Tier AWS và mô hình serverless để duy trì hệ thống với chi phí trung bình < 50 USD/tháng.
- **Nâng cao kỹ năng nhóm phát triển:** Thành viên dự án tiếp cận thực tế với quy trình DevOps, triển khai CI/CD, và tối ưu ứng dụng trên nền tảng cloud.

### 9. Hạn chế của dự án

- **Mô hình AI tiếng Việt còn hạn chế:** Khả năng nhận dạng giọng nói vùng miền hoặc hóa đơn viết tay chưa đạt độ chính xác cao.
- **Chưa có ứng dụng di động riêng:** Phiên bản MVP chỉ hỗ trợ nền web, chưa có mobile app native.
- **Giới hạn người dùng:** Kiến trúc hiện tại chỉ tối ưu cho 50–100 người dùng hoạt động; khi mở rộng quy mô cần tái cấu trúc hạ tầng.
- **Phụ thuộc kết nối Internet:** Mọi thao tác xử lý và lưu trữ đều qua cloud, không thể hoạt động offline.
- **Chưa triển khai hệ thống bảo mật nâng cao:** Mới dừng ở xác thực Cognito và mã hóa cơ bản, chưa có MFA (Multi-Factor Authentication) hay log bảo mật chuyên sâu.