---
title: "Các bài blogs đã dịch"
date: "2025-09-09"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

### [Blog 1 - Chuyển hướng lưu lượng ra Internet thông qua một transparent forward proxy](3.1-Blog1/)

Blog này giải thích cách triển khai giải pháp transparent forward proxy để kiểm tra tập trung lưu lượng truy cập Internet ra ngoài trên AWS. Bạn sẽ tìm hiểu tại sao transparent proxy quan trọng đối với các tổ chức cần kiểm tra toàn bộ lưu lượng ra ngoài mà không cần cấu hình cài đặt proxy tường minh trên từng thiết bị client, cách sử dụng Web Cache Communication Protocol (WCCP) để chuyển hướng lưu lượng một cách liền mạch thông qua các proxy server, và cách tích hợp giải pháp này với AWS Transit Gateway, AWS Network Firewall, và các thiết bị ảo của bên thứ ba. Bài viết hướng dẫn bạn qua thiết kế kiến trúc, cấu hình định tuyến, phân tích luồng gói tin, và cung cấp các trường hợp sử dụng thực tế cho truy cập Internet an toàn, phòng chống mất mát dữ liệu, và các yêu cầu tuân thủ quy định.

### [Blog 2 - Xây dựng ứng dụng multi-Region Serverless có khả năng phục hồi trên AWS](3.2-Blog2/)

Blog này giải thích cách xây dựng các ứng dụng serverless đa vùng có khả năng phục hồi trên AWS để đảm bảo tính khả dụng cao cho các dịch vụ quan trọng. Bạn sẽ tìm hiểu tại sao kiến trúc đa vùng là cần thiết cho các ứng dụng không thể chịu được sự gián đoạn ở cấp vùng (như hệ thống xác thực, bộ xử lý thanh toán, và các tính năng game thời gian thực), cách lựa chọn giữa các mô hình triển khai Active-Passive và Active-Active dựa trên mục tiêu thời gian phục hồi và ràng buộc ngân sách của bạn, và cách các dịch vụ serverless AWS với mô hình định giá pay-for-value làm cho triển khai đa vùng tiết kiệm chi phí hơn so với các phương pháp truyền thống. Bài viết hướng dẫn bạn triển khai một bộ authorizer serverless đa vùng sử dụng Amazon API Gateway, AWS Lambda, Amazon Route 53, và DynamoDB Global Tables, đồng thời đề cập đến các phương pháp hay nhất cho chiến lược failover, giám sát sức khỏe, khả năng quan sát, và kiểm thử chaos engineering.

### [Blog 3 - Tóm tắt hàng tuần về AWS: AWS Transform, Amazon Neptune, và nhiều hơn nữa (Ngày 08 tháng 09 năm 2025)](3.3-Blog3/)

Blog này cung cấp bản tóm tắt hàng tuần về các thông báo mới nhất của AWS và các sự kiện sắp tới trong tuần ngày 8 tháng 9 năm 2025. Bạn sẽ tìm hiểu về các dịch vụ AWS mới được ra mắt bao gồm khả năng đánh giá mở rộng của AWS Transform cho việc di chuyển detached storage, hỗ trợ global cross-region inference của Amazon Bedrock cho Anthropic Claude Sonnet 4, tính năng public endpoints mới của Amazon Neptune để đơn giản hóa việc truy cập cơ sở dữ liệu, tích hợp ECS Exec vào AWS Management Console để khắc phục sự cố container dễ dàng hơn, và cấu hình thông báo tổ chức của AWS User Notifications cho quản lý cảnh báo tập trung. Bài viết cũng nêu bật các sự kiện AWS sắp tới bao gồm AWS Summits ở nhiều thành phố khác nhau, AWS re:Invent 2025 tại Las Vegas, và các AWS Community Days do cộng đồng tổ chức trên khắp thế giới.
