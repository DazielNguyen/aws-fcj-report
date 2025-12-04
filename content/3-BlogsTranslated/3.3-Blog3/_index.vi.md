---
title: "Blog 3"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# **Tóm tắt hành tuần về AWS: AWS Transform, Amazon Neptune, và nhiều hơn nữa (Ngày 08 tháng 09 năm 2025\)**

bởi Esra Kayabali | ngày 08 tháng 09 năm 2025 | trong [Amazon Bedrock](https://aws.amazon.com/vi/blogs/aws/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/), [Amazon Elastic Container Service](https://aws.amazon.com/vi/blogs/aws/category/compute/amazon-elastic-container-service/), [Amazon Neptune](https://aws.amazon.com/vi/blogs/aws/category/database/amazon-neptune/), [Announcements](https://aws.amazon.com/vi/blogs/aws/category/post-types/announcements/), [AWS Transform](https://aws.amazon.com/vi/blogs/aws/category/artificial-intelligence/generative-ai/aws-transform/), [AWS User Notifications](https://aws.amazon.com/vi/blogs/aws/category/management-and-governance/aws-user-notifications/), [Launch](https://aws.amazon.com/vi/blogs/aws/category/news/launch/), [News](https://aws.amazon.com/vi/blogs/aws/category/news/) | [Permalink](https://aws.amazon.com/vi/blogs/aws/aws-weekly-roundup-aws-transform-amazon-neptune-and-more-september-8-2025/) | Comments | Share  
 

Mùa hè đã khép lại ở Utrecht, nơi tôi sống tại Hà Lan. Trong hai tuần nữa, tôi sẽ tham dự [AWS Community Day 2025](https://awscommunityday.nl/2025/), tổ chức tại Kinepolis Jaarbeurs Utrecht vào ngày 24 tháng 09\. Sự kiện kéo dài một ngày sẽ quy tụ hơn 500 chuyên gia cloud trên khắp Hà Lan, với 25 phiên breakout trải rộng 5 track kỹ thuật. Ngày hội sẽ mở đầu bằng các virtual keynotes lúc 9:00 sáng, tiếp theo là các phiên song song tập trung vào các triển khai thực tiễn của serverless architectures và container optimization strategies, mang lại giá trị cho mọi cấp độ kinh nghiệm.

AWS Community Day Netherlands 2024 năm ngoái đã quy tụ một cộng đồng đa dạng gồm các practitioner, diễn giả và người yêu thích AWS, cùng nhau tạo nên một hội nghị do cộng đồng dẫn dắt với giá trị chia sẻ tri thức cao. Nếu bạn dự định tham dự, cứ thoải mái tìm gặp tôi để trao đổi về các dịch vụ **AWS** hoặc chia sẻ kinh nghiệm triển khai cloud của bạn\!

![0-AWSNEWS-2266](/images/3-BlogsTranslated/3.1-Blog3/0-AWSNEWS-2266.png)

## **Các lần ra mắt tuần trước**

Hãy cùng điểm qua các thông báo mới của tuần trước.

[Đánh giá của AWS Transform hiện bao gồm lưu trữ tách rời](https://aws.amazon.com/vi/about-aws/whats-new/2025/09/aws-transform-assessments-detached-storage/) – AWS Transform đã mở rộng khả năng assessment để phân tích on-premises cơ sở hạ tầng lưu trữ tách biệt, giúp khách hàng xác định migration total cost of ownership (TCO). Assessment hiện đánh giá Storage Area Network (SAN), Network Attached Storage (NAS), file servers, object storage, và virtual environments, đồng thời đề xuất dịch vụ đích trên AWS phù hợp như Amazon S3, Amazon EBS, và Amazon FSx. Công cụ cung cấp so sánh TCO toàn diện giữa môi trường hiện tại và AWS, kèm khuyến nghị tối ưu hiệu năng và chi phí. Vì storage có thể chiếm tới 45% tổng cơ hội migration, nâng cấp này giúp khách hàng hình dung các lựa chọn migration trên AWS. AWS Transform assessment hiện khả dụng tại US East (N. Virginia) và Europe (Frankfurt).

[Amazon Bedrock hiện hỗ trợ tính năng suy luận liên khu vực toàn cầu cho Anthropic Claude Sonnet 4](https://aws.amazon.com/vi/about-aws/whats-new/2025/09/amazon-bedrock-global-cross-region-inference-anthropic-claude-sonnet-4/) – Model Anthropic Claude Sonnet 4 trong Amazon Bedrock nay hỗ trợ Global cross-Region inference, cho phép các inference requests được định tuyến đến bất kỳ commercial AWS Region được hỗ trợ nào để xử lý. Nâng cấp này tối ưu tài nguyên sẵn có và tăng model throughput bằng cách phân phối lưu lượng qua nhiều Region. Trước đây, bạn có thể chọn cross-Region inference profiles gắn với từng khu vực (US, EU, APAC). Global cross-Region inference profile mới mang lại linh hoạt bổ sung cho các generative AI không cần ràng buộc địa lý, giúp xử lý traffic bursts ngoài kế hoạch và tăng throughput. Hướng dẫn triển khai chi tiết có tại [Amazon Bedrock documentation](https://docs.aws.amazon.com/bedrock/latest/userguide/cross-region-inference.html).

[Cơ sở dữ liệu Amazon Neptune hiện đã hỗ trợ Điểm cuối công cộng, giúp truy cập phát triển trở nên đơn giản hơn](https://aws.amazon.com/vi/about-aws/whats-new/2025/09/aws-neptune-database-public-endpoints/) – Amazon Neptune nay hỗ trợ Public Endpoints, cho phép kết nối trực tiếp đến Neptune databases từ bên ngoài VPC mà không cần cấu hình mạng phức tạp. Tính năng này giúp nhà phát triển truy cập graph databases an toàn từ máy phát triển cá nhân mà không cần VPN hoặc bastion hosts, đồng thời vẫn đảm bảo bảo mật qua IAM authentication, VPC security groups, và encryption in transit. Bạn có thể bật Public Endpoints cho các Neptune clusters chạy engine version 1.4.6 trở lên qua AWS Management Console, AWS CLI, hoặc AWS SDK. Tính năng này không tính phí bổ sung ngoài Neptune pricing tiêu chuẩn, và khả dụng ở mọi AWS Region nơi Neptune Database được cung cấp. Chi tiết triển khai có trong [Amazon Neptune documentation](https://docs.aws.amazon.com/neptune/latest/userguide/intro.html).

[ECS Exec hiện đã được hỗ trợ trên Bảng điều khiển quản lý AWS](https://aws.amazon.com/vi/about-aws/whats-new/2025/09/ecs-exec-aws-management-console/) – Amazon ECS nay hỗ trợ ECS Exec trực tiếp trong AWS Management Console, cho phép secure, interactive shell access vào container đang chạy mà không cần mở inbound ports hay quản lý SSH keys. Trước đây chỉ có qua API/CLI/SDK, tính năng này giúp troubleshooting thuận tiện khi truy cập container ngay trong console. Bạn có thể bật ECS Exec khi tạo/cập nhật services và standalone tasks, rồi kết nối tới container bằng cách chọn “Connect” trên trang chi tiết task, mở phiên tương tác qua CloudShell. Console cũng hiển thị AWS CLI command tương ứng để dùng trên máy cục bộ. Tính năng khả dụng ở tất cả AWS commercial Regions và được ghi trong [ECS developer guide](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ecs-exec.html).

[Cấu hình thông báo tổ chức cho thông báo người dùng AWS hiện đã có sẵn rộng rãi](https://aws.amazon.com/vi/about-aws/whats-new/2025/09/general-availability-organizational-notification-configurations-aws-user-notifications/) – AWS User Notifications nay hỗ trợ Organizational Notification Configurations, giúp người dùng AWS Organizations cấu hình và quan sát notifications tập trung trên toàn tổ chức. Management accounts hoặc delegated administrators có thể cấu hình thông báo cho các organizational units cụ thể hoặc cho toàn bộ accounts trong tổ chức. Dịch vụ hỗ trợ cấu hình notifications cho bất kỳ Amazon EventBridge event được hỗ trợ, như console sign-ins without MFA, với thông báo hiển thị trong Console Notifications Center của admin và AWS Console Mobile Application. User Notifications hỗ trợ tối đa 5 delegated administrators và khả dụng tại mọi AWS Region nơi dịch vụ được cung cấp. Chi tiết triển khai có tại [AWS User Notifications user guide](https://docs.aws.amazon.com/notifications/latest/userguide/managing-org-notifications.html).

[Để xem danh sách đầy đủ các thông báo của AWS, hãy theo dõi trang What’s New at AWS.](https://aws.amazon.com/vi/new/)

## **Sự kiện AWS sắp tới**

Đánh dấu lịch và đăng ký các sự kiện AWS sắp tới.

[AWS Summits](https://aws.amazon.com/vi/events/summits/) – Sự kiện trực tuyến và trực tiếp miễn phí kết nối cộng đồng cloud computing để giao lưu, cộng tác và học hỏi về AWS. Đăng ký tại thành phố gần bạn: [Zurich](https://aws.amazon.com/vi/events/summits/zurich/) (Ngày 11 tháng 09), [Los Angeles](https://aws.amazon.com/vi/events/summits/los-angeles/) (Ngày 17 tháng 09), và [Bogotá](https://aws.amazon.com/es/events/summits/bogota/) (Ngày 09 tháng 10).

[AWS re:Invent 2025](https://reinvent.awsevents.com/?trk=ba8b32c9-8088-419f-9258-82e9375ad130&sc_channel=ell) – Hẹn gặp tại Las Vegas từ December 1–5, nơi những người tiên phong cloud từ khắp thế giới tụ hội để cập nhật đổi mới AWS, học hỏi ngang hàng, thảo luận chuyên sâu do chuyên gia dẫn dắt và mở rộng kết nối. Đừng quên khám phá [event catalog](https://registration.awsevents.com/flow/awsevents/reinvent2025/eventcatalog/page/eventcatalog?trk=ba8b32c9-8088-419f-9258-82e9375ad130).

[AWS Community Days](https://aws.amazon.com/vi/events/community-day/?trk=e61dee65-4ce8-4738-84db-75305c9cd4fe&sc_channel=el&?trk=ba8b32c9-8088-419f-9258-82e9375ad130&sc_channel=el) – Chuỗi hội nghị do cộng đồng dẫn dắt, có thảo luận kỹ thuật, workshop, và hands-on labs dẫn dắt bởi các người dùng AWS chuyên gia và lãnh đạo ngành chia sẻ: [Baltic](https://awsbaltic.eu/) (Ngày 10 tháng 09), [Aotearoa](https://aws-community-day.nz/inperson.html) (Ngày 18 tháng 09), [Nam Phi](https://www.awscommunityday.co.za/) (Ngày 20 tháng 09), [Bolivia](https://www.facebook.com/awscommunitydaybolivia/) (Ngày 20 tháng 09), [Bồ Đào Nha](https://awscommunityday.pt/) (Ngày 27 tháng 09).

Duyệt tất cả [các sự kiện trực tiếp và trực tuyến do AWS tổ chức tại đây.](https://aws.amazon.com/vi/events/explore-aws-events/)

Vậy là hết cho tuần này. Hẹn gặp lại bạn vào Thứ 2 tuần tới trong Tóm tắt hàng tuần\!

[— Esra](https://www.linkedin.com/in/esrakayabali/)

*Bài viết này là một phần của series [Tóm tắt hàng tuần](https://aws.amazon.com/vi/blogs/aws/tag/week-in-review/). Quay lại mỗi tuần để xem nhanh những tin tức và thông báo thú vị từ AWS\!*

TAGS: [Week in Review](https://aws.amazon.com/vi/blogs/aws/tag/week-in-review/)

 


|<img src="/images/3-BlogsTranslated/3.1-Blog3/esrakayabali11-400x400-1.jpg" alt="Vijay_Menon" width="350" style="float: left; margin-right: 15px;"/> |  **Esra Kayabali**  <br/> Esra Kayabali là Senior Solutions Architect tại AWS, chuyên về analytics gồm data warehousing, data lakes, big data analytics, batch và real-time data streaming, cùng data integration. Cô có hơn mười năm kinh nghiệm software development và solution architecture. Cô đam mê học hỏi cộng tác, chia sẻ tri thức và dẫn dắt cộng đồng trên hành trình công nghệ cloud.                |
| ---------------------------------------- | ------------------------------------------------------------------------------------------ |