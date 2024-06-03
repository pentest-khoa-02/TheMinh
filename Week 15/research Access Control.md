## Lỗ hổng Access Control là gì?
- **Access control - Kiểm soát truy cập** là việc áp dụng các ràng buộc về ai hoặc cái gì được ủy quyền để thực hiện các hành động hoặc truy cập tài nguyên. Trong ngữ cảnh của ứng dụng web, kiểm soát truy cập phụ thuộc vào xác thực và quản lý phiên:
    - **Authentication - Xác thực**: xác nhận rằng người dùng chính là người họ nói.

    - **Session management - Quản lý phiên**: xác định những yêu cầu HTTP tiếp theo nào đang được thực hiện bởi cùng một người dùng.

    - **Access control - Kiểm soát truy cập**: xác định xem người dùng có được phép thực hiện hành động mà họ đang cố gắng thực hiện hay không.

- **Broken Access Control - Kiểm soát truy cập bị phá vỡ** là lỗi phổ biến và thường gây ra lỗ hổng bảo mật nghiêm trọng. Các lỗi bảo mật xảy ra khi hệ thống không áp dụng hoặc không thực thi đúng các cơ chế kiểm soát quyền truy cập. Điều này cho phép người dùng truy cập trái phép vào các tài nguyên hoặc chức năng mà họ không được phép truy cập.

<p align="center">
<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%2015/images/1.png" width="666px">
</p>

## Các loại lỗ hổng Access Control
**Horizontal Access Controls - Kiểm soát truy cập theo chiều ngang**: Người dùng truy cập vào tài nguyên của người dùng khác có cùng mức độ quyền.

```
https://developers.redhat.com/author?Id=273801

https://developers.redhat.com/author?Id=273802
```

**Vertical Access Controls - Kiểm soát truy cập theo chiều dọc**: Người dùng có quyền truy cập vào chức năng hoặc tài nguyên mà chỉ người dùng cấp cao hơn mới được phép truy cập.

```
https://developers.redhat.com/contributor/dashboard

​​​​​​​https://developers.redhat.com/admin/dashboard
```

**Context-dependent Access Controls - Kiểm soát truy cập phụ thuộc vào ngữ cảnh**: Kiểm soát quyền truy cập dựa trên ngữ cảnh không đủ chặt chẽ, cho phép người dùng truy cập vào tài nguyên hoặc chức năng mà họ không nên có quyền, tùy thuộc vào ngữ cảnh cụ thể.

- **Insecure Direct Object References (IDOR)**: Truy cập trực tiếp vào các đối tượng dựa trên tham số không an toàn.

## Nguyên nhân
- **Thiếu kiểm tra quyền truy cập:** Không kiểm tra quyền truy cập tại tất cả các điểm mà người dùng tương tác với hệ thống.

- **Phân quyền không đúng cách:** Cấp quyền truy cập cho người dùng hoặc nhóm người dùng không phù hợp.

- **Lỗi lập trình:** Các lỗi lập trình dẫn đến việc bỏ qua hoặc thực thi sai các cơ chế kiểm soát quyền truy cập.

## Hậu quả
- **Rò rỉ dữ liệu nhạy cảm:** Người dùng trái phép có thể truy cập và lấy cắp thông tin nhạy cảm.

- **Thay đổi dữ liệu trái phép:** Dữ liệu có thể bị sửa đổi hoặc xóa bỏ bởi người dùng không có quyền.

- **Leo thang đặc quyền:** Hacker có thể leo thang đặc quyền gây ra các tác động nghiêm trọng, ảnh hưởng đến toàn bộ hệ thống và dữ liệu trên server

- **Tấn công hệ thống:** Lỗ hổng có thể được sử dụng để thực hiện các cuộc tấn công khác.

- **Mất uy tín và tổn thất tài chính:** Các tổ chức có thể phải chịu tổn thất tài chính lớn và mất uy tín với khách hàng.

## Chức năng thường tồn tại lỗ hổng
- Các trang quản trị (Admin pages)

- Các chức năng CRUD (Create, Read, Update, Delete)

- Trang thông tin cá nhân và các chức năng quản lý tài khoản

- Chức năng tải lên và quản lý tệp tin

## Cách phát hiện
- **Kiểm tra logic ứng dụng**: Đánh giá xem các quy tắc kiểm soát truy cập có được thực thi đúng cách hay không.

- **Phân tích quyền truy cập**: Kiểm tra và đánh giá cấu hình quyền truy cập của các thành phần hệ thống.

- **Kiểm tra mã nguồn**: Xem xét mã nguồn để phát hiện các lỗi liên quan đến quyền truy cập.

- **Kiểm tra bảo mật**: Sử dụng các công cụ kiểm tra bảo mật tự động và thử nghiệm thủ công để phát hiện lỗ hổng.

## Khai thác lỗ hổng Access Control
- **Tấn công thủ công**: Thử nghiệm và thay đổi các tham số truy vấn để truy cập trái phép vào các tài nguyên hoặc chức năng không được phép.

- **Sử dụng công cụ tấn công**: Các công cụ như Burp Suite hoặc OWASP ZAP có thể được sử dụng để tự động phát hiện và khai thác lỗ hổng.

## Phương pháp kiểm soát truy cập
*Có ba phương pháp chung để thực hiện kiểm soát truy cập logic trong hệ thống phần mềm:* 

**Discretionary access control (DAC) - Kiểm soát truy cập tùy ý** là một phương tiện hạn chế quyền truy cập vào các đối tượng (ví dụ: tệp, thực thể dữ liệu) dựa trên danh tính và nhu cầu biết của các chủ thể (ví dụ: người dùng, quy trình) và/hoặc nhóm mà đối tượng đó thuộc về. Hầu hết các hệ điều hành đều triển khai loại kiểm soát truy cập này.

**Role-based access control (RBAC) - Kiểm soát truy cập dựa trên vai trò** là một mô hình để kiểm soát quyền truy cập vào tài nguyên trong đó các hành động được phép đối với tài nguyên được xác định bằng vai trò thay vì bằng danh tính chủ thể riêng lẻ.
- Ví dụ: các chuyên gia nhân sự về nhân sự không được phép tạo tài khoản mạng.

**Managed access control (MAC)- Kiểm soát truy cập được quản lý** là một phương tiện hạn chế quyền truy cập vào tài nguyên hệ thống dựa trên độ nhạy cảm (như được biểu thị bằng nhãn) của thông tin có trong tài nguyên hệ thống và ủy quyền chính thức (nghĩa là cho phép) của người dùng để truy cập thông tin đó nhạy cảm. Ngay cả khi một người vượt qua các hạn chế bảo mật khác, MAC vẫn kiểm tra các thẻ.

## Cách ngăn chặn
- Đừng bao giờ chỉ dựa vào tính năng che giấu để kiểm soát quyền truy cập.

- Mặc định, hãy từ chối quyền truy cập.

- Sử dụng kiểm soát truy cập dựa trên vai trò (RBAC) để áp đặt các giới hạn thích hợp cho từng vai trò. 

- Sử dụng một cơ chế toàn ứng dụng duy nhất để thực thi các biện pháp kiểm soát truy cập.

- Kiểm tra kỹ lưỡng và kiểm tra các biện pháp kiểm soát quyền truy cập để đảm bảo chúng hoạt động như thiết kế.

- Kiểm tra quyền truy cập ở mọi tầng: ở cả phía máy chủ và phía người dùng.

- Sử dụng các framework bảo mật.

- Đánh giá và kiểm tra thường xuyên.