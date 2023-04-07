# Project Spring Commerce
- Ứng dụng bán hàng online đơn giản sử dụng SpringBoot, Hibernate, MySQL, Spring Security, Thymeleaf
## Các chức năng sẵn có:
- Đăng nhập với tài khoản đã được tạo sẵn trong database (username/password: admin/123, customer/123)
- Người dùng phải xác thực tài khoản bằng mật khẩu trước khi truy vập vào trang web thông qua Form Login của Spring Security
- Cho phép cấu hình các quyền truy cập với các tài nguyên khác nhau
- Bảo vệ khỏi các cuộc tấn công XSS, CSRF, SQL Injection
- Quản lý phiên làm việc của người dùng bao gồm đăng nhập, đăng xuất và quản lý thời gian hết phiên 
- Tài khoản có ROLE_ADMIN (admin): có quyền xem danh sách, add, edit sản phẩm, ngoài ra có thể thêm hoặc xóa sản phẩm trong giỏ hàng, đồng thời chỉnh được số lượng sản phẩm và có thể thanh toán, xem được danh sách hóa đơn, chi tiết hóa đơn
- Tài khoản ROLE_CUSTOMER (customer): có quyền xem danh sách sản phẩm,  ngoài ra có thể thêm hoặc xóa sản phẩm trong giỏ hàng, đồng thời chỉnh được số lượng sản phẩm và có thể thanh toán, xem được danh sách hóa đơn, chi tiết hóa đơn
- Sản phẩm có hình ảnh, có yêu cầu địa chỉ người nhận khi tiến hành thanh toán, các thông tin về sản phẩm và thông tin khách nhận hàng sẽ có đủ trong hóa đơn chi tiết
- Sản phẩm có phân trang (paging)
## Các hạn chế:
- Giao diện đơn giản
- Chưa có chức năng lọc (filter) theo thuộc tính sản phẩm
- Chưa có giao diện sản phẩm chi tiết
## Sơ đồ quan hệ thực thể (ER Diagram)
![ERD](https://github.com/darkfrince0101/51900846_TranDucVan_Midterm/blob/2a535305f05ff84552f1c97d87e330ddf084618d/result_img/ERD.png)
- Mối quan hệ một-nhiều giữa Account và Order: Mỗi tài khoản (Account) có thể có nhiều đơn hàng (Order), trong khi một đơn hàng chỉ thuộc về một tài khoản.

- Mối quan hệ một-nhiều giữa Product và OrderDetail: Mỗi sản phẩm (Product) có thể xuất hiện trong nhiều chi tiết đơn hàng (OrderDetail), trong khi một chi tiết đơn hàng chỉ thuộc về một sản phẩm.

- Mối quan hệ một-nhiều giữa Order và OrderDetail: Mỗi đơn hàng (Order) có thể có nhiều chi tiết đơn hàng (OrderDetail), trong khi một chi tiết đơn hàng chỉ thuộc về một đơn hàng.
## Software development principles, patterns and practices
### Model-View-Controller (MVC)
Project tuân theo kiến trúc MVC, trong đó:
- model: xử lý, thao tác liên quan đến dữ liệu như lưu trữ, truy vấn, cập nhật
- view: hiển thị dữ liệu và tương tác với người dùng thông qua giao diện
- controller: xử lý các yêu cầu từ người dùng (view) bằng việc điều hướng đến các thao tác dữ liệu (modal)
### Object-relational mapping (ORM)
- Project sử dụng Hibernate là công cụ ORM để ánh xạ các đối tượng Java vào các bảng cơ sở dữ liệu và ngược lại qua package entity và cấu hình trong application.properties giúp đơn giản hóa các hoạt động cơ sở dữ liệu.
### Dependency Injection (DI)
- Project sử dụng Spring Framework, cung cấp chức năng DI và inversion of control (IoC) giúp quản lý các phụ thuộc và giảm sự ràng buộc của các thành phần
### Service-oriented architecture (SOA)
- Project sử dụng một lớp dịch vụ để đóng gói các business logic và các hoạt động cơ sử dữ liệu, giúp tái sử dụng cao, tinh gọn và dễ bảo mật
### RESTful API
- Project triển khai RESTful API bằng cách sử dụng Spring MVC tuân theo giao thức HTTP và cung cấp một giao diện mới đồng nhất để truy cập tài nguyên
### Thymeleaf templates
- Project sử dụng Thymeleaf, một công cụ Java template phía server để tạo các trang HTML động, giúp dễ dàng tùy chỉnh và cập nhật giao diện người dùng
## Code Structure
- Project bao gồm các folder: Spring-Commerce, folder result_img chứa các hình ảnh và file README
Project có cấu trúc mã nguồn theo mô hình Maven
### 'src/main/java'
- 'com.example.demo': package cơ bản của project
- 'config': Chứa các file cấu hình thông báo và tính bảo mật của website
- 'controller': chứa các file controller để xử lý các yêu cầu từ phía người dùng
- 'dao': Chứa các lớp truy cập cơ sở dữ liệu
- 'entity': Chứa các lớp đại diện cho các thực thể cơ sở dữ liệu
- 'form': chứa các lớp tiếp nhận thông các form từ các file html đẻ thêm hoặc sửa đổi thông tin sản phẩm, đơn hàng trên website
- 'model': Chứa các lớp đại diện cho đối tượng trong website
- 'pagination': có chức năng đóng gói dữ liệu phân trang (pagination) trả về cho giao diện người dùng
- 'service': cung cấp UserDetails cho quá trình xác thực và phân quyền người dùng khi đăng nhập vào hệ thống
- 'utils': bao gồm các method được sử dụng để làm việc với file CartInfo trong Session
- 'validator': dùng để xác thực dữ liệu nhập vào từ người dùng, đồng thời kiểm tra tính hợp lệ của các thông tin được nhập vào trong quá trình thêm, sửa, xóa sản phẩm, đơn hàng trên website
### 'src/main/resources'
- 'static': chứa các hình ảnh, file css để hiển thị trên giao diện
- 'tenmmplates': chứa các file html để hiển thị cho người dùng
## Step to run
- Clone project bằng lệnh git clone 
- Mở project Spring-Commerce bằng IDE 
- Install các dependency trong file pom.xml
- Trong MySQL Workbench: tạo một cơ sở dữ liệu tên là 'springcommerce', giải nén file spring_commerce.zip và exercute file sql vào MySQL Workbench để chạy các query cấu hình cho database springcommerce
- Vào application.properties thay đổi username, password tương ứng với account đã đăng nhập trong MySQL Workbench
- Chạy project bằng file main SpringCommerceApplication.java
- Truy cập vào đường dẫn http://localhost:8080/ để sử dụng website
- Ảnh sản phẩm em để ở mục src/main/resources/static/img trong trường hợp thầy muốn tạo sản phẩm mới
- **Lưu ý**: khi em sử dụng trên brower google chorme thì khi chạy trang web thì nó bị lỗi phông chữ như sau:
![error](https://github.com/darkfrince0101/51900846_TranDucVan_Midterm/blob/2a535305f05ff84552f1c97d87e330ddf084618d/result_img/error.png)
- Nhưng khi chạy ở Microsoft Edge thì nó hiện ra trang chủ như bình thường:
![homepage](https://github.com/darkfrince0101/51900846_TranDucVan_Midterm/blob/2a535305f05ff84552f1c97d87e330ddf084618d/result_img/homepage.png)
## Postman APIs snapshot
### GET: Login (/admin/login)
![GET-admin-login](https://github.com/darkfrince0101/51900846_TranDucVan_Midterm/blob/2a535305f05ff84552f1c97d87e330ddf084618d/result_img/GET-admin-login.png)
### GET: Admin Page (/admin/accountInfo)
![GET-admin-accountInfo](https://github.com/darkfrince0101/51900846_TranDucVan_Midterm/blob/2a535305f05ff84552f1c97d87e330ddf084618d/result_img/GET-admin-accountInfo.png)
### GET: Order List Page (/admin/orderList)
![GET-admin-orderList](https://github.com/darkfrince0101/51900846_TranDucVan_Midterm/blob/2a535305f05ff84552f1c97d87e330ddf084618d/result_img/GET-admin-orderList.png)
### GET: Create Product Page (/admin/product)
![GET-admin-product](https://github.com/darkfrince0101/51900846_TranDucVan_Midterm/blob/2a535305f05ff84552f1c97d87e330ddf084618d/result_img/GET-admin-product.png)
### POST: Save Product (/admin/product)
![POST-admin-product](https://github.com/darkfrince0101/51900846_TranDucVan_Midterm/blob/2a535305f05ff84552f1c97d87e330ddf084618d/result_img/POST-admin-product.png)
### GET: Order Detail Page (/admin/order)
![GET-admin-order](https://github.com/darkfrince0101/51900846_TranDucVan_Midterm/blob/2a535305f05ff84552f1c97d87e330ddf084618d/result_img/GET-admin-order.png)
### POST: Update Quantity Of Product In Cart (/shoppingCart)
![POST-shoppingCart](https://github.com/darkfrince0101/51900846_TranDucVan_Midterm/blob/2a535305f05ff84552f1c97d87e330ddf084618d/result_img/POST-shoppingCart.png)
### GET: Cart Page (/shoppingCart)
![GET-shoppingCart](https://github.com/darkfrince0101/51900846_TranDucVan_Midterm/blob/2a535305f05ff84552f1c97d87e330ddf084618d/result_img/GET-shoppingCart.png)
### GET: Customer Information Page (/shoppingCartCustomer)
![GET-shoppingCartCustomer](https://github.com/darkfrince0101/51900846_TranDucVan_Midterm/blob/2a535305f05ff84552f1c97d87e330ddf084618d/result_img/GET-shoppingCartCustomer.png)
### POST: Save Customer Information (/shoppingCartCustomer)
![POST-shoppingCartCustomer](https://github.com/darkfrince0101/51900846_TranDucVan_Midterm/blob/2a535305f05ff84552f1c97d87e330ddf084618d/result_img/POST-shoppingCartCustomer.png)
### GET: Confirm Information Page (/shoppingCartConfirmation)
![GET-shoppingCartConfirmation](https://github.com/darkfrince0101/51900846_TranDucVan_Midterm/blob/2a535305f05ff84552f1c97d87e330ddf084618d/result_img/GET-shoppingCartConfirmation.png)
### POST: Submit Cart (/shoppingCartConfirmation)
![POST-shoppingCartConfirmation](https://github.com/darkfrince0101/51900846_TranDucVan_Midterm/blob/2a535305f05ff84552f1c97d87e330ddf084618d/result_img/POST-shoppingCartConfirmation.png)
### GET: Thank You Page (/shoppingCartFinalize)
![GET-shoppingCartFinalize](https://github.com/darkfrince0101/51900846_TranDucVan_Midterm/blob/2a535305f05ff84552f1c97d87e330ddf084618d/result_img/GET-shoppingCartFinalize.png)
### GET: Image's Product Page (/productImage)
![GET-productImage](https://github.com/darkfrince0101/51900846_TranDucVan_Midterm/blob/2a535305f05ff84552f1c97d87e330ddf084618d/result_img/GET-productImage.png)
