# **Module 4 - Dịch vụ lưu trữ trên AWS**
## **I. Amazon Simple Storage Service - S3**
### **1. Giới thiệu về S3**
-  **Amazon S3** là một dịch vụ lưu trữ dạng *kho lưu trữ ở mức* ***đối tượng***, đơn vị nhỏ nhất mà mình lưu trữ xuống hệ thống lưu trữ sẽ là **1 object**, khi lưu trữ như vậy nếu như mình muốn thay đổi nội dung trong **object**, mình bắt buộc phải ghi đè và tạo ra một object mới và **overwrite object cũ**, bạn phải thực hiện thay đổi rồi tải lại toàn bộ tập tin đã sử đổi. 
- Một thứ để lưu ý nữa là nó khác lưu trữ dạng khối như trên ổ cứng trên máy tính truyền thống, giả sử file doc của mình có 1000 dòng, nếu như mình xóa 1 dòng thì nó sẽ thay đổi trong 1 block đó, còn dạng object chỉ cần xóa 1 dòng nó sẽ phải tải lại toàn bộ 999 dòng còn lại, thì coi như nó sẽ tạo 1 object mới đè lên lớp object cũ như mình có note từ bài giảng ở trên. 
- S3 phù hợp với các loại dữ liệu ghi một lần đọc nhiều lần. (**WORM - Write Once Read Many)

### **2. Một số đặc tính của Amazon S3**
- **Amazon S3 không giới hạn** tổng số lượng khối lượng dữ liệu lưu trữ mà chúng ta đưa vào. 
- Mỗi 1 đối tượng (object) ở trong S3 dung lượng tối đa chỉ **5TB**
- Mặc định, dữ liệu Amazon S3 sẽ được nhân bản trên 3 AZ trong 1 Region, nghĩa là sao? Mình sẽ giải thích ở dưới
- Dữ liệu nào khi đưa lên AWS sẽ được nhân lên 3 bản, chỉ trừ trường hợp Elastic Block Store, 3 nhân bản sẽ nằm trong 1 AZ mà thôi, mục đích giả sử như nếu 1 AZ trong S3 bị sập thì sao, thì chúng ta vẫn còn dữ liệu ở trên 2 AZ khác trong 1 Region -> Nó cho chúng ta độ sẵn sàng cao hơn **High Availability** trong S3.
- Amazon S3 có khả năng kích hoạt sự kiện (***trigger event***) cho phép bạn kích hoạt tự động các hành động khi một số sự kiện xảy ra, như tải lên hoặc xóa đối tượng khỏi một vùng lưu trữ cụ thể. 
- Giải thích về trigger event: Khi chúng ta kích hoạt được cái event đó thì chúng ta có thể chạy được những cái **serverless function** ->Phần này học sau
- Ví dụ về **Trigger Event**: 
    + Khi mình upload 1 file ảnh lên S3, thì mình có thể **trigger** 1 cái **serverless fuction** dùng để *resize* file ảnh, thành 1 file ảnh nhỏ hơn. 
- Khi upload 1 file lên S3, bản chất trong file đó sẽ có những file chạy ngầm của S3 để đảm bảo dữ liệu được toàn vẹn và đồng nhất. 
### **3. Độ toàn vẹn Amazon S3**
- Amazon S3 được thiết kế để đạt được độ bền (**durability**) lên đến 99.999999999% (11 con số 9) và độ sẵn sàng (**high availability**) 99.99% (4 con số 9). 
- Amazon S3 hỗ trợ **multiplepart** để upload các đối tượng lớn lên bucket.
- Chúng ta cần tạo các **S3 bucket** để có thể lưu trữ các dối tượng trong Amazon S3.
    + https://[tên bucket].s3.amazonaws.com -> URL của bucket khi được tạo 
    + https://[tên bucket].s3.amazonaws.com/capture.mp4 -> URL của object khi chúng ta Upload lên S3
### **4. Cách thức Upload và Truy cập dữ liệu trên S3**
- Có nhiều cách để upload dữ liệu lên S3 như: 
    + Sử dụng giao diện web AWS Management Console
    + Sử dụng AWS CLI
    + Sử dụng SDK của AWS
    + Sử dụng API của AWS
- Dùng API PUT
    + Sử dụng 1 Protocol HTTP để tương tác với S3 
    + Dùng HTTP PUT để Upload dữ liệu lên S3 -> Object: Key = photo.gif 
    + Key thứ 2 Key = /image/phôt.gif
- Dùng API GET
    + Để lấy dữ liệu thì dùng HTTP GET - Nếu lấy được thành công nó sẽ báo quyền **200 OK - photo.gif**
- Làm việc với S3 thông qua REST API.(HTTP)
### **5. S3 - Access Point**

- **Amazon S3 Access Point** là tính năng cho phép tạo các điểm kết nối *(hostname unique)* dành cho ứng dụng, người dùng đơn lẻ hoặc theo nhóm. 
    + Chúng ta có thể cấu hình phân quyền khác nhau cho mỗi access point được tạo ra
    + Tạo S3 access points cho các ứng dụng với **quyền truy cập khác nhau**.

- Amazon S3 chia vùng lưu trữ ra nhiều lớp lưu trữ ( storage class ) giúp chúng ta tối ưu hóa chi phí.
- Các cấp lưu trữ ( Storage Class của S3 ):
    + **S3 Standard:** Dữ liệu được truy cập thường xuyên
    + **S3 Standard IA:** Dữ liệu không truy cập thường xuyên
    + **S3 Intelligent Tiering:** Tự động di chuyển các đối tượng giữa các cấp lưu trữ theo số ngày đối tượng không được truy cập.
    + **S3 One Zone IA:** Dữ liệu có thể tái tạo lại, được lưu trữ dài hạn, không truy cập thường xuyên nhưng cần truy cập nhanh
    + **Amazon Glacier / Deep Archive:** Lưu trữ dữ liệu ít truy cập

    + Chúng ta có thể thiết lập tự động hóa vòng đời của dữ liệu **(Object Life Cycle Management)** được lưu trữ trong Amazon S3. Bằng cách sử dụng chính sách vòng đời, chúng ta có thể luân chuyển dữ liệu trong 1 S3 bucket giữa các cấp lưu trữ theo thời gian (ngày) tùy chỉnh.

>Hiểu về vòng đời của các cấp lưu trữ như thế nào?

![Module04_1.5_AccessPoint](aws-fcj-report/TAKE_NOTES_&_LABS/Module_04/Image_module_04/Module04_1.5_AccessPoint.png)

- **Object Life Cycle Managenment** sẽ được di chuyển object sau **số ngày chúng ta quy định**, được tính từ ngày object được tạo. 

### **6. S3 - Static Website & CORS**

- Amazon S3 có tính năng cho phép host các static website (html, media ...), phù hợp cho **Single Page Application.** (Ứng dụng web hoặc trang web tương tác với người dùng bằng cách tự động viết lại trang web hiện tại với dữ liệu mới từ máy chủ web sử dụng javascript và các framework của nó như AngularJs, ReactJS, thay vì phương pháp mặc định của trình duyệt web tải toàn bộ trang mới).

- Amazon S3 hỗ trợ **CORS.** CORS là một cơ chế cho phép nhiều tài nguyên khác nhau (fonts, Javascript, v.v...) của một trang web có thể được truy vấn từ domain khác với domain của trang đó. CORS là viết tắt của từ **Cross-origin resource sharing.**

*https://docs.aws.amazon.com/AmazonS3/latest/userguide/cors.html*

> Kiến trúc S3 - Static Website (Web tĩnh)

![Module04_1.6_StaticWebsite](aws-fcj-report/TAKE_NOTES_&_LABS/Module_04/Image_module_04/Module04_1.6_StaticWebsite.png)

- **Amazon S3** có tính năng cho phép host các static website (html, media,..) phù hợp cho **Single Page Application**.

> Kiến trúc S3 - CORS
![Module04_1.6_CORS](aws-fcj-report/TAKE_NOTES_&_LABS/Module_04/Image_module_04/Module04_1.6_CORS.png)

- **Amazon S3** cho phép **cấu hình chính sách CORS** (Cross Origin Resource Sharing) cho phép client web applications tương tác với các tài nguyên nằm ở domain khác.

### **7. S3 - Control access**
- Amazon S3 có 2 cơ chế kiểm soát quyền truy cập tới bucket
- **S3 Access Control List (ACL)** là một cơ chế kiểm soát truy cập có trước IAM. Tuy nhiên, nếu bạn đã sử dụng S3 ACL và thấy đủ thì không cần thay đổi. **ACL S3 được gắn bucket và object của S3**. Nó xác định tài khoản hoặc nhóm AWS nào được cấp quyền truy cập và loại quyền truy cập.
- **S3 Bucket Policy** và IAM policy xác định quyền cấp đối tượng bằng cách cung cấp các đối tượng đó trong phần Resource trong policy của bạn. Câu lệnh sẽ áp dụng cho các đối tượng đó trong bucket. Việc **hợp nhất các quyền dành riêng cho đối tượng thành một chính sách** (trái ngược với nhiều ACL S3) giúp bạn **dễ dàng hơn trong việc xác định các quyền truy cập.**
> Ví dụ xóa một object

![Module04_1.7_Control_access](aws-fcj-report/TAKE_NOTES_&_LABS/Module_04/Image_module_04/Module04_1.7_Control_access.png)

- Đối với các object tất cả đều ở ngang hàng với nhau, được thiết kế nhằm mục đích để hệ thống có thể scale-out, mở rộng theo chiều ngang hiệu quả hơn
- Khi có thêm những object S3 mới, hệ thống S3 tự động phân vùng, và tự chia nhỏ thành nhiều phân vùng khác nhau. 
- Dùng thuật toán Hash
- Mỗi **object** trong S3 đều **ngang hàng**, không phân cấp (**hierarchy**) và được gán 1 **object key**. 
- Ví dụ : /image/sample.jpg , sample.jpg

### **8. S3 - Endpoint & Versioning**
> Kiến trúc S3 - Endpoint

![Module04_1.8_Endpoint](aws-fcj-report/TAKE_NOTES_&_LABS/Module_04/Image_module_04/Module04_1.8_Endpoint.png)

- Điểm truy cập Amazon S3 (**S3 Endpoint**) là tính năng cho phép truy cập đến S3 bucket thông qua mạng riêng của AWS. Mặc định, việc truy cập tới S3 là thông qua internet.
- S3 Endpoint không kết nối qua Internet
> Kiến trúc S3 - Version

![Module04_1.8_Versioning](aws-fcj-report/TAKE_NOTES_&_LABS/Module_04/Image_module_04/Module04_1.8_Versioning.png)

- Chúng ta có thể kích hoạt tính năng lập phiên bản (**Versioning**) cho phép bạn **khôi phục đối tượng sau khi vô tình xóa hay ghi đè**, có thể hỗ trợ trước việc bị tấn công ransomware/encryption attack
    + Nếu xóa một đối tượng, thay vì xóa đối tượng đó, thì Amazon S3 sẽ đánh dấu tập tin đã Xóa.
    + Nếu ghi đè đối tượng, thì một phiên bản đối tượng mới sẽ xuất hiện trong bucket.

- **Versioning** cho phép bạn khôi phục đối tượng sau khi vô tình xóa hay ghi đè, có thể hỗ trợ trước việc bị tấn công **randomware / encryption attack. 

=> Trong cả 2 trường hợp chúng ta đều có thể khôi phục phiên bản trước đó.

### **9. S3 - Object Key & Performance**
- Mỗi object trong S3 đều ngang hàng, không phân cấp (hierachy) và được gán 1 object key. 
    + Ví dụ: /image/sample.jpg ,sample.jpg
- Sâu bên dưới S3 chia ra các Partitions, Partition sẽ được chia ra tự động khi lượng request tăng cao hoặc số lượng S3 object keys lớn. (làm chậm tốc độ tìm kiếm object trong partition). 
- S3 lưu trữ key map (key map cũng được chia ra nhiều partition và được hash bởi prefix - tiền tố của object key). 
- Để tối ưu S3 performance có thể dùng **random prefix** (**/fscd**/img/sample.jpg **thay vì** /img/sample.jpg). Mục tiêu của việc làm này là khiến S3 lưu trữ các object trên nhiều partitions nhất có thể vì **performance của S3 dựa trên số lượng partitions**. 






## **II. Amazon Storage Gateway** 

## **III. Snow Family**

## **IV. Disaster Recovery on AWS**

## **V. AWS Backup**







