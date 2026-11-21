# Danh sách lớp v0 — Phạm Thanh Tùng · G01

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | eye_state | open / closed / unknown | Đo chỉ số PERCLOS (tỷ lệ phần trăm thời gian mắt nhắm) để cảnh báo tài xế ngủ gật hoặc mất tỉnh táo | Có, thấy rõ khe mắt trên ảnh NIR trừ khi bị lóa đèn hoặc kính cản |
| 2 | gaze_zone | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Xác định vùng chú ý thị giác; phát hiện tài xế lơ đãng (nhìn xuống đùi, nhìn màn hình giải trí quá thời gian cho phép) | Có, suy diễn qua hướng đầu (head pose) kết hợp tâm đồng tử mắt |
| 3 | head_pose (yaw / pitch / roll) | Góc liên tục (-180° đến +180°) | Bổ trợ định hướng vùng nhìn, phát hiện tư thế gục đầu ngủ hoặc quay mặt sang bên quá lâu | Có, các mốc hình học khuôn mặt nổi rất rõ trên ảnh NIR |
| 4 | phone (state) | held / mounted / lap | Phát hiện hành vi sử dụng điện thoại khi đang điều khiển phương tiện (nguy cơ gây tai nạn cao) | Có (hình dạng máy, viền màn hình), nhưng mất màu sắc vỏ máy |
| 5 | hand (on_wheel, side) | on_wheel: yes / no / unknown; side: left / right | Giám sát bàn tay đặt trên vô lăng (Hands-On Detection) phục vụ các tính năng tự hành cấp độ 2/3 (ADAS L2/L3) | Có, đường viền bàn tay và vành vô lăng phân tách rõ |
| 6 | face_expression / yawning | yawn / normal / talk / unknown | Nhận diện biểu cảm ngáp liên tục hoặc nói chuyện kéo dài làm giảm độ tập trung khi lái xe | Có, đo khoảng cách giữa hai mốc môi trên và môi dưới (lip_upper, lip_lower) |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person (seat, seatbelt) | seat: rear_left / rear_middle / rear_right; seatbelt: worn_correct / worn_incorrect / not_worn / unknown | Đếm số lượng hành khách khoang sau; kích hoạt nhắc nhở thắt dây an toàn cho từng vị trí ghế tương ứng | Có thấy người; dây an toàn khó nhìn trên IR nếu trùng màu áo sẫm |
| 2 | child_seat (seat, occupied) | seat: rear_left / rear_middle / rear_right; occupied: yes / no / unknown | Cảnh báo trẻ em bị bỏ quên trên xe (Child Presence Detection - CPD) để kích hoạt còi/điều hòa khẩn cấp | Có, hình dạng ghế trẻ em đặc trưng và kích thước lớn |
| 3 | infant_seat (seat, facing) | seat: rear_left / rear_middle / rear_right; facing: rear / front | Tự động vô hiệu hóa túi khí nếu lắp nôi trẻ em quay ngược (rear-facing) ở ghế trước, hoặc cảnh báo lắp nôi sai quy cách | Có, nhận dạng hình dáng nôi xách và hướng quai xách |
| 4 | object (seat, type) | seat: rear_left / rear_middle / rear_right; type: bag / box / cup / other | Phát hiện hành lý/đồ vật bỏ quên khi tắt máy rời xe; hỗ trợ chống trộm và nhắc nhở tư trang | Có (dựa vào hình khối hình học), mất thông tin màu sắc |
| 5 | seat_occupancy | empty / human / child_seat / object | Tổng hợp trạng thái toàn bộ các ghế trong cabin để điều khiển hệ thống điều hòa vùng thông minh và túi khí | Có, phân biệt rõ người/vật/ghế trống qua độ tương phản nhiệt/hình dạng |
| 6 | passenger_posture | normal / sleeping / out_of_position / leaning | Đánh giá tư thế ngồi bất thường (OutOfPosition - OOP) của hành khách để điều chỉnh lực bung túi khí an toàn | Có, thấy rõ biên dạng cơ thể người |

## 2 câu hỏi leo thang

Câu hỏi bạn muốn hỏi người viết guideline (hoặc khách hàng) vì guideline v1.0 chưa trả lời. Mỗi câu kèm **tên khung** làm ví dụ.

1. Câu hỏi: Khi tài xế đeo kính râm quang học nhưng chụp dưới camera NIR lại trông trong suốt (thấy rõ tròng mắt bên trong), guideline nên quy ước giá trị `glasses` là `clear` (theo hiện tượng nhìn thấy trên ảnh) hay `sun` (theo loại kính thực tế bên ngoài)?
   Khung ví dụ: D02
   Bạn tạm gán thế nào và vì sao: Tạm gán `clear` vì nhìn xuyên qua tròng kính thấy rõ con ngươi và mí mắt theo đúng định nghĩa ở mục 4.5 ("clear là kính cận, nhìn xuyên được tròng"). Tuy nhiên với mô hình thực tế, nếu hệ thống cần biết tài xế có đeo kính râm hay không để bù sáng thì cần một quy chuẩn dứt khoát.

2. Câu hỏi: Khi trên ghế trẻ em (child_seat) có đặt kèm đồ vật nhỏ (như thú bông, bình nước) nằm gọn bên trong, guideline quy định vẽ 2 box riêng cùng seat; vậy với các phụ kiện đi liền theo ghế (đệm lót, mái che gập) có tính là object độc lập hay thuộc về child_seat?
   Khung ví dụ: S03_rgb
   Bạn tạm gán thế nào và vì sao: Tạm gán `child_seat` bao trùm toàn bộ ghế và chỉ vẽ thêm `object` (type = other) cho vật thể rời tách biệt đặt trong lòng ghế theo mục 4.8. Cần guideline bổ sung kích thước ngưỡng tối thiểu của đồ vật trong ghế trẻ em để tránh gán nhãn vụn vặt gây nhiễu cho mô hình phát hiện vật thể.
