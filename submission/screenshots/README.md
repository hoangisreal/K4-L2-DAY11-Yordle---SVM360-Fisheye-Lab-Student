# Nguồn ảnh minh chứng

- `hoang-cvat-truck-bike-236370.png`: ảnh chụp CVAT của Role A trước khi khóa bản B4-edge; dùng để trao đổi xe thùng bạt (`L1 Truck`) và cụm người/xe hai bánh ở `adasind_236370.jpg`.
- `hoang-cvat-threewheeler-258420-early.png`: ảnh chụp CVAT của Role A ở bản sớm của `adasind_258420.jpg`; cho thấy hai xe ba bánh và vùng ego đã vẽ lúc đó. Ảnh này **không chứng minh** polygon hoặc box của bản đã khóa cuối cùng. Đối chiếu bản khóa bằng `submission/r1_craft/annotations.xml` và `submission/r2_qa/qa_overlay.html`.

Overlay kiểm bản khóa r1 nằm ở `submission/r2_qa/qa_overlay.html`; overlay CVAT sau rework đã được kiểm trên job trước khi Role A export v2. Hai ảnh PNG là ảnh thật của CVAT nhưng được chụp trước khi khóa, nên không dùng để chứng minh ranh box/polygon cuối cùng hoặc bản v2. Chúng cũng không chứng minh một lượt QA mù cá nhân của Role B. Role B kiểm tra r1/v2 khóa ngày 29/09 sau khi đã xem reference/model và xác nhận các finding; xem `submission/r2_qa/qa_review.md` để phân biệt artifact QA ban đầu với lượt recheck có tham chiếu.
