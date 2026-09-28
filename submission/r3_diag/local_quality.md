# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `0e903a3746f549ad38af583de4a3dd448f6d60a8d48d8baa067129a3f4df0dad`; slice `B4-edge`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_236370.jpg, adasind_258420.jpg, adasind_310008.jpg. Frame thiếu trong export: không.
TP=15; FP=6; FN=5; số lần đối chiếu=25; mean IoU của TP=0.820.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.600 | 0.912 | 0.840 |
| precision | 0.714 | 0.756 | 0.333 |
| recall | 0.750 | 0.756 | 0.500 |
| jaccard | 0.577 | 0.611 | 0.250 |
| dice | 0.732 | 0.729 | 0.400 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 4 | 2 | 0 | 0.920 | 0.667 | 1.000 | 0.667 | 0.800 |
| Car | 1 | 2 | 1 | 0.880 | 0.333 | 0.500 | 0.250 | 0.400 |
| Pedestrian | 7 | 2 | 2 | 0.840 | 0.778 | 0.778 | 0.636 | 0.778 |
| ThreeWheeler | 2 | 0 | 2 | 0.920 | 1.000 | 0.500 | 0.500 | 0.667 |
| Truck | 1 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_236370.jpg | 7 | 0 | 0 | 1.000 | 1.000 | 1.000 |
| adasind_258420.jpg | 5 | 4 | 3 | 0.417 | 0.556 | 0.625 |
| adasind_310008.jpg | 3 | 2 | 2 | 0.500 | 0.600 | 0.600 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Car | Pedestrian | ThreeWheeler | Truck | <missing> |
|---|---:|---:|---:|---:|---:|---:|
| Bike | 4 | 0 | 0 | 0 | 0 | 0 |
| Car | 0 | 1 | 0 | 0 | 0 | 1 |
| Pedestrian | 0 | 0 | 7 | 0 | 0 | 2 |
| ThreeWheeler | 0 | 1 | 0 | 2 | 0 | 1 |
| Truck | 0 | 0 | 0 | 0 | 1 | 0 |
| <extra> | 2 | 1 | 2 | 0 | 0 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
