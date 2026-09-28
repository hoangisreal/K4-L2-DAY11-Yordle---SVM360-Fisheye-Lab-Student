# Sensor context

- Rig/camera: ba frame B4-edge là ảnh dọc 1080 × 1920 từ một camera fisheye gắn trên xe đang di chuyển. Ảnh không cung cấp vị trí/góc lắp chính xác, thông số nội tại, ngoại tại hay phiên bản calibration. Không suy ra danh tính front/rear/left/right của hệ SVM bốn camera từ ba frame này.
- Ego body: ở cả ba frame đều thấy người hoặc bộ phận xe chở camera phía trái và sát mép dưới (chân, tay lái hoặc thân xe). Bóng đổ trên mặt đường không phải thân xe. Polygon `ego_body` cần bám phần thân/gương/tay lái nhìn thấy, không ôm bóng hay mặt đường.
- Lens circle: vùng ảnh hữu ích nằm trong vòng kính gần tròn/oval, đỉnh cung ở phần trên và đáy cung gần mép dưới; bên ngoài là viền đen rõ ở trên và dưới. Hai polygon `lens_border` mỗi frame được import sẵn và cần soát theo đúng vành đen trên ảnh gốc.
