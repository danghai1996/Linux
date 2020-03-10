# Install Word Press on CentOS 7


## 1. Tổng quan
WordPress là một hệ thống quản lí nội dung miễn phí và mã nguồn mở xây dựng dựa trên PHP và MySQL. Được phát hành vào năm 2003, đến nay WordPress đã trở thành một trong những hệ thống quản lí website phổ biến nhất thế giới với hơn 60 triệu website (số liệu năm 2019).

<img src = "https://i.imgur.com/gPZc09f.png">

## 2. Cài đặt
### **Bước 1: Chuẩn bị**

Đầu tiên, ta cần cài đặt bộ LAMP trên máy của bạn.
Có thể tham khảo tại [đây](https://news.cloud365.vn/huong-dan-cai-dat-lamp-tren-centos-7/)

### **Bước 2: Tạo cơ sở dữ liệu và tài khoản cho WP**

Ở bước chuẩn bị, mình đã cài Mariadb cho cơ sở dũ liệu. Bạn cũng có thể thao tác tương tự với MySQL.

Đăng nhập vào tài khoản root của database:
```
[root@localhost ~]# mysql -u root -p

Enter password:
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 11
Server version: 5.5.64-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>

```

Terminal chuyển sang MariaDB.

Ta tạo Database cho WP. Ở đây ta đặt là `testdbwp`
```
MariaDB [(none)]> CREATE DATABASE testdbwp;
Query OK, 1 row affected (0.00 sec)
```
Tạo tài khoản riêng để quản lí DB. Tên tài khoản: admin, Mật khẩu: admin
```
MariaDB [(none)]> CREATE USER admin@localhost IDENTIFIED BY 'admin';
Query OK, 0 rows affected (0.00 sec)
```

Bây giờ ta sẽ cấp quyền quản lí cơ sở dữ liệu cho user mới tạo:
```
MariaDB [(none)]> GRANT ALL PRIVILEGES ON testdbwp.* TO admin@localhost IDENTIFIED BY 'admin';
Query OK, 0 rows affected (0.00 sec)
```

Sau đó xác thực lại những thay đổi về quyền:
```
MariaDB [(none)]> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)
```

Sau đó, ta thoát ra khỏi MariaDB
```
MariaDB [(none)]> exit
Bye
```

### **Bước 3: Tải và cài đặt WordPress**
Cài gói hỗ trợ `php-gd`:
```
[root@localhost ~]# yum -y install php-gd
```

Tải xuống WordPress phiên bản mới nhất:
Nếu chưa cài đặt `wget` thì có thể cài bằng câu lệnh `# yum install wget`.
```
[root@localhost ~]# wget https://wordpress.org/latest.tar.gz
```
**Lưu ý:** Bạn cần để ý tới thư mục đang lưu trữ file wordpress đang được tải xuống. Ở đây mình lưu tại thư mục `/root`.

Ta sẽ giải nén file `latest.tar.gz`:
```
[root@localhost ~]# tar xvfz latest.tar.gz
```

**Lưu ý:** giải nén sẽ ra thư mục wordpress có đường dẫn `/root/wordpress`.

Copy các file trong thư mục WordPress tới đường dẫn `/var/www/html`
```
[root@localhost ~]# cp -Rvf /root/wordpress/* /var/www/html
```

### **Bước 4: Cấu hình WordPress**
Chuyển tới đường dẫn `/var/www/html`
```
[root@localhost ~]# cd /var/www/html
[root@localhost html]#
```

File cấu hình wordpress là `wp-config.php`. Tuy nhiên tại đây chỉ có file `wp-config-sample.php`. Tiến hành copy lại file cấu hình như sau:
```
[root@localhost html]# cp wp-config-sample.php wp-config.php
```

Mở file `wp-config.php` bằng `vi` để chỉnh sửa:
<img src = "https://i.imgur.com/et4biWR.png"> 

Chỉnh lại tên database, username, password đã đặt ở bước 2. (db_name: `testdbwp`, username: `admin`, pass: `admin`) và lưu lại.


### **Bước 5: Hoàn tất cài đặt giao diện**
Trên trình duyệt gõ địa chỉ IP server vào thành URL, ta được giao diện như sau:
<img src = "https://i.imgur.com/m6MGrHc.png">

Nhập các thông tin cần thiết rồi Install WordPress.
<img src = "https://i.imgur.com/YBCvUZz.png">

Như vậy là bạn đã thiết lập thành công. Tiến hành đăng nhập vào WordPress:
<img src = "https://i.imgur.com/5F4JMda.png">

Giao diện sau khi đăng nhập vào WordPress:
<img src = "https://i.imgur.com/Q6i1uGz.png">

### **Bước 6: Phân quyền thư mục WP**
Khi upload ảnh hay đăng bài viết sẽ xuất hiện lỗi sau:
<img src = "https://i.imgur.com/vKJPwqE.png">

Bạn cần phân quyền thư mục wordpress cho user apache để user này được phép tạo các thư mục và lưu trữ các tệp tin tải lên.
```
[root@localhost ~]# chown -R apache:apache /var/www/html/*
[root@localhost ~]# chmod -R 755 /var/www/html/*
```

Như vậy là bạn đã có thể tiến hành upload ảnh và đăng bài viết lên trang wordpress của mình.