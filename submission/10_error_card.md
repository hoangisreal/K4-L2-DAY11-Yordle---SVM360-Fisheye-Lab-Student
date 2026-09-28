# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B4 | MISSING | 2 |
| center | B4 | SPURIOUS | 2 |
| center | B4 | WRONG_CLASS | 2 |
| center | C0 | SPURIOUS | 1 |
| edge | B4 | BOX_GEOMETRY | 1 |
| edge | B4 | DUPLICATE | 2 |
| edge | B4 | MISSING | 3 |
| edge | B4 | SPURIOUS | 2 |
| edge | C0 | SPURIOUS | 1 |
| edge | C0 | WRONG_CLASS | 1 |
| mid | B4 | BOX_GEOMETRY | 3 |
| mid | B4 | MISSING | 4 |
| mid | B4 | SPURIOUS | 14 |
| mid | B4 | WRONG_CLASS | 2 |
| unknown | B4 | IGNORE_SCOPE | 1 |

## Top defects
- SPURIOUS: 20 (ví dụ frame adasind_019560.jpg)
- MISSING: 9 (ví dụ frame adasind_258420.jpg)
- WRONG_CLASS: 5 (ví dụ frame adasind_019560.jpg)

## Phân tích của bạn

Các bảng là số đếm của những dòng finding, không phải số lỗi độc lập hay tỷ lệ lỗi. Local quality của bản r1 đối teaching reference là TP=15, FP=6, FN=5; mean IoU của TP=0.820. Car là nhãn yếu nhất theo precision (0.333) và recall (0.500); ThreeWheeler recall là 0.500. Ở `adasind_258420.jpg` có TP=5/FP=4/FN=3, trong khi `adasind_236370.jpg` có TP=7 và không có FP/FN. Khi IoU tăng từ 0.30 lên 0.70, số matched L ở mid giảm 7→4 và spurious tăng 4→7; kết quả nhạy với ngưỡng/geometry. Các số này mô tả phép so vài frame, không phải điểm rubric.

Ở slice B4-edge, tín hiệu cần ưu tiên cho model là các proposal chồng lên xe ba bánh nhưng mang nhiều class: tại `adasind_258420.jpg`, M4 gọi auto-rickshaw mép trái là `Truck`, M8 gọi xe ba bánh giữa ảnh là `Truck`, M11 gọi xe bên phải là `Car`; tại `adasind_310008.jpg`, M6/M7 cùng chồng lên xe ba bánh nhưng lần lượt là `Truck` và `Bus`. R04 quy định các xe này là `ThreeWheeler`. Nhiều proposal trên cùng vật có thể vừa làm tăng `SPURIOUS` vừa làm người gán nhãn nhầm rằng có thêm vật.

- **Nguyên nhân khả dĩ (`why`):** các finding M4/M8/M11/M6/M7 được ghi `E4_model_domain` như giả thuyết vì các xung đột class lặp lại trên ảnh fisheye. Ba frame chỉ đủ nêu vấn đề ở các ví dụ này, chưa chứng minh nguyên nhân tổng quát hay tỷ lệ lỗi của model.
- **Cách sửa và owner:** giữ nhãn người theo vật nhìn thấy và R04; không chép các proposal model thành vật mới. `ai_team` nên kiểm class confusion và proposal trùng trên một tập fisheye ThreeWheeler lớn hơn, có nhãn đã phân xử độc lập. Hoàng đã sửa các lỗi nhãn người P1 chắc chắn ở P5; `qa` cần phân xử box Car L3/R5 và các box nhỏ L2/L7/L8 còn mở ở frame 258420 (Ticket 2).
- **Bằng chứng:** `submission/r3_diag/model_compare.md`, các dòng M4/M8/M11/M6/M7 trong `submission/findings.csv`, R04 tại `docs/02-rules-vi.md`, và ảnh cảnh gốc `submission/screenshots/hoang-cvat-threewheeler-258420-early.png` (ảnh CVAT sớm, dùng nhận diện cảnh; báo cáo model là bằng chứng class M).
