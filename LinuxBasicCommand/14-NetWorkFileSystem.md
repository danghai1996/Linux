# Network File System (NFS)

## Giới thiệu
NFS ( Network File System ) về cơ bản được phát triển để chia sẻ các tệp và thư mục giữa các hệ thống Linux Unix bởi Sun microsystems vào năm 1980. Nó cho phép bạn gắn kết các hệ thống tệp cục bộ của mình qua mạng và các máy chủ từ xa để tương tác với chúng khi chúng được gắn cục bộ trên cùng một hệ thống.

## Lợi ích của NFS
- NFS cho phép truy cập cục bộ vào các tệp từ xa.
- Nó sử dụng kiến trúc client/server tiêu chuẩn để chia sẻ tệp giữa các máy
- Với NFS , không cần thiết cả hai máy đều chạy trên cùng một hệ điều hành.
- Với sự trợ giúp của NFS, có thể định cấu hình các giải pháp lưu trữ tập trung.
- Người dùng có được dữ liệu của họ bất kể vị trí thực tế.
- Không cần làm mới thủ công cho các tập tin mới.
- Phiên bản mới hơn của NFS cũng hỗ trợ *acl*, *mount root* ảo.
- Có thể được bảo mật với Tường lửa và [Kerberos](https://vi.wikipedia.org/wiki/Giao_th%E1%BB%A9c_Kerberos).

## Dịch vụ NFS
Đây là một System V-launched. NFS bao gồm `portmap` và `nfs-utils package`:

- `portmap`: Nó ánh xạ các cuộc gọi được thực hiện từ các máy khác đến dịch vụ RPC chính xác (không bắt buộc với NFSv4 ).
- `nfs`: Nó dịch các yêu cầu chia sẻ tệp từ xa thành các yêu cầu trên hệ thống tệp cục bộ.
- `rpc.mountd`: Dịch vụ này có trách nhiệm lắp và unmount toàn bộ các hệ thống tập tin.

## Các tệp quan trọng cho cấu hình NFS
- `/etc/export`: Đây là tệp cấu hình chính của NFS, tất cả các tệp và thư mục đã xuất được xác định trong tệp này ở cuối Máy chủ NFS.
- `/etc/fstab`: Để gắn một thư mục NFS trên hệ thống của bạn trên các lần khởi động lại , chúng ta cần tạo một mục trong /etc/fstab.
- `/etc/sysconfig/nfs`: Tệp cấu hình của NFS để kiểm soát cổng rpc và các dịch vụ khác đang nghe.

## Triển khai NFS
### Mô hình
2 máy CentOS-7:
- Client
- Server

Cài đặt và cấu hình NFS để chia sẻ giữa Client với Server.

### Cài đặt NFS trên NFS_Client và NFS_Server
`# yum install -y nfs-utils`

### IP của 2 máy
|Hostname|Network|Interface|IP Address|NetMask|Gateway|DNS|
|-|-|-|-|-|-|-|
|Client|||||||
|Server|||||||