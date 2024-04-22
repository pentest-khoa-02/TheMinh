### Mô hình MVC là gì?
* MVC là viết tắt của cụm từ “Model-View-Controller“. Đây là mô hình thiết kế được sử dụng trong kỹ thuật phần mềm. MVC là một mẫu kiến trúc phần mềm để tạo lập giao diện người dùng trên máy tính. MVC chia thành ba phần được kết nối với nhau và mỗi thành phần đều có một nhiệm vụ riêng của nó và độc lập với các thành phần khác. Tên gọi 3 thành phần:
  - Model (dữ liệu): Quản lí xử lí các dữ liệu.
  - View (giao diện): Nới hiển thị dữ liệu cho người dùng.
  - Controller (bộ điều khiển): Điều khiển sự tương tác của hai thành phần Model và View.
<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%202/MVC/image/MVC.webp" width="456px" align="center">

* Mô hình MVC (MVC pattern) thường được dùng để phát triển giao diện người dùng. Nó cung cấp các thành phần cơ bản để thiết kế một chương trình cho máy tính hoặc điện thoại di động, cũng như là các ứng dụng web.

### Một số mô hình khác MVC được sử dụng trong lập trình web:

* 1.MVP

  - Bao gồm 3 thành phần chính: Model, View, và Presenter.

  - Mô hình MVP có sự phân tách rõ ràng giữa Model và View. Mối liên kết duy nhất giữa View và Presenter là thông qua các dữ liệu.

  - Trong MVP, View là bộ phận có chức năng ủy thác đầu vào cho Presenter. Mỗi View đều có một liên kết với Presenter tương ứng thông qua giao diện.

  - Mô hình này thường được sử dụng khi không thể binding dữ liệu qua DataContext.
* 2.MVVM

  - Là mô hình bao gồm các thành phần: Model, View, ViewModel. Mô hình này có khả năng ràng buộc dữ liệu giữa 2 thành phần của hệ thống là View và ViewModel. Đây là chức năng giúp tách biệt rõ ràng giữa giao diện của người dùng và ứng dụng một cách logic.

  - MVVM thích hợp với WPF và Silverlight. Khi sử dụng MVVM cho WPF hay Silverlight, sẽ không có các thao tác xử lý sự kiện điển hình vốn được dùng trong code giao diện. Nó được sử dụng khi có thể binding dữ liệu qua DataContext.

  - Riêng đối với MVC, mô hình này được sử dụng khi MVVM hay MVP không phát huy hiệu quả trong quá trình lập trình web. Đa phần đó là tình huống mà View và những phần còn lại của chương trình không phải luôn luôn ở trạng thái available.
### Ưu và nhược điểm của mô hình MVC
* Ưu điểm:

  - Dễ dàng bảo trì mã, dễ dàng mở rộng và phát triển

  - Các thành phần của mô hình này có thể được kiểm tra hoàn toàn độc lập với người dùng

  - Dễ dàng hỗ trợ cho các khách hàng mới

  - Có thể thực hiện song song việc phát triển các thành phần khác nhau

  - Đơn giản hóa bằng cách chia web thành ba phần: Model, View, Controller

  - Chỉ sử dụng mẫu Front Controller để xử lý các yêu cầu của web thông qua một bộ điều khiển duy nhất

  - Hỗ trợ tốt nhất cho việc phát triển web theo hướng thử nghiệm

  - MVC hoạt động tốt với các ứng dụng được hỗ trợ bởi giới lập trình web

  - Thân thiện với công cụ tìm kiếm

  - Tất cả các đối tượng độc lập với nhau, do vậy bạn có thể kiểm tra một cách hoàn toàn riêng biệt.

  Không những vậy,  MVC  tương đối nhẹ và tiết kiệm diện tích băng thông bởi nó không cần sử dụng Viewstate. Điều đó giúp website hoạt động tốt và ổn định khi người dùng thực hiện quá nhiều thao tác tương tác như gửi hay nhận dữ liệu liên tục.
* Nhược điểm:
  - Khó đọc, thay đổi, kiểm tra đơn vị hoặc sử dụng lại mô hình này

  - Đôi lúc điều hướng khung có thể phức tạp vì nó giới thiệu các lớp trừu tượng mới, đòi hỏi người dùng phải thích ứng với các tiêu chí phân tách của MVC.

  - Không hỗ trợ việc xác thực chính thức

  - Vừa làm tăng sự phức tạp vừa làm giảm hiệu quả của dữ liệu

  - Gây khó khăn khi sử dụng với giao diện người dùng hiện đại

  - Bắt buộc phải có nhiều lập trình viên để tiến hành lập trình song song.

  - Cần có kiến ​​thức tổng hợp về công nghệ.

  - Bảo trì nhiều mã trong Bộ điều khiển

  MVC được sử dụng trong các dự án lớn. Với các dự án nhỏ, việc áp dụng mô hình MVC không được thích hợp bởi nó khá cồng kềnh. Nó cũng tiêu tốn nhiều thời gian để phát triển cũng như trung chuyển dữ liệu. Tuy nhiên, so với những mô hình khác, MVC vẫn là sự lựa chọn hàng đầu cho lập trình ứng dụng nói chung và cả lập trình web nói riêng.
### Vì sao nên sử dụng mô hình MVC?
* Quy trình phát triển nhanh hơn

  - MVC hỗ trợ phát việc phát triển nhanh chóng và song song. Nếu một mô hình MVC được dùng để phát triển bất kỳ ứng dụng web cụ thể nào, một lập trình viên có thể làm việc trên View và một developer khác có thể làm việc với Controller để tạo logic nghiệp vụ cho ứng dụng web đó.

  - Do đó, ứng dụng mô hình MVC có thể được hoàn thành nhanh hơn ba lần so với các ứng dụng mô hình khác.
* Khả năng cung cấp nhiều chế độ view
  - Trong mô hình MVC, bạn có thể tạo nhiều View cho chỉ một mô hình. Ngày nay, nhu cầu có thêm nhiều cách mới để truy cập ứng dụng và đang ngày càng tăng. Do đó, việc sử dụng MVC để phát triển chắc chắn là một giải pháp tuyệt vời.

  - Hơn nữa, với phương pháp này, việc nhân bản code rất hạn chế. Vì nó tách biệt dữ liệu và logic nghiệp vụ khỏi màn hình.
* Các sửa đổi không ảnh hưởng đến toàn bộ mô hình
  - Đối với bất kỳ ứng dụng web nào, người dùng có xu hướng thay đổi thường xuyên. Bạn có thể quan sát thông qua những thay đổi thường xuyên về màu sắc, font chữ, bố cục màn hình. Hay là thêm hỗ trợ thiết bị mới cho điện thoại hay máy tính bảng…

  - Việc thêm một kiểu view mới trong MVC rất đơn giản. Vì phần Model không phụ thuộc vào phần View. Do đó, bất kỳ thay đổi nào trong Model sẽ không ảnh hưởng đến toàn bộ kiến trúc.
* MVC Model trả về dữ liệu mà không cần định dạng
  - MVC pattern có thể trả về dữ liệu mà không cần áp dụng bất kỳ định dạng nào. Do đó, các thành phần giống nhau có thể được sử dụng với bất kỳ giao diện nào.

  - Ví dụ: tất cả loại dữ liệu đều có thể được định dạng bằng HTML. Ngoài ra, nó cũng có thể được định dạng bằng Macromedia Flash hay Dream Viewer.
* Hỗ trợ kỹ thuật Asynchronous
  - Kiến trúc MVC có thể được tích hợp với cả JavaScript Framework. Có nghĩa là, các ứng dụng MVC có thể hoạt động ngay cả với các file PDF, trình duyệt riêng cho web hay các widget trên desktop.

  - Ngoài ra, MVC cũng hỗ trợ kỹ thuật Asynchronous, giúp các developer phát triển các ứng dụng có thể load rất nhanh.
* Nền tảng MVC thân thiện với SEO
  - Nền tảng MVC hỗ trợ phát triển các trang web thân thiện với SEO. Bằng nền tảng này, bạn có thể dễ dàng phát triển các URL thân thiện với SEO để tạo ra nhiều lượt truy cập hơn.

  - Những ngôn ngữ như JavaScript hay jQuery có thể được tích hợp với MVC. Từ đó phát triển nhiều ứng dụng web giàu tính năng, đặc biệt là với mô hình MVC trong Java.
