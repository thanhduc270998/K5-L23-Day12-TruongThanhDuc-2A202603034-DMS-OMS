# Danh sách lớp v0 — Trương Thành Đức · G08

## DMS (7 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | eye_left, eye_right | open / closed / unknown | Phát hiện tài xế buồn ngủ khi nhắm mắt lâu hoặc chớp mắt chậm | Có, trừ lúc kính bị chói đèn LED hoặc tay che |
| 2 | gaze_zone | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Biết tài xế có đang nhìn đường không hay bị phân tâm nhìn màn hình, nhìn xuống đùi | Có, nhưng ảnh NIR tối hoặc đeo kính thì khó nhìn rõ |
| 3 | face13 | 13 điểm mặt (occluded / outside) | Tính hướng quay đầu, độ mở mắt và phát hiện ngáp | Có, ban đêm vẫn thấy rõ hơn RGB |
| 4 | glasses | none / clear / sun / unknown | Biết tài xế có đeo kính không để hệ thống tránh nhận nhầm trạng thái mắt | Thấy được gọng kính, nhưng kính râm trên NIR hay nhìn giống kính thường nên dễ để unknown |
| 5 | hand (whose, side, on_wheel) | driver/passenger; left/right; yes/no/unknown | Kiểm tra tay tài xế có đang đặt trên vô lăng không, nhất là lúc cần nhận lại lái | Có, nhưng tay ở xa đèn hoặc vùng tối khó nhìn rõ có chạm vô lăng chưa |
| 6 | phone | held / mounted / lap | Cảnh báo tài xế đang cầm hoặc dùng điện thoại khi lái xe | Hơi khó, vì mất màu và vật tối gần tay khó phân biệt cạnh hay màn hình |
| 7 | person.seatbelt | worn_correct / worn_incorrect / not_worn / unknown | Nhắc tài xế thắt dây an toàn hoặc báo khi cài dây sai (luồn dưới nách, lệch vai) | Có nếu dây nổi trên áo, áo tối màu hoặc thiếu sáng thì khó thấy |

## OMS (7 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person (theo seat) | driver / front_passenger / rear_left / rear_middle / rear_right | Đếm số người và biết ghế nào đang có người để nhắc dây an toàn, chỉnh điều hòa, bung túi khí | Có (nhìn theo dáng người) |
| 2 | person.seatbelt | worn_correct / worn_incorrect / not_worn / unknown | Nhắc hành khách ghế trước và ghế sau thắt dây đúng cách | Tùy độ tối và màu áo, dây dễ bị lẫn vào áo tối |
| 3 | child_seat | seat; occupied: no / unknown | Nhận biết ghế có lắp ghế trẻ em để hỗ trợ cảnh báo quên trẻ trong xe | Có (nhìn theo hình dạng) |
| 4 | infant_seat | seat; facing: rear / front | Biết có nôi em bé và đặt quay trước hay sau để tắt túi khí ghế phụ khi lắp quay sau, tránh quên trẻ | Có (nhìn theo hình dạng và chiều đặt) |
| 5 | object | seat; type: bag / box / cup / other | Phân biệt đồ đạc với người ngồi để đỡ báo nhầm nhắc dây an toàn và nhắc đồ bỏ quên | Thấy được dáng đồ vật nhưng không có màu nên khó phân biệt loại |
| 6 | face (OMS) | box khuôn mặt | Giúp chắc chắn hơn đó là người thật chứ không phải đồ vật trên ghế | Có, trừ lúc người ngồi cúi xuống hoặc quay mặt đi |
| 7 | camera_blocked (frame_meta) | yes / no | Báo khi camera bị vật gì che mất để hệ thống biết đang không quan sát được cabin | Có, thấy rõ vùng bị chắn trước ống kính |

## 2 câu hỏi leo thang

1. Câu hỏi: Trong guideline v1.0, `child_seat.occupied` chỉ có `no` và `unknown`, còn phần giới thiệu ghi SVIRO không có trẻ em ngồi. Nếu gặp hình giống trẻ em hoặc búp bê ngồi trong `child_seat`/`infant_seat` thì mình có vẽ thêm `person` ở trong không, hay thêm giá trị `yes` vào `occupied`, hay bỏ qua không gán?
   - Khung ví dụ: `G08 S02_rgb`, `G08 S02_ir` (ghế `rear_left`), `G08 S01_rgb` (ghế `rear_right`).
   - Bạn tạm gán thế nào và vì sao: Lúc đầu mình vẽ thêm box `person` bên trong và để `occupied = yes`, nhưng sau đối chiếu lại guideline và bài của bạn cùng nhóm mới thấy schema không cho phép `yes`. Phần này mình ghi lại để hỏi coach chốt cách xử lý cho đúng, còn tạm thời không nên tự thêm giá trị ngoài guideline.

2. Câu hỏi: Trên ảnh `D##` bị xoay 90 độ, khi tài xế đeo kính và mắt nhìn hơi lệch giữa kính lái (`road`) với màn hình giữa (`center`), lại thêm ảnh NIR khá tối thì dựa vào dấu hiệu nào để chọn `road` hay `center` thay vì để hết sang `other`?
   - Khung ví dụ: `G08 D03`, `G08 D05`.
   - Bạn tạm gán thế nào và vì sao: Mình tạm chọn `other` theo mục 4.5 (không chắc thì để `other`) chứ không đoán `road`, vì ảnh `D03` rất tối khó nhìn hướng tròng mắt và trong nhóm mình với bạn Quang cũng gán khác nhau ở mấy khung này.
