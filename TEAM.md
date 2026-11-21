# TEAM — Ngày 12

Mã bộ ảnh: **G08** · Hình thức: nhóm

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Huỳnh Nhật Quang| 2A202603113 | đã gán đủ | Nhóm | 11 |
| Trương Thành Đức  | 2A202603034 | đã gán đủ | Nhóm | |
| Vũ Việt Anh  | 2A202603214 | đã gán đủ | Nhóm | |

Ca ba bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):
**G08 S01 (`infant_seat` — `seat`):** Không thống nhất vị trí ghế sau (`rear_left` hay `rear_right`) do góc nhìn chéo từ camera trước xuống hàng ghế sau.
**G08 D01, D03, D05 (`face` — `gaze_zone`):** Hướng nhìn của tài xế nằm ở ranh giới giữa nhìn thẳng đường (`road`), màn hình trung tâm (`center`) và vùng khác (`other`).

## Cá nhân

### Trương Thành Đức - 2A202603034
- Phần mình làm: Chạy `cabin_check diff` để review chéo bài của Quang, cùng nhóm đối chiếu các chỗ lệch nhãn và ghi lại mấy ca khó (`S01`, `D01`, `D03`, `D05`) để hỏi coach.
- Điều mình học được hôm nay: Gán ghế phải tính theo chiều xe chứ không theo góc ảnh, trái/phải của mắt và tay tính theo người (nhất là ảnh `D##` bị xoay 90°), và chỗ nào không thấy rõ thì ghi `unknown` thay vì đoán.
