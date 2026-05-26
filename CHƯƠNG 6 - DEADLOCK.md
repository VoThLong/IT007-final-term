# ÔN TẬP HỆ ĐIỀU HÀNH - CHƯƠNG 6: DEADLOCK

## 1. Bản chất của Deadlock
* **Định nghĩa:** Một tập các tiến trình bị block (đứng hình), mỗi tiến trình đang giữ tài nguyên và lại đi đợi một tài nguyên khác do một tiến trình trong tập đó giữ. Chúng đợi một sự kiện sẽ không bao giờ xảy ra.

## 2. Bốn điều kiện CẦN (Phải xảy ra đồng thời)
1. **Loại trừ tương hỗ (Mutual Exclusion):** Ít nhất 1 tài nguyên bị giữ ở chế độ độc quyền (non-sharable), không thể dùng chung cùng lúc (vd: máy in).
2. **Giữ và chờ (Hold and Wait):** Tiến trình đang ôm khư khư ít nhất 1 tài nguyên, nhưng vẫn há mồm đợi tài nguyên khác do kẻ khác giữ.
3. **Không trưng dụng (No Preemption):** Tài nguyên chỉ được nhả ra một cách tự nguyện bởi tiến trình đang giữ nó (sau khi nó chạy xong). HĐH không thể cưỡng chế giật lại.
4. **Chu trình đợi (Circular Wait):** Tồn tại một vòng lặp khép kín các tiến trình đợi tài nguyên của nhau: P0 đợi P1, P1 đợi P2,..., Pn đợi P0.

## 3. Ba Chiến Lược Giải Quyết Deadlock
| Chiến lược | Bản chất | Đặc điểm / Nhược điểm |
| :--- | :--- | :--- |
| **1. Ngăn ngừa (Prevention)** | Phá vỡ ít nhất 1 trong 4 điều kiện cần bằng luật cứng của HĐH. | Cực đoan, bóp nghẹt hệ thống, gây lãng phí tài nguyên khủng khiếp hoặc đói tài nguyên (Starvation). |
| **2. Tránh (Avoidance)** | HĐH cần tiến trình khai báo trước **tối đa** số tài nguyên sẽ dùng. HĐH linh hoạt check thuật toán (Banker) để luôn giữ hệ thống ở **Trạng thái an toàn (Safe State)**. | Đòi hỏi khai báo trước, thuật toán tốn overhead chạy nền. |
| **3. Phát hiện (Detection)** | Cứ cho chạy bét nhè, thi thoảng quét đồ thị xem có chu trình không. Có thì bẻ cổ (kill/rollback) tiến trình để giải quyết. | Dễ thở ban đầu, nhưng tốn chi phí rà quét và cực kì tốn kém/nguy hiểm khi phải Rollback dữ liệu. |

*Lưu ý: Nếu RAG (Đồ thị cấp phát) có chu trình + tài nguyên Single-instance -> Chắc chắn Deadlock. Nếu Multiple-instances -> Chưa chắc.*