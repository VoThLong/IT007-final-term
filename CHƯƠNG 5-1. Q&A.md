### Tài liệu 2: Tổng hợp Câu hỏi Luyện tập & Đánh đố

# TỔNG HỢP CÂU HỎI & ĐÁP ÁN - ĐỒNG BỘ TIẾN TRÌNH

**Câu 1 (Race Condition cấp độ Assembly)**
* **Hỏi:** Theo dõi luồng thực thi đan xen giữa Producer và Consumer từ T1 đến T6 (Quantum Time ngắt giữa chừng). Kết quả `count` cuối cùng là bao nhiêu và tiến trình nào bị "mất dấu" kết quả?
* **Đáp án:** Giá trị `count` cuối cùng trong bộ nhớ bằng 6[cite: 138, 143, 144, 150, 151]. Tiến trình Consumer bị mất dấu cập nhật (lost update) vì giá trị 4 mà nó vừa ghi xuống [cite: 159, 160, 162, 163] đã lập tức bị Producer ghi đè bằng giá trị 6 ngay ở bước tiếp theo[cite: 150, 151].

**Câu 2 (Cạm bẫy Bộ nhớ & Hàm fork)**
* **Hỏi:** Một đoạn code C sử dụng `fork()` sinh tiến trình cha và con. Cả hai cùng gọi hàm giảm một biến toàn cục chung. Có xảy ra Race Condition không?
* **Đáp án:** KHÔNG. Hàm `fork()` tạo ra tiến trình con có không gian bộ nhớ nhân bản nhưng độc lập hoàn toàn với cha. Biến toàn cục nằm ở hai địa chỉ vật lý khác nhau, do đó không thỏa mãn điều kiện tranh chấp "dữ liệu được chia sẻ", không sinh ra Race Condition[cite: 224, 225].

**Câu 3 (Biến dùng chung của Kernel)**
* **Hỏi:** Bài toán cấp phát PID chỉ ra `next_available_pid` có thể gây Race Condition[cite: 202, 204, 205]. Tại sao hai tiến trình độc lập bộ nhớ lại tranh chấp được biến này? Nó nằm ở đâu?
* **Đáp án:** Biến này là tài nguyên dùng chung nằm ở Kernel (không gian lõi Hệ điều hành). Lời gọi `fork()` là một System Call, khiến các tiến trình yêu cầu tài nguyên dưới mức Kernel đồng thời nên mới dẫn đến tranh chấp[cite: 197, 204, 216].

**Câu 4 (Vi phạm tiêu chuẩn Progress)**
* **Hỏi:** Giải pháp phần mềm 1 (dùng biến `turn`) vi phạm tiêu chuẩn Progress như thế nào? 
* **Đáp án:** Xảy ra khi tiến trình P0 nhường `turn` cho P1 và thoát ra ngoài làm việc riêng (Remainder Section). Nếu P1 ở bên ngoài vô thời hạn và không có nhu cầu vào Vùng tranh chấp, lệnh trả `turn` về lại cho P0 sẽ vĩnh viễn không chạy. Hậu quả là P1 đang ở ngoài nhưng lại cản trở P0 muốn vào Vùng tranh chấp lần nữa[cite: 460, 477, 478, 481, 482, 483]. 

**Câu 5 (Rủi ro Kiến trúc Hiện đại)**
* **Hỏi:** Nếu thuật toán Peterson bị CPU đảo ngược thứ tự thực thi 2 lệnh độc lập (`turn` gán trước, `flag` gán sau), tiêu chuẩn Mutual Exclusion có bị phá vỡ không?
* **Đáp án:** CÓ. Do việc gán `flag` bị đẩy xuống sau, khi tiến trình P1 xét điều kiện vào lặp `while`, nó thấy `flag` của P0 vẫn đang là `false` nên chui thẳng vào CS. P0 chạy sau cũng xét điều kiện tương tự và lọt vào CS do `turn` đã bị đổi. Hậu quả là 2 tiến trình cùng nằm trong Vùng tranh chấp[cite: 747, 748, 749].

**Câu 6 (Khóa Mutex & Deadlock)**
* **Hỏi:** Mutex lock đang được khóa (`acquire`), tiến trình đang ở trong Critical Section thì bị ép kết thúc đột ngột (`terminate`) trước khi kịp gọi `release()`. Chuyện gì sẽ xảy ra?
* **Đáp án:** Khóa vĩnh viễn không được mở. Toàn bộ các tiến trình/người dùng khác khi gọi hàm xin khóa `acquire()` sẽ bị chặn lại vĩnh viễn, dẫn đến tình trạng treo hệ thống, Deadlock hoặc Starvation.