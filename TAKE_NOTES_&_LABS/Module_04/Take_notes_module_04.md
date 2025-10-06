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
- Amazon S3 được thiết kế để đạt được độ bền (**durability**) lên đến 99.999999999% (11 con số 9) và độ sẵn sàng (**high availability) 99.99% (4 con số 9). 

## **II. Amazon Storage Gateway**

## **III. Snow Family**

## **IV. Disaster Recovery on AWS**

## **V. AWS Backup**







