# Escalation ticket

## Ticket 1

- **Vấn đề:** model gán sai class hoặc sinh proposal xung đột trên xe ba bánh; có thêm nghi vấn tách người lái xe hai bánh thành `Pedestrian` riêng.
- **Frame / object_ref:** `adasind_258420.jpg` — M4 `Truck` chồng vị trí R1 auto-rickshaw `ThreeWheeler`, M8 `Truck` chồng L4/R4 `ThreeWheeler`, M11 `Car` chồng L5/R8 `ThreeWheeler`; kiểm tra thêm `adasind_310008.jpg` M6 `Truck` và M7 `Bus` cùng chồng lên L1/R1 xe `ThreeWheeler`. Nghi vấn rider split: M2 ở `adasind_236370.jpg`, M5/M7/M10 ở `adasind_258420.jpg`; M7 còn chưa phân xử được là rider hay người riêng.
- **Rule liên quan:** R04 (`ThreeWheeler`) và R03 (rider); `findings.csv` round `r3_diag`. M-only là output model, không tự động đổi nhãn người.
- **Ảnh chụp:** `submission/screenshots/hoang-cvat-threewheeler-258420-early.png` cho cảnh gốc của frame 258420; bảng class/model có thể truy lại trong `submission/r3_diag/model_compare.md`.
- **Expected impact:** nếu proposal được dùng làm pre-label mà không QA, xe ba bánh có thể bị gán thành Truck/Car/Bus hoặc bị tính thành nhiều vật; rider có thể bị thêm Pedestrian riêng. Cả hai làm tăng sửa nhãn và gây lệch phân loại/đếm vật. Đây là tác động dự kiến, chưa phải kết luận về tỷ lệ lỗi sản xuất vì hiện chỉ có ba frame một camera.
- **Owner:** `ai_team`.
- **Recommendation:** đánh giá trên tập fisheye lớn hơn, phân tầng theo camera/loại xe, có nhãn ThreeWheeler và rider được hai người gán độc lập rồi phân xử; đo sai class, proposal chồng/trùng và rider split riêng. Giữ người duyệt theo R03/R04 cho tới khi phép kiểm đó hoàn tất.
- **Dấu vết quyết định:** các finding `r3_diag` M2/M4/M5/M7/M8/M10/M11 tại `adasind_236370.jpg` hoặc `adasind_258420.jpg` và M6/M7 tại `adasind_310008.jpg` có `action=escalate`; quyết định D08 trong `40_decision_log.csv` có `status=escalated`.

## Ticket 2

- **Vấn đề:** ranh box và số vật nhỏ trong cụm giao thông xa tại `adasind_258420.jpg` chưa phân xử được chắc chắn từ một ảnh mờ/che khuất và teaching reference chưa phải gold.
- **Frame / object_ref:** `adasind_258420.jpg` — L3/R5/M6 Car có hai ranh box khác nhau; cần xác định phần xe thật sự nhìn thấy theo R02. Cùng cụm còn L2 Bike, L7 Bike và L8 Pedestrian: cần kiểm chúng là cá thể riêng trong phạm vi H=40 hay box trùng/người ngồi trên xe theo R01/R03.
- **Rule liên quan:** R01, R02, R03. Không xóa hoặc co box chỉ vì một nguồn khác không khớp.
- **Ảnh chụp:** `submission/screenshots/hoang-cvat-threewheeler-258420-early.png` để định vị cụm vật trong cảnh. Ảnh chụp ở bản sớm, không xác nhận ranh box của bản khóa; đối chiếu `submission/r1_craft/annotations.xml`, `submission/rework/annotations-v2.xml`, `submission/r1_craft/compare.html` và ảnh gốc `assets/images/adasind_258420.jpg` khi phân xử.
- **Expected impact:** nếu tự coi R5 là đáp án hoặc tự xóa L2/L7/L8, số missing/spurious và kết luận lỗi người gán nhãn trên slice ba frame có thể đổi theo một quyết định chưa đủ bằng chứng. Chưa đưa các ca này vào gold set.
- **Owner:** `qa` — reviewer thứ hai hoặc Lab Coach xem ảnh gốc ở độ phân giải đầy đủ, kiểm từng vật với R01–R03 và ghi quyết định giữ/sửa cùng tọa độ.
- **Recommendation:** giữ nguyên v2 đã khóa cho tới khi review độc lập; sau phân xử mới sửa task CVAT, export và khóa lại nếu cần. Ghi kết quả và mã khóa mới vào decision log và hồ sơ bàn giao.
- **Dấu vết quyết định:** finding `r1_craft` L3+R5 và `r3_diag` L3+M6/R5 đã có `action=escalate`, D03 có `status=escalated`. Các finding L2/L7/L8 ở hai round cũng dùng `action=escalate`, gắn với D07 `status=escalated`.
