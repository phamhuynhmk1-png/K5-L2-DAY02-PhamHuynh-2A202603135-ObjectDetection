# Mini guideline — bài làm cá nhân

Thứ tự lớp dùng trong bài (theo `data.yaml`): `0: car`, `1: van`, `2: truck`, `3: bus`.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` | Xe con chở người: sedan, hatchback, SUV, taxi, xe MPV gầm thấp | Mui thấp, đuôi xe dốc hoặc có cốp tách rời; SUV/MPV vẫn là `car` nếu mui không cao vuông như van |
| `truck` | Xe chở hàng có cabin tách biệt với thùng hàng: xe tải thùng, xe ben, xe bồn, xe cứu hộ | Cabin phía trước + thùng/bồn/cẩu phía sau; bánh lớn, thường có hai trục trở lên |
| `bus` | Xe chở khách cỡ lớn: xe buýt thành phố, xe buýt nối toa, xe khách | Thân dài hình hộp, nhiều cửa sổ dọc hai bên, cửa lên xuống ở hông |
| `van` | Xe thùng/minivan thân hộp liền khối, mui cao, chở người hoặc hàng nhẹ; minibus nhỏ | Thân hộp cao, đầu xe ngắn, kính sau gần thẳng đứng; ngắn hơn hẳn `bus` |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: box ôm sát phần thân xe nhìn thấy được (cả gương, cản), không lấy thêm bóng xe, mặt đường hay xe bên cạnh; mỗi xe một box riêng, không gộp hai xe vào một box.
- Vật thể bị che khuất: vẫn gán nếu còn nhận ra được lớp; box chỉ bao phần nhìn thấy, không đoán phần bị che.
- Vật thể bị cắt bởi rìa ảnh: gán box chạm đúng rìa ảnh nếu phần còn lại đủ để nhận ra lớp; không kéo box ra ngoài ảnh.
- Vật thể rất nhỏ/mơ hồ: không gán xe ở quá xa, cao dưới khoảng 3% chiều cao ảnh hoặc chỉ còn vài pixel, vì không xác định chắc được lớp và vị trí box.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_007` | Nhiều xe rất nhỏ ở cuối đường, phía xa camera, chỉ còn vài pixel | Không gán các xe cao dưới ~3% ảnh; chỉ gán xe còn thấy rõ hình dạng | Không xác định chắc được lớp và cạnh box; gán sẽ tạo box mơ hồ, sai lệch |
| `drive_019` | Hai xe MPV/SUV thân khá cao ở làn bên trái, dễ nhầm với `van` | Gán `car` | Mui không cao vuông, đầu xe dài, có dáng xe con; `van` chỉ dành cho xe thân hộp liền khối mui cao |
| `drive_012` | Xe chở khách cỡ nhỏ (minibus), thân hộp nhưng ngắn | Gán `van` | Ngắn hơn hẳn xe buýt thành phố, không có nhiều cửa sổ dọc như `bus`; thân hộp liền khối giống van |
