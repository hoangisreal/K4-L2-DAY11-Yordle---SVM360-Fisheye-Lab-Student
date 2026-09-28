# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 4 | 0 | 0 | 2 | 2 | — |
| mid | 9 | 3 | 5 | 2 | 7 | SPURIOUS (3) |
| edge | 7 | 2 | 1 | 1 | 1 | MISSING (1) |

## Nhận xét

- **Nhãn người (L):** khác biệt tập trung ở `mid` (3 missing, 5 spurious); `edge` đứng sau (2 missing, 1 spurious); `center` không có missing/spurious. Frame `adasind_258420.jpg` đóng góp nhiều ca mid, gồm box Car nhỏ và cụm Bike/Pedestrian chồng lấn; hai vật missing ở edge là R1 và R7, đã thêm ở v2.
- **Model (M):** phần thừa lớn nhất ở `mid` (7), sau đó `center` (2) và `edge` (1); missing tương ứng 2/2/1. Các box nhiều class trên xe ba bánh và rider/person có thể liên quan dữ liệu fisheye, che khuất, méo rìa hoặc hành vi model; ba frame chưa đủ phân biệt nguyên nhân hay suy ra xu hướng tổng quát. Với Car L3/R5, M6 gần box L3 trong khi teaching reference hẹp hơn; ca đã được giữ mở để người soát thứ hai phân xử thay vì coi reference là gold.
