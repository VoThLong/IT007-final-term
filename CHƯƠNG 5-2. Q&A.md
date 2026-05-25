### FILE 2: NGÂN HÀNG CÂU HỎI "GÀI BẪY" & ĐÁP ÁN

# BỘ CÂU HỎI ÔN TẬP TƯ DUY - HỆ ĐIỀU HÀNH (ĐÓNG TÀI LIỆU)

**Câu 1: Dùng Counting Semaphore để giải quyết Mutual Exclusion (Loại trừ tương hỗ) thì phải khởi tạo biến S bằng bao nhiêu? Tại sao?**
* **Đáp án:** Bắt buộc khởi tạo `S = 1`[cite: 259]. Vì Mutual Exclusion yêu cầu tại 1 thời điểm chỉ có DUY NHẤT 1 tiến trình ở trong Vùng tranh chấp. Nếu khởi tạo lớn hơn 1, nhiều tiến trình sẽ lọt qua hàm `wait()` và phá nát dữ liệu dùng chung.

**Câu 2: Nếu gọi lệnh in ra giá trị của biến Semaphore (loại có hàng đợi) và nhận được kết quả S = -4, con số này nói lên điều gì?**
* **Đáp án:** Có chính xác 4 tiến trình đang bị hệ thống block (ngủ) trong hàng đợi (Waiting Queue) của Semaphore này để chờ được cấp tài nguyên[cite: 332, 333].

**Câu 3 (Bounded-Buffer): Trong bài toán Bộ đệm có giới hạn, chuyện gì xảy ra nếu tiến trình Producer (Người sản xuất) gọi `wait(mutex)` TRƯỚC `wait(empty)` trong tình huống mảng buffer đang đầy?**
* **Đáp án:** Xảy ra **Deadlock**. Producer chiếm khóa `mutex` thành công nhưng bị ngủ ở `empty` vì hết chỗ. Consumer sau đó muốn vào lấy bớt dữ liệu để tạo chỗ trống thì bị kẹt ở `mutex` do Producer chưa nhả khóa. Cả 2 chờ nhau vô hạn. Điều kiện cốt lõi: Luôn phải chờ tài nguyên (trống/đầy) trước khi chờ khóa (mutex).

**Câu 4 (Dining-Philosophers): Giải pháp dùng mảng Semaphore cho 5 triết gia bị vướng lỗi thiết kế nào khiến toàn bộ hệ thống sập?**
* **Đáp án:** Nếu cả 5 triết gia cùng bốc đũa bên trái lên cùng một lúc [cite: 894, 896, 897], tất cả đều chờ chiếc đũa bên phải của mình (đang bị người bên phải cầm). Vòng tròn chờ đợi này sinh ra Deadlock.

**Câu 5 (Dining-Philosophers): Giải thuật Monitor cho phép 1 triết gia cầm đũa nếu 2 người kế bên KHÔNG ăn (`state[(i+4)%5] != EATING` và `state[(i+1)%5] != EATING`). Tại sao vẫn xảy ra Starvation (Đói)?**
* **Đáp án:** Vì giải thuật không cấp độ ưu tiên hay bộ đếm thời gian chờ. Nếu ông số 1 và số 3 **luân phiên** nhau ăn (ông 1 bỏ đũa xuống thì ông 3 bốc lên và ngược lại), điều kiện để ông số 2 được ăn (cả 1 và 3 cùng không ăn) sẽ không bao giờ thỏa mãn, khiến ông số 2 bị đói vĩnh viễn dù hệ thống vẫn đang hoạt động.