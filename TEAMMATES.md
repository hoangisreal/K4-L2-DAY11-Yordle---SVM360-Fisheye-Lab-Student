# Thành viên và phân vai — Day11 SVM 360 Fisheye

## 1. Thông tin nhóm

- Tên nhóm: Yordle.
- Slice chung: `B4-edge`.
- Thành viên: Nguyễn Việt Hoàng (`02140`, F03), Nguyễn Văn Tiến (`02056`, F01), Nguyễn Đình Đại (`02107`, F02).
- Nhóm dùng một hồ sơ chung theo luồng bàn giao A → B → C. `mode.json` và `team.json` ghi đúng ba vai trên cùng slice `B4-edge`; không chạy lại lệnh chia slice mặc định cho checkout đã khóa.

## 2. Phân công và bằng chứng

| Vai | Thành viên | Trách nhiệm | Artifact và mức xác nhận |
|---|---|---|---|
| A · Annotator | Nguyễn Việt Hoàng | Gán nhãn Parking, C0 và B4-edge; self-QC; khóa r1; rework và export/khóa v2 | Role A thực hiện và bàn giao [Parking](submission/parking/annotations.xml), [C0](submission/p1_calib/annotations.xml), [r1](submission/r1_craft/annotations.xml), [self-QC](submission/r1_craft/selfqc.md) và [v2](submission/rework/annotations-v2.xml). Lock r1: `0E90-3A37`; lock v2: `F070-18D5`. |
| B · QA/reviewer | Nguyễn Văn Tiến | Kiểm tra artifact QA được giao, đối chiếu r1/v2 và xác nhận các finding đã xem | Bốn finding `r2_qa`, overlay và bảng recheck là artifact được tạo từ workflow của project. Role B kiểm tra đúng bản r1/v2 đã khóa ngày 29/09/2026 sau khi đã xem reference/model, xác nhận các finding và không bổ sung ý kiến. Đây là review có tham chiếu, không được ghi thành một lượt QA mù cá nhân. |
| C · Diagnostic/điều phối | Nguyễn Đình Đại | Kiểm tra bộ diagnostic, decision/escalation, sampling/gold-plan và phần tổng hợp trước nộp | Các báo cáo được tạo từ workflow của project và được Role C kiểm tra/xác nhận. Role C xác nhận các escalation, xem lại bản khóa ngày 29/09/2026 và kiểm tra kết quả `check` cùng trạng thái repo trước bàn giao. Không coi việc xác nhận là bằng chứng Role C tự tạo toàn bộ báo cáo từ đầu. |

## 3. Bàn giao theo pha

| Mốc | Bàn giao | Artifact chính | Kết quả và trạng thái |
|---|---|---|---|
| P0 · Môi trường và vai | Nhóm chốt Role A/B/C và slice `B4-edge` | `mode.json`, `team.json`, `sensor_context.md`, parking export | Parking có 3 `parking_line` và 1 `free_space`; kế hoạch sampling đủ 200 frame. |
| P1/P2 · Hiệu chuẩn và khóa r1 | Role A bàn giao C0 và r1 cho Role B/C | `p1_calib/`, `r1_craft/`, lock `0E90-3A37` | XML và mã khóa khớp; r1 được giữ nguyên làm mốc so sánh. |
| P3 · QA | Artifact QA ban đầu được tạo trong workflow; Role B kiểm tra và xác nhận | `r2_qa/qa_review.md`, `qa_overlay.html`, bốn dòng `r2_qa` trong `findings.csv` | Artifact ban đầu ghi điều kiện trước reference. Evidence hiện có chỉ chứng minh Role B review sau khi đã xem reference/model; vì vậy không gán lượt blind pass cho một thành viên cụ thể. |
| P4 · Diagnostic và quyết định | Role C kiểm tra bộ báo cáo và xác nhận các quyết định/escalation | `r3_diag/`, `findings.csv`, `40_decision_log.csv`, `30_escalation_ticket.md`, sampling/gold-plan | Có 41 finding và 8 quyết định; D03, D07, D08 giữ trạng thái `escalated`. Teaching reference không được coi là gold. |
| P5 · Rework và kiểm bản sửa | Role A sửa/export/khóa v2; Role B kiểm tra lại; Role C xem bản khóa | `annotations-v2.xml`, `lock2.txt`, `delta.md`, phần P5 trong `qa_review.md` | Matched 15→19, missing 5→1, spurious 6→4. Hai missing R1/R7 và các sửa đổi frame 310008 đã hoàn tất; L3/R5 và L2/L7/L8 ở frame 258420 vẫn mở. |
| P6 · Tổng hợp | Role C kiểm tra bộ hồ sơ hoàn chỉnh | `manifest.json`, exit ticket và các artifact trong `submission/` | `failed_gates=[]`; trạng thái unresolved/escalated được giữ nguyên để reviewer thứ hai hoặc Lab Coach xử lý. |

## 4. Bất đồng và phối hợp

- `adasind_310008.jpg`, L2/L5, R02: artifact QA nêu nghi vấn trùng. Role A đối chiếu ảnh gốc, giữ hai người và chỉnh box theo từng cá thể trong v2. Role B kiểm tra bản v2 đã khóa và xác nhận kết quả.
- `adasind_258420.jpg`, L3/R5/M6 và L2/L7/L8: bằng chứng hiện có chưa đủ để kết luận chắc chắn. Role C xác nhận giữ trạng thái `escalated`; Ticket 2 yêu cầu reviewer thứ hai hoặc Lab Coach phân xử trên ảnh gốc.
- Các xung đột class ThreeWheeler và rider split từ model được chuyển cho `ai_team` theo D08/Ticket 1. Ba frame chỉ là ví dụ, không dùng để kết luận tỷ lệ lỗi tổng quát.
- Sampling plan gồm 4 camera × normal/hard, tổng 200 frame. Gold-set plan yêu cầu hai người gán độc lập và người thứ ba phân xử; ba frame ADASIND không được coi là gold cho hệ bốn camera.


## 5. Trạng thái chốt hồ sơ

- [x] Role A đã khóa r1 `0E90-3A37` và v2 `F070-18D5`.
- [x] Role B đã kiểm tra r1/v2 khóa ngày 29/09/2026 và xác nhận các finding trong lượt review có tham chiếu.
- [x] Role C đã kiểm tra bộ báo cáo, xác nhận escalation và kiểm tra cổng kỹ thuật.
- [x] manifest.json tại commit chốt có failed_gates rỗng.
- [x] Repo nhóm Public, ảnh và các bằng chứng mở được.
- [x] C đã push và gửi link repo nhóm + commit qua kênh lớp công bố.

Chỉ gán công việc cho thành viên khi có artifact hoặc bước xác nhận tương ứng. Việc một vai kiểm tra/chấp nhận artifact không được diễn đạt thành việc vai đó tự tạo artifact từ đầu.
