# iSCSI

## 1. iSCSI là gì?
**iSCSI** là **Internet SCSI** (*Small Computer System Interface*) : là một giao thức cho phép truyền tải các lệnh SCSI qua mạng IP bằng cách sử dụng giao thức TCP/IP. Nó truy cập thiết bị lưu trữ theo dạng block-level là truy cập theo từng khối.

Lệnh iSCSI được đóng gói trong lớp TCP/IP và truyền qua mạng nội bộ LAN hoặc cả qua mạng Internet Public mà không cần quan tâm đến các thiết bị chuyện biệt như Fiber Channel, chỉ cần cấu hình đúng Gigabit ethernet và iSCSI.

iSCSI sử dụng không gian nhớ ảo như LUN trên linux, VHD’s trên windows, giảm chi phí vì sử dụng các thiết bị sẵn có như switch, hub, router, …