# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: Nguyễn Hữu Tài   Nhóm: SOLO   Ngày: 16/9/2026

> Cách dùng: copy file này thành `reports/REPORT.md`. Điền bằng số liệu do công cụ sinh ra;
> không tự ước lượng hoặc sửa số trong file JSON.

## 1. Nhãn của tôi

| Chỉ số | Giá trị |
| --- | ---: |
| Số ảnh đã gán | 20 |
| Số skeleton | 27 |
| v=2 / v=1 / v=0 | 242 / 191 / 26 |
| Thời gian trung bình mỗi ảnh | 7 phút |

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`):

1. `right_hip` — 74%
2. `left_ear` — 67%
3. `right_ear` — 59%

Chúng có đúng là những khớp bạn thấy khó gán nhất không? Nếu không, giải thích.

Các khớp có `%v=1` cao nhất chủ yếu phản ánh việc các khớp này thường bị che khuất trong tập ảnh. Tuy nhiên, `%v=1` cao không đồng nghĩa hoàn toàn với việc đó là những khớp khó xác định vị trí giải phẫu nhất. Kết quả kiểm tra còn cho thấy một số lỗi khác cần xem lại, như đảo trái/phải ở `left_shoulder/right_shoulder` và `left_hip/right_hip` trong `train_02` và `train_16`, cũng như việc dùng `v=0` bất thường ở `train_04` và `train_10`.

## 2. Chấm với gold

| Chỉ số | Trước rework | Sau rework |
| --- | ---: | ---: |
| OKS trung bình | 0.923 | 0.916 |
| OKS@0.50 | 0.897 | 0.966 |
| OKS@0.75 | 0.897 | 0.966 |
| Lỗi `dao_trai_phai` | 1 | 1 |
| Lỗi `nham_nguoi` | 2 | 0 |
| Lỗi `xoa_khop_bi_che` | 0 | 0 |

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

- `train_13.jpg` + người #1 + toàn bộ 17 keypoint + bổ sung người bị thiếu và gán lại đầy đủ các keypoint theo đúng vị trí.
- `train_13.jpg` + người #2 + toàn bộ 17 keypoint + bổ sung người bị thiếu và gán lại đầy đủ các keypoint theo đúng vị trí.
- `train_19.jpg` + người #1 + `left_wrist`, `right_wrist` và các keypoint trái/phải liên quan + sửa lại cặp trái/phải bị đảo, đồng thời đặt lại `left_wrist` và `right_wrist` đúng vị trí khớp.

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?** Ảnh đó dễ hay khó? Nếu là ảnh dễ,
bạn nghĩ vì sao mình vẫn sai?

`train_19.jpg` người #1: OKS 0.391 -> Đảo trái/phải. Ảnh đó khó, bởi người trong ảnh quay mặt ngang 1 góc xấp xỉ 90 độ khiến cho vị trí 2 mắt và 2 tai trái phải gần như tương đương thậm chí nếu góc quay mặt lớn hơn 90 thì trái phải sẽ bị đảo.

## 4. Model

| Chỉ số | yolo26n-pose gốc | Sau fine-tune | Chênh |
| --- | ---: | ---: | ---: |
| pose_mAP50 | 0.8450 | 0.8450 | +0.0000 |
| pose_mAP50-95 | 0.6853 | 0.6853 | +0.0000 |
| pose_precision | 0.9734 | 0.9749 | +0.0015 |
| pose_recall | 0.8462 | 0.8462 | +0.0000 |
| box_mAP50-95 | 0.8119 | 0.8044 | -0.0075 |

### Trả lời năm câu hỏi ở cuối notebook

> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.

1. `pose_mAP50-95` thay đổi bao nhiêu? Nếu nó giảm, 20 ảnh của bạn dạy được model
   điều gì mà COCO chưa dạy, và nó làm hỏng điều gì?

`pose_mAP50-95` không thay đổi: từ 0.6853 ở model `yolo26n-pose` gốc lên 0.6853 sau fine-tune, chênh lệch 0.0000.

Do đó, với kết quả trên tập test này, chưa có bằng chứng cho thấy 20 ảnh train đã tạo ra một thay đổi đo được ở `pose_mAP50-95`. Vì chỉ số này không giảm nên câu hỏi về việc 20 ảnh dạy thêm điều gì nhưng đồng thời làm hỏng điều gì không thể kết luận từ kết quả này.

2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu? Model tìm *người* dễ hơn hay tìm
   *khớp* dễ hơn? Vì sao?

`box_mAP50-95 = 0.8044`, trong khi `pose_mAP50-95 = 0.6853`, chênh nhau 0.1191.

Vì vậy, xét theo hai chỉ số này, model đạt kết quả cao hơn ở nhiệm vụ xác định bounding box người so với xác định chính xác vị trí 17 keypoint. Điều này phù hợp với việc xác định một vùng bao quanh người đơn giản hơn so với việc định vị chính xác từng khớp, đặc biệt ở các khớp nhỏ hoặc bị che khuất.

3. Một ảnh test model đoán sai - gọi tên lỗi theo bốn loại của slide 43
   (lệch nhẹ / đảo trái/phải / nhầm người / trượt hẳn):

Ở `train_19.jpg`, người #1, model mắc lỗi **đảo trái/phải** ở các khớp liên quan đến bên trái/phải và **trượt hẳn** ở `left_wrist` và `right_wrist`. Trong đó, `đảo trái/phải` là lỗi nguy hiểm vì làm sai quan hệ trái/phải của bộ xương, còn `trượt hẳn` là trường hợp chấm keypoint vào vị trí không có khớp.

4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model? Ai đúng, và bạn dựa vào đâu?

Ảnh có OKS thấp nhất giữa model và nhãn của tôi là `train_19.jpg`. Skeleton người #1 có OKS = 0.323. Khi đối chiếu với gold, chính skeleton này cũng được xác định có lỗi `đảo trái/phải` và `trượt hẳn` ở `left_wrist` và `right_wrist`. Sau khi xem lại ảnh tôi thấy `left_wrist` và `right_wrist` đánh khá chuẩn về mặt giải phẫu, vấn đề trái phải thì do mặt người trong ảnh đang quay ngang so với màn hình, việc ước lượng mắt, tai trái có thể sai lệch và không thể xác nhận 1 cách chính xác. Bởi vậy, không thể kết luận ai sai ai đúng.

5. Ảnh bạn gán tệ nhất có *cũng* là ảnh model đoán tệ nhất không? Nếu có, điều đó
   nói gì về bức ảnh đó?

Không. Trước rework, lỗi annotation nghiêm trọng nhất của tôi nằm ở `train_13.jpg`, nơi tôi thiếu hai người so với gold. Trong khi đó, OKS thấp nhất giữa model và nhãn của tôi là ở `train_19.jpg` với OKS = 0.323.

Điều này cho thấy hai trường hợp lỗi không hoàn toàn trùng nhau: `train_13.jpg` có vấn đề về số lượng người được gán, còn `train_19.jpg` có vấn đề về vị trí và trái/phải của keypoint. Vì vậy, không thể dùng việc model cũng có điểm thấp để tự động kết luận rằng annotation của tôi sai.

## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người,
khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.

<!-- Cấu trúc gợi ý: (1) train_XX + người thứ mấy + keypoint; (2) căn cứ thị giác như phần cơ
thể liền kề, trang phục hoặc vật che; (3) vì sao khớp còn trong khung (v=1) hay đã ra khỏi
khung (v=0). -->

## 5. Một rule evidence bạn đã dùng

Trong `train_11.jpg`, người #1, tôi phải quyết định trạng thái visibility cho keypoint `right_knee`, `left_knee`, `right_ankle` và `left_ankle`. Phần đầu gối theo kiến thức giải phẫu vẫn nằm trong ảnh dù bị che toàn bộ (bởi vậy tôi để v=1), nhưng đối với phần cổ chân thì lại dựa vào tư thế chân của nhân vật trong ảnh để xác định còn hay ngoài ảnh (tôi để v=0).