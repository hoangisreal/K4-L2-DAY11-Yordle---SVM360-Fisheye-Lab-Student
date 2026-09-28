# Guideline patch

- **Rule mới đề xuất (R12 — người trong cụm chồng lấn):** khi từng người vẫn phân biệt được trên ảnh gốc, vẽ một box cho mỗi người theo phần nhìn thấy; hai box được phép chồng nếu cơ thể thật sự chồng. Không dùng một box phủ nhiều người. Chỉ dùng `ignore_region.reason=crowd_or_group` khi không thể tách đáng tin cậy từng cá thể; không đồng thời vẽ box cá thể cho phần đã đưa vào vùng ignore.
- **Áp dụng cho:** class `Pedestrian`, box người chồng lấn và `ignore_region` có reason `crowd_or_group`, nhất là vùng mid/edge fisheye.
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** R02 yêu cầu bám phần nhìn thấy, R06 có `crowd_or_group`, nhưng chưa nêu ngưỡng quyết định “còn phân biệt được” và chưa cảnh báo rõ box một người không nên phủ cá thể bên cạnh. Ở `adasind_310008.jpg`, bốn người riêng biệt ở mép trái tạo các box chồng nhau; QA ban đầu hỏi liệu L2/L5 có trùng. Ảnh gốc cho thấy hai người trái là hai cá thể, nên v2 chỉnh từng box thay vì xóa người.
- **`rules_version` mới:** đề xuất `v1.1.0`; chờ người quản lý guideline duyệt, không tự sửa `docs/02-rules-vi.md` hay hồi tố C0/r1.
- **Hiệu lực từ:** chỉ round/slice bắt đầu sau khi patch được duyệt và đội nhãn đã được thông báo; trước đó tiếp tục dùng `v1.0.0`.
