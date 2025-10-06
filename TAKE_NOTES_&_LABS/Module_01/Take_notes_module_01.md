# **FIRST CLOUD JOURNEY BOOSCAMP 2025**
_______________________________________________________________
## **Module 01 - 01: Điện toán đám mây là gì?**
Tổng quan: 
- Các khái niệm về điện toán đám mây? 
	+ Điện toán đám mây là việc phân phối các tài nguyên CNTT theo nhu cầu của người dùng qua Internet, và được tính theo chi phí theo nhu cầu và mức độ sử dụng.
- Lợi ích của điện toán đám mây?
	+ Sử dụng bao nhiêu -> Tính tiền bấy nhiêu -> Tối ưu hóa chi phí sử dụng. 
	+ Tăng {tốc độ} phát triển -> các tính năng tự động hóa -> được quản trị bởi nhà cung cấp dịch vụ. 
	+ Linh hoạt thêm bớt tài nguyên tùy ý.
	+ Mở rộng quy mô ứng dụng lên toàn cầu. 
_______________________________________________________________
## **Module 01 - 02: AWS, Điều gì tạo nên sự khác biệt?**
Sự khác biệt của AWS:
- Nhà cung cấp hạ tầng Cloud dẫn đầu trong 13 năm liên tiếp. 
- Khác biệt về {**tầm nhìn**} và {**văn hóa**}
- Triết lí của AWS: Khách hàng sẽ càng ngày càng trả ít tiền hơn cho cùng dịch vụ cũng như tính năng và tài nguyên sử dụng => Khách hàng sử dụng càng nhiều thì giá sẽ giảm theo AWS.
- Đưa việc mang lại giá trị thực sự cho khách hàng lên hàng đầu trong tất cả các nguyên tắc lãnh đạo {**Leadership Principle**}.
 
	+ ***[Customer Obsession]***: Đặt lợi ích khách hàng ưu tiên hàng đầu, như nhân viên của AWS sẽ không bị nặng về doanh số bán hàng -> tư vấn giúp khách hàng tối ưu được chi phí và luôn đứng trong vai trò của khách hàng.
	+ ***[Ownership]***: Làm việc như người sở hữu công ty, luôn tìm cách tốt nhất để phát triển công ty, chứ không phải làm việc cho lợi ích cá nhân để phát triển bản thân và gây thiệt hại cho công ty, do đó nó sẽ không đem lại lợi ích cho cả hai. 
	+ ***[Invent and Simplify]***: Delivery and Result: Mang lại giá trị thực sự cho khách hàng -> Giúp khách hàng thành công -> Làm việc cho công ty như là làm việc cho chính mình -> Kết quả là điều hiển nhiên phải tới 
_______________________________________________________________
## **Module 01 - 03: Bắt đầu hành trình lên mây như thế nào?**

Làm sao để thành một bầu trời đầy sao trong tương lai của mình? 

- AWS luôn cung cấp nhiều khóa học nhất cho người học và những khóa học đều đem lại chiều sâu nhất trong tất cả các nhà cung cấp dịch vụ. Do đó mình có thể tự học để có thể trở thành chuyên gia về nền tảng Cloud của AWS. 
- Học hỏi từ những người bạn mới hoặc các anh chị đi trước về nền tảng này thì => Không bao giờ thua thiệt, chỉ thua thiệt nếu không học và không hành động. => Solution: Kết bạn mới (nhưng phải đúng bạn đúng người). 
- Làm mọi thứ một mình => Không đem lại hiệu quả cao => không nên bó buộc trong những bài lab của các nhà cung cấp dịch vụ => Vì tự trải nghiệm, tự mắc lỗi, sẽ dễ dàng có những kinh nghiệm gần gũi và thực tế nhất
- Đăng kí tài khoản AWS sớm để được trải nghiệm thông qua **Free Tier**.
- Các nhà cung cấp khóa học thứ 3 uy tín: 
	+ https://udemy.com/ 
	+ https://cloudguru.com/
- Lộ trình học AWS: 
	+ https://aws.amazon.com/vi/training/learning-paths/
- AWS chú trọng vào những dự án workshop thông qua dùng các dịch vụ của AWS, những bài lab cá nhân sẽ có giá trị sau này cho bản thân, để sau này có thể show cho các nhà tuyển dụng cũng như những dự án chân thực và giá trị mà bản thân đem lại cho thị trường. 
_______________________________________________________________

## **Module 01 - 04: Hạ tầng toàn cầu của AWS** 
- Một trung tâm dữ liệu có thể chứa hàng chục ngàn máy chủ và các thiết bị phần cứng của AWS đều được dùng các thiết bị có thiết kế được tối ưu hóa riêng cho hoạt động của AWS.

- ***[Availability Zone(AZ)]***: Bao gồm một hay nhiều trung tâm dữ liệu (Data Center), các AZ được thiết kế đồng thời để không xảy ra sự cố ảnh hưởng đồng thời cả 2 AZ một lúc (fault isolation)

	+ Giữa 2 AZ kết nối riêng -> tốc độ cao.
	+ Nhưng triển khai dịch vụ và ứng dụng thì tối thiệu phải trên 2 AZ

- ***[Region]***: Bao gồm tối thiểu 3 Availability Zone. 
	+ Hiện tại có hơn 25 Region trên toàn cầu. 
	+ Region được kết nối với nhau bởi mạng -> backbone của AWS. 
	+ Default data & services ở các region -> độc lập với nhau (Trừ một số dịch vụ ở quy mô global)

- ***Mind map dễ hiểu:***

*Chú thích*

**AZ**: Availability Zone

**DC**: Data Center


				      [REGION]
				       /   \	
 				      AZ    AZ
	             	 /  \  / \
                   DC   DC DC DC
- 	Người dùng gần các region nào thì dùng gần region đó -> giảm độ trễ 
- 	Generative AI -> Region US
- 	Lựa chọn Region thường sẽ liên quan đến chi phí.
- 	Quy mô lớn -> Khách hàng nhiều -> Giá thành rẻ. 

- ***[Edge Locations]***: Là mạng lưới trung tâm dữ liệu thứ cấp, được thiết kế sự dụng các dịch vụ mạng biên
	+ CloudFront (CDN)
	+ Web Application Firewall (WAF)
	+ Route 53 (DNS Service)
_______________________________________________________________
## **Module 01 - 05: Công cụ Quản Lý AWS Services**
**[AWS Management Console - Root Login]**

- Cách đăng nhập: gồm 2 cơ chế
	+ ***Root User***: Tài khoản dùng đăng kí AWS account đầu tiên, cực kì quan trọng, hạn chế dùng root account -> làm bảo mật 2 lớp -> MFA -> Lấp lại không dùng nữa
	+ ***IAM User***: Nó là 1 tài khoản con giúp các user quản lí cũng như truy xuất các tài nguyên cần dùng. 
	+ login account xong tạo IAM user -> Chỉ cần cung cấp account ID trong Root Account.
 => Services cung cấp các dịch vụ -> Mỗi service có trang management riêng cho phép chúng ta sử dụng các tính năng (feature) của dịch vụ đó. 

- Support Center: Tạo ra các Support Case -> yêu cầu đội ngũ AWS hỗ trợ.
- Cách chạy: 

      USER -> PASSWORD -> AWS MANAGEMENT CONSOLE -> AWS SERVICES ENDPOINT

**[AWS Command Line Interface (CLI)]**
- Cách chạy 

      USER -> ACCESS KEY / SECRET ACCESS KEY -> AWS COMMAND LINE INTERFACE (AWS CLI) -> AWS SERVICE ENDPOINT

- Cho phép triển khai các chức năng tương đương các chức năng như các dịch vụ AWS trên trình duyệt. 

**[AWS SDK - Software Development Kit]**
- AWS SDK giúp đơn giản hóa trong việc xây dựng các ứng dụng của mình, muốn tận dụng được các dịch vụ và tính năng của AWS cung cấp
- AWS SDK có bộ thư viện hỗ trợ nhiều ngôn ngữ khác nhau
	+ Gọi API request 
	+ Quản lí thông tin xác thực (management credentials). 
	+ Thử lại (Retry)
 	+ Sắp xếp dữ liệu (Data Marshaling - chuẩn hóa dữ liệu) 
	+ Tuần tự hóa(Serialization - Chuyển objects sang bytes stream)
	+ Giải mã hóa (Deserialization - Chuyển Bytes stream về lại object)
	
_______________________________________________________________
## **Module 01 - 06: Tối ưu hóa chi phí trên AWS**
- Lựa chọn cấu hình tài nguyên và nơi lưu trữ dữ liệu phù hợp. 
- Các phương thức thanh toán giảm giá: 
	+ Reserved instance: Xài bao nhiêu tính bấy nhiêu
	+ Saving plan: Cam kết lâu dài, cam kết như 1 năm , 2 năm sẽ có mức discount tương ứng
	+ Spot: Tài nguyên tạm, cho thuê lượng tài nguyên có sẵn đó, với chi phí rất thấp, nhưng nếu khi người bán cần và cần mở rộng thì cái server đó có thể bị lấy lại bất cứ lúc nào. 
- Xóa các tài nguyên không sử dụng, bật tự động các tài nguyên không cần chạy 24/7. 
- Tận dụng các dịch vụ serverless. -> Phi máy chủ, nó sẽ các dịch vụ không cần máy chủ. 

**[Kiến trúc tối ưu để giải quyết yêu cầu của doanh nghiệp]**
- Dữ liệu nên đặt trong dịch vụ lưu trữ nào? -> Đặt ở đó bao lâu -> Bao lâu thì xuống cơ sở dữ liệu thứ cấp -> Cơ sở dữ liệu của mình như cái schema, cái lược đồ/ được thiết kế như thế nào -> Chọn loại cơ sở dữ liệu nào phù hợp -> Mình có nên sự dụng Cloud Native được quản lí bởi AWS hay không? -> Hay là dùng một dịch vụ open-sources chạy trên một máy chủ ảo của AWS 

=>>> Tùy vào mỗi dự án, Mỗi dự án và yêu cầu có ràng buộc riêng, do đó mình có thể tối ưu được việc chi phí trên AWS. 
  

- Cài đặt sử dụng AWS Budget (Vd: Tui dùng $10 thì gửi cảnh báo cho tui, hoặc gửi mức chi phí cảnh báo theo nhu cầu của mình) -> Có bài thực hành cho phần này.
- Quản lí chi phí theo phòng ban, ứng dụng với Cost Allocation Tag. (Vd: 1 phòng nhiều người, thì sẽ biết được ai dùng bao nhiêu, cả phòng ban dùng bao nhiêu.)
- Tối ưu hóa chi phí là việc làm LIÊN TỤC, liên tục theo dõi để tối ưu hóa chi phí. 

***Hai cách tạo ra giá trị cho doanh nghiệp của mình:***

	GIÚP DOANH NGHIỆP KIẾM TIỀN
	GIÚP DOANH NGHIỆP TIẾT KIỆM TIỀN

**[CÔNG CỤ TÍNH TOÁN CHI PHÍ]**

Link công cụ: https://calculator.aws/#/

- Cho phép tạo các estimate các dịch vụ thông dụng.
- Có thể chia sẻ các estimate cho người khác. 
- Chi phí sẽ khác biệt theo từng Region, theo từng dịch vụ, theo từng cấu hình mà mình mong muốn. 

**[Working with AWS Support]**
- AWS have 4 main packages support: 
	+ Basic (Explore): Khám các tính năng và dịch vụ gì?
	+ Developer (Test / Dev): Xây dựng môi trường Test và Dev, Yêu cầu về mặt kĩ thuật 
	+ Business (Production): 
	+ Enterprise (Large Enterprise): Cho các doanh nghiệp lớn. 
-> Có thể nâng cấp các gói hỗ trợ trong thời gian ngắn để đẩy nhanh tốc độ hỗ trợ khi có sự cố quan trọng cần xử lý nhanh. 

_______________________________________________________________
## **Module 01 - 07: Thực hành và nghiên cứu bổ sung.** 

### **Lab: 000001**
 - Tạo tài khoản AWS 
 - Thiết lập MFA cho tài khoản AWS(Root) 
 - Tài khoản và Nhóm Admin
 - Hỗ trợ xác thực tài khoản.

### **Lab: 000007**
 - Tạo Cost Budget
 - Tạo Usage Budget 
 - Tạo Reservation Budget
 - Tạo Saving plans Budget. 

### **Lab: 000009**
 - Đọc và thấy sự khác nhau giữa các gói hỗ trợ của AWS. 
 - Truy cập AWS Support. 
 - Quản lí yêu cầu hỗ trợ. 

### **[Nghiên cứu bổ sung] - AWS Well Architected Framework (Hơn 100 câu hỏi)**
 - Tìm hiểu về các: 
	+ Khái nghiệm 
	+ Nguyên tắc thiết kế
	+ Biện pháp tốt nhất về kiến trúc để thiết kế và vận hành hệ thống của bạn trong môi trường điện toán đám mây. 

- Sử dụng Framework bằng cách trả lời các câu hỏi. 
	+ Cần biết được mức độ phù hợp giữa kiến trúc của mình với các phương pháp tốt nhất được khuyến nghị. 
- Khi sử dụng AWS WAF tích hợp trên AWS Management Console sẽ có hướng dẫn để cải thiện kiến trúc hiện tại của mình. 


























