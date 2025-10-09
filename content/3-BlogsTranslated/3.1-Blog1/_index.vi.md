---
title: "Xây dựng ứng dụng multi-Region Serverless có khả năng phục hồi trên AWS"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

bởi Vamsi Vikash Ankam | vào ngày 08 tháng 09 năm 2025 | trong [Advanced (300)](https://aws.amazon.com/blogs/compute/category/learning-levels/advanced-300/), [Resilience](https://aws.amazon.com/blogs/compute/category/resilience/), [Serverless](https://aws.amazon.com/blogs/compute/category/serverless/), [Technical How-to](https://aws.amazon.com/blogs/compute/category/post-types/technical-how-to/) | [Permalink](https://aws.amazon.com/blogs/compute/building-resilient-multi-region-serverless-applications-on-aws/) | Share

Các ứng dụng mission-critical đòi hỏi tính sẵn sàng cao và khả năng chống chịu trước các gián đoạn tiềm ẩn. Trong trò chơi trực tuyến, hàng triệu người chơi kết nối đồng thời, khiến các thách thức về tính sẵn sàng trở nên rõ rệt. Khi nền tảng game gặp sự cố, người chơi mất tiến độ, giải đấu bị gián đoạn, và danh tiếng thương hiệu bị ảnh hưởng. Môi trường truyền thống thường cấp phát dư thừa tài nguyên tính toán để đối phó các thách thức này, dẫn đến thiết lập phức tạp cùng chi phí hạ tầng và vận hành cao. Hạ tầng Amazon Web Services [(AWS) serverless](https://aws.amazon.com/serverless/) hiện đại mang lại một cách tiếp cận hiệu quả hơn. Bài viết này trình bày các thực tiễn kiến trúc tốt nhất để xây dựng ứng dụng serverless có khả năng phục hồi, minh họa qua việc triển khai cơ chế ủy quyền multi-[Region](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/) serverless.

## **Tổng quan**

Nếu chỉ nhận ra tầm quan trọng của tính sẵn sàng sau khi đã trải qua thảm họa thì đã quá muộn. Ứng dụng có thể thất bại vì nhiều lý do như sự cố hạ tầng, lỗi mã nguồn, lỗi cấu hình, đột biến lưu lượng bất ngờ, hoặc gián đoạn dịch vụ ở cấp độ regional. Các dịch vụ nghiệp vụ trọng yếu như hệ thống xác thực, bộ xử lý thanh toán, và tính năng game thời gian thực đòi hỏi tính sẵn sàng cao. Để giảm thiểu tác động đến trải nghiệm người dùng và doanh thu kinh doanh, hãy thiết lập [bounded recovery times](https://docs.aws.amazon.com/prescriptive-guidance/latest/aws-multi-region-fundamentals/fundamental-1.html)  cho các dịch vụ trọng yếu trong thời gian xảy ra sự cố.

Các kiến trúc AWS serverless vốn dĩ cung cấp tính sẵn sàng cao thông qua triển khai multi-Availability Zone (AZ) và khả năng mở rộng tích hợp. Các dịch vụ này giảm thiểu việc quản trị hạ tầng đồng thời vận hành theo mô hình định giá pay-for-value ở cấp độ Regional. Mô hình AWS serverless pay-for-value cho phép triển khai cost-effective multi-Region, khiến đây trở thành lựa chọn lý tưởng để xây dựng kiến trúc có khả năng phục hồi.

![][image1]

*Hình 1\. Biểu đồ cho thấy các nguyên nhân gây lỗi, tác động của chúng và tần suất xảy ra*

Biểu đồ trước đó ánh xạ các failures—from lỗi vận hành thường gặp cho tới những sự kiện thảm họa hiếm gặp. Nó hướng dẫn các tổ chức ưu tiên các chiến lược khôi phục multi-Region dựa trên xác suất xảy ra và tác động tiềm tàng đối với doanh nghiệp.

## **Các quyết định Regional**

Để xác định cách tiếp cận multi-Region phù hợp, hãy đánh giá cẩn trọng các yếu tố sau:

1. Đánh giá liệu các yêu cầu [Recovery Time Objective (RTO) and Recovery Point Objective (RPO)](https://aws.amazon.com/blogs/mt/establishing-rpo-and-rto-targets-for-cloud-applications/) của bạn có thể được đáp ứng trong một Region đơn lẻ, hay cần một kiến trúc multi-Region là cần thiết để đạt được các mục tiêu khôi phục của bạn.  
2. Liệu các lợi ích kinh doanh của dự phòng multi-Region có lớn hơn chi phí vận hành của việc sao chép dữ liệu, đồng bộ hóa, và chi phí cùng độ phức tạp triển khai gia tăng hay không?  
3. Đánh giá liệu các luật về chủ quyền dữ liệu, yêu cầu tuân thủ, hoặc hạn chế địa lý có ngăn việc sao chép dữ liệu giữa các AWS Regions cụ thể hay không.  
4. Đảm bảo rằng các Regions được chọn trong một giải pháp "multi-Region" có khả năng tương thích dịch vụ, giới hạn quota, và mức giá phù hợp với nhu cầu của bạn.

Sau khi đánh giá các yêu cầu này, nếu tổ chức xác định cần khối lượng công việc multi-Region, thì họ phải chọn giữa hai mẫu kiến trúc: triển khai Active-Passive hoặc Active-Active. Mỗi mẫu đưa ra lợi ích và đánh đổi riêng về khả năng phục hồi, chi phí, và độ phức tạp vận hành.

## **Mẫu triển khai multi-Region**

Các phần sau đây phác thảo các mẫu triển khai multi-Region khác nhau: Active-Passive, và Active-Active.

### **Active-Passive**

Trong mẫu này, một AWS Region đóng vai trò “Active” Region, xử lý toàn bộ lưu lượng sản xuất, trong khi các Region(s) khác ở trạng thái “Passive”, như thể hiện trong hình sau. Passive Region(s) sao chép dữ liệu và cấu hình từ Active Region mà không phục vụ yêu cầu, và sẵn sàng xử lý khi xảy ra gián đoạn ở “Active” Region. Tùy theo mức độ quan trọng của ứng dụng, passive Regions triển khai mức độ sẵn sàng hạ tầng khác nhau: hạ tầng triển khai đầy đủ (Hot Standby), triển khai một phần (Warm Standby), hoặc hạ tầng cốt lõi tối thiểu (Pilot Light).

Kiến trúc Active-Passive truyền thống cần đầu tư đáng kể cho hạ tầng nhàn rỗi: load balancer, auto-scaling group, running compute resources, và monitoring systems. Các tổ chức có thể sử dụng các ứng dụng AWS serverless với mô hình định giá pay-for-value để chủ yếu trả chi phí sao chép dữ liệu, không phải tài nguyên tính toán nhàn rỗi. AWS quản lý hạ tầng bên dưới, loại bỏ phần lớn chi phí vận hành.

Hạn ngạch dịch vụ, giới hạn API, và thiết lập concurrency phải tương ứng giữa các AWS Regions để để cung cấp khả năng failover liền mạch. [AWS Lambda](https://aws.amazon.com/lambda/) cung cấp [provisioned concurrency](https://docs.aws.amazon.com/lambda/latest/dg/provisioned-concurrency.html) để giữ functions warm và phản hồi nhanh, đặc biệt hữu ích cho các Regions thứ cấp trong quá trình failover. Nó giúp giảm cold start bằng cách duy trì môi trường warm execution, do đó hệ thống có thể xử lý đột biến lưu lượng với ít cold start hơn. Lưu ý provisioned concurrency phát sinh [costs](https://aws.amazon.com/lambda/pricing/) tính toán bất kể mức sử dụng. Cân nhắc triển khai auto-scaling cho provisioned concurrency dựa trên các mẫu lưu lượng để tối ưu chi phí trong các giai đoạn nhàn rỗi.

Mẫu này phù hợp với các tổ chức đang tìm kiếm giải pháp cost-effective disaster recovery (DR), bởi vì chi phí AWS serverless chỉ áp dụng khi tài nguyên được sử dụng tích cực tại Region thứ cấp. Các dịch vụ quản lý như [Amazon DynamoDB Global Tables](https://aws.amazon.com/dynamodb/) và [Amazon Aurora Global Database](https://aws.amazon.com/rds/aurora/) xử lý sao chép dữ liệu, giúp đơn giản hóa triển khai. Cơ chế ủy quyền serverless được trình bày ở phần sau minh họa mẫu này trong thực tế.

![][image2]

*Hình 2: Mẫu Active-Passive với các đường chấm chỉ ra các standby Regions, trong khi mẫu Active-Active phục vụ lưu lượng đồng thời*

### **Active-Active**

Trong mẫu này, multiple Regions phục vụ lưu lượng đồng thời, phân phối tải và cung cấp khả năng failover nhanh chóng. Kiến trúc Active-Active là [expensive](https://aws.amazon.com/blogs/architecture/understand-resiliency-patterns-and-trade-offs-to-architect-efficiently-in-the-cloud/) và được thiết kế cho mức sẵn sàng cao nhất. Tuy nhiên, chúng không mặc định cung cấp DR cho mọi dạng lỗi tiềm ẩn. Cách tiếp cận này phù hợp với các ứng dụng cần định tuyến theo vị trí địa lý, hoặc yêu cầu sẵn sàng cao nhất.

Triển khai Active-Active đòi hỏi kỹ thuật nghiêm ngặt để xử lý đồng bộ dữ liệu và giải quyết xung đột. Mỗi Region phải được sized để gánh toàn bộ tải ứng dụng nếu một Region khác bị suy giảm dịch vụ. Người dùng đang hoạt động được phân bổ trên các AWS Regions, vì vậy gián đoạn ở một Region sẽ chuyển hướng toàn bộ lưu lượng sang các Regions còn lại, điều này đòi hỏi họ phải xử lý load kết hợp. Để cải thiện khả năng phục hồi của ứng dụng, hãy triển khai [retry mechanisms](https://aws.amazon.com/builders-library/timeouts-retries-and-backoff-with-jitter/), [circuit breaker](https://docs.aws.amazon.com/prescriptive-guidance/latest/cloud-design-patterns/circuit-breaker.html), và chiến lược fallback. Lập kế hoạch cho [static stability](https://docs.aws.amazon.com/whitepapers/latest/aws-fault-isolation-boundaries/static-stability.html) bằng cách pre-provisioning capacity và áp dụng bộ nhớ đệm client-side. Các dịch vụ như [Amazon Route 53](https://aws.amazon.com/route53/) với định tuyến latency-based và [Amazon DynamoDB](https://aws.amazon.com/dynamodb/) Global Tables với [strong consistency](https://aws.amazon.com/blogs/aws/build-the-highest-resilience-apps-with-multi-region-strong-consistency-in-amazon-dynamodb-global-tables/) cung cấp nền tảng nhưng cần kiểm thử kỹ dưới nhiều kịch bản lỗi khác nhau. Bài viết này không đề cập đến triển khai Active-Active.

## **Multi-Region serverless authorizer**

Để minh họa kịch bản Active-Passive, chúng ta xây dựng một ứng dụng mẫu cho thấy cách xây dựng multi-Region serverless authorizer sử dụng [Amazon API Gateway](https://aws.amazon.com/api-gateway/), [Lambda](https://aws.amazon.com/pm/lambda/?refid=1992d44e-5bf5-47d8-8711-4ea10542b61b) functions và Amazon Route53. Các nền tảng game và giải trí hiện đại lưu trữ các dịch vụ trọng yếu như ghép cặp người chơi, phát trực tiếp, và phân tích thể thao thời gian thực. Những dịch vụ này phụ thuộc vào hệ thống ủy quyền vững chắc—khi ủy quyền thất bại, người chơi không thể tham gia trận đấu, người xem mất quyền truy cập luồng phát, và sự kiện trực tiếp không khả dụng. Bài viết này trình bày cách xây dựng fault-tolerant, multi-Region serverless authorizer trong khi vẫn duy trì chi phí thấp hơn so với các môi trường truyền thống.

Kiến trúc Serverless multi-Region thường bao gồm các lớp Định tuyến, Tính toán, và Dữ liệu. Khi triển khai multi-Region deployments, việc sao chép dữ liệu giữa các AWS Regions là điều thiết yếu, bất kể các dịch vụ tính toán được sử dụng. Lớp tính toán phải ưu tiên tính bất biến để đảm bảo xử lý sự kiện an toàn trên các AWS Regions.

Sử dụng [Powertools for Lambda](https://docs.aws.amazon.com/powertools/python/latest/utilities/idempotency/) để xử lý tính bất biến hiệu quả, hoặc triển khai các giải pháp tùy chỉnh bằng cách sử dụng unique event IDs với DynamoDB như một kho lưu trữ có tính bất biến. Dù bài viết tập trung vào triển khai dịch vụ authorizer, mẫu này có thể áp dụng để xây dựng các multi-Region microservice cho nhiều chức năng trọng yếu, như quản lý phiên chơi, điều phối phân phối nội dung, quản lý tùy thích người dùng, và dịch vụ hồ sơ.

## **Tổng quan demo**

Để minh họa vận hành multi-Region serverless authorizer, chúng ta có thể xem xét quy trình làm việc: 

1. Ứng dụng frontend xác thực với Identity Provider để lấy token xác thực.

2. Token xác thực được gửi đến một multi-Region DNS endpoint có khả năng phục hồi, được lưu trữ trên Route 53 trong bản demo này.

3. Route 53 định tuyến yêu cầu kèm token đến API Gateway ở primary Region.

4. Route 53 giám sát sức khỏe ứng dụng bằng một hàm Lambda giả lập trong demo này. Trong môi trường sản xuất, hãy triển khai các kiểm tra sức khỏe sâu để giám sát toàn bộ ngăn xếp dịch vụ.

5. Khi ủy quyền thành công, ứng dụng nhận phản hồi. Nếu Route 53 phát hiện suy giảm ở primary Region, nó kích hoạt cảnh báo [Amazon CloudWatch](https://aws.amazon.com/vi/cloudwatch/), mà chủ sở hữu ứng dụng có thể dùng để đánh giá và phê duyệt chuyển hướng lưu lượng sang Region thứ cấp.

6. Lưu lượng mới sẽ được định tuyến đến API Gateway ở Region thứ cấp sau khi được phê duyệt failover thủ công.

7. Các kiểm tra sức khỏe của Route 53 tiếp tục giám sát sức khỏe primary Region và khôi phục định tuyến lưu lượng khi Region này phục hồi.

![][image3]

*Hình 3: Quy trình làm việc Multi-Region serverless authorizer với Route53 failover giữa các primary Region và thứ cấp*

Hình trên cho thấy kiến trúc minh họa cả khả năng failover và fallback thông qua cảnh báo CloudWatch và quy trình phê duyệt thủ công. Cách tiếp cận này phù hợp với thực tiễn tốt cho ứng dụng trọng yếu, nơi việc failover tự động không được khuyến nghị dù về mặt kỹ thuật là khả thi. Nhóm có thể dùng cách này để đánh giá mức sẵn sàng kỹ thuật, tác động kinh doanh, và đưa ra quyết định phù hợp về thời điểm và tác động tiềm tàng đến doanh thu.

[Bản demo](https://github.com/aws-samples/AWS_Serverless_Resiliency_Samples/tree/main/multi-region-authorizer) triển khai multi-Region serverless authorizer đóng vai trò là kiến trúc tham chiếu. Các triển khai thực tế cần đánh giá kỹ chiến lược failover dựa trên mức độ quan trọng của doanh nghiệp và các yêu cầu vận hành.

**Testing các kịch bản multi-Region**

Ứng dụng demo lưu trữ frontend trên [Amazon Elastic Container Service (Amazon ECS)](https://aws.amazon.com/vi/ecs/). Cấu hình health check của Route 53 trong [GitHub này](https://github.com/aws-samples/AWS_Serverless_Resiliency_Samples/blob/main/multi-region-authorizer/deployment/domain-deployments.yaml) xác định các tham số failover chính:

1. FailureThreshold: Chỉ định số lần kiểm tra tình trạng liên tiếp không thành công trước khi Route 53 đánh dấu endpoint là unhealthy.  
2. RequestInterval:  
   1. Standard: Chu kỳ 30 giây ($0.50 mỗi health check/tháng)  
   2. Fast: Chu kỳ 10 giây ($1.00 mỗi health check/tháng)

\`\`\`  
Route53HealthCheck:  
    Type: AWS::Route53::HealthCheck  
    Properties:  
      HealthCheckConfig:  
        FailureThreshold: 2  
        FullyQualifiedDomainName: \!Ref DomainName  
        Port: 443  
        RequestInterval: 10  
        ResourcePath: /failure  
        Type: HTTPS  
      HealthCheckTags:  
        \- Key: Environment  
          Value: Production  
        \- Key: Name  
          Value: multi-authorizer-health-check  
\`\`\`

Chu kỳ nhanh giúp phát hiện lỗi nhanh hơn. Tuy nhiên, nó làm tăng chi phí health check thông qua nhiều hoạt động ghi log, xử lý yêu cầu, và tài nguyên tính toán backend. Các vấn đề tạm thời như trục trặc mạng, lỗi thoáng qua, hoặc độ trễ từ bên thứ ba có thể tự khắc phục trong vài phút. Việc triển khai xử lý retry hiệu quả sẽ giới thiệu các phức tạp không cần thiết và tiềm ẩn inconsistencies dữ liệu. Hãy chọn chu kỳ phù hợp dựa trên SLAs kinh doanh và cân nhắc chi phí.

Để kiểm thử kịch bản failover, kiến trúc sử dụng một hàm Lambda giả làm endpoint health check. Chúng tôi kích hoạt cảnh báo CloudWatch bằng cách mô phỏng mã trạng thái phản hồi 500 từ hàm này, điều này sẽ thúc đẩy quá trình quyết định failover thủ công, như minh họa ở hình sau.

![][image4]

*Hình 4\. Ảnh chụp màn hình console hiển thị multi-authorizer-health-check với trạng thái “Unhealthy”*

Bộ nhớ đệm DNS xảy ra ở nhiều tầng (trình duyệt, hệ điều hành, ISP, và VPN). Để quan sát hành vi failover ngay lập tức, hãy xóa bộ nhớ đệm trình phân giải DNS ở từng tầng

Để kiểm thử khả năng phục hồi toàn diện hơn, cân nhắc áp dụng thực hành chaos engineering. Bạn có thể dùng [chaos-lambda-extension](https://github.com/aws-cli-tools/chaos-lambda-extension) để đưa độ trễ hoặc sửa đổi phản hồi hàm theo cách có kiểm soát. [AWS Fault Injection Service](https://aws.amazon.com/vi/fis/) (AWS FIS), một dịch vụ được quản lý toàn phần, cho phép thực hiện các thí nghiệm fault inject để cải thiện khả năng phục hồi, hiệu năng và khả năng quan sát. Kết hợp các công cụ này giúp xác thực kiến trúc multi-Region dưới nhiều điều kiện lỗi có kiểm soát.

## **Khả năng quan sát trong triển khai multi-Region**

## Triển khai kiến trúc multi-Region chỉ là bước đầu. Khả năng quan sát Cross-Region đòi hỏi theo dõi tài nguyên của Region A từ Region B và ngược lại. CloudWatch cho phép điều này thông qua giám sát [cross-account and cross-Region](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Cross-Account-Cross-Region.html), cung cấp logs và metrics hợp nhất trong một dashboard. Triển khai kiểm tra tình trạng hoạt động chuyên sâu để xác minh chức năng quan trọng của ứng dụng trên các AWS Regions.

Mặc dù các dịch vụ AWS serverless được phân phối, việc xác định lỗi chính xác đòi hỏi kết hợp nhiều điểm dữ liệu. Cảnh báo CloudWatch [composite](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Create_Composite_Alarm.html) giúp gom các tín hiệu này lại, tạo điều kiện cho quyết định sáng suốt. Cân nhắc triển khai giải pháp giám sát tùy chỉnh để truy vết yêu cầu end-to-end xuyên các AWS Regions. Góc nhìn toàn diện này giúp quản lý độ phức tạp của multi-Region và phản ứng nhanh với các vấn đề tiềm ẩn.

## **Kết luận**

Xây dựng ứng dụng multi-Region có khả năng phục hồi đòi hỏi cân nhắc kỹ các mẫu kiến trúc, chi phí, và độ phức tạp vận hành. Các dịch vụ AWS Serverless, với mô hình pay-for-value, giảm đáng kể thách thức khi triển khai kiến trúc multi-Region. Mẫu authorizer được trình bày trong bài cho thấy cách tổ chức có thể đạt tính sẵn sàng cao mà không cần gánh chi phí hạ tầng nhàn rỗi như cách tiếp cận truyền thống. Nhóm có thể làm theo các mẫu kiến trúc và thực tiễn tốt này để xây dựng giải pháp vững chắc, hiệu quả chi phí, duy trì tính sẵn sàng dịch vụ trong thời gian gián đoạn.

Để tìm hiểu các khái niệm về khả năng phục hồi, hãy truy cập [AWS Developer Center](https://builder.aws.com/learn/topics). Mã nguồn đầy đủ của bản demo dùng trong bài viết có sẵn tại [GitHub repository](https://github.com/aws-samples/AWS_Serverless_Resiliency_Samples/tree/main/multi-region-authorizer) của chúng tôi. Để mở rộng kiến thức về serverless, hãy truy cập [Serverless Land](https://serverlessland.com/).