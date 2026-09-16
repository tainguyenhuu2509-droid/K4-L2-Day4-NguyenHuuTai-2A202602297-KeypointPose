# Mini guideline - nhóm: SOLO  |  người gán: Nguyễn Hữu Tài  |  ngày: 16/9/2026

> Điền file này **trong lúc** gán nhãn, không phải sau khi xong. Mỗi lần bạn dừng lại
> hơn 10 giây để phân vân, đó là một dòng phải ghi vào đây.

## 1. Luật bắt buộc (đã thống nhất cả lớp - không sửa)

- Bộ 17 điểm COCO, đúng tên, đúng thứ tự. Lấy từ file `.SVG` chung.
- Mọi người trong ảnh đều có **đủ 17 điểm**. Điểm không dùng được thì gắn cờ, không xoá.
- Trái/phải tính theo **cơ thể người**, không theo bức ảnh.
- Bị che, còn trong khung -> `v = 1`, **vẫn đặt chấm** ở vị trí ước lượng.
- Ra ngoài mép ảnh -> `v = 0`, **không** đặt chấm.
- Không dùng `Hidden` (`h`) - nó không được lưu vào file.

## 2. Luật của nhóm bạn (phải điền)

| Tình huống | Luật nhóm bạn chọn | Vì sao |
| --- | --- | --- |
| Hông của người mặc quần áo dài | v=1 | hông còn trong ảnh nhưng vì quần áo dài nên không thể xác định chính xác vị trí giải phẫu ![alt text](image.png) |
| Tai bị tóc hoặc mũ bảo hiểm che một phần | v=1 | vì không thể xác định chính xác vị trí giải phẫu |
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) | điền các khớp ở phần trên v=1 hoặc v=2 cụ thể, các phần ở dưới v=0 | các phần không có trong ảnh điền v=0, các phần còn lại v=1 hoặc v=2 cụ thể theo từng trường hợp |
| Cổ tay nằm sau tay lái / sau thân mình | v=1 | còn trong khung ảnh, bị che nên không thể xác định chính xác |
| Hai người chồng lên nhau | các khớp bị che và được xác định giải phẫu là còn trong ảnh có v =1 | Vì các khớp đó chỉ bị che |
| Người nhỏ đến mức nào thì không gán nữa | người nhỏ đến mức các khớp quá gần nhau trên ảnh thì không gán | Rất khó phân biệt khi các khớp ở quá gần nhau |


Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh `______`, người thứ `___`, khớp `______`

- Mơ hồ ở chỗ nào:
- Bạn quyết thế nào:
- Vì sao:
- Nếu người khác quyết ngược lại thì model học sai cái gì:

### Ca 2 - ảnh `______`, người thứ `___`, khớp `______`

- Mơ hồ ở chỗ nào:
- Bạn quyết thế nào:
- Vì sao:
- Nếu người khác quyết ngược lại thì model học sai cái gì:

### Ca 3 - ảnh `______`, người thứ `___`, khớp `______`

- Mơ hồ ở chỗ nào:
- Bạn quyết thế nào:
- Vì sao:
- Nếu người khác quyết ngược lại thì model học sai cái gì:

## 4. Sau khi so visibility report với bạn cùng nhóm

- Khớp lệch `%v=1` nhiều nhất: `______` (bạn `___%` / họ `___%`)
- Nguyên nhân là **guideline chưa rõ** hay **một trong hai bên gán sai**:
- Luật mới bổ sung vào mục 2 sau khi thống nhất:
