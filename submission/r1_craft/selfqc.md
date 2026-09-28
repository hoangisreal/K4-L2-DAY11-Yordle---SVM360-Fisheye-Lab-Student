# Tự soát

- Cảnh báo tự động `Tên task thiếu raw_fisheye` đã được xác nhận thủ công: tên task trong CVAT đúng.

## Checklist thủ công
- [x] Phạm vi H=40 và vật cần vẽ
- [x] lens_border và ego_body
- [x] Class sáu nhãn
- [x] Rider và Bike
- [x] Geometry trên ảnh fisheye gốc
- [x] truncated và occluded
- [x] Vật thiếu hoặc box trùng
- [x] ignore_region có reason
- [x] Tên task raw_fisheye và export CVAT 1.1

## Ghi chú kiểm thủ công trên bản export

- Đã rà overlay của đủ ba frame. Các box đối tượng đều cao ít nhất 40 px; class, rider/Bike, hình học và attribute nhìn chung khớp ảnh. Xe thùng bạt trắng ở `adasind_236370.jpg` là xe chở hàng, nhãn `Truck` phù hợp R04.
- Ở `adasind_310008.jpg`, các box Pedestrian đã tách theo từng người nhìn thấy; bản mới không còn cặp cùng class IoU > 0.7. Đã rà cụm người bên trái trên ảnh phóng to.
- Bản mới có hai polygon `lens_border` và một polygon `ego_body` có reason trong từng frame; Role A xác nhận vùng đã kiểm tra và đạt R07.
- XML là CVAT for images 1.1; Role A xác nhận tên task trong CVAT có chứa `raw_fisheye`. Cảnh báo tự động được giữ lại như ghi chú vì bộ đọc XML lấy tên nhãn thay vì tên task.
- Bản cuối đã export lại từ CVAT và khóa thành `submission/r1_craft/annotations.xml`; mã khóa `0E90-3A37` ở `lock.txt` (21 box, 13 polygon). Role A bàn giao đúng bản khóa này cho bước QA; mức độc lập thực tế của lượt review được ghi trong `submission/r2_qa/qa_review.md`.

## Fill ratio (K12)
- adasind_236370.jpg box 7 center: 0.638
- adasind_236370.jpg box 5 edge: 0.622
- adasind_310008.jpg box 3 edge: 0.432
- adasind_310008.jpg box 2 edge: 0.407
mean edge: 0.487 (n=3)
mean center: 0.638 (n=1)
