# CronTab

## CronTab là gì?
Crontab là nơi lưu trữ tất cả các dòng lệnh đã lập lịch sẵn. Nó sẽ tự động chạy các lệnh đó khi đến thời gian đã định trước hoặc theo đúng chu khì đã định.

## Cấu trúc của CronTab
Mỗi crontab có 5 trường để xác định lịch trình thực hiện.

<img src = "https://i.imgur.com/gvKEBYv.png">

Nếu 1 cột được để giá trị là `*` thì có nghĩa là câu lệnh sau đó sẽ được thực hiện tại mọi thời điểm tương ứng với vị trí đó.

Ví dụ:
- `0,20,40 * * * * <câu_lệnh>` : câu lệnh sẽ thực hiện tại các phút thứ 0, phút thứ 20, phút thứ 40.
- `*/20 * * * * <câu_lệnh>` : câu lệnh sẽ thực hiện 20 phút 1 lần tính từ khi hoàn thành lệnh.
- `20 14 * * 1,2,3,4,5 <câu_lệnh>` : câu lệnh sẽ thực hiện vào lúc 14h20p các ngày từ thứ 2 đến thứ 6 trong tuần.

**Chú ý:** Khi thêm `@reboot <câu_lệnh>` : câu lệnh sẽ thực hiện ngay khi hệ thống khởi động.


## Một số câu lệnh để thao tác với Crontab
1. `crontab -l` : Hiển thị file crontab
2. `crontab -r` : Xóa file crontab
3. `crontab -e` : Tạo hoặc chỉnh sửa file crontab

Nếu máy chưa được cài đặt sẵn `crontab` thì khi ta dùng lệnh `crontab -l` sẽ hiển thị:
```
-bash: crontab: command not found
```

Ta cài đặt crontab và khởi động nó:
```
[root@localhost ~]# yum install cronie
[root@localhost ~]# systemctl start crond.service
[root@localhost ~]# systemctl enable crond.service
[root@localhost ~]# systemctl status crond.service
```

## Ví dụ về Crontab
Tạo `crontab` chạy file `date.sh` để ghi thông tin thời gian vào file `date.log `.

Tạo 1 file `date.sh` có tác dụng in ra thời gian hệ thống có nội dung như sau:
```
[root@localhost ~]# cat date.sh

#!/bin/bash
echo $(date) >> /root/date.log
```

Thêm crontab chạy file `date.sh`:
```
[root@localhost ~]# crontab -e
```

Ta sẽ để cứ 1 phút sẽ ghi thông tin thời gian hệ thống 1 lần:
```
*/1 * * * * sh /root/date.sh
```

Vậy là đã xong. Sau vài phút ta kiểm tra file `date.log` sẽ có kết quả tương tự như sau:
```
[root@localhost ~]# cat date.log

Sat Dec 21 14:08:01 +07 2019
Sat Dec 21 14:09:01 +07 2019
Sat Dec 21 14:10:01 +07 2019
Sat Dec 21 14:11:01 +07 2019
Sat Dec 21 14:12:01 +07 2019
Sat Dec 21 14:13:01 +07 2019
Sat Dec 21 14:14:01 +07 2019
Sat Dec 21 14:15:01 +07 2019
```