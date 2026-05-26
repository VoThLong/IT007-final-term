# GIẢI MÃ BÀI TẬP THUẬT TOÁN BANKER (Trích Slide 66)

## 1. Dữ liệu ban đầu
* **Hệ thống có:** A(3), B(3), C(2), D(1) nằm trong Available.

| Tiến trình | Allocation (Đang giữ) | Max (Cần tối đa) | Need (Tính ra: Max - Alloc) |
| :--- | :--- | :--- | :--- |
| **P0** | 2 0 0 1 | 4 2 1 2 | 2 2 1 1 |
| **P1** | 3 1 2 1 | 5 2 5 2 | 2 1 3 1 |
| **P2** | 2 1 0 3 | 2 3 1 6 | 0 2 1 3 |
| **P3** | 1 3 1 2 | 1 4 2 4 | 0 1 1 2 |
| **P4** | 1 4 3 2 | 3 6 6 5 | 2 2 3 3 |

## 2. Check Trạng Thái An Toàn (Tìm Safe Sequence)
Khởi đầu với `Available = (3, 3, 2, 1)`
1. Quét tìm `Need <= Available`: Chọn **P0** (vì 2,2,1,1 <= 3,3,2,1).
2. P0 chạy xong, nhả Allocation. `Available` mới = (3,3,2,1) + (2,0,0,1) = **(5,3,2,2)**.
3. Quét tiếp: Chọn **P3** (vì 0,1,1,2 <= 5,3,2,2).
4. P3 chạy xong, nhả Allocation. `Available` mới = (5,3,2,2) + (1,3,1,2) = **(6,6,3,4)**.
5. Lúc này tài nguyên dồi dào, quét tiếp sẽ thấy P1, P2, P4 đều thỏa mãn.
**=> Hệ thống An toàn. Chuỗi hợp lệ: <P0, P3, P1, P2, P4>**

## 3. Xử lý Request đột ngột: P1 xin (1, 1, 0, 0)
Quy tắc 3 bước tử thần không được bỏ qua:
* **Bước 1 (Check Need):** (1, 1, 0, 0) <= Need P1 (2, 1, 3, 1). -> OK.
* **Bước 2 (Check Available):** (1, 1, 0, 0) <= Available hệ thống (3, 3, 2, 1). -> OK.
* **Bước 3 (Giả định cấp phát - Quan trọng nhất):**
    * `Available` hụt đi: (3,3,2,1) - (1,1,0,0) = **(2, 2, 2, 1)**
    * `Alloc` P1 phình ra: (3,1,2,1) + (1,1,0,0) = (4, 2, 2, 1)
    * `Need` P1 giảm đi: (2,1,3,1) - (1,1,0,0) = (1, 0, 3, 1)
* **Check Safe lại với Available = (2, 2, 2, 1):** * P0 có Need (2, 2, 1, 1) <= (2, 2, 2, 1). P0 mở đường được!
    * P0 chạy xong gom lại đồ thì dư dả cho các P khác.
**=> Kết luận: Duyệt cấp phát ngay cho P1 vì hệ thống vẫn nằm trong Safe State.**