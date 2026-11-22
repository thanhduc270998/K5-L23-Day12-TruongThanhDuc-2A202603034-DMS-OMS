# Tự đánh giá — Trương Thành Đức · G08

## 1. Tự rà soát 4 cảnh

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| `S08_rgb.png` | `person` (trong `infant_seat`) | `extra`, `seat_flip` | Vẽ thừa box `person` lồng trong `infant_seat`, lại còn gán nhầm `seat=rear_left` trong khi bên `S08_ir` là `rear_right` | Đã sửa ở bản v2 |
| `S07_ir.png` | `face` (ghế `rear_right`) | `lr_flip` | Gán `eye_left=open`, `eye_right=unknown`, bị đảo ngược so với bản `S07_rgb` của chính mình | Đã sửa ở bản v2 |
| `D04.png` | `face13` (`mouth_left`) | `flag` | Để `occluded=0` ở điểm khóe miệng trái, lúc so với bài Quang mới thấy cần kiểm lại để bật cờ che khuất | Đã sửa ở bản v2 |
| `D01.png` | `person`, `face`, `face13`, `hand` | `ok` | Đủ box và 13 điểm mặt, mắt trái có `y` lớn hơn mắt phải đúng chiều ảnh xoay 90 độ, hai tay đúng trái/phải theo người | Không cần |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

- **Lỗi:** Vẽ thừa box `person` lồng bên trong `infant_seat` / `child_seat` (lặp ở `S01`, `S02`, `S04`, `S08`) và chọn `occupied=yes` ở `S02` dù guideline v1.0 không có giá trị `yes`.
- **Vì sao mình mắc:** Nhìn thấy trong ghế có hình giống trẻ em nên theo thói quen vẽ thêm `person`, đọc chưa kỹ mục 3 và 4.2 nên quên quy định không gán trẻ em và không dùng `occupied=yes` trên bộ SVIRO.
- **Lần sau tránh bằng cách:** Trước khi gán sẽ đọc kỹ bảng "Gán và không gán" (mục 4.2) và các giá trị hợp lệ trong `labels_cabin_v1.json`; gặp trường hợp lạ ngoài guideline thì hỏi coach ngay thay vì tự thêm nhãn.

## 3. Ghi chú về disagreement_log

- **Dòng Quang đúng và mình sai:** `S07_ir.png` — `face` (`eye_left`, `eye_right`): mình gán `open` / `unknown`, còn Quang gán `unknown` / `open` (trùng với chính bản `S07_rgb` của mình).
- **Mình học được gì:** Lúc copy hoặc chỉnh lại thuộc tính giữa bản `_rgb` và `_ir` rất dễ bấm nhầm trái/phải nếu làm nhanh; lần sau gán xong cặp ảnh cùng cảnh nên rà lại hai bản cạnh nhau một lượt cho khỏi tự lệch nhau.
