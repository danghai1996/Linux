# S5.3 - `INNER JOIN`

Trong bài viết này, ta sẽ tìm hiểu cách sử dụng mệnh đề `INNER JOIN` để lấy dữ liệu từ nhiều bảng dựa trên các điều kiện.

## Chức năng
`INNER JOIN` khớp từng hàng trong 1 bảng với mỗi hàng trong bảng khác và cho phép bạn truy vấn các hàng có chứa các cột chung từ 2 bảng.

## Cú pháp cơ bản
```
SELECT
    select_list
FROM t1
INNER JOIN t2 ON join_condition1
INNER JOIN t3 ON join_condition2
...;
```

Trong đó:
- Bảng chính là `t1`
- Bảng chỉ định sẽ được nối với bảng chính: `t2`, `t3`, ...
- Điều kiện nối xác định quy tắc khớp các hàng của bảng chính với các bảng chỉ định.

Sơ đồ Venn minh họa cách hoạt động của `INNER JOIN`:
<img src = "https://i.imgur.com/2tLh5xM.png">

## Ví dụ về cách sử dụng
Ta sử dụng 2 bảng `products` và `productlines`:
<img src ="https://i.imgur.com/5NK3aOy.png">

Theo sơ đồ, ta thấy bảng `products` có cột `productLine` tham chiếu giá trị của cột `productLine` của bảng `productlines`. Cột `productLine` trong bảng `products` được gọi là khóa ngoại.

**Yêu cầu**: 
- Lấy `productCode` và `productName` từ bảng `products`
- Lấy `textDescription` của dòng sản phẩm từ bảng `productlines`

