# **Module 3 - Dịch vụ Compute VM trên AWS**
## **I. Amazon Elastic Compute Cloud (EC2)**
### **1. Giới thiệu về EC2**
- **EC2** giống máy chủ ảo hoặc máy chủ vật lí truyền thống
- **EC2** có khả năng *khởi tạo nhanh, khả năng co giãn tài nguyên mạnh mẽ, linh hoạt.*
- **EC2** có thể hỗ trợ các workload như lưu trữ web, ứng dụng, cơ sở dữ liệu, dịch vụ xác thực và bất cứ công việc nào khác mà máy chủ thông thường có thể đáp ứng.

### **2. EC2 - Instance Type**

***Link tham khảo:***
(https://aws.amazon.com/ec2/instance-types/?ncl=h_ls)

- Cấu hình của Amazon EC2 không được tùy chọn tùy ý, mà lựa chọn cấu hình thông qua việc
lựa chọn các EC2 Instance type. 

***Sơ đồ kiến trúc của máy chủ ảo EC2***

![Module 3.1 EC2 Architec](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_03/Image_module_03/Module%203.1%20EC2%20Architec.png)

- Instance type quyết định các yếu tố :
    + CPU (Intel / AMD / ARM ( Graviton 1/ 2/3) / GPU)
    + Memory
    + Network
    + Storage

### **3. EC2 - AMI /Backup /Key Pair**
- Sử dụng **AMI (Amazon Machine Image)** có thể **provision** ra -> **một hoặc nhiều EC2 Instances** cùng lúc. 
    + AMI có sẵn của AWS, trên AWS Market Place và custom AMI tự tạo từ EC2 Instances.
- **AMI** bao gồm:
    + Root OS volumes 
    + Quyền sử dụng **AMI** quy định tài khoản AWS được sử dụng 
    + **Mapping EBS volume** sẽ được tạo và gán vào EC2 Instances.
- EC2 instance có thể được **backup** bằng cách tạo **snapshot**.

***Kiến trúc EC2 AMI*** 

![Module 3.3 EC2 AMI](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_03/Image_module_03/Module%203.3%20EC2%20AMI%20Architec.png)

- **Key pair** (public key và private key) dùng để mã hóa thông tin đăng nhập cho EC2 Instance.

***Kiến trúc EC2 Key Pair*** 

![Module 3.3 EC2 Key Pair](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_03/Image_module_03/Module%203.3%20EC2%20Key%20Pair.png)

### **4. EC2 - Elastic Block Store** 
- **Amazon EBS** cung cấp block storage và được gán trực tiếp vào EC2 Instance , tuy được gán trực tiếp như 1 RAW device, EBS về bản chất hoạt động độc lập với EC2 và được kết nối thông qua mạng riêng của EBS.

- **EBS** có hai nhóm đĩa chính là **HDD và SSD**, được thiết kế để đạt độ sẵn sàng 99.999% bằng cách **replicate dữ liệu giữa 3 Storage Node trong 1 AZ**.
    + EBS nó hỗ trợ tốt hơn môi trường truyền thống bằng cách replicate nhân 3 dữ liệu tránh thất thoát và làm mất dữ liệu đó là lí do Cloud tốt hơn môi trường truyền thống. 
    + HDD: Tập ghi tuần tự sẽ được ưu tiên, thao tác copy một file lớn copy vào ổ cứng, ghi tuần tự xuống ổ đĩa cứng đó. 
    + SSD: Lưu trữ dạng flash, có tốc độ đọc ghi ngẫu nhiên cao. 

***Kiến trúc EBS với EC2***

![Module 3.4 EC2 - EBS](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_03/Image_module_03/Module%203.4%20EC2%20-%20EBS.png)

- EBS về bản chất **hoạt động độc lập với EC2** và được kết nối thông qua mạng riêng của EBS **trong cùng 1 AZ. EC2 không thể hoạt đọng mà không có EBS**. 
- Tối thiểu phải có EBS Volumn chứa hệ điều hành của chúng ta trong đó. 
    + Giả sử EC2 error, thì dữ liệu của chúng ta vẫn còn, thì nhà cung cấp dịch vụ cho khởi tạo lại máy chủ, cho chạy lại cái máy chủ đó dựa trên cái volumn này. -> Dịch chuyển EC2 sang Hardware Node khác, vẫn kết nối với Volumn này, tính năng này có sẵn. 
- Có một số EC2 Instances đặc thù được tối ưu hóa hiệu năng của EBS. (Optimized EBS Instances)
- EBS volumes, mặc định chỉ được gán vào 1 EC2 Instances, EC2 Instances chạy trên **Hypervisor Nitro** có thể dùng 1 EBS volume gắn vào nhiều EC2 Instances. (EBS Multi attach)
- EBS được backup bằng cách thực hiện snapshot vào **S3 (Simple Storage Storage)**
- Snapshot đầu tiên là **full**, tất cả các snapshot tiếp theo là **incremental**.

### **5. EC2 - Instance Store** 

- **Instance store** là vùng đĩa **NVME** tốc độ cực cao, nằm trên physical node chạy các máy ảo
EC2.
    + **Instance store** sẽ **bị xóa hết dữ liệu** khi chúng ta thực hiện **stop EC2 instance.**
    + **Instance store** **không bị xóa dữ liệu** khi chúng ta thực hiện **restart máy, hoặc bị crash.**
    + **Instance store không replicate dữ liệu dự phòng** nên thường **không khuyên khích lưu trữ** dữ liệu quan trọng.
       
        + Sử dụng trong các trường hợp cần hiệu năng cực cao lên tới hàng triệu IOPS
          
            + Khi sử dụng thường được replicate dữ liệu vào một EBS volume để bảo đảm an toàn.

***Kiến trúc EC2 - Instance Store***

![Module 3.5 EC2 - Instance Store](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_03/Image_module_03/Module%203.5%20EC2%20-%20Instance%20Store.png)

- Sử dụng trong các trường hợp cần hiệu năng cực cao lên tới hàng triệu IPOS
    + swap 
    + paging
    + buffer / cache
    + log

### **6. EC2 - User data**
- **EC2 user data** là đoạn script chạy một lần khi provision EC2 Instance từ AMI.
- Tùy hệ điều hành mà chúng ta sẽ sử dụng bash shell scripts (Linux) / powershell (Windows).
- Bạn có thể kiểm tra user data của EC2 tại: http://169.254.169.254/latest/user-data.

***Kiến trúc EC2 - User Data***

![Module 3.6 EC2 - User Data](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_03/Image_module_03/Module%203.6%20EC2%20-%20User%20Data.png)

### **7. EC2 - Meta Data**
- **EC2 Metadata** là các thông tin liên quan tới bản thân EC2 instances, ví dụ địa chỉ IP Private, Public, Hostname, Security Groups...
- Kiểm tra Metadata: http://169.254.169.254/latest/meta-data/

***Ví dụ về Metadata***

![Module 3.7 EC2 - Metadata Example](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_03/Image_module_03/Module%203.7%20EC2%20-%20Metadata%20Example.png)

- Dùng thông tin **EC2 Metadata** để thiết lập hostname cho EC2 Instance Linux với EC2 user data. 

***Tại sao chúng ta cần EC2 - Metadata này?***
- Giả sử bạn muốn triển khai một cái ứng dụng trên EC2 Instance của mình trong một môi trường tự động -> Chúng ta muốn lấy đúng cái Hostname của cái EC2 này thì phải thông qua Metadata để lấy được các thông tin cần lấy. 

- EC2 Metadata thường được dùng trong việc tự động hóa, có những cái script no
nó chạy sâu trong máy chủ chẳng hạn, làm sao để script biết được thông tin của chính nó. -> bằng cách thức lấy thông tin metadata thông qua URL nội bộ. 

- Giả sử chúng ta chạy 1 cái script trong cái EC2 Instance Linux, muốn tăng dung lượng ổ cứng EBS -> Để muốn tăng được dung lượng phải thông qua Instance-ID thì mình mới chạy đúng câu lệnh để tăng dung lượng cho nó. 

=> Cần metadata để thực hiện các công việc tự động hóa, để chạy được những câu lệnh bên trong EC2 Instance -> Lấy những thông tin liên quan đến nó ở bên ngoài, chứ không phải ở bên trong hệ điều hành. 

### **8. EC2 - EC2 Auto Scaling** 
- **EC2 Auto Scaling** là tính năng hỗ trợ tăng giảm số lượng EC2 Instance dựa theo các điều kiện cụ thể (scaling policy) .
- **EC2 Auto Scaling** có thế tự đăng ký các EC2 Instance vào Elastic Load Balancer.
- **EC2 Auto Scaling** hoạt động trên nhiều AWS Availability Zone.
- **EC2 Auto Scaling** có thể hỗ trơ nhiều Pricing options khác nhau.

***Kiến trúc hoạt động của EC2 Auto Scaling***

***ActiveConnectionCount metric is **high*****

![Module 3.8 EC2 - EC2 Auto Scaling - High](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_03/Image_module_03/Module%203.8%20EC2%20-%20EC2%20Auto%20Scaling%20-%20High.png)

***Giải thích:***
- Giả sử ActiveConnectionCount metric is **high**
   
    => Hiệu năng hệ thống bị ảnh hưởng khi số lượng kết nối quá nhiều, phần Backend xử lý không kịp. 

- Với tính năng Auto Scaling thì chúng ta sẽ tạo một Auto Scaling Group nó có thể span across nhiều AZ

- Với Auto Scaling Group này chúng ta phải tăng số lượng máy chủ lên. Và đăng kí cái máy chủ mới đó với Application Load Balancer. 

***ActiveConnectionCount metric is **normal*****

![Module 3.8 EC2 - EC2 Auto Scaling - Normal](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_03/Image_module_03/Module%203.8%20EC2%20-%20EC2%20Auto%20Scaling%20-%20Normal.png)

***Giải thích:***

- Thì những cái Request sẽ được chia tải ra, khi chia tải như vậy thì cái ActiveConnectionCount metric is **normal**

    => Hiệu năng hệ thống trở về bình thường khi số lượng EC2 Instance được tăng lên, giúp khả năng xử lý của Backend nhanh hơn. 

***ActiveConnectionCount metric is **low*****

![Module 3.8 EC2 - EC2 Auto Scaling - Low](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_03/Image_module_03/Module%203.8%20EC2%20-%20EC2%20Auto%20Scaling%20-%20Low.png)

***Giải thích:***

- Sau khi số lượng kết nối, request giảm, ví dụ chúng ta chạy một cái sự kiện giảm giá thì số lượng kết nối ban đầu sẽ cao, sau khi hết sự kiện sẽ giảm xuống thấp, thì chúng ta đâu cần phải duy trì số lượng máy chủ lớn, chúng ta có thể giảm số lượng máy.
- Thì lúc này nó sẽ thực hiện thao tác Scale - IN, thì máy chủ ảo lúc ban đầu được tạo ra để giải quyết vấn đề lượng truy cập cao, giờ đây chúng ta xóa bớt đi 2 máy chủ Derminate đi. 
    
    => Thì hệ thống lúc này từ LOW sẽ trở về lại NORMAL
   
    => Khi số lượng kết nối giảm, số instance sẽ được giảm xuống (scale in) để tiết kiệm chi phí.

### **9. EC2 - Pricing Option**
- EC2 bao gồm **4 Options giá**: 

    1. **On-demand**: Trả theo giờ /phút /giây, sử dựng bao nhiêu tính tiền bấy nhiêu, gói mắc nhất. Phù hợp cho các workload chạy lên tới 6 tiếng 1 ngày. 

    2. **Reserved Instance**: Cam kết sử dụng theo kì hạn 1-3 năm để lấy discount, tuy nhiên bị giới hạn theo EC2 Instance type /family. 

    3. **Saving Plans**: Cam kết sử dụng theo kì hạn 1-3 năm để lấy discount, có thể không bị giới hạn bởi EC2 Instance Type Family. 

    4. **Spot Instance**: Tận dụng tài nguyên dư, giá rẻ tuy nhiên khi cần thì AWS sẽ terminate instance trong 2 phút.

- Kết hợp nhiều **Pricing Options** trong **EC2 Auto Scaling Group**.  

    + **Reserved Instance/ Saving Plan**: Số lượng EC2 minimum
    + **On-Demand Instance**: Auto EC2, thêm EC2 khi có người dùng mới kết nối vào
    + **On-Demand Instance /Spot Instance**: Ứng dụng thiết kế để có thể chịu lỗi, khi máy chủ bị stop bất ngờ, bị terminate.

## **II. Amazon Lighsail**
- **Amazon Lightsail** là dịch vụ tính toán có chi phí thấp (giá tính theo tháng chỉ **bắt đầu từ 3,5$ /tháng**) ngoài ra mỗi Instance Lightsail tạo ra cũng sẽ có một mức data transfer đi kèm. (data transfer này có mức giá rẻ hơn data transfer từ EC2 tương đối nhiều).

- **Amazon Lightsail** phù hợp cho các workload nhẹ, môi trường test dev, không yêu cầu tải
CPU cao liên tục > hơn 2 giờ mỗi ngày.

- **Amazon Lightsail** cũng có khả năng backup bằng snapshot tương tự như EC2. 

- **Amazon Lightsail** chạy trong một VPC đặc biệt, có thể kết nối tới VPC thông thường qua 1 click VPC Peering. 

***Kiến trúc Amazon Lightsail***

![Module 4.1 Amazon Lightsail](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_03/Image_module_03/Module%204.1%20Amazon%20Lightsail.png)

- Lightsail nó cũng giống như EC2 nhưng nó vẫn có sự khác biệt. 

- Để kể nối giữa 2 máy chủ Lightsail và EC2 thì nó sẽ thông qua Peering connections 

- Một click thì hai máy chủ kết nối với nhau

- Amazon Light sail chạy trong một VPC đặc biệt, có thể kết nối tới VPC thông thường qua 1 click VPC Peering. 

- Một đặc điểm của Lightsail đó là chúng ta có thể tạo ra snapshots của Lightsail Instance mà chúng ta có thể chuyển đổi thành EC2 Instance được luôn. 

- Giả sử các demo của chúng ta khi chạy thử trên Lightsail khi đến một cái ngưỡng nhất định thì chúng ta có thể nâng cấp lên EC2. 

- Lightsail Instance ngoài giá rẻ, nhưng data transfer trong mỗi Instance thì khá nhiều còn rẻ. 

## **III. Amazon EFS/FSX**
### **1. EFS (Elastic File System)**
- **EFS (Elastic File System)** cho phép tạo các NFSv4 Network volume (ổ cứng mạng) và gán nhiều vào EC2 Instance cùng lúc, quy mô lưu trữ lên đến hàng petrabyte. **EFS chỉ support Linux.** 

- Sử dụng **EFS** chí tính chi phí theo **dung lượng sử dụng** (trong khi EBS tính phí theo dung lượng cấp phát.)

- EFS có thể được cấu hình để mount vào môi trường on-premise qua DX (Direct Connect) hoặc VPN. 

***Kiến trúc EFS***

![Module 4.2 Kiến trúc EFS](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_03/Image_module_03/Module%204.2%20Ki%E1%BA%BFn%20tr%C3%BAc%20EFS.png)

- Tạo ra Mount Target và Mapping với EFS thì trên EC2 có thể sử dụng được. 
- Sử dụng Protocol NFS v4.

### **2. Amazon FSx**
- FSx cho phép tạo các NTFS volume và gán vào nhiều EC2 Instances cùng lúc sử dụng giao thức SMB ( Server Message Block ) ,FSx support Windows và Linux.

- Sử dụng FSx chỉ tính chi phí theo dung lượng sử dụng ( trong khi EBS tính phí theo dung lượng cấp phát ).
- FSx hỗ trợ tính năng deduplication , giúp giảm chi phí 30- 50% cho các trường hợp sử dụng thông thường
    + **deduplication**: là một trong những tính năng hay của FSx, giúp giảm trùng lập dữ liệu và giảm được chi phí lưu trữ. 

***Kiến trúc của FSx***

![Module 4.3 Amazon FSx](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_03/Image_module_03/Module%204.2%20Ki%E1%BA%BFn%20tr%C3%BAc%20EFS.png)


- FSx không khác gì nhiều so với EFS, chúng ta phải cần tạo một console riêng cho FSx. -> Tạo ta FSx File system. -> Thông qua SMB tới EC2. 

## **IV. AWS Application Migration Service (MGN)**
### **1. Tổng quan về AWS Application Migration Service (MGN)**

- **AWS Application Migration Service (MGN)** dùng để **migrate và replicate** phục vụ mục đích xây dựng **Disaster Recovery Site** cho các máy chủ thực, ảo lên môi trường AWS.

- **Application Migration Service (MGN)** liên tục sao chép các máy chủ nguồn sang EC2 Instance trên tài khoản AWS **(asynchronous /synchronous).**

- MGN trong quá trình sao chép sẽ sử dụng các máy staging có số lượng và quy mô cấu hình nhỏ hơn máy chủ gốc rất nhiều. -> Giúp giảm thiểu chi phí nếu như chúng ta muốn xây dựng **Disaster Recovery Site**

- Khi thực hiện **cut-over** MGN sẽ tự động tạo và chạy các máy chủ EC2 trên AWS.

=> **Hiểu cơ bản đó là một dịch vụ modernization hệ thống, chuyển từ môi trường truyền thống on-premise sang môi trường Clou.**


***Kiến trúc của Amazon MGN***

![Module 5.1 Amazon MGN](https://github.com/DazielNguyen/AWS_FCJ_FA25_VAD_NOTES_LESSON/blob/main/Module_03/Image_module_03/Module%205.1%20Amazon%20MGN.png)

- **Stagging:** Vùng đón dữ liệu -> Tạo ra Stagging Area (Tạo ra các máy chủ ảo có cấu hình nhỏ -> **1 Replication server** nó có thể support **25 máy chủ nguồn Source Machine**)

- Những cái nội dung trong ổ đĩa ở **on-premise** sẽ được **relicate** lên -> **Stagging EBS volumes**. 

- Cấu hình của **Source server** rất là to nhưng Stagging nó khá nhỏ nhưng vẫn cân được ,vì thế MGN giúp chúng ta tiết kiệm chi phí để xây dựng được 1 cái **Disaster Recovery** ,xây dựng được một môi trường có thể phục hồi nếu có sự cố xảy ra.

- Chỉ tốn chi phí cho dịch vụ lưu trữ là nhiều. 

- Từ các Stagging này thì chúng ta có thể **Launched** lên được Target EC2. Sau khi các máy chủ được khởi chạy lên thì chúng sẽ mapping với vùng -> EBS Volumes

-  **MGN có 2 đặc điểm chính:**
    + Giúp chúng ta chuyển từ on-premises lên AWS
    + Giúp chúng ta tạo một môi trường Disaster Recovery ở trên Cloud với mức chi phí thấp. 

_______________________________________________________________
## **V. Thực hành và nghiên cứu bổ sung.** 

### **Lab: 000004**
 - Thao tác EC2 cơ bản.
    + Tạo máy chủ EC2 
    + Thực hiện snapshot EC2 Instance
    + Cài đặt ứng dụng trên EC2

### **Lab: 000027**
 - Quản lí tài nguyên bằng Tag và Resource Group
    + Sử dụng Tag
    + Sử dụng Resource Group

### **Lab: 000008**
 - Quản lí tài nguyên với Amazon Cloud Watch
    + CloudWatch Agent
    + Tạo CloudWatch Dashboard 
    
### **Lab: 000006**
 - Triển khai Autoscaling Group
    + Khởi tạo Launch Template
    + Khởi tạo Target Group
    + Khởi tạo Load Balancer
    + Khởi tạo Auto Scaling Group
    + Kiểm tra kết quả. 
### **Lab: 000045**
 - Bắt đầu với Amazon Lightsail
    + Chuẩn bị
    + Kiểm tra ứng dụng trên Lightsail 
    + Sử dụng Lightsail Loadbalancer
    + Sử dụng RDS
    + Dịch chuyển sang EC2.

### **[Nghiên cứu bổ sung] - Microsoft Workloads on AWS**

Link: [https://www.youtube.com/playlist?list=PLhr1KZpdzukdJ|IxuIUM7pMB7aJ2_FfTP]

***Phần hướng dẫn của Tuần 3:***

- Series các bài thực hành bố sung dành cho việc chạy các máy chủ và ứng dụng của Microsoft trên AWS

- Bổ sung kiến thức về hệ điều hành 
- Bổ sung các kiến thức về hệ điều hành Linux như LBI1, LBI2
- Bổ sung các kiến thức về hệ điều hành Window học thêm về hệ thống quản trị Bundo. Tham khảo các series thực hành









