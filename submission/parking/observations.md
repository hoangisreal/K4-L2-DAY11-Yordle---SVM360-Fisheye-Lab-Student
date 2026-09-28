# Quan sát vạch ô đỗ

- Hai vạch `parking_line` đã vẽ (mô tả vị trí trong ảnh): Đã vẽ các vạch kẻ ô đỗ màu trắng xiên ở khu vực tiền cảnh (nửa dưới khung hình), đây là các vạch phân chia rõ ràng ranh giới giữa các ô đỗ xe riêng biệt.
- Một vạch/dấu sơn hoặc biên **không** vẽ, và vì sao: Không vẽ đường chân rào chắn/mép biên xa phía sau và các vạch mờ dẫn hướng ở hậu cảnh vì chúng không mang chức năng phân chia từng ô đỗ xe (stall divider).
- Polygon `free_space` dừng ở đâu; có phần bị che nào không: Polygon free_space chỉ bao phủ phần mặt đường nhựa trống của lối xe chạy chính giữa hai dãy ô đỗ, dừng lại ngay trước mép ngoài của các vạch chia ô đỗ (parking_line) và không đi xuyên vào bên trong ô đỗ hay vạch sơn.
- Ca chưa chắc cần hỏi người soát (nếu không có, ghi “không có”): không có
