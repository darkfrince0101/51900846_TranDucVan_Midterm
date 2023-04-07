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
- Chua có giao diện sản phẩm chi tiết
## Sơ đồ quan hệ thực thể (ER Diagram)
![ERD](https://github.com/darkfrince0101/51900846_TranDucVan_Midterm/blob/fcb2541c2a4d0a5b6d477f502cfef70f55943670/result/ER%20Diagram.png?raw=true)
- Mối quan hệ một-nhiều giữa Account và Order: Mỗi tài khoản (Account) có thể có nhiều đơn hàng (Order), trong khi một đơn hàng chỉ thuộc về một tài khoản.

- Mối quan hệ một-nhiều giữa Product và OrderDetail: Mỗi sản phẩm (Product) có thể xuất hiện trong nhiều chi tiết đơn hàng (OrderDetail), trong khi một chi tiết đơn hàng chỉ thuộc về một sản phẩm.

- Mối quan hệ một-nhiều giữa Order và OrderDetail: Mỗi đơn hàng (Order) có thể có nhiều chi tiết đơn hàng (OrderDetail), trong khi một chi tiết đơn hàng chỉ thuộc về một đơn hàng.
