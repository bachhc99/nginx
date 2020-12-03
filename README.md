# nginx
## Nội dung bài viết.
- [I. NGINX là gì? NGINX hoạt động ntn?](#1)
- [II. Cách cài đặt NGINX cho ubuntu.](#2)

## I.NGINX là gì? NGINX hoạt động ntn?<a name="1"></a>
## 1.Sự ra đời của NGINX.
NGINX chính thức ra đời vào tháng 10/2014. Đây là phần mềm giúp server có tốc độ và khả năng mở rộng lớn nhất, đồng thời, xử lý và thao tác trên hàng nghìn kết nối cùng lúc. Do đó, rất nhiều “ông lớn” công nghệ hiện nay đều lựa chọn NGINX như Google, Adobe, Netflix, WordPress…
## 2.NGINX là gì?
NGINX là một phần mềm web server mã nguồn mở, sử dụng kiến trúc hướng sự kiện (event-driven) không đồng bộ (asynchronous). Mục tiêu ban đầu để phục vụ HTTP cache nhưng sau được áp dụng vào reverse proxy, HTTP load balancer và các giao thức truyền mail như IMAP4, POP3, và SMTP.
Vậy chúng ta có thêm 1 vài khái niệm mới như POP3,SMTP,IMAP mình sẽ nói qua 1 chút về nó nhé 
Đầu tiên là POP3:
POP3 được sử dụng để kết nối tới server email và tải email xuống máy tính cá nhân thông qua ứng dụng email client như Outlook, Thunderbird, Windows Mail, Mac Mail…
<img src="https://wikimatbao.azureedge.net/wp-content/uploads/2019/07/pop3-l%C3%A0-g%C3%AC.png">.


Thông  thường, email client sẽ có tùy chọn bạn có muốn giữ mail trên server sau khi tải về hay không. Nếu bạn đang truy cập một tài khoản bằng nhiều thiết, chúng tôi khuyên là nên chọn giữ lại bản copy trên server nếu không thiết bị thứ 2 sẽ không thể tải mail về được vì nó đã bị xóa sau khi tải về trên thiết bị 1.

Cũng đáng để lưu ý là POP3 là giao thức 1 chiều, có nghĩa là email được “kéo” từ email server từ xa xuống email client.
Tiếp theo là IMAP:
IMAP là viết tắt của Internet Message Access Protocol, là giao thức chuẩn Internet được sử dụng bởi các ứng dụng email để truy xuất thư email từ máy chủ thư qua kết nối TCP/IP.
Giống như POP3, IMAP cũng  được dùng để kéo email về emails client, tuy nhiên khác biệt với POP3 là nó chỉ kéo email headers về, nội dung email vẫn còn trên server. Đây là kênh liên lạc 2 chiều, thay đổi trên mail client sẽ được chuyển lên server.
Port IMAP mặc định:

Port 143 – port không mã hóa
Port 993 – SSL/TLS port, cũng có thể được gọi là IMAPS
Để Website trở nên chuyên nghiệp thì việc sử dụng Email theo tên miền riêng là một trong những việc cần phải thực hiện ngay. Bạn có thể tìm hiểu thêm về dịch vụ này tại Mắt Bão để được hỗ trợ tư vấn.

Chúng ta cùng tiếp tục tìm hiểu SMPT là gì nhé.
SMTP được dùng để liên lạc với server từ xa và gửi email từ mail client tới mail server và sau đó được gửi đến server mail của email nhận. Quá trình này được điều khiển bởi Mail Transfer Agent (MTA) trên email server của bạn. Cũng vậy, SMTP chỉ được dùng cho mục đích gửi email.
<img src="https://wikimatbao.azureedge.net/wp-content/uploads/2019/07/smtp-la-gi.png">.

SMTP ports:

Port 25 – port không mã hóa
Port 465 – SSL/TLS port, cũng có thể được gọi là SMTPS
## 3.Vậy thì NGINX hoạt động ntn?
Về cơ bản, NGINX cũng hoạt động tương tự như các web server khác. Khi bạn mở một trang web, trình duyệt của bạn sẽ liên hệ với server chứa website đó. Server sẽ tìm kiếm đúng file yêu cầu của website và gửi về cho bạn. Đây là một trình tự xử lý dữ liệu single – thread, nghĩa là các bước được thực hiện theo một trình tự duy nhất. Mỗi yêu cầu sẽ được tạo một thread riêng.

Tuy nhiên, NGINX hoạt động theo kiến trúc bất đồng bộ (asynchronous) hướng sự kiện (event driven). Nó cho phép các threads tương đồng được quản lý trong một tiến process. Mỗi process hoạt động sẽ bao gồm các thực thể nhỏ hơn, gọi là worker connections dùng để xử lý tất cả threads.

Worker connections sẽ gửi các yêu cầu cho worker process, worker process sẽ gửi nó tới master process, và master process sẽ trả lời các yêu cầu đó. Đó là lý do vì sao một worker connection có thể xử lý đến 1024 yêu cầu tương tự nhau. Nhờ vậy, NGINX có thể xử lý hàng ngàn yêu cầu khác nhau cùng một lúc.
# II.Cách cài đặt NGINX cho ubuntu.<a name="2"></a>
## 1.Đầu tiên, tiến hành update các gói trong hệ thống :
```
sudo apt install -y update
```
Cài đặt Nginx cho máy chủ Ubuntu của bạn :

```
sudo apt install -y nginx
```
Kiểm tra phiên bản Nginx:
```
sudo nginx -v
nginx version: nginx/1.17.10 (Ubuntu)
```
Cho phép Nginx khởi động cùng hệ thống :
```
sudo systemctl enable nginx
```
Khởi động và kiểm tra trạng thái của dịch vụ Nginx :

```
systemctl start nginx 
systemctl status nginx
```
```
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2020-04-27 09:34:14 +07; 5min ago
       Docs: man:nginx(8)
   Main PID: 7569 (nginx)
      Tasks: 5 (limit: 2318)
     Memory: 6.0M
     CGroup: /system.slice/nginx.service
             ├─7569 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
             ├─7570 nginx: worker process
             ├─7571 nginx: worker process
             ├─7572 nginx: worker process
             └─7573 nginx: worker process

Thg 4 27 09:34:14 Ubuntulab systemd[1]: Starting A high performance web server and a reverse proxy server...
Thg 4 27 09:34:14 Ubuntulab systemd[1]: Started A high performance web server and a reverse proxy server.
```
## 2.Bước tiếp theo cấu hình tường lửa.
Sử dụng ufw để biết cách sử dụng cấu hình tường lửa cho Nginx :
```
sudo ufw app list 
```
nó sẽ có đầu ra như sau :
```
Available applications:
  CUPS
  Nginx Full
  Nginx HTTP
  Nginx HTTPS
  OpenSSH
```
Ta thấy rằng đối với nginx, có 3 cấu hình có thể để cấu hình cho nginx, nhưng hiện tại mình chưa có cấu hình sử dụng SSL đối với trang web nên mình chỉ cho lưu lượng đi qua port 80.

Kích hoạt điều trên bằng cách sử dụng câu lệnh sau:
```
sudo ufw allow 'Nginx HTTP'
```
Sau đó kiểm tra lại thay đổi với lệnh sau:
```
sudo ufw status
```
## 3.Bước 3: Kiểm tra trang web.
Để kiểm tra trang web, ta mở trình duyệt và nhập vào địa chỉ ip của máy chủ Nginx.
```
http://IP_address 
```
ta sẽ được điều hướng đến trang web mặc định của Nginx :
<img src="https://news.cloud365.vn/wp-content/uploads/2020/04/image-116.png">.
Khi bạn hiển thị như này tức là đã cài đặt thành công và nginx đã sẵn sàng để được quản lý.

Nginx với nhiều tính năng mở rộng có thể là 1 ứng dụng tuyệt vời đối với hệ thống của bạn. Trong hướng dẫn này mình đã hướng dẫn các bạn cách cài đặt Nginx cho Ubuntu 20.04, để tham khảo nhiều hơn nữa các tính năng cũng như giải pháp sử dụng Nginx cho hệ thống của mình.
