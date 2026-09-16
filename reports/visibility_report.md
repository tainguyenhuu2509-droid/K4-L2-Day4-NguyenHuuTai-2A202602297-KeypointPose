# Visibility report

- Thư mục nhãn: `dataset/labels/train`
- 20 ảnh, 27 skeleton, trung bình 16.04 khớp có v > 0 mỗi người
- Tổng: v=2 242 | v=1 191 | v=0 26

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 20 | 7 | 0 | 26% |
| 1 | left_eye | 16 | 11 | 0 | 41% |
| 2 | right_eye | 15 | 12 | 0 | 44% |
| 3 | left_ear | 9 | 18 | 0 | 67% |
| 4 | right_ear | 11 | 16 | 0 | 59% |
| 5 | left_shoulder | 21 | 6 | 0 | 22% |
| 6 | right_shoulder | 23 | 4 | 0 | 15% |
| 7 | left_elbow | 17 | 10 | 0 | 37% |
| 8 | right_elbow | 19 | 8 | 0 | 30% |
| 9 | left_wrist | 15 | 12 | 0 | 44% |
| 10 | right_wrist | 16 | 10 | 1 | 37% |
| 11 | left_hip | 11 | 15 | 1 | 56% |
| 12 | right_hip | 6 | 20 | 1 | 74% |
| 13 | left_knee | 13 | 11 | 3 | 41% |
| 14 | right_knee | 12 | 11 | 4 | 41% |
| 15 | left_ankle | 10 | 9 | 8 | 33% |
| 16 | right_ankle | 8 | 11 | 8 | 41% |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
