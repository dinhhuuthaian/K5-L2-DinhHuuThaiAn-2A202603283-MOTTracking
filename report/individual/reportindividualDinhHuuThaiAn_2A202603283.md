# Báo cáo cá nhân — NguyenVanDemo-DEMO2024

> **FILE MẪU ĐÃ ĐIỀN** — chỉ để xem format. Không nộp file này.
> Đề B (MSSV demo `DEMO2024`). Số frame ghi theo CVAT (0–149).
> Ảnh che khuất ở mục 3 là đường dẫn mẫu; bạn phải chụp ảnh thật của mình.

Đoạn video: MOT17-09, 150 frame (frame 1–150), nguồn MOTChallenge, giấy phép CC BY-NC-SA 3.0.

## 0. Thông tin học viên

- Họ tên: Đinh Hữu Thái An
- MSSV: 2A202603283
- Mã đề (A/B/C): **A**
- Email: dinhhuuthaian9191@gmail.com
- Link repository: https://github.com/dinhhuuthaian/K5-L2-DinhHuuThaiAn-2A202603283-MOTTracking
- Giờ bắt đầu: 16h
- Giờ kết thúc: 21h

## 1. Xem trước đoạn video (CP0)

Ghi **trước khi vẽ**, mỗi người một dòng.

| Mã | Frame xuất hiện | Frame cuối thấy được | Rẽ / dừng / đổi tốc độ ở frame | Bị che ở frame | Ghi chú |
|---|---|---|---|---|---|
| P1 | 0 | 137 | ~35–42 đổi tốc độ bắt đầu đi nhanh hơn | 112 (đi sau người khác) | Ra khỏi khung trước 139 → sẽ bật `outside` |
| P2 | 0 | 148 | ~38 dừng | bị che ở 106 | người chọn là cp2 |
| P3 | 0 | 149 | ~37 dừng | bị che ở 38 | Ra khỏi khung trước 110 → sẽ bật `outside` |
| P4 | 40 | 149 | gần như không thay đổi gì | không bị che | Dễ lẫn với p5 khi đi sát |
| P5 | 2 | 149 | gần như không thay đổi gì | không bị che | Dễ lẫn với P4 lúc đi sát |

## 2. Keyframe và thời gian (CP1, CP4)

Số keyframe lấy từ kết quả `src/check_submission.py`.

| Mã | Số keyframe | Keyframe ở frame | Số frame có mặt | Keyframe / 100 frame | Thời gian (phút) | Chỗ khó |
|---|---|---|---|---|---|---|
| P1 | 97 | 0, 10, 20, 30, 40, 89, 90, 98, 100, 102, 103, 108, 113, 136, 137, 138, 139, 140 | 138 | 70,3 | 18 | Đoạn che 113-140 |
| P2 | 20 | 0, 10, 20, 30, 40, 60, 77, 81, 89, 90, 92, 94, 95, 96, 105 | 121 | 13,5 | 12 | Đoạn che 102-138 |
| P3 | 15 | 0, 10, 20, 30, 40, 41, 42, 45, 49, 50, 51, 54, 55, 56, 57, 58, 59, 60, 75, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 105, 106, 107, 111, 117, 118, 119, 125, 131, 132, 133, 134, 135, 136, 137, 142, 143, 144, 145, 147, 148, 149 | 150 | 13,8 | 11 | outside từ 109  |
| P4 | 52 | 0, 10, 20, 30, 40, 60, 65, 73, 74, 75, 84, 85, 88, 90, 91, 92, 93, 97, 100, 101, 105, 107, 123, 124, 125, 126, 127, 128, 131, 135, 136, 137, 140, 141, 142, 143, 145, 146, 147, 148, 149 | 110 | 34,7 | 10 | không có gì khó |
| P5 | 41 | 0 | 0 | 0 | 0 | 0 |
| **Tổng** | **225** | | **695** | | **32** | |

Keyframe / 100 frame của cả bài = tổng keyframe ÷ tổng số frame có mặt × 100 = 60 ÷ 659 × 100 ≈ **9,1**

Bạn đặt keyframe nhiều nhất ở người nào? Vì sao (người đó rẽ, dừng, lại gần camera hay bị che)?

P1 — vì có đoạn bị che dài và đổi hướng trước/sau chỗ che; cần keyframe dày quanh 69–70 và 95–96 để nội suy không cắt góc và không nhảy box khi tắt `outside`.

## 3. Đoạn bị che (CP2)

Người bị che: `P2`

| Mốc | Frame |
|---|---:|
| Bắt đầu bị che một phần (bật `occluded`) | 106 |
| Mất hẳn (bật `outside`) | 112 |
| Hiện lại (tắt `outside`) | 136 |
| Thấy rõ trở lại (tắt `occluded`) | 141 |

- Thời gian khuất hẳn: **17** frame = **0,57** giây (17/30).
- Quyết định: **giữ cùng ID**.
- Lý do (trả lời 3 câu: khuất bao lâu so với 60 frame, ngoại hình có khớp, chỗ hiện lại có đúng hướng và tốc độ):

1. Khuất hẳn 17 frame ≪ 60 frame (ngưỡng 2 giây của lớp) → đủ điều kiện giữ cùng track.  
2. Áo/quần và dáng lúc hiện lại khớp P1 trước khi che; không nhầm với người đi ngang.  
3. Hiện lại đúng phía đường đi cũ, tốc độ tương đương → tắt `outside` ở 95, chỉnh box (keyframe mới), không tạo track mới.

Ảnh chụp màn hình:

![Trước khi che](images/che_1_truoc.png)
![Giữa đoạn che, thấy cờ trên panel object](images/che_2_giua.png)
![Sau khi hiện lại, cùng ID](images/che_3_sau.png)

*(Trong bản nộp thật: đặt 3 ảnh đã chụp vào `report/individual/images/` với đúng tên trên.)*

## 4. Tự review ID (CP3)

Lượt 1 theo người (đi ngược từ frame 149 về 0 trên CVAT), lượt 2 theo cảnh (nhảy 10 frame). Ít nhất 3 dòng; không có lỗi thì ghi một dòng "đã kiểm hai lượt, không lỗi".

Loại lỗi dùng đúng một trong 7 mã: `id_switch`, `fragmentation`, `lost`, `merge`, `false_track`, `drift`, `flag`.

| Frame | Mã người | Loại lỗi | Mô tả một câu | Phát hiện ở lượt | Đã sửa? |
|---:|---|---|---|---|---|
| 52 | P5 | `lost` | đọc báo cáo thì thấy p5 có keyframe nhưng lại k có frame ạ | 1 | Chưa sửa được ạ |


Tổng hợp số lỗi theo loại:

| `id_switch` | `fragmentation` | `lost` | `merge` | `false_track` | `drift` | `flag` |
|---:|---:|---:|---:|---:|---:|---:|
| 0 | 0 | 1 | 0 | 0 | 0 | 0 |

Lỗi nào chỉ lượt 2 (theo cảnh) mới thấy, lượt 1 (theo người) không thấy? Vì sao?

## 5. File xuất và kết quả tự kiểm (CP4)

| Kiểm tra | Kết quả |
|---|---|
| Tên file MOT 1.1 | `DinhHuuThaiAn_mot.zip` |
| Tên file CVAT for video 1.1 | `DinhHuuThaiAn_cvat_video.zip` |
| Số track ID khác nhau trong `gt/gt.txt` (phải là 5) | 5 |
| Frame `outside` không có dòng trong `gt.txt` (đúng / sai) | đúng |
| Job đã completed trên CVAT máy cá nhân | có |

Dán phần tóm tắt in ra từ `src/check_submission.py`:

Số frame in theo CVAT (bắt đầu từ 0). Trong gt.txt, frame_id = frame CVAT + 1.

=== File MOT 1.1: DinhHuuThaiAn_mot.zip ===
  Số track ID: 5   |   Tổng số box: 695
  [OK]        Đúng 5 track ID.

  Track | Frame có mặt | Số frame | Đoạn vắng (outside)
      1 |   0–137      |      138 | -
      2 |   0–147      |      148 | -
      3 |   0–108      |      109 | -
      4 |   0–149      |      150 | -
      5 |   0–149      |      150 | -


=== File CVAT for video 1.1: DinhHuuThaiAn_cvat_video.zip ===

  Track | Nhãn   | Frame thấy | Keyframe | KF/100 frame | Frame occluded | Lần bật outside
      0 | person |        138 |       97 |         70.3 |             26 |               1
              Track 0: keyframe ở frame [0, 3, 10, 20, 22, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 52, 53, 54, 55, 56, 57, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100, 101, 102, 103, 104, 105, 106, 107, 108, 109, 110, 111, 112, 116, 118, 119, 120, 124, 125, 132, 133]
  [CẢNH BÁO]  Track 0: 70 keyframe / 100 frame > 50. Quá dày, dồn keyframe vào chỗ rẽ / dừng / bị che.
      1 | person |        148 |       20 |         13.5 |             58 |               1
              Track 1: keyframe ở frame [0, 10, 20, 30, 40, 89, 90, 98, 100, 102, 103, 108, 113, 136, 137, 138, 139, 140, 141, 142]
      2 | person |        109 |       15 |         13.8 |             20 |               1
              Track 2: keyframe ở frame [0, 10, 20, 30, 40, 60, 77, 81, 89, 90, 92, 94, 95, 96, 105]
      3 | person |        150 |       52 |         34.7 |              0 |               0
              Track 3: keyframe ở frame [0, 10, 20, 30, 40, 41, 42, 45, 49, 50, 51, 54, 55, 56, 57, 58, 59, 60, 75, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 105, 106, 107, 111, 117, 118, 119, 125, 131, 132, 133, 134, 135, 136, 137, 142, 143, 144, 145, 147, 148, 149]
      4 | person |        150 |       41 |         27.3 |              0 |               0
              Track 4: keyframe ở frame [0, 10, 20, 30, 40, 60, 65, 73, 74, 75, 84, 85, 88, 90, 91, 92, 93, 97, 100, 101, 105, 107, 123, 124, 125, 126, 127, 128, 131, 135, 136, 137, 140, 141, 142, 143, 145, 146, 147, 148, 149]
      5 | person |          0 |        0 |          0.0 |              0 |               0
              Track 5: keyframe ở frame []
  [CẢNH BÁO]  Track 5 chỉ thấy 0 frame: có thể là shape rời (vẽ bằng Shape) hoặc track thừa.

  Tổng: 225 keyframe / 695 frame có mặt = 32.4 keyframe / 100 frame
  [OK]        Đọc được 6 track từ annotations.xml.

=== Tóm tắt ===
  Lỗi: 0   |   Cảnh báo: 2
  Không có lỗi định dạng. Mở CVAT xem lại từng [CẢNH BÁO]; cảnh báo đúng ý bạn thì ghi lý do vào báo cáo.

## 6. Ba câu kết

1. Nếu được gán lại, bạn sẽ đặt keyframe khác ở đâu? Vì sao?
   p1 và p5 ở keyframe 10~20 tại vì khi đó thì thấy rõ người chắc chắn sẽ đi vào khung hình	
  
2. Có chỗ nào bạn không chắc "cùng ID hay ID mới"? Bạn đã quyết định và ghi chú thế nào?

   Trong quá trình tracking, em không có trường hợp nào quá phân vân về việc giữ ID cũ hay tạo ID mới. Em dựa vào vị trí xuất hiện, hướng di chuyển, trang phục và đặc điểm của người để xác định ID.

3. Một lỗi ID trong job của bạn (nếu không còn sót, chọn lỗi đã sửa) có thể làm xe tự lái dự đoán sai chuyển động của người đó như thế nào? Lỗi đó ảnh hưởng MOTA hay IDF1 nhiều hơn?
   
   Lỗi mất track (lost) có thể khiến hệ thống xe tự lái không nhận diện và theo dõi liên tục được một người đi bộ. Khi người đó xuất hiện lại, hệ thống có thể không xác định được đó là người đã theo dõi trước đó, dẫn đến dự đoán sai hướng và quỹ đạo di chuyển. Lỗi này ảnh hưởng đến IDF1 nhiều hơn vì IDF1 đánh giá khả năng duy trì danh tính của đối tượng qua các frame, trong khi MOTA tập trung nhiều hơn vào số lượng lỗi phát hiện và theo dõi như false positive, false negative và ID switch.

## Bonus (nếu làm)

### B1 — Hai người đi sát

Không làm (hết thời gian sau CP4).

### B2 — So cách đặt keyframe

Không làm.

### B3 — So với tracker có sẵn

Không làm.

## 7. Tài liệu tham khảo và công cụ AI đã dùng

- `docs/GUIDELINE.md`, `docs/CVAT_CHEATSHEET.md`, `docs/MOT_FORMAT.md`, `CHECKPOINTS.md`
- CVAT Community local (`localhost:8080`) + `src/setup_local_lab.py`, `src/check_submission.py`
- Công cụ AI: Cursor (hỏi format báo cáo / làm rõ quy ước keyframe và `outside`); không nhờ AI gán nhãn hộ trên CVAT
