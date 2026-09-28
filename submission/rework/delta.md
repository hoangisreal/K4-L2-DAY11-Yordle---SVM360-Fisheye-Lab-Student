# Rework delta

| zone | matched before | matched after | missing before | missing after | spurious before | spurious after |
|---|---:|---:|---:|---:|---:|---:|
| center | 4 | 4 | 0 | 0 | 0 | 0 |
| mid | 6 | 8 | 3 | 1 | 5 | 4 |
| edge | 5 | 7 | 2 | 0 | 1 | 0 |

## Findings action=rework
- adasind_258420.jpg R1 MISSING: đã sửa
- adasind_258420.jpg R7 MISSING: đã sửa
- adasind_310008.jpg L1+R1 WRONG_CLASS: đã sửa
- adasind_310008.jpg L5+R4 BOX_GEOMETRY: đã sửa
- adasind_258420.jpg R1 MISSING: đã sửa
- adasind_258420.jpg R7+M12 MISSING: đã sửa
- adasind_310008.jpg L1 SPURIOUS: đã sửa
- adasind_310008.jpg L5 SPURIOUS: đã sửa
- adasind_310008.jpg R1 MISSING: đã sửa
- adasind_310008.jpg R4+M4 MISSING: đã sửa

## Giải thích sau P5

- Trên ba frame này, phép ghép với teaching reference tăng matched từ 15 lên 19; missing giảm từ 5 xuống 1 và spurious giảm từ 6 xuống 4. Khác biệt lớn nhất là `mid` (matched 6→8, missing 3→1, spurious 5→4) và `edge` (matched 5→7, missing 2→0, spurious 1→0); `center` giữ nguyên 4 matched. Đây là số mô tả phép ghép trên ba frame, không phải điểm rubric hay tỷ lệ lỗi tổng thể.
- Đã thêm R1 ThreeWheeler và R7 Pedestrian ở `adasind_258420.jpg`, sửa class L1 Car→ThreeWheeler và chỉnh L2/L5 thành hai box người riêng ở `adasind_310008.jpg`; các vị trí/rule/kết quả kiểm lại ở `submission/r2_qa/qa_review.md` và `submission/findings.csv`.
- L3/R5 Car ở `adasind_258420.jpg` vẫn lệch extent: r1/v2 L3 và model M6 gần nhau, teaching R5 hẹp/lệch hơn. Ảnh mờ và che khuất nên v2 giữ box L3 của r1, không co box chỉ để tăng matched; các dòng này chuyển `E5_unresolved`, `action=escalate` và chờ reviewer thứ hai. Chúng không thuộc danh sách rework đã xác nhận.
- L2/L7/L8 trong cùng frame cũng chưa đủ bằng chứng để kết luận là box hợp lệ hay thừa/trùng. V2 giữ nhãn để bảo toàn bản đã khóa; các finding `E5_unresolved` dùng `action=escalate` và được gom vào Ticket 2, D07 để reviewer thứ hai kiểm từng vật trước khi sửa.
- Teaching reference chưa là gold; các thay đổi ở đây phản ánh mẫu một camera/ba frame. Muốn kết luận hơn cần phân xử độc lập trên ảnh gốc và một mẫu rộng hơn.
