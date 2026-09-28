# Nguồn ảnh minh chứng

- `hoang-cvat-truck-bike-236370.png`: ảnh chụp CVAT do Hoàng cung cấp trước khi khóa bản B4-edge; dùng để trao đổi xe thùng bạt (`L1 Truck`) và cụm người/xe hai bánh ở `adasind_236370.jpg`.
- `hoang-cvat-threewheeler-258420-early.png`: ảnh chụp CVAT do Hoàng cung cấp ở bản sớm của `adasind_258420.jpg`; cho thấy hai xe ba bánh và vùng ego đã vẽ lúc đó. Ảnh này **không chứng minh** polygon hoặc box của bản đã khóa cuối cùng. Đối chiếu bản khóa bằng `submission/r1_craft/annotations.xml` và `submission/r2_qa/qa_overlay.html`.

QA mù/recheck đã được Codex thực hiện theo chỉ dẫn của người dùng; overlay kiểm bản khóa r1 ở `submission/r2_qa/qa_overlay.html`, còn overlay CVAT sau rework đã được kiểm trên job trước khi export. Hai ảnh PNG có sẵn là ảnh thật của CVAT nhưng là ảnh trước khóa; không dùng chúng làm bằng chứng rằng Tiến đã tự QA mù hay rằng chúng thể hiện bản v2. Theo lời người dùng, Tiến đã xem lại r1/v2 khóa ngày 29/09 và đồng ý sau khi đã xem reference/model; xem `submission/r2_qa/qa_review.md` để phân biệt hai lượt soát.
