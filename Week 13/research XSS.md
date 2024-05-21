## Lỗ hổng XSS là gì?
- Cross-site scripting (thường được gọi là XSS) là một dạng lỗ hổng Client-side tiêu biểu nhất. Trong quá trình khai thác, kẻ tấn công thực hiện việc nhúng mã độc (thường là JavaScript) vào trang web của người khác, sau đó khi người dùng truy cập vào trang web đó, mã độc sẽ được thực thi trên trình duyệt của họ, từ đó đạt được mục đích của kẻ tấn công.  
- Cuộc tấn công thực sự xảy ra khi nạn nhân **truy cập** trang web hoặc ứng dụng web thực thi mã độc hại. Trang web hoặc ứng dụng web trở thành phương tiện cung cấp tập lệnh độc hại đến trình duyệt của người dùng. Cross-Site Scripting là một trong những kĩ thuật tấn công phổ biến nhất hiện nay, được liệt vào danh sách những kỹ thuật tấn công nguy hiểm nhất với ứng dụng web.

<p align="center">
<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%2013/images/1.png" width="666px">
</p>

## Chức năng thường tồn tại lỗ hổng
- Các cuộc tấn công kịch bản chéo trang có thể xảy ra ở bất cứ nơi nào mà người dùng độc hại có thể được phép đăng tài liệu không được kiểm soát lên một trang web đáng tin cậy để những người dùng hợp lệ khác sử dụng.

- **Biểu mẫu nhập liệu (forms)**: Các trường nhập liệu như tên người dùng, email, tin nhắn, bình luận, tìm kiếm,..

- **URL**: Các tham số trong URL có thể bị chèn mã độc.

- **Các trang hiển thị dữ liệu người dùng**: Bảng điều khiển, trang cá nhân, trang hiển thị bình luận,..

- **Cookie và Storage**: Các giá trị được lưu trữ và sử dụng lại.

## Các loại tấn công XSS
- Có 3 loại tấn công XSS chính là: **Reflected XSS**, **Stored XSS**, **DOM Based XSS**

### Reflected XSS
- Reflected XSS là dạng tấn công thường gặp nhất trong các loại hình XSS. Với Reflected XSS, hacker không gửi dữ liệu độc hại lên server nạn nhân, mà gửi trực tiếp link có chứa mã độc cho người dùng, khi người dùng click vào link này thì trang web sẽ được load chung với các đoạn script độc hại.  Reflected XSS thường dùng để ăn cắp cookie, chiếm session,… của nạn nhân hoăc cài keylogger, trojan … vào máy tính nạn nhân.

- Có nhiều hướng để khai thác thông qua lỗi Reflected XSS, một trong những cách được biết đến nhiều nhất là chiếm phiên làm việc (session) của người dùng, từ đó có thể truy cập được dữ liệu và chiếm được quyền của họ trên website.

<p align="center">
<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%2013/images/2.png" width="666px">
</p>

### Stored XSS
- Stored XSS là dạng tấn công mà hacker chèn trực tiếp các mã độc vào cơ sở dữ liệu của website. Dạng tấn công này xảy ra khi các dữ liệu được gửi lên server không được kiểm tra kỹ lưỡng mà lưu trực tiếp vào cơ sở dữ liệu. Khi người dùng truy cập vào trang web này thì những đoạn script độc hại sẽ được thực thi chung với quá trình load trang web.

- Ví dụ, khi người tấn công bình luận một chuỗi chứa mã độc vào một bài viết trên một trang web công cộng, mã độc đó được lưu trữ và hiển thị trong bài viết đó, người dùng khác truy cập vào dẫn tới thực thi script và trở thành nạn nhân.

<p align="center">
<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%2013/images/3.png" width="666px">
</p>

<p align="center">
<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%2013/images/4.png" width="666px">
</p>

### DOM Based XSS
- DOM Based XSS (còn được gọi là DOM XSS) là kỹ thuật khai thác XSS dựa trên việc thay đổi cấu trúc DOM của tài liệu, cụ thể là HTML. Nơi lỗ hổng bảo mật tồn tại trong các tập lệnh phía máy khách mà trang web/ứng dụng luôn cung cấp cho khách truy cập. Cuộc tấn công này khác với Reflected XSS và Stored-XSS ở chỗ trang web/ứng dụng không phân phối trực tiếp tập lệnh độc hại đến trình duyệt của mục tiêu. 
- Trong một cuộc tấn công DOM-based XSS, trang web/ứng dụng có các tập lệnh phía máy khách dễ bị tấn công sẽ phân phối tập lệnh độc hại đến trình duyệt của mục tiêu. Tương tự như Reflected XSS, một cuộc tấn công DOM-based XSS không lưu trữ tập lệnh độc hại trên chính máy chủ dễ bị tấn công.

Ví dụ - một website có URL đến trang đăng ký như sau:

http://example.com/register.php?message=Please+fill+in+the+form

Khi truy cập đến thì chúng ta thấy một Form rất bình thường

<p align="center">
<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%2013/images/5.png" width="666px">
</p>

Thay vì truyền

`message=Please+fill+in+the+form`

thì truyền

```html
message=<label>Gender</label>
<select class = "form-control" onchange="java_script_:show()"><option value="Male">Male</option><option value="Female">Female</option></select>
<script>function show(){alert();}</script>
```

Khi đấy form đăng ký sẽ trở thành như thế này:

<p align="center">
<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%2013/images/6.png" width="666px">
</p>

Người dùng sẽ chẳng chút nghi ngờ với một form “bình thường” như thế này, và khi lựa chọn giới tính, Script sẽ được thực thi

<p align="center">
<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%2013/images/7.png" width="666px">
</p>

## Nguyên nhân
- **Không kiểm tra và lọc dữ liệu đầu vào**: Dữ liệu người dùng không được kiểm tra, xác thực và lọc trước khi hiển thị.

- **Không mã hóa dữ liệu đầu ra**: Không mã hóa đúng cách dữ liệu khi hiển thị trên trang web.

- Sử dụng các **công nghệ hoặc framework cũ**, không có các biện pháp bảo vệ chống XSS.

## Hậu quả 
- **Đánh cắp thông tin**: Thông tin nhạy cảm như cookie, token xác thực, thông tin cá nhân bị đánh cắp.

- **Chiếm quyền điều khiển tài khoản**: Hacker có thể đọc bất kỳ dữ liệu nào và thực hiện các hành động tùy ý bằng cách mạo danh người dùng (đăng bài trên mạng xã hội hoặc thực hiện các giao dịch ngân hàng).

- **Gây hại cho danh tiếng**: Ảnh hưởng xấu đến danh tiếng của trang web hoặc công ty.

- **Tạo điều kiện cho các cuộc tấn công khác**: Có thể tạo điều kiện cho các cuộc tấn công nghiêm trọng hơn như CSRF (Cross-Site Request Forgery).

## Mức độ rủi ro của lỗ hổng XSS
- **Tác động lên người dùng**: Mất thông tin cá nhân, tài khoản bị chiếm đoạt.

- **Tác động lên doanh nghiệp**: Tổn thất tài chính, mất lòng tin từ khách hàng, chịu phạt từ cơ quan quản lý.

- **Phát tán phần mềm độc hại**

- **Tấn công lừa đảo (Phishing)**

### Tác động của XSS trên máy chủ
- Người dùng có thể truy cập một cách độc lập vào trang có chứa **tập lệnh độc hại**

- **Đánh cắp dữ liệu** từ cơ sở dữ liệu thông qua người dùng

- **Làm giảm hiệu suất** và gây lỗi hệ thống

- **Phát tán sâu hơn** các cuộc tấn công

**Mức độ rủi ro: Cao**, tùy thuộc vào mức độ nhạy cảm của thông tin bị đánh cắp và quy mô của trang web.

## Cách phát hiện - Detect
- **Kiểm tra thủ công**: Nhập các đoạn mã độc hại vào các trường đầu vào `ví dụ: <script>alert(0)</script>` để xem kết quả hiển thị.

- **Sử dụng công cụ tự động**: Các công cụ như OWASP ZAP, Burp Suite, Acunetix để quét và phát hiện lỗ hổng.

- **Kiểm tra mã nguồn**: Kiểm tra và review mã nguồn để phát hiện các chỗ không xử lý đúng dữ liệu đầu vào và đầu ra.

## Khai thác - Exploit
- **Tạo các URL độc hại**: Tạo các URL chứa mã độc và lừa người dùng nhấp vào.

- **Gửi biểu mẫu độc hại**: Gửi các biểu mẫu có chứa mã độc tới trang web để lưu trữ hoặc phản hồi ngay lập tức.

- **Thực hiện tấn công DOM-based**: Chèn mã độc vào các trường đầu vào để thay đổi DOM của trang web.

## Cách ngăn chặn lỗ hổng XSS - Prevent
- **Kiểm tra và lọc dữ liệu đầu vào**: Sử dụng whitelist để chỉ chấp nhận những ký tự hợp lệ.

- **Mã hóa dữ liệu đầu ra**: Sử dụng các hàm mã hóa để đảm bảo rằng dữ liệu được hiển thị an toàn.

- **Sử dụng các công cụ bảo mật**: Sử dụng các framework bảo mật như OWASP ESAPI hoặc các tính năng bảo mật sẵn có của các framework như React, Angular.

- **Cập nhật thư viện** lên phiên bản mới nhất

- **Kiểm tra bảo mật** định kỳ và thường xuyên