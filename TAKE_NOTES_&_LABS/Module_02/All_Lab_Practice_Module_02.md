# **Module 02 - Lab: 000003** - Bắt đầu với Amazon Virtual Private Cloud (VPC) và AWS Site-to-Site VPN

## Link: https://000003.awsstudygroup.com/vi/
- Khởi tạo VPC
    + Cấu hình tường lửa VPC 
    + Thực hành tạo 1 VPC
    + Cấu hình Site to Site VPN

### 1. Các bước thực hành
#### 1.1 Tạo VPC.
- Tạo môi trường mạng ảo riêng biệt trong AWS
- Thiết lập không gian địa chỉ IP cho VPC
- Cấu hình các tính năng DNS cơ bản

        Step 1: Truy cập VPC -> Your VPCs -> Nhấn Crete VPC
        |
        Step 2: Cấu hình VPC
                + Resources: Chọn VPC only
                + Name tag: Nhập ASG
                + IPv4 CIDR: Nhập 10.10.0.0/16
        |
        Step 3: Kích hoạt DNS cho VPC
                + Chọn Edit VPC settings
                + Mở tab DNS settings
                + Bật Enable DNS resolution
                + Bật Enable DNS hostnames
                + Bật Enable Network Address Usage metrics
                + Lưu thay đổi
    
#### 1.2 Tạo Subnets.
- Subnet là phân đoạn mạng con trong VPC
- Cho phép phân phối tài nguyên theo vùng sẵn sàng (AZ)
- Hỗ trợ phân loại mạng public và private

        Step 1: Truy cập VPC -> Subnets -> Nhấn Create Subnet
        |
        Step 2: Chọn VPC ASG đã tạo trước đó. 
        |
        Step 3: Cấu hình Subnet đầu tiên - Public Subnet 1
        |       + Subnet name: Nhập Public Subnet 1
        |       + Availability Zone: Chọn ap-southeast-1a
        |       + IPv4 Subnet CIDR: Nhập 10.10.1.0/24
        |       + Click Create subnet
        |
        Step 4: Tạo Public Subnet 2
        |       + Subnet name: Nhập Public Subnet 2
        |       + Availability Zone: Chọn ap-southeast-1b
        |       + IPv4 Subnet CIDR: Nhập 10.10.2.0/24
        |       + Click Create subnet
        |
        Step 5: Tạo Private Subnet 1
        |       + Subnet name: Nhập Private Subnet 1
        |       + Availability Zone: Chọn ap-southeast-1a
        |       + IPv4 Subnet CIDR: Nhập 10.10.3.0/24
        |       + Click Create subnet
        |
        Step 6: Tạo Private Subnet 2
        |       + Subnet name: Nhập Private Subnet 2
        |       + Availability Zone: Chọn ap-southeast-1b
        |       + IPv4 Subnet CIDR: Nhập 10.10.4.0/24
        |       + Click Create subnet
        |
        Step 7: Cấu hình Auto-assign Public IP -> Mục đích: Cho phép tự động cấp phát địa chỉ IP công cộng cho các instance trong public subnet.
        |       + Chọn subnet từ danh sách -> Set up từng cái Subnet theo các bước dưới
        |       + Click Actions
        |       + Chọn Edit subnet settings
        |       + Bật Enable auto-assign public IPv4 address
        |       + Click Save

***Khi tạo Subnet***
- Sự khác biệt giữa các IP ở mỗi Subnet là khác nhau, và AZ,  nếu không để ý thì dễ bị nhầm lẫn

***Lưu ý về Availability Zone AWS sử dụng hai khái niệm:***

- **Availability Zone (AZ):** Tên hiển thị (ví dụ: ap-southeast-1a)
- **AZ ID:** Định danh thực tế của AZ AWS ánh xạ ngẫu nhiên AZ với AZ ID giữa các tài khoản để đảm bảo phân phối tài nguyên đồng đều.

#### 1.3 Tạo Internet Gateway
- Internet Gateway (IGW) là thành phần VPC cho phép kết nối internet
- Cung cấp điểm kết nối giữa VPC và internet
- Hỗ trợ giao tiếp hai chiều cho các tài nguyên trong VPC

        Step 1: Truy cập VPC -> Internet Gateway -> Nhấn Crete Internet Gateway
        |
        Step 2: Cấu hình Internet Gateway
        |       + Name tag: Nhập Internet Gateway
        |       + Click Create internet gateway
        Step 3: Kết nối với VPC 
        |       + Click Actions trong Internet Gateway
        |       + Chọn Attach to VPC
        |       + Chọn VPC ASG từ danh sách (VPC ID sẽ tự động điền)
        |       + Click Attach internet gateway.

***Xác nhận trạng thái sau khi gắn thành công:***

- State của Internet Gateway sẽ chuyển sang Attached
- IGW đã sẵn sàng định tuyến lưu lượng internet cho VPC

#### 1.4 Tạo Route Table
- Route Table là thành phần định tuyến lưu lượng mạng trong VPC
- Xác định đường đi cho các gói tin giữa các subnet và internet
- Cho phép kiểm soát luồng dữ liệu vào/ra VPC

        Step 1: Truy cập VPC -> Route tables -> Crete route table
        |
        Step 2: Cấu hình Route Table
        |       + Name: Nhập Route table-Public
        |       + VPC: Chọn VPC ASG (VPC ID sẽ tự động điền)
        |       + Click Create route table
        |
        Step 3: Cấu hình định tuyến -> Thêm route cho Internet Gateway
        |       + Click Actions -> Trong Route table
        |       + Chọn Edit routes
        |
        Step 4: Cấu hình route mới
        |       + Click Add route
        |       + Destination: Nhập 0.0.0.0/0 (đại diện cho internet)
        |       + Target: Chọn Internet Gateway và chọn IGW đã tạo
        |       + Click Save changes
        |
        Step 5: Liên kết với Subnet -> Thiết lập subnet associations
        |       + Chọn tab Subnet associations
        |       + Click Edit subnet associations
        |
        Step 6: Chọn các public subnet
        |       + Mở rộng cột Subnet ID để xem chi tiết
        |       + Chọn cả 2 public subnet đã tạo
        |       + Click Save associations

#### 1.5 Tạo Security Group
- Security Group là tường lửa ảo cho các tài nguyên AWS
- Hoạt động như danh sách kiểm soát truy cập (ACL) ở cấp instance
- Cho phép kiểm soát lưu lượng vào/ra theo port và protocol

***Tạo Security Group cho Public Subnet***

        Step 1: Truy cập VPC -> Security Group -> Crete Security Group
        |
        Step 2: Cấu hình Security Group
        |       + Security Group name: Nhập Public subnet - SG
        |       + Description: Nhập Allow SSH and Ping for servers in public subnet
        |       + VPC: Chọn VPC ASG
        |
        Step 3: Thiết lập Inbound Rules
        |       + Click Add rule
        |       + Rule 1:
        |               Type: SSH
        |               Source: My IP (địa chỉ IPv4 public của bạn)
        |       + Rule 2:
        |               Type: All ICMP - IPv4
        |               Source: Anywhere (cho phép ping từ mọi nơi)
        | 
        Step 4: Xác nhận Outbound Rules và tạo Security Group
        |
        Step 5: Kiểm tra Security Group đã tạo

***Tạo Security Group cho Public Subnet***

        Step 1: Truy cập VPC -> Security Group -> Crete Security Group
        |
        Step 2: Cấu hình Security Group
        |       + Security Group name: Nhập Private subnet - SG
        |       + Description: Nhập Allow SSH and Ping for servers in private subnet
        |       + VPC: Chọn VPC ASG
        |
        Step 3: Thiết lập Inbound Rules cho SSH
        |       + Click Add rule
        |       + Type: SSH
        |       + Source: Custom
        |       + Chọn Security Group Public subnet - SG
        |
        Step 4: Thêm rule cho ICMP
        |       + Click Add rule
        |       + Type: All ICMP - IPv4
        |       + Source: Anywhere
        |  
        Step 5: Xác nhận Outbound Rules và tạo Security Group
        |
        Step 6: Kiểm tra Security Group đã tạo

***Cấu hình Security Group cho VPC Endpoints***

        Step 1: Tạo security group bổ sung cho VPC endpoints:
        |       + Quay lại Security Groups
        |       + Nhấp Create security group
        |       + Security group name: Nhập VPC-Endpoints-SG
        |       + Description: Nhập Security group for VPC endpoints
        |       + VPC: Chọn VPC ASG từ dropdown
        | 
        Step 2: Cấu hình quy tắc security group cho VPC Endpoints:
        |       - Inbound rules:
        |         + Nhấp Add rule
        |         + Type: Chọn HTTPS
        |         + Source: Chọn Custom và nhập 10.10.0.0/16 (VPC CIDR)
        |         + Description: Nhập HTTPS access from VPC resources
        |       - Outbound rules: Giữ mặc định (Cho phép tất cả traffic)
        |       - Nhấp Create security group
        |
        Step 3: Cập nhật Private Subnet Security Group để truy cập VPC endpoint:
        |       - Chọn Private subnet - SG
        |       - Nhấp Actions > Edit outbound rules
        |       - Đảm bảo quy tắc outbound sau tồn tại:
        |         + Type: HTTPS
        |         + Destination: 0.0.0.0/0
        |         + Description: HTTPS to AWS services and VPC endpoints
        |       - Nhấp Save rules

***Xác nhận Cấu hình:***

- Kiểm tra ba Security Groups đã tạo: 
   + **Public subnet - SG**: Cho phép SSH từ IP của bạn và ICMP từ VPC 
   + **Private subnet - SG**: Cho phép SSH từ Public subnet và ICMP từ VPC 
   + **VPC-Endpoints-SG**: Cho phép HTTPS từ VPC để truy cập AWS services
#### 1.6 Kích hoạt Flow Logs
***Kích hoạt VPC Flow Logs để Giám sát Bảo mật***

**VPC Flow Logs là gì?**
- VPC Flow Logs ghi lại thông tin về lưu lượng IP đi vào và ra khỏi các network interface trong VPC của bạn. Dữ liệu này rất quan trọng cho việc giám sát bảo mật, khắc phục sự cố mạng và kiểm toán tuân thủ.

**Hướng dẫn Cấu hình VPC Flow Logs từng bước**
        
        ```
        Step 1. Truy cập giao diện VPC Flow Logs:

        - Điều hướng đến console VPC
        - Chọn Your VPCs từ menu bên trái
        - Chọn VPC ASG của bạn
        - Nhấp vào tab Flow logs
        - Nhấp Create flow log
        
        Step 2. Cấu hình các thiết lập Flow Log:

        - Filter: Chọn All (ghi lại tất cả lưu lượng được chấp nhận, từ chối và toàn bộ)
        - Maximum aggregation interval: Chọn 1 minute (để giám sát chi tiết)
        - Destination: Chọn Send to CloudWatch Logs
        - Destination log group: Nhập /aws/vpc/flowlogs
        - IAM role: Chọn Create a new role (AWS sẽ tạo các quyền cần thiết)

        Step 3. Cấu hình định dạng log (Tùy chọn - Nâng cao):

        - Log format: Giữ AWS default format cho workshop này
        - Đối với môi trường production, bạn có thể tùy chỉnh định dạng để bao gồm các trường bổ sung
        
        Step 4. Thêm tags để quản lý tài nguyên:

        - Key: Name
        - Value: ASG-VPC-FlowLogs
        - Nhấp Create flow log
        
        Step 5: Xác minh việc tạo Flow Log:

        - Bạn sẽ thấy thông báo thành công
        - Flow Log sẽ xuất hiện trong tab Flow logs với trạng thái Active
        ```


**Hiểu về Dữ liệu Flow Log**

- Định dạng Bản ghi Flow Log -> Mỗi bản ghi flow log chứa các thông tin chính sau:

  + srcaddr, dstaddr: Địa chỉ IP nguồn và đích
  + srcport, dstport: Cổng nguồn và đích
  + protocol: Số protocol (6=TCP, 17=UDP, 1=ICMP)
  + action: ACCEPT hoặc REJECT
  + bytes, packets: Các chỉ số về khối lượng lưu lượng

**Các trường hợp sử dụng Giám sát Bảo mật** 

- VPC Flow Logs cho phép bạn:

  + Phát hiện các mẫu lưu lượng bất thường
  + Xác định cấu hình sai security group
  + Giám sát các nỗ lực rò rỉ dữ liệu
  + Khắc phục sự cố kết nối
  + Đáp ứng yêu cầu tuân thủ

**Truy cập Dữ liệu Flow Log**

        ```
        Step 6. Xem Flow Logs trong CloudWatch:
        - Điều hướng đến console CloudWatch
        - Chọn Log groups từ menu bên trái
        - Tìm và chọn /aws/vpc/flowlogs
        - Nhấp vào một log stream để xem dữ liệu flow thực tế
        ```

**Thực hành Bảo mật Tốt nhất**
- Kích hoạt Flow Logs trên tất cả VPC production và thiết lập CloudWatch alarms cho các hoạt động đáng ngờ như:

  + Khối lượng lớn kết nối bị từ chối
  + Các mẫu lưu lượng ra ngoài bất thường
  + Kết nối đến các địa chỉ IP độc hại đã biết

**Cân nhắc Chi phí**
- VPC Flow Logs phát sinh phí cho việc lưu trữ CloudWatch Logs và nhập dữ liệu. Để tối ưu chi phí:

  + Sử dụng sampling (ghi lại 1 trong N gói tin) cho môi trường lưu lượng cao
  + Thiết lập thời gian lưu trữ log phù hợp
  + Cân nhắc gửi logs đến S3 để lưu trữ dài hạn với chi phí thấp hơn
**Ghi chú Quan trọng**

- Flow Logs không ghi lại dữ liệu thời gian thực; thường có độ trễ vài phút
- Flow Logs không ghi lại lưu lượng đến/từ Amazon DNS servers
- Các truy vấn metadata đến instance metadata service (169.254.169.254) không được ghi lại

### 2. Các vấn đề gặp phải và cách giải quyết vấn đề.
**Không kết nối SSH vào VStudio được?**
1. Test cổng 22 trước. 
nc -vz ec2-54-254-136-81.ap-southeast-1.compute.amazonaws.com 22

Nó sẽ đưa ra cái IP: 115.78.229.21
2. Mở đúng IP trong Security Group

        ```
        EC2 → Instances → chọn instance của bạn → tab Security → click vào Security group.
        Edit inbound rules → Add rule:
        Type: SSH
        Port: 22
        Source: 115.78.229.21/32
        Save.
        ```
3. Nếu "succeeded", SSH luôn:

```
chmod 400 /Users/vananhduy/Downloads/aws-keypair.pem 
ssh -o IdentitiesOnly=yes \
    -i /Users/vananhduy/Downloads/aws-keypair.pem \
    ec2-user@ec2-54-254-136-81.ap-southeast-1.compute.amazonaws.com
```



# **Module 02 - Lab: 000058** - Làm việc với Amazon System Manager - Session Manager
## Link: https://000058.awsstudygroup.com/vi/
 - System Manager - Session Manager 
    + Tạo kết nối đến máy chủ EC2
    + Quản lí sessioin logs
    + Sử tính năng Port Forwarding
### 1. Các khái niệm mới trong bài LAB: 

#### **Session Manager**

- **Session Manager** là một chức năng nằm trong dịch vụ System Manager của AWS, Session Manager cung cấp khả năng quản lý các máy chủ một cách an toàn mà **không cần mở port SSH, không cần Bastion Host hoặc quản lý SSH key.** 

- **Session Manager** cũng giúp dễ dàng tuân thủ các chính sách của công ty yêu cầu quyền truy cập có kiểm soát, đảm bảo việc bảo mật nghiêm ngặt và ghi log truy việc truy cập trong khi vẫn cung cấp cho người dùng cuối quyền truy cập đa nền tảng.

- Với việc sử dụng Session Manager, bạn sẽ có được **những ưu điểm** sau:

  + Không cần phải mở cổng 22 cho giao thức SSH.
  + Có thể cấu hình để kết nối không cần đi ra ngoài internet.
  + Không cần quản lý private key của server để kết nối SSH.
  + Quản lý tập trung được user bằng việc sử dụng AWS IAM.
  + Truy cập tới server một cách dễ dàng và đơn giản bằng một cú click chuột.
  + Thời gian truy cập nhanh chóng hơn các phương thức truyền thống như SSH.
  + Hỗ trợ nhiều hệ điều hành khác nhau như Linux, Windows, MacOS.
  + Log lại được các phiên kết nối và các câu lệnh đã thực thi trong lúc kết nối tới server.

- Với những ưu điểm trên, bạn có thể **sử dụng Session Manager** thay vì sử dụng kỹ thuật **Bastion host** giúp chúng ta **tiết kiệm** được **thời gian** và **chi phí** khi quản lý server Bastion.


### 2. Thực hành

#### 1. Tạo **Lab VPC**
        Cấu hình: 
        - Tại mục Resource to create chọn: VPC only
        - Tại mục Name tag điền Lab VPC.
        - Tại mục IPv4 CIDR điền : 10.10.0.0/16.
        - Click Create VPC.

#### 2. Tạo **Public subnet**
        
        Cấu hình
        - Tại mục VPC ID click chọn Lab VPC.
        - Tại mục Subnet name điền Lab Public Subnet.
        - Tại mục Availability Zone chọn Availability zone đầu tiên.
        - Tại mục IPv4 CIRD block điền 10.10.1.0/24
        - Sau đó Enable auto-assign public IPv4 address.
        - Tạo Internet Gateway sau đó Attach vào VPC - Đặt tên Lab IWG
        - Create route table. -> Tên Lab Publicrtb - Chọn Lab VPC
        - Cấu hình Route table đó vào Internet Gatewat 
        - Sau đó Associate Subnet

#### 3. Tạo **Private subnet**

        Cấu hình: 
        - Tại mục VPC ID click chọn Lab VPC.
        - Tại mục Subnet name điền Lab Private Subnet.
        - Tại mục Availability Zone chọn Availability zone đầu tiên.
        - Tại mục IPv4 CIRD block điền 10.10.2.0/24.

#### 4. Tạo các **security group**

        Cấu hình 1: (security group cho Linux instance nằm trong public subnet)
        - Tại mục Security group name, điền SG Public Linux Instance.
        - Tại mục Description, điền SG Public Linux Instance.
        - Tại mục VPC, click dấu X để chọn lại Lab VPC bạn đã tạo cho bài lab này.        

        Cấu hình 2: (Tạo security group cho Windows instance nằm trong private subnet)
        - Tại mục Security group name, điền SG Private Windows Instance.
        - Tại mục Description, điền SG Private Windows Instance.
        - Tại mục VPC, click dấu X để chọn lại Lab VPC bạn đã tạo cho bài lab này.
        - Thêm Outbound rule cho phép kết nối TCP 443 tới 10.10.0.0/16 ( CIDR của Lab VPC chúng ta đã tạo)

        Cấu hình 3: Tạo security group cho VPC Endpoint
        - Tại mục Security group name, điền SG VPC Endpoint.
        - Tại mục Description, điền SG VPC Endpoint.
        - Tại mục VPC, click dấu X để chọn lại Lab VPC bạn đã tạo cho bài lab này
        - Xóa Outbound rule.
        - Thêm Inbound rule cho phép TCP 443 đến từ 10.10.0.0/16 ( CIDR của Lab VPC chúng ta đã tạo ).
#### 5. Tạo Public Linux EC2
[https://000058.awsstudygroup.com/vi/2-prerequiste/2.1-createec2/2.1.5-createec2linux/]

#### 6. Tạo Private EC2 Windows 
[https://000058.awsstudygroup.com/vi/2-prerequiste/2.1-createec2/2.1.6-createec2windows/]

#### 7. Kết nối đến máy chủ Public
[https://000058.awsstudygroup.com/vi/3-accessibilitytoinstances/3.1-public-instance/]

**Note(!!!)**
```
Ở trên, chúng ta đã tạo kết nối vào public instance mà không cần mở cổng SSH 22, giúp cho việc bảo mật tốt hơn, tránh mọi sự tấn công tới cổng SSH.
Một nhược điểm của cách làm trên là ta phải mở Security Group outbound ở cổng 443 ra ngoài internet. Vì là public instance nên có thể sẽ không vấn đề gì nhưng nếu bạn muốn bảo mật hơn nữa, bạn có thể khoá cổng 443 ra ngoài internet mà vẫn sử dụng được Session Manager. Chúng ta sẽ đi qua cách làm này ở phần private instance dưới đây.
```

#### 8. Tạo kết nối đến máy chủ EC2 Private

        ```
        1. Kích hoạt tính năng DNS hostnames trên VPC.
        Truy cập đến giao diện quản trị của dịch vụ VPC
        - Click Your VPCs.
        - Chọn Lab VPC.
        - Click Actions.
        - Click Edit VPC settings.
        - Tại mục DNS setting.
        - Click tick cho Enable DNS hostnames.
        - Click Save.
        ```

#### 9. Tạo VPC Endpoint
- Chúng ta sẽ tạo 3 interface endpoint yêu cầu bởi Session Manager:
- Interface endpoint:
   + com.amazonaws.region.ssm
   + com.amazonaws.region.ec2messages
   + com.amazonaws.region.ssmmessages

   ```
   1. Tạo VPC Endpoint SSM
   [https://000058.awsstudygroup.com/vi/3-accessibilitytoinstances/3.2-private-instance/3.2.2-createvpcendpoint/3.2.2.1-endpointssm/]
   2. Tạo Endpoint ssmmessages

   ```
### 3. Các vấn đề gặp phải và cách giải quyết vấn đề.







# **Module 02 - Lab: 000019**
## Link: https://0000019.awsstudygroup.com/vi/
### 1. Các bước thực hành
### 2. Điểm cần lưu ý: 
### 3. Các vấn đề gặp phải và cách giải quyết vấn đề.
 - Thiết lập VPC Peering
    + Cập nhật Network ACL 
    + Tạo kết nối Peering 
    + Cấu hình Route tables 
    + Kích hoạt Cross-Peer DNS. 

# **Module 02 - Lab: 000020**
## Link: https://000020.awsstudygroup.com/vi/
### 1. Các bước thực hành
### 2. Điểm cần lưu ý: 
### 3. Các vấn đề gặp phải và cách giải quyết vấn đề.
 - Thiết lập Transit Gateway
    + Thiết lập hạ tầng
    + Tạo Transit Gateway -> Nối nhiều VPC lại với nhau
    + Transit Gateway Attachments
    + Tạo Route Table cho TGW
    + Thêm Gateway vào Route Tables & Kiểm tra kết quả

# **Module 02 - Lab: 000010**
## Link: https://000010.awsstudygroup.com/vi/
### 1. Các bước thực hành
### 2. Điểm cần lưu ý: 
### 3. Các vấn đề gặp phải và cách giải quyết vấn đề.
 - Hybrid DNS
    + Thiết lập Hybrid DNS
    + Tạo Outbound Endpoint
    + Tạo Route 53 Resolver Rule
    + Tạo Inbound Endpoint.

