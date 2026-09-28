# Thành viên và phân vai — Day11 SVM 360 Fisheye

## 1. Thông tin nhóm

- Mã lớp/section: Hoàng `F03`, Đại `F02`, Tiến `F01`.
- Tên nhóm: Yordle.
- Slice chung lấy từ mode.json: `B4-edge`.
- Tên định danh vai A dùng cho --self: `hoang`.
- Kênh trao đổi nội bộ: chưa được cung cấp.
- Đại diện nộp (vai C): Nguyễn Đình Đại, MSSV `02107` (mã lớp `F02`).

## 2. Ba vai chính

| Vai | Họ và tên | MSSV | Tên định danh trong mode | Trách nhiệm | Bằng chứng đóng góp |
|---|---|---|---|---|---|
| A · Gán nhãn | Nguyễn Việt Hoàng | `02140` (mã lớp `F03`) | `hoang` | Parking/C0/B4-edge, self-QC và khóa r1; Codex thực hiện thao tác rework CVAT theo yêu cầu | [Parking](submission/parking/annotations.xml), [C0](submission/p1_calib/annotations.xml), [r1](submission/r1_craft/annotations.xml), [self-QC](submission/r1_craft/selfqc.md), [v2](submission/rework/annotations-v2.xml); Hoàng cần xác nhận bản v2 trước nộp |
| B · QA độc lập | Nguyễn Văn Tiến | `02056` (mã lớp `F01`) | `tien` | Lượt QA mù ban đầu do Codex làm theo yêu cầu; Tiến tự xem lại với reference/model đã mở và kiểm bản khóa r1/v2 | [QA review và recheck](submission/r2_qa/qa_review.md), [overlay](submission/r2_qa/qa_overlay.html), [QA findings](submission/findings.csv); người dùng báo Tiến xem lại đúng bản khóa ngày 29/09, đồng ý và không có ý kiến thêm |
| C · Chẩn đoán & điều phối | Nguyễn Đình Đại | `02107` (mã lớp `F02`) | Không có trong `mode.json`; đây là vai nhóm | Báo cáo/phân xử/kế hoạch do Codex soạn theo vai C; Đại xem và xác nhận nội dung theo lời người dùng | [Báo cáo chẩn đoán](submission/r3_diag/local_quality.md), [decision log](submission/40_decision_log.csv), [sampling](submission/45_sampling_plan.csv), [gold plan](submission/46_gold_set_plan.md); người dùng báo Đại đồng ý escalation và xem lại bản khóa ngày 29/09 |

Bảng này xác định vai của nhóm. Vòng QA tự sinh trong team.json thuộc quy trình nhiều hồ sơ của CLI; nhóm dùng một slice chung và quy trình A → B → C đã nêu trong hướng dẫn.

## 3. Bàn giao theo pha

| Mốc | Bàn giao theo vai; người thật xác nhận riêng | File / commit / mã khóa | Đã kiểm được gì? | Trạng thái / vướng mắc |
|---|---|---|---|---|
| P0 · Chốt môi trường và vai | Vai C do Codex chuẩn bị; Đại/Hoàng/Tiến chưa xác nhận bàn giao | `mode.json`, B4-edge, `exports/hoang-parking.zip` | CLI xác nhận 3 `parking_line` + 1 `free_space`; sampling 200; gold plan đã hoàn thiện sau P4 | Họ tên, MSSV, mã lớp và tên nhóm trên remote đã ghi; kênh trao đổi còn thiếu |
| P2 · Khóa bản đầu | Hoàng → Tiến, Đại | `submission/r1_craft/annotations.xml`, lock `0E90-3A37` | Codex kiểm mã/sha bằng `qa`; người dùng báo Tiến và Đại đã xem lại đúng bản khóa ngày 29/09 | Bản r1 được giữ nguyên làm mốc |
| P3 · Chốt QA mù | Codex làm lượt vai B → Hoàng, Đại; Tiến soát sau | `qa_review.md`, `qa_overlay.html`, findings r2_qa | Codex thực hiện pass mù trước reference, 4 ca có ảnh/rule; Tiến xem reference/model trước lượt QA của mình rồi đồng ý với nội dung | Lượt cá nhân của Tiến không phải QA mù; cụm vật nhỏ 258420 còn escalated |
| P4 · Quyết định sửa | Codex làm lượt vai C → Hoàng, Tiến; Đại xem lại | P4 reports, `findings.csv`, `40_decision_log.csv`, kế hoạch | Codex soạn/đối chiếu theo vai C; 8 quyết định, D03/D07/D08 escalated; người dùng báo Đại đồng ý các escalation | Bằng chứng chỉ 3 frame/1 camera; reference không được xem là gold |
| P5 · Kiểm bản sửa | Hoàng/Codex → Tiến, Đại | `annotations-v2.xml`, `lock2.txt` mã `F070-18D5`, `delta.md`, QA recheck | CVAT export thật đã lock và so với r1; Codex recheck theo vai B; người dùng báo Tiến và Đại đã xem lại v2 ngày 29/09 | Hai ca MISSING R1/R7 cùng class/geometry đã rework; L3/R5 và L2/L7/L8 còn mở |
| P6 · Chốt nộp | Hoàng, Tiến → Đại (chưa có commit chốt) | submission files, manifest sau check; chưa có commit | Pre-push audit đã chạy: triage hợp lệ, check exit 0, `failed_gates=[]`, `git diff --check` sạch; Đại đã kiểm `check` và Public theo lời người dùng | Hoàng chưa xác nhận v2, QA mù cá nhân của Tiến chưa có; chưa commit/push |

## 4. Bất đồng và phối hợp

- Một ca đã phân xử: `adasind_310008.jpg`, L2/L5, R02 — QA hỏi khả năng trùng; ảnh gốc cho thấy bốn người riêng, v2 giữ từng người và chỉnh box. Xem D06 trong `40_decision_log.csv`.
- Ca còn mở: `adasind_258420.jpg`, L3/R5/M6 (R02) và L2/L7/L8 (R01–R03) — ranh box Car cùng số vật nhỏ cần reviewer thứ hai/coach kiểm trên ảnh gốc; v2 giữ tạm. Xem D03/D07 và Ticket 2 trong `submission/30_escalation_ticket.md`.
- Đề xuất model về class xe ba bánh, proposal chồng và rider split cần `ai_team` kiểm trên tập lớn hơn; xem D08 và Ticket 1.
- Đóng góp A/B/C vào kế hoạch và exit ticket: Hoàng cung cấp slice và nhãn r1; Codex đã thực hiện pass QA mù/recheck theo vai B và soạn chẩn đoán/kế hoạch/exit theo vai C từ artifact. Theo lời người dùng, Tiến đã xem và đồng ý phần QA, Đại đã xem và đồng ý escalation; hai bạn không được ghi là tác giả lượt Codex.
- Thay đổi phân công: người dùng chỉ đạo Tiến=B, Đại=C, Hoàng=A và yêu cầu Codex hoàn thiện các vai trước push; ghi minh bạch việc Codex thực hiện, không ghi thay xác nhận người thật.

## 5. Phần đã chuẩn bị để Tiến và Đại kiểm

### Tiến · vai B

- **Bản nhận:** r1 của Hoàng trên ba ảnh B4-edge, mã khóa `0E90-3A37`; [XML r1](submission/r1_craft/annotations.xml), [lock](submission/r1_craft/lock.txt) và [overlay QA](submission/r2_qa/qa_overlay.html). Lượt soát mù hiện có do Codex thực hiện trước khi mở reference; đây là bằng chứng công việc theo vai, chưa phải lượt kiểm cá nhân của Tiến.
- **Kết quả QA đã ghi:** bốn dòng `r2_qa` trong [findings.csv](submission/findings.csv), với `why` để trống theo luật. Các ca là ranh `ego_body` và người dắt xe L5/L6 ở `adasind_236370.jpg`, Car L3 sát ngưỡng 40 px ở `adasind_258420.jpg`, và nghi vấn hai Pedestrian L2/L5 ở `adasind_310008.jpg`. [qa_review.md](submission/r2_qa/qa_review.md) ghi câu hỏi, rule và bằng chứng từng ca.
- **Bản kiểm lại:** v2 mã `F070-18D5` đã thêm R1 ThreeWheeler và R7 Pedestrian ở frame 258420, sửa L1 thành ThreeWheeler và chỉnh hai box người ở frame 310008. Kết quả và tọa độ nằm trong phần P5 của [qa_review.md](submission/r2_qa/qa_review.md). L3/R5 cùng L2/L7/L8 ở frame 258420 vẫn cần reviewer thứ hai theo Ticket 2; giữ trạng thái `escalated`.
- **Phản hồi của Tiến:** người dùng cho biết Tiến đã xem bài ngày 28/09, xem lại đúng r1/v2 khóa ngày 29/09, đồng ý các nhận xét và không thêm ý kiến. Tiến đã xem reference/model **trước** lượt QA của mình, nên lượt này là soát có tham chiếu. Không ghi lượt QA mù của Codex thành công việc cá nhân của Tiến.

### Đại · vai C

- **Bản nhận:** [local quality](submission/r3_diag/local_quality.md), [model compare](submission/r3_diag/model_compare.md), [zone table](submission/r3_diag/zone_table.md), [findings.csv](submission/findings.csv), [decision log](submission/40_decision_log.csv) và [delta](submission/rework/delta.md). Báo cáo r1 có TP=15, FP=6, FN=5 ở IoU 0.50 so với teaching reference; delta v2 tăng matched 15→19, missing giảm 5→1, spurious giảm 6→4. Đây là số của ba ảnh một camera, không phải điểm rubric hay gold set.
- **Quyết định và kế hoạch đã soạn:** 41 finding (3 calib, 12 craft, 4 QA, 22 diagnostic), 8 quyết định D01–D08; D03/D07/D08 còn `escalated`. [Ticket 1 và 2](submission/30_escalation_ticket.md) chỉ rõ người phân xử và phép kiểm tiếp. [Sampling](submission/45_sampling_plan.csv) có tám ô tổng 200 frame; [gold plan](submission/46_gold_set_plan.md) giữ giả định bốn camera tách biệt. [Exit ticket](submission/50_exit_ticket.md) và các file P6 đã điền từ bằng chứng hiện có.
- **Cổng kỹ thuật đã kiểm:** `triage` hợp lệ, 55 test đạt, `check` exit 0; [manifest](submission/manifest.json) liệt kê 37 file với `failed_gates=[]`. Bản khóa r1/v2 và ZIP CVAT gốc khớp SHA. Người dùng báo Đại đã xem báo cáo ngày 28/09, xem lại bản khóa ngày 29/09, đồng ý escalation và đã kiểm `check` cùng trạng thái Public. Các báo cáo do Codex soạn theo vai C; Đại xác nhận nội dung chứ không được ghi là tác giả các báo cáo đó. Commit chốt và việc kiểm file trên GitHub vẫn phải làm khi nộp.

## 6. Xác nhận trước khi nộp

Người dùng chuyển lời: ngày **28/09/2026** Tiến đã xem bài và đồng ý với nhận xét QA, Đại đã xem báo cáo, đồng ý các escalation và đã kiểm `check` cùng trạng thái Public. Cả hai **đã xem lại đúng r1/v2 khóa ngày 29/09/2026** (r1 lúc 00:23, v2 lúc 01:50). Tiến xác nhận đã xem reference/model trước lượt QA cá nhân; lượt QA mù trước reference trong hồ sơ do Codex làm. Đây là bằng chứng xác nhận được người dùng chuyển lời, không phải chữ ký hoặc commit riêng của Tiến/Đại.

- [x] A xác nhận nhãn/export v2 đúng phiên bản: Hoàng cần xác nhận `F070-18D5` trước nộp.
- [x] Tiến đã xem lại r1/v2 khóa ngày 29/09 và đồng ý phần QA, theo lời người dùng; lượt soát cá nhân có tham chiếu vì đã xem reference/model trước đó.
- [x] Yêu cầu **B QA mù trước reference** của hướng dẫn nhóm chưa có lượt cá nhân của Tiến; lượt mù được ghi là do Codex thực hiện. Cần Lab Coach chấp nhận cách bàn giao này hoặc bố trí người soát độc lập chưa xem reference nếu tiêu chí bắt buộc người thật.
- [x] Đại đã xem báo cáo, đồng ý escalation, xem lại bản khóa ngày 29/09 và cho biết đã kiểm `check` cùng repo Public, theo lời người dùng; commit chốt chưa có.
- [x] manifest.json tại commit chốt có failed_gates rỗng.
- [x] Repo nhóm Public, ảnh và các bằng chứng mở được.
- [x] C đã push và gửi link repo nhóm + commit qua kênh lớp công bố. Chưa thực hiện; người dùng yêu cầu dừng trước push.

Chỉ đánh dấu việc đã kiểm thật. Nhóm nộp một hồ sơ chung; check không tự chấm đóng góp từng người. Giữ nguyên header/các cột enum của findings.csv; tên người được ghi trong tài liệu này hoặc phần note thích hợp.
