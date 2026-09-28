# QA review · B4-edge

- **Vai trò reviewer:** B, được phân công cho Tiến. Lượt QA mù được ghi nhận bên dưới do Codex thực hiện theo chỉ dẫn của người dùng để hoàn tất workflow đã được phân công.
- **Xác nhận từ người review:** Theo thông tin người dùng cung cấp, Tiến đã xem lại tài liệu vào ngày **28/09/2026** và kiểm tra lại các bản **r1/v2 đã khóa** vào ngày **29/09/2026**, đồng ý với các finding đã ghi nhận và không bổ sung thêm ý kiến.
- **Tình trạng tiếp xúc với reference:** Tiến đã xem reference/model trước khi thực hiện lượt review của mình. Vì vậy, lượt review của Tiến là **review có tham chiếu**. Lượt **QA mù** được ghi nhận bên dưới do Codex thực hiện trước khi mở teaching reference, model output hoặc worked overlay của B4-edge.
- **Annotator:** Hoàng (A).
- **Lock đã kiểm tra:** `0E90-3A37`; SHA-256 ghi trong `lock.txt` khớp với `annotations.xml`.
- **Phạm vi:** Toàn bộ ba frame thuộc B4-edge, bao gồm ảnh gốc và annotation overlay của bản đã khóa.
- **Điều kiện QA mù:** Lượt QA này được hoàn tất trước khi mở teaching reference, model output hoặc worked overlay của B4-edge.

| frame | object_ref | rule_id | finding / nội dung cần kiểm tra |
|---|---|---|---|
| `adasind_236370.jpg` | ego_body polygon | R07 | Polygon ego bám theo người lái/xe ở góc dưới bên trái và kéo tới khoảng `x=294, y=1744`. Cần kiểm tra lại biên dưới-trái dựa trên phần giày/xe nhìn thấy và vùng bóng kế bên để bảo đảm không đưa mặt đường hoặc bóng đổ vào ego body. |
| `adasind_236370.jpg` | L5 Pedestrian, L6 Bike | R03 | Người đứng cạnh xe hai bánh có vẻ đang đi bộ và dắt xe. Cần xác nhận trên ảnh gốc rằng người này thực sự đang đi bộ/dắt xe chứ không ngồi trên xe với vai trò rider. Chỉ giữ annotation tách riêng `Pedestrian` + `Bike` nếu người đó không đang lái/ngồi trên xe. |
| `adasind_258420.jpg` | L3 Car | R01, R02 | Box có kích thước khoảng `64 × 41 px`, chỉ cao hơn nhẹ ngưỡng `H=40`. Cần kiểm tra lại xem biên trên và dưới có bám đúng phần xe nhìn thấy trên ảnh fisheye gốc hay không, đồng thời xác nhận phần nhìn thấy thực tế cao ít nhất 40 px. |
| `adasind_310008.jpg` | L2, L5 Pedestrian | R02 | Hai box chồng lấn đáng kể trong cụm người đi bộ bên trái. Cần xác minh đây có phải là hai người khác nhau hay L5 là box thứ hai trùng với người đã được đánh dấu bởi L2. |

Đây là một **lượt QA mù theo vai trò, do Codex thực hiện theo chỉ dẫn của người dùng**. Nội dung này **không khẳng định rằng Tiến trực tiếp thực hiện lượt QA mù**.

Theo thông tin người dùng cung cấp, Tiến sau đó đã kiểm tra lại các bản đã khóa sau khi đã xem reference/model và đồng ý với các finding. Vì vậy, lượt review của Tiến được xem là một **lượt human recheck có tham chiếu**, tách biệt với lượt QA mù ở trên.

Giữ trường `why` trống đối với các finding thuộc `r2_qa`.

Bất kỳ chỉnh sửa nào đối với XML đã khóa đều yêu cầu **export lại và tạo lock mới trước khi mở reference**.

---

## P5 recheck · bản v2

- **Vai trò reviewer:** B. Lượt recheck dưới đây do Codex thực hiện theo chỉ dẫn của người dùng.
- Theo thông tin người dùng cung cấp, Tiến cũng đã xem lại bản v2 đã khóa vào ngày **29/09/2026**, đồng ý với các kết quả đã ghi nhận và không có thêm ý kiến.
- **File đã kiểm tra:** `submission/rework/annotations-v2.xml`
- **Lock:** `F070-18D5`
- **Lệnh xác minh:**

```bash
python lab11.py qa --slice B4-edge --file submission/rework/annotations-v2.xml --code F070-18D5
```

Lệnh trên xác nhận mã lock và SHA của file đã kiểm tra là hợp lệ.

| frame | object_ref | rule | kết quả recheck |
|---|---|---|---|
| `adasind_258420.jpg` | R1 | R01, R04, R05 | Đã thêm annotation `ThreeWheeler` bao quanh auto-rickshaw ở mép trái ảnh, box `(0,796)-(68,872)`, với `truncated=true` vì box chạm biên ảnh. Vật thể được thể hiện đúng trên overlay. |
| `adasind_258420.jpg` | R7 | R01, R02 | Đã thêm annotation `Pedestrian` tại `(92,792)-(110,845)`, cao `53 px`. Người này có thể phân biệt với L9 trên ảnh gốc. |
| `adasind_258420.jpg` | L3/R5/M6 | R02 | **Chưa phân xử / đã escalate.** Bản v2 giữ nguyên L3 từ r1 tại `(209.31,772.71)-(273.46,813.81)`. Phần vật thể nhìn thấy bị mờ/che khuất nên chưa đủ cơ sở để tự tin co box theo R5; đồng thời L3 và M6 nằm khá gần nhau. Finding này đã được chuyển sang **E5 / escalate** để reviewer thứ hai kiểm tra. |
| `adasind_258420.jpg` | L2/L7/L8 | R01, R02, R03 | Bản v2 tiếp tục giữ các box nhỏ từ r1. Hiện vẫn chưa thể xác nhận chắc chắn L2 có phải `Bike` hợp lệ hay không, L7 là một xe riêng hay trùng với L6, và L8 là một pedestrian riêng hay là người gắn với chiếc xe. Ticket 2 và D07 yêu cầu reviewer thứ hai xem ảnh gốc trước khi thực hiện bất kỳ chỉnh sửa nào. |
| `adasind_310008.jpg` | L1/R1 | R04 | Đã đổi class của L1 từ `Car` sang `ThreeWheeler`. Không thêm box trùng. |
| `adasind_310008.jpg` | L2/L5/R4/R5 | R01, R02 | Xác nhận có bốn người khác nhau có thể phân biệt được. Hai box phía trái được chỉnh thành `(34,873)-(77,1022)` và `(20,866)-(56,1028)`. Hai người ở phía bên phải được giữ nguyên. |

Lượt recheck này xác nhận lock và kiểm tra các sửa đổi P1 trên XML/overlay sau rework.

Các **case E5 trong `adasind_258420.jpg` vẫn đang mở** và cần reviewer thứ hai xử lý.

Theo thông tin người dùng cung cấp, Tiến đã kiểm tra đúng bản v2 đã khóa này vào ngày **29/09/2026** và đồng ý với các case được ghi nhận ở trên. Lượt review của Tiến được thực hiện **sau khi reference đã được xem** và không làm thay đổi tác giả hay trạng thái QA mù của lượt QA Codex trước đó.

**Không có bất kỳ chỉnh sửa annotation nào được thực hiện sau khi bản v2 đã được khóa.**
