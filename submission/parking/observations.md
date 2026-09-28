# Quan sát vạch ô đỗ

- Các `parking_line` được giữ: vạch chia ô ở tiền cảnh giữa ảnh (x≈408–531, y≈652–720) và vạch chia ô ở tiền cảnh bên phải (x≈697–960, y≈622–685). Có thêm đoạn sơn chia ô sát mép dưới bên trái (x≈25–29, y≈682–720).
- Vạch/biên không gán `parking_line`: dải trắng dài chạy gần ngang phía sau dãy ô, khoảng y≈508–542. Nó giống mép/ranh giới của dãy hơn là vạch chia hai ô riêng lẻ; không kéo thành `parking_line`.
- `free_space`: một polygon bao lối xe chạy nhìn thấy giữa dãy ô phía xa và các vạch chia ô ở tiền cảnh; polygon dừng trước các vạch chia ô phía trước. Không bao ô có xe đang đỗ hoặc bầu trời/cây phía sau bãi.
- Ca chưa chắc cần hỏi người soát: chưa có; nếu người soát không đồng ý với dải trắng dài ở ranh dãy, xem lại ảnh core và ảnh contrast cùng hướng dẫn parking.

## Export đã cập nhật

Task parking trong CVAT đã được thay bằng 3 polyline `parking_line` và 1 polygon `free_space`. Đã xem overlay trong job: polygon phủ lối xe chạy giữa hai dãy; ba polyline nằm trên vạch chia ô ở tiền cảnh. Đã export lại CVAT for images 1.1, tắt Save images, lưu ZIP tại `exports/hoang-parking.zip` và chạy `python lab11.py parking --file exports/hoang-parking.zip`; công cụ xác nhận 3 `parking_line`, 1 `free_space` trên đúng ảnh core.
