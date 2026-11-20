# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): **Dao Binh An**  
Người kiểm (học viên): **Nguyễn Hồ Bắc**  
Ngày: **20/11/2026**  Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `data/daobinhan-front/annotations.xml`; không có manifest nên chưa xác minh revision.  
Số ảnh kiểm: **6 (A01–A06)** (+ 0 ảnh thêm)   Số nhãn đã kiểm (shape + tag): **79** (55 shape + 24 tag)



## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 ảnh | 2 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 6 ảnh (L1/R1 nhìn thấy ở A01–A04; A05–A06 không thấy vạch) | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 14 lane | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 14 lane | 0 lỗi rõ qua soát trực quan* | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 14 lane | 0 xác định; A03 chờ coach | chính |
| QC1-06 style, color, kind | sai thuộc tính | 14 lane | 0 lỗi rõ qua soát trực quan* | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 26 shape (drivable, crosswalk, road_curb) | 0 lỗi rõ qua soát trực quan* | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 6 đèn | 0 lỗi rõ qua soát trực quan* | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 15 shape (9 biển, 6 đèn) | 0 lỗi rõ qua soát trực quan* | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 9 biển | 0 lỗi rõ qua soát trực quan* | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 0 (không áp dụng cho ảnh front) | 0 | chính |
| QC1-12 file | lỗi file | 1 XML đọc được; chưa có zip/manifest để kiểm gói | 0 lỗi file xác nhận | nhẹ / nặng |


## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-01 | A01 | tag `camera` (id không có trong XML) | nặng | Giá trị `fisheye_front`; trong lô front phải là `front`. |
| 2 | QC1-01 | A02 | tag `camera` (id không có trong XML) | nặng | Giá trị `fisheye_front`; trong lô front phải là `front`. |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A03 | Checkpoint nhắc occluded, nhưng chưa xác định chắc polyline/đoạn bị che từ ảnh. Đề nghị coach chỉ đoạn trước khi cộng lỗi QC1-05. | Chưa có; chưa tính lỗi xác định. |
| `daobinhan-front` | Có thể cung cấp zip export và manifest để kiểm định dạng gói, revision, ảnh kèm theo và khả năng mở lại không? | Chưa có. Chưa ảnh hưởng quyết định vì đã có lỗi nặng. |

## Quyết định
Lỗi nặng: **2**   Lỗi chính: **0 / 79 nhãn = 0 %**   Lỗi nhẹ: **0 xác nhận**   Ca chờ lead: **1 ảnh (A03)**; không ảnh hưởng quyết định Rework vì đã có lỗi nặng  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): **Có lỗi nặng QC1-01 ở A01 và A02; chỉ một lỗi nặng cũng đủ Rework. Tỷ lệ lỗi chính hiện dưới 5%, nhưng không thay đổi quyết định.**

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).

## Ngoại lệ cần coach xác nhận cho lô của người kiểm (Nguyễn Hồ Bắc)

Mục này không cộng vào thống kê QC lô Daobinhan ở trên. Bản nộp của Nguyễn Hồ Bắc còn cảnh báo QC1-02: A05 L1/R1 (đường không thấy vạch), A06 L1/R1 (giao lộ dưới cầu), A07 L1 (bên trái là dải phân cách), A08 L1 (khu giao lộ, không xác định chắc vạch trái), A09 R1 (bên phải là lề/vùng đỗ xe). Đã xem ảnh gốc; đề nghị coach xác nhận ngoại lệ từng ảnh. **Chưa có xác nhận**, không ghi là đã được miễn.
