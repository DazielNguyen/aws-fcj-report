---
title: "Blog 1"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# **Chuyển hướng lưu lượng ra Internet thông qua một transparent forward proxy**

bởi Vijay Menon | vào ngày 08 tháng 09 năm 2025 | trong [Amazon VPC](https://aws.amazon.com/vi/blogs/networking-and-content-delivery/category/compute/amazon-vpc/), [AWS Transit Gateway](https://aws.amazon.com/vi/blogs/networking-and-content-delivery/category/networking-content-delivery/aws-transit-gateway/), [AWS Transit Gateway network manager](https://aws.amazon.com/vi/blogs/networking-and-content-delivery/category/networking-content-delivery/aws-transit-gateway/aws-transit-gateway-network-manager/), [Networking & Content Delivery](https://aws.amazon.com/vi/blogs/networking-and-content-delivery/category/networking-content-delivery/) | [Permalink](https://aws.amazon.com/vi/blogs/networking-and-content-delivery/redirecting-internet-bound-traffic-through-a-transparent-forward-proxy/) | Share

Centralized egress là nguyên tắc sử dụng một điểm kiểm tra chung, duy nhất cho toàn bộ lưu lượng mạng đi ra Internet. Cách tiếp cận này có lợi về mặt bảo mật vì nó hạn chế việc phơi lộ tới các tài nguyên độc hại có thể truy cập từ bên ngoài, như hạ tầng malware [command and control](https://en.wikipedia.org/wiki/Botnet#Command_and_control) (C\&C). Hoạt động kiểm tra này thường được thực hiện bởi firewall như [AWS Network Firewall](https://aws.amazon.com/vi/network-firewall/), và khách hàng thường cũng muốn chèn một forward proxy trên đường đi có hoặc không có firewall. Proxy có thể hoạt động ở hai chế độ: chế độ [explicit proxy](https://en.wikipedia.org/wiki/Proxy_server), trong đó mọi client cần truy cập Internet được cấu hình dùng explicit proxy và gửi lưu lượng outbound được hỗ trợ thông qua cấu hình explicit proxy. Một triển khai như vậy được mô tả trong bài, [How to set up an outbound VPC proxy with domain whitelisting and content filtering](https://aws.amazon.com/vi/blogs/security/how-to-set-up-an-outbound-vpc-proxy-with-domain-whitelisting-and-content-filtering/). Tuy nhiên, có những hệ thống không thể cấu hình explicit proxy, và khách hàng thường tìm cách để transparently redirect lưu lượng từ những hệ thống như vậy sang Internet thông qua proxy.

Trong bài viết này, tôi giải thích một kiến trúc có thể dùng để triển khai proxy trên đường egress ra Internet và transparently lưu lượng tới đó bằng [Web Cache Communication Protocol (WCCP)](https://en.wikipedia.org/wiki/Web_Cache_Communication_Protocol). Tôi sẽ trình bày tổng quan khái niệm về việc triển khai transparent proxy với WCCP trong kiến trúc dựa trên [AWS Transit Gateway](https://aws.amazon.com/vi/transit-gateway/). Các chi tiết triển khai cụ thể có thể khác nhau tùy theo yêu cầu của tổ chức và công nghệ bạn chọn.

## **Các trường hợp sử dụng thực tế**

Dưới đây là ba trường hợp sử dụng thực tế.

1. **Secure internet access:** Tổ chức có thể dùng kiến trúc này để đảm bảo toàn bộ lưu lượng Internet outbound đi qua các kiểm soát bảo mật mà không cần cấu hình explicit proxy trên từng thiết bị client.

2. **Data loss prevention:** Kiểm tra lưu lượng transparently cho phép doanh nghiệp phát hiện và chặn dữ liệu nhạy cảm rời khỏi mạng, ngay cả khi các endpoint không hỗ trợ cấu hình explicit proxy.

3. **Regulatory compliance:** Các ngành công nghiệp có yêu cầu tuân thủ nghiêm ngặt có thể thực hiện kiểm tra và ghi nhật ký liên tục tất cả lưu lượng mạng để đáp ứng các tiêu chuẩn theo quy định.

## **Điều kiện tiên quyết**

Trước khi bắt đầu, bạn nên quen thuộc với các khái niệm và dịch vụ mạng của AWS sau:

- [Amazon Virtual Private Clouds (Amazon VPCs)](https://aws.amazon.com/vi/vpc/)
- [Route tables](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html)
- [AWS Transit Gateway](https://docs.aws.amazon.com/vpc/latest/tgw/what-is-transit-gateway.html)
- [Transit Gateway Connect attachments](https://docs.aws.amazon.com/vpc/latest/tgw/tgw-connect.html)
- [AWS Network Firewall](https://aws.amazon.com/vi/network-firewall/)
- [NAT Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html)
- Thiết bị ảo của bên thứ ba (WCCP-compliant routers and proxy servers) chức năng WCCP.

## **Tổng quan về kiến trúc**

Kiến trúc tập trung vào một Egress VPC chứa các WCCP-compliant virtual routers và proxy server chạy trên [Amazon Elastic Compute Cloud (Amazon EC2)](https://aws.amazon.com/vi/ec2/). Các virtual router này redirect lưu lượng tới proxy bằng WCCP. Thiết lập này cho phép kiểm tra minh bạch và lọc lưu lượng truy cập mà không cần thay đổi cấu hình phía máy khách. Hình 1 cho thấy sơ đồ, theo sau là các chi tiết của kiến trúc.

![Hình 1: Sơ đồ kiến trúc tổng thể](/images/3-BlogsTranslated/3.1-Blog1/WCCPBlogArchitecture-v1-Page-1.jpg)

<p style="text-align: center;">Hình 1: Sơ đồ kiến trúc tổng thể</p>

## **Các thành phần chính**

**Transit Gateway:** Transit Gateway đóng vai trò hub trung tâm cho kết nối mạng, cho phép quản lý đơn giản hóa các kết nối giữa VPCs và mạng on-premises. Trong kiến trúc của chúng tôi, Transit Gateway định tuyến lưu lượng giữa nhiều Spoke VPCs, cũng như giữa Spoke VPCs và Internet thông qua Egress VPC để kiểm tra.

**Transit Gateway Connect attachments:** Connect attachment cung cấp khả năng tích hợp thiết bị ảo bên thứ ba với Transit Gateway. Trong thiết kế của chúng tôi, các attachments:

- Kết nối Transit Gateway với WCCP-compliant routers thông qua [Generic routing encapsulation (GRE)](https://en.wikipedia.org/wiki/Generic_routing_encapsulation) chạy trên Connect attachment
- Cho phép chuyển hướng lưu lượng mà không cần sửa đổi route table trong từng VPC
- Mang lại linh hoạt cho mở rộng và tính sẵn sàng cao

Bạn có thể tham khảo bài, [Simplify SD-WAN connectivity with AWS Transit Gateway Connect](https://aws.amazon.com/vi/blogs/networking-and-content-delivery/simplify-sd-wan-connectivity-with-aws-transit-gateway-connect/), như làm nền tảng để triển khai Transit Gateway với Connect attachments. Sau đó, bạn có thể sửa đổi cách triển khai để phù hợp với các yêu cầu được nêu trong bài này.

**Egress VPC:** Egress VPC là môi trường chuyên biệt:

- Chứa các WCCP-compliant routers and proxy servers chạy trên Amazon EC2 trong private subnet
- Chứa firewall trong các private subnet riêng
- Thực thi chính sách bảo mật tập trung bằng proxy và firewall
- Sử dụng NAT Gateway trong public subnet để kết nối Internet thông qua Internet Gateway (IGW)

**WCCP-compliant routers running on Amazon EC2:** Đây là thành phần nòng cốt của triển khai transparent proxy:

- Nằm **inline** trên đường đi của lưu lượng từ Spoke VPCs ra Internet
- Intercept lưu lượng dựa trên chính sách đã cấu hình
- Redirect các loại lưu lượng cụ thể tới proxy server
- Trả lưu lượng đã xử lý về đường đi ban đầu

**Proxy servers running on Amazon EC2:** Đây là các thiết bị ảo dựa trên Amazon EC2 hoạt động như forward proxy (ví dụ [Squid](<https://en.wikipedia.org/wiki/Squid_(software)>)) tương tác và và nhận lưu lượng được chuyển hướng từ thiết bị định tuyến WCCP đã đề cập trước đó. Sử dụng WCCP, chúng áp các chính sách cấu hình cho toàn bộ lưu lượng egress và chuyển tiếp tới chức năng bảo mật tiếp theo trên đường đi. Trong ví dụ này, chúng tôi sử dụng AWS Network Firewall. Tuy nhiên, các proxy này có thể daisy chain với các hệ thống bảo mật/kiểm tra khác, như hệ thống [Data Loss Protection](https://en.wikipedia.org/wiki/Data_loss_prevention_software) (DLP), trên đường đi trước khi lưu lượng được định tuyến ra Internet.

## **Kết nối**

Như thể hiện ở Hình 1, Spoke VPCs kết nối tới Transit Gateway bằng VPC attachment. Các attachment này được associate với Spoke VPC Route Table (việc định tuyến sẽ được giải thích ở phần sau). Egress VPC kết nối tới cùng Transit Gateway bằng VPC attachment, và một Connect attachment được cấp phát giữa Transit Gateway và Egress VPC qua VPC attachment này. Connect attachment này được dùng để thiết lập GRE tunnel giữa Transit Gateway và thiết bị ảo trong Egress VPC, đóng vai trò WCCP router. Egress VPC này có kết nối Internet thông qua IGW đính kèm.

## **Định tuyến (tham khảo Hình 1\)**

- Spoke VPCs: Mỗi Spoke VPC cần truy cập Internet có các subnet gắn với route table chứa default route trỏ tới Transit Gateway được gắn với VPC đó. Cấu hình này định tuyến toàn bộ lưu lượng đi Internet tới Transit Gateway, nơi VPC attachment của Spoke VPC được gắn với Transit Gateway Spoke Route Table.

- Transit Gateway Configuration:

  - Transit Gateway Spoke Route Table chứa các route được propagate cho tất cả Spoke VPCs và một default route được propagate từ Connect attachment. Default route này được tạo bởi WCCP virtual appliance trong Egress VPC và được advertised tới Transit Gateway thông qua BGP peering trên GRE tunnel.

  - Trên Transit Gateway, Egress VPC attachment được gắn với Egress Route Table. Bảng này chứa route được propagate tới Egress VPC CIDR từ Egress VPC attachment, cũng như các route được propagate tới toàn bộ Spoke VPC CIDR từ các attachment tương ứng.

  - Connect attachment được gắn với route table riêng của nó. Route table này chứa các route của Spoke VPC được propagate cũng như default route advertised bởi WCCP router trên phiên BGP thông qua GRE tunnel.

- Egress VPC Configuration: Egress VPC cần cấu hình định tuyến bổ sung để kích hoạt chức năng transparent proxy.

  - Thiết bị WCCP router trong private subnet thiết lập GRE tunnel với Transit Gateway và tạo phiên BGP peering.

  - Thông qua các phiên BGP này, WCCP router advertise tuyến đường default route đến Transit Gateway và nhận toàn bộ các tiền tố của Spoke VPC.

  - WCCP router chuyển hướng lưu lượng đi Internet tới forward proxy trong cùng subnet bằng WCCP (thảo luận chi tiết sẽ được đưa ra sau trong bài này).

- Subnet-specific Routing: private subnets (WCCP Router và Proxy servers).

  - Route table có các entry cho Transit Gateway CIDR connect attachment peers trỏ về Transit Gateway.

  - Default route trỏ tới firewall ở private subnet riêng.

- Private subnets (firewalls):

  - Default route trỏ tới NAT Gateway trong public subnet thuộc [AWS Availability Zone’s (AZ’s)](https://aws.amazon.com/vi/about-aws/global-infrastructure/regions_az/) tương ứng.

  - Các định tuyến tới WCCP router ENI trong cùng AZ cho lưu lượng chiều về không khớp quy tắc chuyển hướng WCCP.

- Public Subnets (NAT Gateways):

  - Default route trỏ tới IGW.

  - Các định tuyến tới firewall endpoint trong cùng AZ cho lưu lượng chiều về không khớp quy tắc chuyển hướng WCCP.

## **Chuyển hướng WCCP**

Toàn bộ lưu lượng đi Internet tới các định tuyến WCCP sẽ được đánh giá theo các quy tắc chuyển hướng WCCP đã cấu hình và được chuyển tiếp tới proxy trong cùng subnet. Để dự phòng, các định tuyến WCCP này cấu hình chuyển hướng **WCCP** để kết nối với proxy ở AZ khác. Chuyển hướng WCCP có thể được cấu hình để xử lý toàn bộ lưu lượng được hỗ trợ hoặc các loại lưu lượng được chọn. Cơ chế cấu hình thay đổi tùy nhà cung cấp thiết bị ảo WCCP. Lưu lượng tới proxy sẽ được đánh giá và xử lý theo cấu hình rồi chuyển tiếp tới firewall trên đường ra Internet. Như đã đề cập, nếu cần, proxy có thể chain với các chức năng khác như DLP.

## **Hướng dẫn gói tin**

Bức hình sau phác thảo hành trình của gói tin.

![Hình 2: Sơ đồ kiến ​​trúc với luồng gói tin](/images/3-BlogsTranslated/3.1-Blog1/WCCPBlogArchitecture-v1-Page-2.jpg)

<p style="text-align: center;">Hình 2: Sơ đồ kiến ​​trúc với luồng gói tin</p>

**Forward path:** Phần này giải thích cách gói tin đi từ tài nguyên trong Spoke VPC tới đích trên Internet thông qua proxy và firewall trong Egress VPC.

- (A) Lưu lượng từ nguồn trong Spoke VPCs đi về Internet theo default route của subnet route table và đi vào Transit Gateway.

- (B) Khi nó ở trong Transit Gateway, nó đi theo tuyến đường trong Spoke Route Table trên Transit Gateway, bảng này chuyển tiếp lưu lượng tới Transit Gateway Connect attachment. Có nhiều GRE tunnel chạy trên Connect attachment, tất cả đều advertise default route tới Transit Gateway, do đó Transit Gateway dùng Equal Cost Multi-Pathing (ECMP) để gửi lưu lượng tới WCCP virtual appliance trong Egress VPC.

- (C) WCCP-virtual appliance chặn lưu lượng và xác định có cần kiểm tra hay không. Lưu lượng cần kiểm tra được redirect tới proxy server, nơi áp dụng security policy, content filtering, hoặc các kiểm soát khác trước khi chuyển tiếp tới Network Firewall.

- (CD) Lưu lượng không khớp quy tắc chuyển hướng WCCP sẽ thoát khỏi WCCP virtual appliance và đi trực tiếp tới Network Firewall theo subnet route table.

- (D) Lưu lượng đã qua proxy được Source NATed sang địa chỉ IP của proxy và rời proxy tới Network Firewall theo subnet route table. Bảng này có default route trỏ tới Network Firewall endpoint trong cùng AZ của Egress VPC.

- (E) Network Firewall kiểm tra lưu lượng và, nếu được phép, gửi tới NAT Gateway trong cùng AZ của Egress VPC theo default route cấu hình trong subnet route table của nó.

- (F) NAT Gateway thực hiện Source NAT trên lưu lượng và gửi tới đích trên Internet.

**Reverse path:** Phần này giải thích cách gói tin chiều về đi từ Internet tới tài nguyên trong Spoke VPC thông qua proxy và firewall trong Egress VPC.

- (G) Lưu lượng chiều về từ Internet đi vào chính NAT Gateway đó do Source NAT.

- (H) Theo subnet route table, NAT Gateway chuyển tiếp lưu lượng tới Network Firewall trong cùng AZ.

- (I) Network Firewall gửi lưu lượng tới proxy server trong cùng AZ nếu luồng này ở chiều đi đã khớp quy tắc chuyển hướng WCCP và đã được Source NAT bởi proxy server.

- (J) Proxy server gửi lưu lượng chiều về của luồng đã qua proxy tới WCCP router sử dụng cấu hình WCCP trên proxy server.

- (IJ) Lưu lượng chiều về của luồng không khớp quy tắc chuyển hướng được Network Firewall gửi tới WCCP router theo subnet route table.

- (K) Có nhiều GRE tunnel từ WCCP router tới Transit Gateway qua Connect attachment. Spoke VPC CIDR được quảng bá tới WCCP router qua các tunnel này. WCCP router dùng ECMP để gửi lưu lượng tới Transit Gateway qua các GRE tunnel.

- (L) Transit Gateway dùng Connect attachment route table để chuyển tiếp lưu lượng tới Spoke VPC attachment tương ứng.

- (M) Trong Spoke VPC, lưu lượng theo local routes để tới đích từ Transit Gateway ENI.

## **Những cân nhắc**

Cân nhắc bốn điểm sau khi thực hiện giải pháp này.

1. **Kích thước thiết bị ảo WCCP**

- Bảo đảm chọn kích thước phù hợp cho WCCP virtual appliance để xử lý khối lượng lưu lượng kỳ vọng. Bạn có thể tham khảo tài liệu [Amazon EC2 instance network bandwidth](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-network-bandwidth.html) để chọn EC2 instance hỗ trợ nhu cầu về lưu lượng truy cập của bạn.
- Lập kế hoạch dự phòng bằng cách triển khai qua nhiều AZ.
- Dự phòng ở cấp component (đối với WCCP router hoặc Proxy server) có thể triển khai bằng [automatic instance recovery.](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-recover.html)

2. **WCCP configuration**

- Định nghĩa service group để phân loại lưu lượng cho các chính sách kiểm tra khác nhau khi cần. Có thể dùng service group khác nhau cho primary và secondary proxy server.
- Cấu hình redirection theo yêu cầu của bạn. Bạn có thể dùng nhiều thuộc tính như port, protocol, source/destination addresses.
- Triển khai authentication giữa WCCP router và proxy server (ngoài phạm vi bài viết này).

3. **Proxy selection**

- Chọn giải pháp proxy hỗ trợ tích hợp WCCP.
- Cân nhắc yêu cầu hiệu năng theo khối lượng lưu lượng dự kiến. Tham khảo tài liệu [Amazon EC2 instance network bandwidth](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-network-bandwidth.html) để chọn EC2 instance hỗ trợ nhu cầu về lưu lượng truy cập của bạn.

4. **Monitoring and logging**

- Triển khai logging toàn diện cho cả WCCP router và proxy server. Dưới đây là một số ví dụ về log cần thu thập. Do triển khai WCCP và proxy phụ thuộc nhà cung cấp/giải pháp, các log này có thể được gọi bằng tên khác nhau. Hãy tham khảo tài liệu nhà cung cấp để biết chi tiết:

**Trên WCCP router:**

1. Trạng thái dịch vụ WCCP, chuyển hướng gói tin, và giao tiếp logs router-to-proxy
2. Thống kê lưu lượng trên interface
3. Số lần ACL khớp cho các rule liên quan WCCP
4. Dữ liệu NetFlow/sFlow phục vụ phân tích lưu lượng  
   **Trên proxy server:**
5. Access log và Error log (client IP, URL, status code, bytes transferred, timing, connection failures, timeouts)
6. Log dịch vụ WCCP (service registration, group membership)
7. Log hiệu năng cache (hit/miss ratio)
8. Log xử lý kết nối (TCP connections, handshakes)
9. Log authentication (nếu áp dụng)
10. Log kiểm tra SSL/TLS (đối với lưu lượng HTTPS)
11. Sử dụng tài nguyên hệ thống (CPU, memory, disk I/O)

- Thiết lập các cảnh báo cho các bất thường về lưu lượng hoặc sự cố sức khỏe của proxy, và tạo dashboards để trực quan hóa các mẫu lưu lượng và các security events. Bạn có thể xuất các logs đã đề cập trước đó sang [Amazon CloudWatch](https://aws.amazon.com/vi/cloudwatch/) để thiết lập các cảnh báo và tạo dashboards.

**Kết luận**

Việc triển khai transparent proxies bằng WCCP với AWS Transit Gateway mang lại một giải pháp mạnh mẽ cho các tổ chức muốn nâng cao security posture mà không làm gián đoạn trải nghiệm người dùng. Việc tập trung các kiểm soát bảo mật trong một egress VPC và sử dụng các router tương thích WCCP cho phép tổ chức đạt được khả năng kiểm tra lưu lượng toàn diện đồng thời duy trì hiệu năng mạng và khả năng mở rộng.

Kiến trúc này mang lại tính linh hoạt để thích ứng với các yêu cầu bảo mật thay đổi và nhu cầu mạng ngày càng tăng, khiến nó trở thành lựa chọn xuất sắc cho các doanh nghiệp muốn củng cố hạ tầng bảo mật đám mây. Để biết thêm thông tin và các lựa chọn kiến trúc cho centralized egress, hãy truy cập AWS Whitepaper, [Centralized egress to internet](https://docs.aws.amazon.com/whitepapers/latest/building-scalable-secure-multi-vpc-network-infrastructure/centralized-egress-to-internet.html).



|<img src="/images/3-BlogsTranslated/3.1-Blog1/vijaymenon.jpeg" alt="Vijay_Menon" width="350" style="float: left; margin-right: 15px;"/> |  **Vijay Menon** <br/> Vijay Menon là một Principal Solutions Architect làm việc tại Singapore, có nền tảng về mạng quy mô lớn và hạ tầng truyền thông. Anh ấy thích học các công nghệ mới và giúp khách hàng giải quyết những vấn đề kỹ thuật phức tạp bằng cách cung cấp các giải pháp sử dụng các sản phẩm và dịch vụ AWS. Khi không hỗ trợ khách hàng, anh ấy thích chạy đường dài và dành thời gian cho gia đình và bạn bè.                  |
| ---------------------------------------- | ------------------------------------------------------------------------------------------ |
