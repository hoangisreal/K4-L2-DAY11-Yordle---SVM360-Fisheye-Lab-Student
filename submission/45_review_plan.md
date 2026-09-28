# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| B4-edge · `adasind_258420.jpg` | Hai P1 missing đã sửa: R1 ThreeWheeler và R7 Pedestrian; bất đồng box Car L3/R5 và ba box nhỏ L2/L7/L8 còn mở; model có class conflict M4/M8/M11 | Mép ảnh có vật nhỏ/che khuất và xe ba bánh; kiểm vật theo ảnh gốc, R01/R02/R03/R04, không lấy model hay teaching reference làm gold | Export r1/v2, `rework/delta.md`, findings L2/L3/L7/L8/R1/R5/R7 và M4/M8/M11, Ticket 2, ảnh CVAT sớm 258420, `model_compare.md` |
| B4-edge · `adasind_310008.jpg` | P1 class L1 Car→ThreeWheeler và geometry cụm người L2/L5 đã sửa; model M6/M7 cho class xung đột trên cùng xe | R04 quyết định class xe; cần giữ box từng người ở cụm chồng lấn và phân biệt lỗi người với lỗi model | Export r1/v2, `rework/delta.md`, findings L1/L5/R1/R4/M6/M7 và `qa_review.md` |

Giới hạn: chỉ ba frame từ một camera, không phải mẫu ngẫu nhiên đại diện; teaching reference chưa được chứng nhận là gold. Số difference/zone chỉ giúp xếp ca cần review, không ước lượng tỷ lệ lỗi của dữ liệu hay bốn camera.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ: kiểm đủ 4 camera × normal/hard và tổng 200; rải frame theo thời gian, địa điểm và sự kiện, giới hạn số frame liền nhau cùng một cảnh rồi thay bằng frame ở đoạn khác. Dành 30 frame hard/20 normal mỗi camera để phát hiện rủi ro, nhưng giữ nhãn `hard` riêng để không gộp thành mẫu đại diện. Vì mẫu cố ý oversample hard và chưa có xác suất chọn đã biết, không thể dùng nó để ước lượng tỷ lệ lỗi; muốn ước lượng cần một mẫu ngẫu nhiên/stratified có trọng số và reference đã phân xử.
