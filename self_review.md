# Tự đánh giá — Phạm Thanh Tùng · G01

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S03_rgb | child_seat | ok | Ghế trẻ em ở vị trí bên phải ảnh ứng với rear_left theo xe; occupied=yes hợp lý | Đã xong |
| S05_ir | child_seat | ok | Đối chiếu chuẩn xác với ảnh RGB cùng cảnh; seat theo xe đúng | Đã xong |
| D01 | hand (trái/phải) | lr_flip | Ban đầu để giá trị mặc định của CVAT là side=left cho cả hai tay; đã sửa lại phân định tay trái/phải theo người | Đã sửa |
| D04 | face13 | ok | Kiểm tra kỹ trên ảnh xoay 90°: mắt trái nằm ở toạ độ y lớn hơn mắt phải; các điểm bị che có gắn cờ occluded/outside | Đã xong |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Để nguyên giá trị mặc định (`side = left`) cho tất cả các đối tượng `hand` ở các khung D01–D06 mà không kiểm tra lại từng tay, đồng thời ban đầu script báo lỗi thuộc tính `child_seat occupied = yes` do schema mặc định chỉ cho phép `unknown/no`.

Vì sao mình mắc: CVAT tự động gán giá trị đầu tiên trong danh mục thuộc tính khi tạo mới hình hộp (`side: left`). Khi thao tác nhanh các khung hình DMS có nhiều đối tượng cùng lúc, mình đã bỏ sót việc mở rộng tab DETAILS bên phải màn hình để đổi lại `side = right` cho bàn tay phải của người lái.

Lần sau tránh bằng cách: Thiết lập thói quen kiểm tra checklist ngay sau khi vẽ xong một đối tượng: Vẽ box -> Bấm mở DETAILS -> Chọn đúng `side` (theo góc nhìn cơ thể người, không theo màn hình) -> Kiểm tra `on_wheel` trước khi chuyển sang đối tượng tiếp theo. Luôn chạy `cabin_check.py` sớm ở các checkpoint nhỏ để phát hiện lỗi thuộc tính hệ thống.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai: Ở một số điểm `face13` trên ảnh D05 (các điểm quanh mắt bị che khuất), bạn mình đánh cờ `occluded` còn mình đánh cờ `outside`. Sau khi đối chiếu lại, vùng mắt vẫn nằm trọn trong khuôn mặt hiển thị trên ảnh, việc ước lượng vị trí giải phẫu mắt tương đối khả thi nên cờ `occluded` của bạn phù hợp và chính xác hơn `outside`. Mình học được cách phân biệt ranh giới rõ ràng hơn giữa việc "không nhìn thấy nhưng ước lượng được vị trí tương đối trên cơ thể" (`occluded`) và "hoàn toàn lệch ra ngoài vùng ảnh hoặc bị che lấp không thể nội suy" (`outside`).
