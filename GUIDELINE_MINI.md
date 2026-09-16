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
| Hông của người mặc quần áo dài | v=1 | hông còn trong ảnh nhưng vì quần áo dài nên không thể xác định chính xác vị trí giải phẫu ![Tình huống 1](Tình%20huống%201.png) |
| Tai bị tóc hoặc mũ bảo hiểm che một phần | v=1 | vì không thể xác định chính xác vị trí giải phẫu ![Tình huống 2](Tình%20huống%202.png) |
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) | điền các khớp ở phần trên v=1 hoặc v=2 cụ thể, các phần ở dưới v=0 | các phần không có trong ảnh điền v=0, các phần còn lại v=1 hoặc v=2 cụ thể theo từng trường hợp ![Tình huống 3](Tình%20huống%203.png) |
| Cổ tay nằm sau tay lái / sau thân mình | v=1 | còn trong khung ảnh, bị che nên không thể xác định chính xác ![Tình huống 4](Tình%20huống%204.png) |
| Hai người chồng lên nhau | các khớp bị che và được xác định giải phẫu là còn trong ảnh có v =1 | Vì các khớp đó chỉ bị che ![Tình huống 5](Tình%20huống%205.png) |
| Người nhỏ đến mức nào thì không gán nữa | người nhỏ đến mức các khớp quá gần nhau trên ảnh thì không gán | Rất khó phân biệt khi các khớp ở quá gần nhau. Không có ảnh nào có trường hợp này|


Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh `train_20.jpg`, người thứ `1`, khớp `left_wrist`

- Mơ hồ ở chỗ nào: Cổ tay và khuỷu tay trái rất khó xác định
- Bạn quyết thế nào: Xác định dựa trên kiến thức giải phẫu
- Vì sao: Cách xác định này giúp giữ đúng quan hệ giải phẫu giữa vai, khuỷu tay và cổ tay.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Nếu xóa keypoint hoặc gán `v=0`, model có thể học rằng những trường hợp khớp bị che thì không cần dự đoán vị trí của khớp đó.

### Ca 2 - ảnh `train_02.jpg`, người thứ `1`, khớp `right_eye`, `left_eye`, `right_ear`, `left_ear` và `nose`

- Mơ hồ ở chỗ nào: người trong ảnh quay mặt ngược lại, vừa mơ hồ về vị trí, nếu không có attribute thì thậm chí có thể bị coi là đánh sai trái phải
- Bạn quyết thế nào: Vẫn đặt keypoint vào vị trí giải phẫu có thể suy ra từ vị trí và hình dạng phần đầu theo đúng thứ tự thực tế.
- Vì sao: Vì dù người quay mặt ngược lại, vị trí các keypoint vẫn có thể được xác định dựa trên quan hệ giải phẫu giữa mắt, tai và mũi; việc giữ đúng thứ tự trái/phải giúp thống nhất cách gán nhãn giữa các ảnh.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Nếu người khác quyết ngược lại thì model học sai cái gì: Model có thể học sai quan hệ trái/phải của các keypoint vùng đầu, dẫn đến việc dự đoán left_eye thành right_eye và ngược lại, tương tự với hai tai, đặc biệt trong những tư thế người quay lưng hoặc quay mặt khỏi camera.

### Ca 3 - ảnh `train_13.jpg`, người thứ `2`, người thứ `3`, toàn bộ keypoint

- Mơ hồ ở chỗ nào: Hai người này quá mờ và quá khó để gán nhãn.
- Bạn quyết thế nào: Vẫn gán nhãn, dựa vào kiến thức giải phẫu để đặt khớp
- Vì sao: Kết quả gold cho thấy `train_13.jpg` ban đầu bị thiếu hai người, với người #1 có OKS = 0.000.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Model có thể học rằng những người quá mờ hoặc khó quan sát thì không cần gán nhãn, dẫn đến việc bỏ sót người và toàn bộ keypoint, làm giảm khả năng phát hiện và ước lượng pose đối với những người có chất lượng hình ảnh thấp.
