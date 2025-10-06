# **Module 2 - Các dịch vụ mạng trên AWS**
## **I. AWS Virtual Private Cloud (VPC)**
### 1. Giới thiệu về Amazon VPC 
- Là một dịch vụ cung cấp môi trường mạng ảo riêng tư, nó được cô lập về mặt logic khỏi các mạng khác ở AWS Cloud, nó hoàn toàn tách biệt với thế giới bên ngoài.
- Amazon VPC cho phép khởi chạy và tạo các tài nguyên AWS vào một mạng ảo mà bạn đã xác định. 
- Giả sử chúng ta tạo ra một lớp mạng ảo: 
    + VPC 10.10.0.0/16 : Trong này có những gì?
    + Các tài nguyên, các máy chủ, các cơ sở dữ liệu, các thiết bị cân bằng tải sẽ được đặt ở đâu trong lớp mạng ảo này?
    + Lớp mạng ảo này liên quan gì đến Availability Zone trong Module 1?
- Mô hình trình bày mạng ảo: 

            AWS Cloud - Account: 3345-2334-1232 "Tài khoản có Unique ID gồm 12 số"
            |
            Region Singapore: ap-southeast-1 (tối thiểu gồm 3 AZ)
            |
            Availability Zone: ap-southest-1b

- VPC nó nằm trong -> **Region** -> thì **VPC** sẽ chạy nhiều máy chủ, các cơ sở dữ liệu trên nhiều **Availability** khác nhau. => Đây là practice cơ bản nhất để triển khai ứng dụng và dịch vụ ở trên cloud, triển khai mô hình ở **multi AZ** để đảm bảo độ ổn định cao.
- AZ (Availability Zone): một cụm trung tâm dữ liệu
- Môi trường truyền thống việc triển khai ứng dụng ở 2 AZ, thì nó giống hai mô hình triển khai ở DC (Data Center) và DR (Disaster Recovery) -> Ở môi trường On-premise thường được gọi là DC/DR 


***Kiến trúc cơ bản của VPC:***

![Kiến trúc VPC cơ bản](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_01_VPC/Image_module_02_01/1.%20VPC%20basic.png)

***Một số tính chất chính và khái niệm của VPC cần nhớ:***
- VPC nằm trong 1 **Region**, khi tạo VPC cần khai báo 1 lớp mạng **CIDR** IPPv4 (bắt buộc) và IPv6 (tùy chọn).
- **Limit** của AWS: -> **5 VPC** -> trên **1 AWS Region** -> trên **1 AWS account**
- Mục đích chính sử dụng VPC *trong thực tế* thường dùng để **phân tách** các môi trường, trong **software development life cycle**, thì nó sẽ chia ra nhiều môi trường như **(Production/Dev/Test/Staging)**. -> Mỗi môi trường chúng ta có thể tạo ra 1 VPC
- Lưu ý: **Isolate** (Cô lập) giữa các **VPC** chỉ là mức các **Network**. Nếu như chúng ta có yêu cầu của người dùng
    + Vd: User không thể nhìn thấy một tài nguyên nguyên cụ thể thì cần tách nhiều AWS Account, nhiều VPC không giải quyết vấn đề này.

***Kiến trúc phân tách các môi trường VPC riêng biệt:***

![Kiến trúc VPC phân tách](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_01_VPC/Image_module_02_01/1.0%20VPC%20ph%C3%A2n%20t%C3%A1ch.png)

### 1.1 VPC - Subnets
- **Subnets** được gọi là mạng con, Amazon VPC cho phép -> tạo nhiều mạng ảo và chia các mạng ảo này thành các mạng con **(Subnet)**.
- VPC Subnet sẽ nằm trong 1 AZ (Availability Zone) cụ thể.
- Khi tạo Subnet, chúng ta chỉ định CIDR cho mạng con đó và đây là một **tập hợp con của khối VPC CIDR**
    + Vd: Cho mỗi **Quận** trong thành phố Hồ Chí Minh được gọi là mỗi **VPC**, thì trong mỗi **Quận** thì sẽ gồm nhiều **Phường** khác nhau thì đó được gọi là **Subnets** của từng **Quận** đó. => Đó còn được gọi là **tập hợp con của khối VPC CIDR**
- Trong mỗi Subnet, AWS sẽ giữ **5 địa chỉ IP**. Ví dụ nếu Subnet có CIDR là 10.10.1.0/24
    + Địa chỉ network (10.10.1.0)
    + Địa chỉ broadcast (10.10.1.255)
    + Địa chỉ cho bộ định tuyến (10.10.1.1)
    + Địa chỉ cho DNS (10.10.1.2)
    + Địa chỉ cho tính toán tương lai (10.10.1.3)

- Phân loại VPC - Subnets
    + Public subnet
    + Private subnet 

    => Bản chất của hai cái này là như nhau, tuy nhiên có quy ước riêng.
    + Nếu đặt tên **"Public Subnet"**, cấu hình như **Public Subnet**, thì nếu đặt các máy chủ ảo vào vùng **Public** này thì nó sẽ được cho phép đi ra **ngoài Internet**
    + Private thì ngược lại -> Không được đưa ra ngoài Internet.
***Kiến trúc VPC Subnets:***

![Kiến trúc VPC - Subnets](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_01_VPC/Image_module_02_01/1.1%20VPC%20subnets.png)
- Mỗi Subnets riêng biệt chỉ nằm trong 1 AZ riêng biệt.

***Làm sao để chúng ta tạo một cái Public Subnet, khi nào chúng ta gọi nó là Public Subnet và khi nào chúng ta gọi đó là Private Subnet? Phần 1.2 sẽ giải thích.*** 

### 1.2 VPC - Route Table
- Route Table (Bảng định tuyến), tập hợp các Route để xác định đường đi bên trong mạng của mình.
- Khi tạo VPC, AWS sẽ tạo một -> **Default Route table**, Default Route table không thể bị xóa bà chỉ chứa **1 Route duy nhất** là Route cho phép tất cả các Subnet trong VPC **liên lạc với nhau**.

***Hình ảnh minh họa***

![Minh họa Default Route table](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_01_VPC/Image_module_02_01/1.2%20Default%20Route%20table.jpg)

- Route table sẽ được gán vào Subnet. 
- Để tạo được Public Subnet, Subnets mà bên trong máy chủ có thể đi ra ngoài Internet, thì chúng ta phải tạo Custom Route table (Bảng định tuyến tùy chỉnh), tuy nhiên không thể xóa Default Route (VPC CIDR - Local), chỉ được thêm subnet chứ không xóa được Default Route. 
### 1.3 VPC - Elastic Network Interface (ENI)
- **Elastics Network Interface (ENI)** là một card ảo, chúng ta có thể chuyển sang các EC2 Instance khác.
- Mỗi máy chủ ảo của chúng ta, khi bật máy chủ lên chúng ta tạo máy chủ ở trong VPC, thì máy chủ của chúng ta sẽ được **cấp một địa chỉ IP**, các địa chỉ IP này không được gán vào tài nguyên máy chủ, mà nó gán vào các card mạng ảo (Elastic Network Interface).
- Tạo ra một máy chủ ảo thì đồng nghĩa chúng ta tạo ra một -> Elastics Network Interface
- Nhưng cái máy chủ này có thể linh hoạt gắn vào những các mạng ảo khác, khá là thông dụng. 
- Giải thích ví dụ dễ hiểu hơn: 
    + Máy chủ ảo: Căn nhà của bạn 
    + Card ảo: Số nhà của bạn. 
    + Thì số nhà của bạn có thể tháo hoặc thay thế bằng một cái số nhà khác, hoặc cái số nhà cũ của bạn sẽ chuyển qua căn nhà khác. 
- Khi chuyển sang một máy chủ mới, thì một card mạng ảo sẽ vẫn **duy trì**.
    + Địa chỉ IP Private
    + Địa chỉ Elastic IP address -> Là một địa chỉ public
    + Địa chỉ MAC -> Là địa chỉ vật lí
- **Elastic IP address (EIP)** là một địa chỉ public IPv4 tĩnh, có thể liên kết với một Elastic Networl Interface. 
    + Khi không sử dụng, sẽ bị charge phí. (Để tránh lãng phí).

***Kiến trúc VPC ENI***

![VPC ENI gồm EC2](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_01_VPC/Image_module_02_01/1.3%20VPC%20n%C3%A2ng%20cao%20g%E1%BB%93m%20EC2.png)

***Giải thích ảnh trên:***
- Trong này chúng ta tạo ra một máy chủ EC2 -> Máy chủ EC2 này sẽ được gán Elastic Network Interface -> ... Ở dưới
- VPC này sẽ cấp: 
    + VPC Private IP
    + Địa chỉ Private IPv4 trong subnet CIDR (Không gian mạng)
    + Giả sử gán cho nó 1 cái địa chỉ IP Private 10.10.1.6
- Để cái EC2 này đi ra ngoài Internet thì nó sẽ được gán vào một cái IP Public
    + Thì nó gán Elastic IP address 
    + Nó là địa chỉ Public IPv4 tĩnh, không thay đổi khi máy ảo restart
    + Địa chỉ gán vào là 134.23.42.15

### 1.4 VPC - Endpoint
- VPC Endoint cho phép chúng ta kết nối các tài nguyên nằm trong VPC tới các dịch vụ AWS được hỗ trợ (AWS PrivateLink - đi qua mạng private của AWS) mà không cần thông qua kết nối Internet. 
- Mục tiêu kết nối từ các tài nguyên, các máy chủ nằm trong VPC tới các dịch vụ khác của AWS nằm bên ngoài VPC.
- Có **2 loại** VPC Endpoint:
    + ***Interface Endpoint:*** Sử dụng một Elastics Network Interface trong VPC cùng với một địa chỉ IP Private để kết nối tới 1 dịch vụ có hỗ trợ cái ENI này.
    + ***Gateway Endpoint:*** Sử dụng một Route table để định tuyến tới endpoint của dịch vụ hỗ trợ. Chỉ có 2 dịch vụ hỗ trợ (S3 và Dynamo DB).

***Kiến trúc VPC Endpoint:***

![VPC Endpoint](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_01_VPC/Image_module_02_01/%201.4%20VPC%20Endpoint.png)

***Giải thích ảnh trên:***
- Giả sử để ra được Internet tới một dịch vụ mà AWS cung cấp, ví dự như Amazon S3 trong hình
    + S3: Cái dịch vụ này tạo ra vùng không gian lưu trữ, thì mặc định rằng nó có phạm vi sẽ nằm ngoài VPC và nó độc lập.
    + Nếu nó nằm ngoài VPC và nó độc lập thì sao -> Thì chúng ta không cần tạo cái VPC trên mà chúng ta có thể tạo ngay cái vùng lưu trữ S3, và chúng ta kết nối với nó bằng cái địa chỉ IP Public. 
    + Việc kết nối ra ngoài Internet nó sẽ bị chậm, và nó sẽ gây phát sinh chi phí khi chúng ta thực hiện đi ra ngoài Internet, chi phí đầu vào sẽ không tính phí nhưng chi phí đầu ra thì sẽ bị tính phí.

    => Với tính năng S3 này của AWS tại sao không cung cấp cho đường đi nội bộ thì AWS mới tạo ra thêm tính năng VPC Gate Endpoint cho S3

- **S3 - VPC Gateway Endpoint**
    + Nó sẽ đi qua mạng riêng và thông qua kết nối với địa chỉ IP Private
### 1.5 VPC - Internet Gateway
- Ở trên đã giải thích về **khái niệm Public Subnets** rồi thì việc tạo ra máy chủ trong Public Subnet thì chúng ta muốn cái máy chủ đó đi ra **ngoài Internet**.
- Tuy nhiên chúng ta chỉ gán địa chỉ IP vào thôi là chưa đủ mà chúng ta cần thực hiện tạo ra thêm 1 cái Internet Router cái tính năng đó còn được gọi là **Internet Gateway**
- **Internet Gateway** là một thành phần của Amazon VPC có khả năng mở rộng quy mô theo **chiều ngang (scale out)** để đảm bảo các máy chủ (EC2 Instance) ở trong VPC có thể truyền thông tin ra ngoài Internet.
- Khi sử dụng **Internet Gateway** thì chúng ta không phải lo về **băng thông** , lưu lượng hay số lượng kết nối cũng như không cần cấu hình tự động mở rộng autoscale , hoặc lo về vấn đề sẵn sàng high availability. 
- **Internet Gateway** đơn giản hóa việc cấu hình network với môi trường truyền thống rất nhiều, nó là một router nhưng chúng ta không kết nối vô được,không có khái niệm remote vào được, nó cũng không cần cập nhật và làm gì cả. -> Đơn giản **Bật lên** rồi **Sử dụng**.

***Để muốn sử dụng **Internet Gateway** này, để cho máy chủ ảo của chúng ta ra ngoài được Internet thì sẽ như thế nào?***

***Kiến trúc VPC Internet Gateway***

![VPC Internet Gateway](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_01_VPC/Image_module_02_01/1.5%20VPC%20Internet%20Gateway.png)

***Giải thích cách để EC2 ra được Internet***
- **Bước 1:** Tạo 1 cái Internet Route table hay được gọi là Internet Gateway.
- **Bước 2:** Cấu hình cái bảng định tuyến tùy chỉnh (Custom Route table) của mình -> ta thấy rằng nó còn giữ lại cái định tuyến mặc định 10.10.0.0/16
    + Tạo 1 cái mạng định tuyến mới được gọi là Destination 0.0.0.0/0 đại điện cho tất cả địa chỉ IP - Target của nó sẽ đi đến (igw-id) hay được gọi là cái ID của Internet Gateway 

- **Bước 3:** Gán Custom Route table vào -> Public subnet -> Thì cái máy chủ của mình có thể đi ra ngoài Internet thông qua Internet Gateway và lấy IP Public của ENI.
- Cấu hình đi ra ngoài Internet cần phải đáp ứng các tiêu chuẩn sau: 
    + EC2 Instance -> Phải có IP Public
    + Custom Route table -> Gắn vào cái Public Subnet -> Phải có đường định tuyến dẫn đến Internet Gateway
    + Phải có Internet Gateway được tạo sẵn trong VCP.
- Tuy nhiên trong thực tế, đa số các trường hợp chúng ta để máy chủ ảo của chúng ta nằm ở môi trường Private Subnet. 

***Giả sử máy chủ của chúng ta nằm ở môi trường Private Subnet mà ra được Internet thì chúng ta làm như thế nào?*** 

### 1.6 VPC - NAT Gateway
- NAT Gatway cho phép các máy chủ ảo EC2 Instance trong Private Subnets có thể truy cập tới Internet hoặc các dịch vụ Internet khác. 
- Chỉ chấp nhận kết nối **chiều ra** và không chấp nhận kết nối **chiều vào**.
- Từ Private Subnets ra ngoài Internet thì -> **OK**
- Từ ngoài Internet đi vào máy chủ ảo EC2 Instance của chúng ta tới Private Subnets thì -> **Không OK, không kết nối được**

***Kiến trúc VPC NAT Gateway***

![VPC NAT Gateway](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_01_VPC/Image_module_02_01/1.6%20VPC%20NAT%20Gateway.png)

***Giải thích cách Private Subnet ra Internet***
- **Bước 1:** Máy chủ ảo EC2 không được đặt trong Public Subnet nữa mà giờ đây, máy chủ ảo EC2 được đặt trong -> Private Subnet -> Và chúng ta có 1 cái địa chỉ IP Private nằm trong Private Subnet này
- **Bước 2:** Tạo NAT Gateway -> Nằm trong Public Subnet
- **Bước 3:** Tạo thêm Custom Route table -> Cấu hình 1 cái định tuyến mới gọi là Destination 10.10.0.0/16 đại diện cho tất cả các địa chỉ IP - Target của nó sẽ đi đến (ngw-id) hay được gọi là ID của NAT Gateway 
- Thì cái Custom Route table -> Gán vào Private Subnet -> Máy chủ EC2 sẽ kết nối với NAT Gateway -> Internet Gateway và từ đó đi ra được Internet

### 1.7 VPC - Security Group (Tường lửa ảo trong VPC)
[https://000003.awsstudygroup.com/vi/2-firewallinvpc/2.1-securitygroup/]
- **Security Group** (SG) là một tường lửa ảo **có lưu giữ trạng thái (stateful)** giúp kiểm soát lượng truy cập **đến và đi** trong tài nguyên của AWS.
    + ***stateful***: Nếu có thể đi vào được trong 1 cái session công việc, thì mình cũng có thể đi ra được.
    + Vd: Chúng ta tạo  1 cái webserver, cái web đó chỉ mở Port 80, cho người dùng cuối có thể kết nối vào. Chiều ra không cần tự cấu hình mở thêm các Port khác.
- Security Group **rule** được hạn chế theo giao thức, theo Protocol, theo địa chỉ IP nguồn, cổng kết nối, hoặc có thể đặt tên thành một Security Group khác.
- Security Group **rule** ***chỉ cho phép rule allow***.
- Security Group được apply lên các card mạng ảo ENI (Elastic Network Interface).

***Hình ảnh ví dụ khi tạo Security Group:***

![VPC Create SG](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_01_VPC/Image_module_02_01/1.7%20VPC%20Create%20SG.png)

***Giải thích***:
- Tạo 1 SG có name: Web Server Security Group 
- Cấu hình phân quyền trong cái **Inbound**

***Kiến trúc VPC Security Group:***

![VPC Security Group](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_01_VPC/Image_module_02_01/1.7.1%20VPC%20Security%20Group.png)

***Giải thích***:
- Phần này chỉ là cấu hình cơ bản
- Thì thấy rằng cái **Inbound Group 1** nó sẽ không có hiện phần chọn cấu hình và nó để trống. 
- Bởi vì mặc định Security Group chặn mọi truy cập đến và cho phép mọi truy cập đi. -> Ta thấy rằng Outbound Rules sẽ được setting cấu hình. 

***Nếu như để mặc định rằng chặn truy cập đến và cho phép truy cập đi này thì -> Giả sử nếu tạo 1 EC2 nếu không truy cập đến được, thì mình rất khó để quản lí nó như không remote desktop được, không SSH đến nó được.***

***Kiến trúc VPC Security Group cho Web Server***

![VPC Security Group Web Server](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_01_VPC/Image_module_02_01/1.7.2%20VPC%20Security%20Group%20Web%20Server.png)

***Giải thích:***
- Ta thấy cái Inbound Rules cho phép Port 80 -> Source là tất cả các địa chỉ IP
    + Khi ta thiết lập như vậy thì ta không biết Clients khách hàng của chúng ta đến từ đâu đều có thể kết nối được Web Server của mình thông qua Port 80
- Còn Outbound Rules sẽ mặc định là đang mở theo cấu hình trên.

***Kiến trúc khi tạo nhiều Security Group***

![VPC Multi Security Group](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_01_VPC/Image_module_02_01/1.7.3%20VPC%20Multi%20Security%20Group.png)

***Giải thích:***
- Cái này chỉ đơn giản nhiều SG trong 1 Subnet, nhưng trong thực tế sẽ có nhiều Subnet hơn. 
- **Web server security group:**
    + **Inbound Rules**:** Cho phép users từ tất cả mọi nơi có thể truy cập vào web server thông qua Port 80. 
    + **Outbound Rules:** Có thể truy cập ra không bị ràng buộc.
- **Database security group:**
    + **Inbound Rules:** Chỉ cho phép các máy chủ EC2 nằm trong cái Web Server mới có thể truy cập vào Database Server thông qua Port 3306 thôi
    + Ý nghĩa khi thiết lập (sg-webserver): Tất cả ENI (Elastic Network Interface) thì có cái địa chỉ IP đó có thể kết nối được tới Database Server.
    + Lí do tại sao không dùng địa chỉ IP nhất định, mà là dùng tên sg-server, bởi vì trong một số trường hợp khi chúng ta auto-scale, cái Server của chúng ta nằm ở nhiều AZ, nằm ở nhiều Subnet khác nhau, nhiều Range IP khác nhau, địa chỉ IP Web Server của mình thay đổi chẳng hạn. 
    + Thay vì mình tự vào và cấu hình cái SG cho EC2 Database, thì mình không cần cấu hình lại, mình chỉ đặt tên và cấu hình một lần thôi.
    + Cái này AWS sẽ tự động cập nhật và update cho mình. 
    + **Outbound Rules:** Có thể truy cập ra không bị ràng buộc.

### 1.8 VPC - Network Access Control List (NACL)
[https://000003.awsstudygroup.com/vi/2-firewallinvpc/2.2-networkacls/]
- **Network Access Control List (NACL)** là một tường lựa ảo **không lưu giữ trạng thái (stateless)** giúp **kiểm soát** lượng truy cập **đến và đi** trong tài nguyên của AWS.
    + ***stateless***: Cấu hình Firewall Rules, cấu hình cả chiều đến và chiều đi. Lưu ý cái chiều đến thì nó sẽ đến từ Port nào và chiều đi nó sẽ ra đi ra từ Port nào nó mới đúng được, 
- NACL được hạn chế theo giao thức, địa chỉ nguồn, cổng kết nối. 
- NACL được áp dụng lên các Amazon VPC Subnets -> Nó ảnh hưởng trực tiếp lên Subnet, khi thay đổi cấu hình của NACL thì nó có thể gây ảnh hưởng đến nhiều máy chủ cùng một lúc, chứ không phải chỉ máy chủ mà mình gán vào không.
    + **Cấu hình tường lửa như thế nào để không ảnh hưởng đến các máy chủ khác, ứng dụng khác trong cùng VPC?** -> Use Security Group
    + Use NACL: Sẽ ảnh hưởng đến các tài nguyên và các máy chủ ảo, cơ sở dữ liệu nằm trong VPC Subnet. 
- **Mặc định NACL** cho phép mọi **truy cập đến và đi.**

***Giao diện cấu hình của NACL:***

![1.8 VPC Set up NACL](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_01_VPC/Image_module_02_01/1.8%20VPC%20Set%20up%20NACL.png)

**Lưu ý:**
- Rule đọc từ trên xuống dưới. Nếu thỏa Rule nào thì lấy Rule đó.

***Kiến trúc VPC NACL***

![1.8.1 VPC NACL Architec](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_01_VPC/Image_module_02_01/1.8.1%20VPC%20NACL%20Architec.png)

**Lưu ý:**
- Với các thiết lập Rule chạy từ trên xuống như vậy, thì khi tạo 1 cái NACL mới và mặc định thì NACL cho phép mọi truy cập đến và đi. 
- Thì để ý Phần Rule # của Inbound và Outbound sẽ set Rule là 1
    + Protocol: All 
    + Port: All
    + Source: All IP Address

### 1.9 VPC - Flow Logs

- **VPC FLow Logs**: là một tính năng cho phép bạn -> nắm bắt thông tin về lưu lượng của các Elastic Network Interface này đến Elastic Network Interface khác, Card mạng này đến Card mạng khác trong VPC.

- Các tập tin logs có thể được xuất bản lên **Amazon Cloud Watch Logs** hoặc **Amazon S3**.

- **VPC Flow Logs không capture** nội dung gói tin.

***Example VPC Flow Logs***

![1.9 VPC Flow Logs](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_02/Module_02_01_VPC/Image_module_02_01/1.9%20VPC%20Flow%20Logs.png)

**Lưu ý:**
- Trong ví dụ này thì chúng ta thấy được VPC FLow Logs sẽ Capture được thông tin gì. 
