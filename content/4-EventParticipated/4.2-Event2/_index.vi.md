---
title: "Event 2"
date: "2025-10-16"
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

# Bài thu hoạch “WORKSHOP KHOA HỌC DỮ LIỆU TRÊN AWS”

### Mục Đích Của Sự Kiện

- Chia sẻ best practices trong thiết kế ứng dụng hiện đại
- Giới thiệu phương pháp DDD và event-driven architecture
- Hướng dẫn lựa chọn compute services phù hợp
- Giới thiệu công cụ AI hỗ trợ development lifecycle

### Danh Sách Diễn Giả

- **Van Hoang Kha** - Cloud Solutions Architec AWS User Group Leader
- **Bach Doan Vuong** - Cloud Develops Engineer AWS Community Builder

### Nội Dung Nổi Bật
- Tổng quan quản lý dịch vụ AI với từng trường hợp. 
- Feature Engineering
- Train, Tune, Deploy 
- Bring your own models. 
#### Giới thiệu & Tầm quan trọng của Cloud trong Data Science
- Các dịch vụ phổ biến cảu AWS có thể hỗ trợ được sinh viên trong quá trình train model như SageMarker
- 
- 
#### Amazon Comprehend
- Chuyên tóm tắt phân loại dữ liệu, và giải pháp cho bài toàn xử lý ngôn ngữ tự nhiên hỗ trợ được nhiều ngôn nhữ khác nhau. 
- Các trường hợp sử dụng thực tế của Amazon Comprehend.   
  + Xử lý tài liệu thông minh
  + Xử lý mail hàng loạt -> Hướng trả lời cho người dùng tích cực hay tieuw cực 
  + Phân tích cảm xúc khách hàng
  + Phân loại và gắn cho tag các type dữ liệu khác nhau. 
  + Phân tích tâm lý khách hàng
  + Phân tích cho tổng đài tư vấn viên -> Trung tâm liên lạc
  + Xác thực thông tin các nhân. 

#### Amazon Translate - Neurak machine translation service.
- Tương tự google dịch
- Có thể tích hợp các website làm đa ngôn ngữ 
- Dễ tích hợp vào ứng dụng 
- Độ chính xác cao theo từng ngữ cảnh khác nhau

#### Amazon Texttrack
- Triết xuất 
#### Tổng quan về Data Science Pipeline trên AWS (S3, Glue, SageMaker).
-
-
-

#### Demo 1: Xử lý và làm sạch dữ liệu từ dataset IMDb với AWS Glue.

- 
-
-

#### Thảo luận chuyên sâu về chi phí, hiệu năng (Cloud vs. On-premise).
-
-
-

#### Hướng dẫn dự án nhỏ sau workshop để củng cố kiến thức.





### Những Gì Học Được

#### Tư Duy Thiết Kế

- **Business-first approach**: Luôn bắt đầu từ business domain, không phải technology
- **Ubiquitous language**: Importance của common vocabulary giữa business và tech teams
- **Bounded contexts**: Cách identify và manage complexity trong large systems

#### Kiến Trúc Kỹ Thuật

- **Event storming technique**: Phương pháp thực tế để mô hình hóa quy trình kinh doanh
- Sử dụng **Event-driven communication** thay vì synchronous calls
- **Integration patterns**: Hiểu khi nào dùng sync, async, pub/sub, streaming
- **Compute spectrum**: Criteria chọn từ VM → containers → serverless

#### Chiến Lược Hiện Đại Hóa

- **Phased approach**: Không rush, phải có roadmap rõ ràng
- **7Rs framework**: Nhiều con đường khác nhau tùy thuộc vào đặc điểm của mỗi ứng dụng
- **ROI measurement**: Cost reduction + business agility

### Ứng Dụng Vào Công Việc

- **Áp dụng DDD** cho project hiện tại: Event storming sessions với business team
- **Refactor microservices**: Sử dụng bounded contexts để identify service boundaries
- **Implement event-driven patterns**: Thay thế một số sync calls bằng async messaging
- **Serverless adoption**: Pilot AWS Lambda cho một số use cases phù hợp
- **Try Amazon Q Developer**: Integrate vào development workflow để boost productivity

### Trải nghiệm trong event

Tham gia workshop **“GenAI-powered App-DB Modernization”** là một trải nghiệm rất bổ ích, giúp tôi có cái nhìn toàn diện về cách hiện đại hóa ứng dụng và cơ sở dữ liệu bằng các phương pháp và công cụ hiện đại. Một số trải nghiệm nổi bật:

#### Học hỏi từ các diễn giả có chuyên môn cao

- Các diễn giả đến từ AWS và các tổ chức công nghệ lớn đã chia sẻ **best practices** trong thiết kế ứng dụng hiện đại.
- Qua các case study thực tế, tôi hiểu rõ hơn cách áp dụng **Domain-Driven Design (DDD)** và **Event-Driven Architecture** vào các project lớn.

#### Trải nghiệm kỹ thuật thực tế

- Tham gia các phiên trình bày về **event storming** giúp tôi hình dung cách **mô hình hóa quy trình kinh doanh** thành các domain events.
- Học cách **phân tách microservices** và xác định **bounded contexts** để quản lý sự phức tạp của hệ thống lớn.
- Hiểu rõ trade-offs giữa **synchronous và asynchronous communication** cũng như các pattern tích hợp như **pub/sub, point-to-point, streaming**.

#### Ứng dụng công cụ hiện đại

- Trực tiếp tìm hiểu về **Amazon Q Developer**, công cụ AI hỗ trợ SDLC từ lập kế hoạch đến maintenance.
- Học cách **tự động hóa code transformation** và pilot serverless với **AWS Lambda**, từ đó nâng cao năng suất phát triển.

#### Kết nối và trao đổi

- Workshop tạo cơ hội trao đổi trực tiếp với các chuyên gia, đồng nghiệp và team business, giúp **nâng cao ngôn ngữ chung (ubiquitous language)** giữa business và tech.
- Qua các ví dụ thực tế, tôi nhận ra tầm quan trọng của **business-first approach**, luôn bắt đầu từ nhu cầu kinh doanh thay vì chỉ tập trung vào công nghệ.

#### Bài học rút ra

- Việc áp dụng DDD và event-driven patterns giúp giảm **coupling**, tăng **scalability** và **resilience** cho hệ thống.
- Chiến lược hiện đại hóa cần **phased approach** và đo lường **ROI**, không nên vội vàng chuyển đổi toàn bộ hệ thống.
- Các công cụ AI như Amazon Q Developer có thể **boost productivity** nếu được tích hợp vào workflow phát triển hiện tại.

#### Một số hình ảnh khi tham gia sự kiện

- Thêm các hình ảnh của các bạn tại đây
  > Tổng thể, sự kiện không chỉ cung cấp kiến thức kỹ thuật mà còn giúp tôi thay đổi cách tư duy về thiết kế ứng dụng, hiện đại hóa hệ thống và phối hợp hiệu quả hơn giữa các team.
