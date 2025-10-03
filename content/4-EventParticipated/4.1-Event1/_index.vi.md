---

title: "Event 1"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 4.1. </b> "

---

# Bài thu hoạch “Vietnam Cloud Day 2025: Ho Chi Minh City Connect Edition for Builders (Track 1: GenAI & Data)”

### Mục Đích Của Sự Kiện

- Tìm hiểu **bảo mật trong GenAI và AI Agent** để tăng cường an toàn cho doanh nghiệp
- Khám phá **AI-Driven Development Lifecycle (AI-DLC)** và ứng dụng vào quy trình phát triển phần mềm
- Xây dựng **nền tảng dữ liệu hợp nhất** nhằm tối ưu cho phân tích và trí tuệ nhân tạo
- Cập nhật **chiến lược và xu hướng GenAI** mới nhất trên AWS

### Danh Sách Diễn Giả

- **Jun Kai Loke** – AI/ML Specialist SA, AWS
- **Kien Nguyen** – Solutions Architect, AWS
- **Tamelly Lim** – Storage Specialist SA, AWS
- **Binh Tran** – Senior Solutions Architect, AWS
- **Taiki Dang** – Solutions Architect, AWS
- **Michael Armentano** – Principal WW GTM Specialist, AWS

### Nội Dung Nổi Bật

## Nội dung chính

1. **Nền tảng dữ liệu thống nhất trên AWS cho AI & Analytics**


    - Xây dựng data platform end-to-end: ingestion → lưu trữ → xử lý → truy cập → quản trị.
    - Xóa silo dữ liệu, con người, quy trình; hỗ trợ self-service & chuẩn hóa governance.
    - Dịch vụ tiêu biểu: S3, Glue, Redshift, Lake Formation, OpenSearch, Kinesis/MSK.

2. **Chiến lược GenAI trên AWS**


    - Tầm nhìn, xu hướng và lộ trình áp dụng GenAI.
    - Amazon Bedrock: chọn model, RAG, guardrails, tối ưu chi phí/độ trễ.
    - AgentCore & Amazon Nova hỗ trợ tích hợp công cụ và frameworks (CrewAI, LangGraph, LlamaIndex...).

3. **Bảo mật ứng dụng GenAI**


    - Rủi ro OWASP LLM; bảo mật nhiều lớp: hạ tầng → mô hình → ứng dụng.
    - 5 trụ cột: Compliance, Privacy, Controls, Risk Management, Resilience.
    - Công cụ: Bedrock Guardrails, Human-in-the-loop, Observability (OpenTelemetry).

4. **AI Agents – Tăng cường năng suất**


    - Từ assistant đến multi-agent systems, tự động hóa và giảm giám sát.
    - Ứng dụng: CSKH, BI với Amazon Q (QuickSight), tự động hóa quy trình.

5. **Độ tin cậy & tính đúng đắn của GenAI**


    - Giảm hallucination bằng Prompt Engineering, RAG, Fine-tuning.
    - RAG workflow: input → embedding → context → LLM → output.

6. **AI-Driven Development Lifecycle (AI-DLC)**


    - Vòng đời: Inception → Construction → Operation.
    - Tiến hóa: AI-Assisted → AI-Driven → AI-Managed.
    - Triển khai với IaC, test tự động, giám sát & quản trị rủi ro.

7. **Amazon SageMaker – Unified Studio**


    - Nền tảng hợp nhất cho data, analytics & AI.
    - Hỗ trợ Lakehouse, governance, Zero-ETL integration (S3 ↔ Redshift, Aurora, DynamoDB, RDS…).
    - MLOps đầy đủ: pipelines, registry, deployment, monitoring.
    - Tích hợp Bedrock & JumpStart để tăng tốc phát triển ứng dụng GenAI.

### Những Gì Học Được

- **Tư duy thiết kế**

  - Thiết kế hệ thống dữ liệu & AI theo hướng end-to-end, loại bỏ silo.
  - Ứng dụng nguyên tắc self-service và governance ngay từ đầu.

- **Kiến trúc kỹ thuật**

  - Tích hợp dịch vụ AWS (S3, Glue, Redshift, SageMaker, Bedrock…) thành nền tảng thống nhất.
  - Áp dụng Zero-ETL, Lakehouse, MLOps để đảm bảo tính mở rộng, quản trị và vận hành bền vững.
  - Tận dụng AI Agents và GenAI frameworks để tự động hóa quy trình & tăng năng suất.

- **Chiến lược**

  - Xác định lộ trình áp dụng GenAI trong doanh nghiệp, cân bằng giữa tốc độ đổi mới và chi phí.
  - Chú trọng bảo mật nhiều lớp: hạ tầng, mô hình, ứng dụng; kết hợp guardrails & human-in-the-loop.
  - Ưu tiên độ tin cậy và tính đúng đắn của AI qua RAG, prompt engineering, fine-tuning.

- **Tư duy phát triển phần mềm**
  - Tiến hóa từ AI-Assisted → AI-Driven → AI-Managed.
  - AI-DLC (AI-Driven Development Lifecycle) giúp chuẩn hóa quy trình phát triển với AI tham gia ở mọi giai đoạn.

### Ứng Dụng Vào Công Việc

- **Trong dự án**:

  - Thử AI Agent cho đăng ký/đăng nhập và hỗ trợ khách hàng.
  - Dùng validation/guardrails để tích hợp GenAI an toàn.

- **Trong học tập & team project**:

  - Áp dụng AI-DLC để chia việc: AI hỗ trợ tạo code/tài liệu, team review & approve.
  - Biết khi nào dùng Lambda (serverless) và khi nào dùng container (ECS/Fargate).

- **Trong vai trò học việc**:
  - Học cách tiếp cận business-first khi viết tài liệu, thu thập yêu cầu.
  - Nhận ra data foundation là yếu tố cốt lõi để GenAI mang lại giá trị.

### Trải nghiệm trong event

Tham gia workshop **“GenAI-powered App-DB Modernization”** là một trải nghiệm rất bổ ích, giúp tôi có cái nhìn toàn diện về cách hiện đại hóa ứng dụng và cơ sở dữ liệu bằng các phương pháp và công cụ hiện đại. Một số trải nghiệm nổi bật:

#### Học hỏi từ các chuyên gia

- Các chuyên gia AWS chia sẻ xu hướng mới về **GenAI, Data Foundation và Security**.
- Hiểu rõ hơn cách xây dựng **nền tảng dữ liệu thống nhất** để phục vụ AI & Analytics.
- Ấn tượng với tầm nhìn **AI Agents** và tiềm năng nâng cao năng suất trong doanh nghiệp.

#### Trải nghiệm kỹ thuật thực tế

- Học cách thiết kế pipeline dữ liệu end-to-end: ingestion → lưu trữ → xử lý → truy cập → governance.
- Tiếp cận các công cụ như **Amazon Bedrock, AgentCore, SageMaker Unified Studio**.
- Trải nghiệm các giải pháp **giảm hallucination** (Prompt Engineering, RAG).
- Hiểu cách áp dụng **AI-DLC** để phân chia task giữa AI và con người trong quá trình phát triển phần mềm.

#### Ứng dụng công cụ và phương pháp

- Tìm hiểu **Bedrock Guardrails** để đảm bảo tính an toàn khi triển khai GenAI.
- Thấy rõ giá trị của **serverless (AWS Lambda)** và khi nào nên dùng **containerization (ECS/Fargate)**.
- Biết cách tận dụng **Amazon Q** cho BI (QuickSight) và hỗ trợ customer support.

#### Kết nối & trao đổi

- Event là cơ hội để trao đổi với chuyên gia AWS và học hỏi từ case study thực tế.
- Nhận ra tầm quan trọng của **business-first approach** trong mọi quyết định công nghệ.

#### Bài học rút ra

- GenAI không chỉ là công cụ, mà cần **chiến lược & kiến trúc kỹ thuật** đúng đắn để tạo giá trị.
- **Dữ liệu và bảo mật** là nền tảng, không có thì AI khó phát huy hiệu quả.
- **AI Agents và AI-DLC** hứa hẹn thay đổi cách chúng ta thiết kế và vận hành hệ thống.

#### Một số hình ảnh khi tham gia sự kiện
