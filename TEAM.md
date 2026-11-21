# TEAM — Ngày 12

Mã bộ ảnh: **G01** · Hình thức: nhóm

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Phạm Thanh Tùng | 2A202603159 | có | Phạm Lam Anh (03029) | 87 |
| Phạm Lam Anh | 2A202603029 | có | Phạm Thanh Tùng (03159) | 87 |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- D01.png · person seatbelt: peer ghi `not_worn`, mình ghi `unknown` (ảnh NIR tối, không thấy rõ dải dây an toàn; áp dụng quy tắc 4.4-1 không thấy thì ghi unknown).
- S07_ir / S08_ir · infant_seat facing: peer ghi `rear`, mình ghi `front` (nôi em bé đặt hướng mặt ra phía trước xe).

## Cá nhân

Mỗi người một mục, 1–2 dòng mỗi ý.

### PhamThanhTung-2A202603159
- Phần mình làm (ngoài 22 ảnh của mình, ví dụ ai review ai, ai tổng hợp ca hỏi coach): Tự gán nhãn độc lập 22 ảnh trên CVAT local, chạy cabin_check các checkpoint, thực hiện diff đối chiếu 87 điểm khác biệt với bạn Phạm Lam Anh, tổng hợp tài liệu và hoàn thiện bộ hồ sơ nộp bài E1–E5.
- Điều mình học được hôm nay: Hiểu rõ nguyên lý góc nhìn trong cabin (ghế gọi theo xe, bộ phận gọi theo cơ thể người); phân biệt rõ giữa ảnh IR mô phỏng và ảnh NIR thực tế; luôn rà soát kỹ thuộc tính mặc định của CVAT trước khi xuất dữ liệu.
