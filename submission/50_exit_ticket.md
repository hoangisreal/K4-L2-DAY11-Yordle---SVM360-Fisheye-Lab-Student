# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling
đã nằm trong file tương ứng nên không hỏi lại ở đây.

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy
   tắc riêng? Vì sao? **Cần policy cross-camera riêng trước khi gọi là `DUPLICATE`.** Cùng một vật có thể đồng thời xuất hiện trên hai ảnh fisheye với hình chiếu, kích thước box và zone khác nhau. Cần biết timestamp đồng bộ, phiên bản calibration và output đích sẽ giữ box theo từng camera hay hợp nhất trong BEV; nếu chưa có policy đó thì hai box có thể đều hợp lệ trong annotation space riêng.
2. Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái
   Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera. **Giữ cùng ID** khi còn bằng chứng hình ảnh cho thấy cùng vật trong cùng camera; thêm keyframe khi hình học/pose thay đổi đáng kể hoặc cần mốc mới theo guideline; đặt `Outside` khi vật rời khỏi trường nhìn theo quy ước của task. Không nối ID qua camera chỉ vì class/appearance giống nhau: cần timestamp đồng bộ, calibration cùng phiên bản, vùng overlap/đặc trưng nhận dạng và policy cross-camera được duyệt.
3. Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`),
   bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm? Ở `adasind_310008.jpg`, finding ban đầu `L2+L5` ghi nhận hai người sát nhau và QA đặt câu hỏi có thể là box trùng. Soi ảnh gốc cho thấy bốn người riêng biệt; v2 giữ hai người phía trái thành hai box riêng và chỉnh ranh từng người, thay vì xóa một box chỉ để giảm overlap. Lượt QA mù này do Codex thực hiện vai B theo chỉ dẫn; theo lời người dùng, Tiến đã xem lại bản khóa ngày 29/09 và đồng ý trong lượt soát có tham chiếu. Nếu làm lại, tôi sẽ phóng to cụm người và chốt từng cá thể trên ảnh gốc trước khi mở reference; với L3/R5 ở frame 258420, tôi sẽ để bất đồng mở cho review thứ hai thay vì ép nhãn theo một nguồn duy nhất.
