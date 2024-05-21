## Lỗ hổng SSRF là gì?
Server-side Request Forgery (SSRF) – giả mạo yêu cầu phía máy chủ là một lỗ hổng bảo mật mà nó cho phép kẻ tấn công sửa đổi tham số trong yêu cầu gửi đi để khiến máy chủ thực hiện truy xuất đến một miền tùy ý mà đó có thể là các dịch vụ chỉ nằm trong nội bộ như là database.

<p align="center">
<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%2011/images/1.png" width="666px">
</p>

Hiểu đơn giản giống như việc có một kẻ giả mạo số điện thoại của vợ bạn và nhắn tin bảo bạn chuyển tiền, thì không nghi ngờ gì cả ngay lập tức bạn chuyển tiền vào số tài khoản ấy. SSRF cũng tương tự như vậy, nên nếu là 1 server thì bạn phải thực sự tỉnh táo trước các yêu cầu từ client.

Ví dụ điển hình:
- Kẻ tấn công trigger lỗ hổng này để máy chủ tạo kết nối với các dịch vụ chỉ dành cho nội bộ: localhost,…
- Tương tự, kết nối tới các hệ thống ngang hàng.
- Tương tự, kẻ tấn công lấy được dữ liệu nhạy cảm mà không cần thông qua xác thực.

### Nguyên nhân
Nguyên nhân chính là do khi thông tin trong một ứng dụng web phải được lấy từ một tài nguyên bên ngoài, các yêu cầu phía máy chủ được sử dụng để tìm nạp tài nguyên và đưa nó vào ứng dụng web nhưng lại không kiểm soát chặt chẽ yêu cầu tìm nạp tài nguyên đó mà cho phép kẻ tấn công có thể hoàn toàn kiểm soát yêu cầu tìm nạp tài nguyên đến bất kì đâu ngay cả những nơi có chứa dữ liệu nhạy cảm.

Trong một vài trường hợp khác, server cho phép người dùng gửi đến 1 đường dẫn url với mục đích lấy dữ liệu vào do người dùng cung cấp và cũng như trường hợp trước, không kiểm soát chặt chẽ đầu vào đó của người dùng dẫn đến những hậu quả khôn lường.

### Hậu quả
Một cuộc tấn công SSRF thành công thường có thể gây ra các hành động truy cập trái phép vào dữ liệu nhạy cảm trong tổ chức, trong chính ứng dụng dễ bị tấn công hoặc trên các hệ thống back-end khác mà ứng dụng có thể giao tiếp.

Trong một số tình huống, lỗ hổng SSRF còn có thể cho phép kẻ tấn công thực hiện tấn công thực thi mã từ xa (RCE) đem lại hậu quả vô cùng nghiêm trọng.

## Chức năng thường tồn tại lỗ hổng SSRF
- Chức năng yêu cầu (request) tài nguyên từ máy chủ từ xa (remote servers) (**Upload from URL**, Import và Export).

- Các hàm tích hợp Cơ sở dữ liệu (Oracle, MongoDB, MSSQL, Postgres) => Ví dụ cho phép người dùng tùy ý nhập thông tin database cần kết nối tới.

- Webmail (POP3, IMAP, SMTP) => Cho phép người dùng nhập tài khoản POP3, IMAP, SMTP.

- Một số hàm thường dẫn tới lỗ hổng SSRF

## Các loại tấn công SSRF
Các cuộc tấn công SSRF thường khai thác mối quan hệ tin cậy, trong chính máy chủ (được gọi là cuộc tấn công SSRF của máy chủ) hoặc giữa máy chủ và các hệ thống phụ trợ khác (được gọi là cuộc tấn công SSRF phía sau).

### Tấn công SSRF máy chủ
Trong cuộc tấn công SSRF máy chủ, kẻ tấn công khai thác một quy trình trong đó trình duyệt hoặc hệ thống máy khách khác truy cập trực tiếp vào URL trên máy chủ. Kẻ tấn công sẽ thay thế URL gốc bằng một URL khác, thường sử dụng IP 127.0.0.1 hoặc tên máy chủ “localhost”, trỏ đến hệ thống tệp cục bộ trên máy chủ. Dưới tên máy chủ này, kẻ tấn công tìm thấy đường dẫn tệp dẫn đến dữ liệu nhạy cảm.

```
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://stock.weliketoshop.net:8080/product/stock/check%3FproductId%3D6%26storeId%3D1
```

```
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://localhost/admin
```

### Tấn công SSRF Back-End
Một biến thể khác của SSRF là khi máy chủ có mối quan hệ đáng tin cậy với thành phần phụ trợ. Nếu khi máy chủ kết nối với thành phần đó và có toàn quyền truy cập, kẻ tấn công có thể giả mạo yêu cầu và giành quyền truy cập vào dữ liệu nhạy cảm hoặc thực hiện các hoạt động trái phép. Các thành phần back-end thường có tính bảo mật yếu vì chúng được coi là được bảo vệ bên trong phạm vi mạng.

```
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://192.168.0.68/admin
```

## Cách phát hiện
Xem lại ứng dụng để tìm bất kỳ trường đầu vào hoặc chức năng nào yêu cầu tìm nạp tài nguyên bên ngoài:
- Ví dụ có thể là **trường URL**, chức năng tải tệp lên hoặc chức năng tìm nạp hình ảnh.

- Thử gửi vào đó 1 url Burp Collaborator để kiểm tra

- Nhập IP nội bộ hoặc localhost vào trường URL.

## Khai thác lỗ hổng SSRF
- Tải nội dung của một tập tin

- Truy cập một đường dẫn hạn chế

- Tìm nạp một tệp cục bộ

- Phương thức HTTP được sử dụng

- Trình tạo PDF

- Bỏ qua bộ lọc chung

## Cách ngăn chặn

- Kiểm tra và lọc URL đầu vào

- Hạn chế quyền truy cập

- Sử dụng WAF

- Mã hóa thông tin quan trọng

*Các biện pháp phòng ngừa chính bao gồm xác thực, lọc và/hoặc vệ sinh thông tin đầu vào của người dùng, sử dụng danh sách cho phép đối với các kết nối ra ngoài và phân đoạn mạng nội bộ để hạn chế phạm vi tiếp cận tiềm tàng của một cuộc tấn công SSRF.*