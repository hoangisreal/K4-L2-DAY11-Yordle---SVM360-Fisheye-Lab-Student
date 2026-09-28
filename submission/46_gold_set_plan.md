# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide,
**không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có
normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference
ADASIND hoặc nhãn bạn vừa vẽ. Nếu cần, dùng `notebooks/day11-svm360-colab.ipynb` để thử tổng phân bổ; notebook
không làm thay phần lý do.

| camera_id | Hard case cần chọn | Vì sao dễ sai | Annotation space / calibration cần giữ | Cách review trước khi gọi là gold |
|---|---|---|---|---|
| front | Người đi bộ hoặc xe hai bánh bị che ở rìa vòng kính; chọn thêm cảnh normal nhìn rõ | Box/class và ngưỡng H=40 dễ bất đồng khi vật nhỏ hoặc méo | Giữ ảnh fisheye gốc, camera_id, độ phân giải, vòng kính, timestamp và phiên bản calibration; không vẽ box theo ảnh BEV | Hai người gán nhãn độc lập theo cùng rule; người thứ ba phân xử ca bất đồng trên ảnh gốc và lưu quyết định |
| rear | Vật bị thân xe che khi lùi hoặc cắt ở biên; chọn thêm cảnh normal ít vật | Dễ nhầm `ego_body`, `lens_border`, `truncated` và vật hợp lệ | Giữ ảnh fisheye gốc, camera_id, timestamp, mask thân xe/vòng kính và phiên bản calibration | Hai người kiểm độc lập cả box lẫn ignore; ca bất đồng chuyển người phân xử, ghi rõ frame và rule |
| left | Vật ở seam trái hoặc chồng lấn với vật khác; chọn thêm cảnh normal | Một vật có thể hiện trên camera trái và camera kề, box khác nhau nhưng đều hợp lệ | Giữ tọa độ trên ảnh gốc, camera_id, timestamp, calibration và liên kết frame đồng thời nếu có | Gán nhãn độc lập trong camera trái; người phân xử xem cặp ảnh đồng thời trước khi áp policy liên camera |
| right | Vật ở seam phải bị méo/cắt hoặc che khuất; chọn thêm cảnh normal | Méo rìa làm box và thuộc tính dễ lệch giữa người gán nhãn | Giữ tọa độ trên ảnh gốc, camera_id, timestamp, calibration và phiên bản rule | Hai người gán nhãn độc lập; người thứ ba phân xử trên ảnh gốc và ghi lại lý do giữ/sửa từng box |

- **Cách lấy mẫu ban đầu:** chia đều 50 frame cho mỗi camera gồm 20 normal và 30 hard, tổng 200. Chủ ý lấy dư hard để tìm lỗi; tỷ lệ lỗi trên mẫu này không đại diện cho toàn bộ 50.000 frame. Trong mỗi ô, rải mẫu theo thời điểm/cảnh và tránh lấy nhiều frame liên tiếp của cùng một sự kiện như các quan sát độc lập. Đây là giả thuyết thiết kế, cần sửa theo phân bố dữ liệu thật nếu có.
- **Điều kiện gọi là gold:** thống nhất rule và annotation space trước; hai người gán nhãn độc lập, người thứ ba phân xử bất đồng, lưu ảnh/frame, quyết định và phiên bản rule/calibration. Chỉ các frame qua vòng đó mới được đưa vào gold set.
- **Khi cần refresh gold set:** camera, vị trí lắp, calibration, xử lý ảnh, taxonomy hoặc guideline thay đổi; hoặc audit phát hiện ca hard mới mà tập hiện tại chưa bao phủ.
- **Ca seam cần policy:** một người đi bộ xuất hiện đồng thời ở front và left với hai box khác nhau. Cần frame đồng bộ bằng timestamp, calibration cùng phiên bản và chính sách output (giữ hai box theo camera hay hợp nhất ở BEV) trước khi nối identity hoặc gọi là lỗi trùng.
- **Giới hạn bằng chứng hiện có:** ba frame ADASIND của bài gán nhãn chỉ đến từ một camera. Peer agreement và local quality trên teaching reference đó không chứng minh chất lượng nhãn hay gold set cho đủ bốn camera.
- **Sau P4 đã đối chiếu:** `findings.csv` và `r3_diag/zone_table.md` của B4-edge; bổ sung cue vật nhỏ/che khuất ở rìa, ThreeWheeler dễ nhầm class và pedestrian chồng lấn vào phần điều chỉnh bên dưới.

## Điều chỉnh sau P4

P4 cho thấy hai nhóm hard cần chủ động phủ trong kế hoạch giả lập: vật nhỏ/che khuất ở rìa và xe ba bánh dễ bị nhầm class; cụm bốn người chồng lấn ở `adasind_310008.jpg` cũng cần tiêu chí box từng cá thể. Vì vậy giữ phân bổ 20 normal/30 hard mỗi camera để tăng cơ hội tìm ca khó, không đổi thành kết luận về tần suất lỗi. Phép kiểm tiếp theo: trên mỗi camera chọn các thời điểm/cảnh tách biệt, cho hai người gán độc lập các hard case rồi phân xử bất đồng theo ảnh gốc, timestamp và calibration. Box Car L3/R5 cùng L2/L7/L8 tại `adasind_258420.jpg` vẫn là ca mở; không đưa các nhãn này vào gold cho tới khi reviewer thứ hai phân xử.
