# Phiếu QC 1 — front.zip, A01–A06

Người được kiểm: **Nguyễn Hồ Bắc** — Mã học viên: **03351**.
Người kiểm: **ĐÀO BÌNH AN** — Mã học viên: **03264**.
Lô được kiểm: `front.zip`. 
Ngày: 20/11/2026. Guideline: Road v1.0.
Revision: không có manifest kèm theo để xác định.
Phạm vi: A01–A06, 6 ảnh; 53 shape + 24 tag = **77 nhãn đã kiểm**.

Tôi kiểm tra 6 ảnh A01–A06 bằng cách đối chiếu nhãn trong file export với ảnh gốc và guideline Road v1.0, kết hợp xem kết quả lint. File ZIP mở được, chứa annotations.xml phiên bản 1.1 và không kèm ảnh.

Trong lần kiểm này, tôi chưa có GT của coach và bảng yêu cầu label theo từng ảnh trên slide nên chưa đánh giá được điểm theo rubric hoặc xác nhận độ lệch tối đa 5 px. Với những nhóm label chưa rõ có bắt buộc hay không, tôi ghi lại để hỏi coach thay vì kết luận là thiếu nhãn.

## Quy ước định danh

XML không lưu ID đối tượng CVAT cho từng shape. `#n` dưới đây là thứ tự phần tử con trong image, đếm từ 1; không phải ID trên giao diện CVAT. Tọa độ là pixel trên ảnh gốc 1280×720. Có thể tìm đối tượng theo label, thuộc tính và tọa độ.

## Tổng hợp theo mã

| Mã | Số mục đã xem | Số lỗi xác định | Mức |
| --- | ---: | ---: | --- |
| QC1-01 tag | 24 tag | 0 | — |
| QC1-02 đủ L1/R1 | 12 vị trí dự kiến trên 6 ảnh | 0; A05–A06 chờ xác nhận không thấy vạch | — |
| QC1-03 position | 12 lane | 0 | — |
| QC1-04 tâm, chiều, điểm dừng | 12 lane | 0 xác định; chưa chứng nhận ngưỡng 5 px | — |
| QC1-05 vạch đứt, che | 12 lane | 0 xác định; A03 cần kiểm thêm ca occluded | — |
| QC1-06 style/color/kind | 12 lane | 0 xác định | — |
| QC1-07 vùng lái, curb, crosswalk | 24 shape | 6 | chính |
| QC1-08 đèn, màu | 11 box đã gán + 1 đèn người đi bộ bị bỏ sót | 1 | chính |
| QC1-09 facing/type/group | 17 box đã gán | 2 | chính |
| QC1-10 biển, hình in | 6 box biển đã gán | 0 xác định | — |
| QC1-11 fisheye | 0; không áp dụng | 0 | — |
| QC1-12 file | 1 ZIP và cấu trúc 6 ảnh trong phạm vi | 0 | — |

Một nhãn có thể được kiểm ở nhiều mã QC1; tổng số nhãn dùng để tính tỉ lệ lỗi là 77. Tôi chỉ kiểm A01–A06 trong file front, chưa đánh giá phần fisheye.

## Danh sách lỗi xác định

| # | Mã | Ảnh | Nhãn | Mức | Bằng chứng và cách sửa |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-07 | A01 | drivable #7 | chính | Vùng giữa L1 và R1 đang mang area_type=alternative; cả 3 polygon A01 đều là alternative. Đổi polygon giữa sang direct. |
| 2 | QC1-07 | A03 | drivable #5, direct | chính | Polygon kéo xuống y=720 giữa x≈232–985, phủ capô nhìn thấy ở đáy ảnh. Cắt biên dưới theo mép capô. |
| 3 | QC1-07 | A03 | drivable #6, alternative | chính | Polygon phải kéo xuống đáy x≈1010–1280, bao phần capô ở góc dưới phải. Cắt theo ranh giới mặt đường/capô. |
| 4 | QC1-07 | A05 | drivable #3, direct | chính | Biên dưới gần ngang y≈575–581, trong khi capô đã xuất hiện cao hơn ở giữa ảnh. Chỉnh biên dưới chạy theo đường cong mép capô. |
| 5 | QC1-09 | A06 | traffic_sign #5, box (560.56,304.99)–(591.99,335.46) | chính | Biển công trường hình thoi cam đang gán group=prohibitory. Theo bảng nhóm biển của guideline, đổi sang warning. |
| 6 | QC1-09 | A06 | traffic_light #7, box (931.48,291.15)–(948.49,334.10) | chính | Đây là cụm đèn ba màu điều khiển xe, đang gán type=pedestrian. Đổi thành vehicle. Không thay màu xanh đang sáng. |
| 7 | QC1-08 | A06 | traffic_light bị thiếu, ngay bên phải/dưới #7 | chính | Có hộp đèn người đi bộ với hình người trắng quanh x≈948–967, y≈337–367, cao hơn 8 px nhưng không có box. Tạo box riêng theo vỏ, type=pedestrian; Road v1.0 không có color=white, cần hỏi lead chọn unknown hay quy ước khác. |
| 8 | QC1-07 | A06 | drivable #9, alternative bên trái | chính | Polygon bao vùng xe đối diện đang hướng về camera. alternative theo guideline là làn cùng chiều bên cạnh. Loại phần ngược chiều khỏi alternative; không cần tạo nhãn thay thế cho phần đó. |
| 9 | QC1-07 | A06 | drivable #8, alternative bên phải | chính | Polygon bao vào khu vực chân cột/đảo bên phải và phần sau cột. Cần chỉnh theo mép đảo thực tế, loại phần này khỏi vùng lái được. |

## Nhận xét từng ảnh

- **A01:** tôi ghi nhận vùng giữa L1 và R1 đang đặt sai area_type, cần đổi sang direct. Hai làn ngoài giữ alternative. L2 trắng đôi và R2 vàng liền phù hợp với vạch sơn quan sát được.
- **A02:** tôi chưa phát hiện lỗi rõ ràng trong các nhãn đã gán. Ảnh có direct, alternative và đủ bốn tag; độ lệch polyline cần đối chiếu GT để kết luận chính xác.
- **A03:** cần sửa hai polygon đang lấn capô. Tôi đề nghị kiểm lại weather/timeofday và đoạn lane có thể bị che với coach. Các đèn nhỏ cần phóng to ảnh gốc để kiểm tra màu.
- **A04:** tôi chưa ghi nhận lỗi rõ ràng trong các shape đã gán. Tag weather=clear cần xem lại vì bầu trời nhiều mây. Vạch R2 có hai nét trắng nên chưa có căn cứ yêu cầu đổi kind=double.
- **A05:** tôi không thấy rõ vạch sơn để yêu cầu bổ sung L1/R1. Cần sửa biên dưới polygon theo mép capô. Đoạn curb bên trái bị xe đỗ che nhiều, chỉ nên giữ phần xác định được.
- **A06:** cần sửa group của biển công trường, type của đèn xe, bổ sung đèn người đi bộ và chỉnh lại hai vùng alternative.

## Ca cần coach/lead xác nhận

| Ảnh | Vấn đề | Trạng thái |
| --- | --- | --- |
| A05, A06 | Lint báo thiếu L1/R1, nhưng ảnh không thấy rõ vạch sơn dọc tương ứng. | Đề nghị coach xem và ghi ngoại lệ QC1-02. Chưa tính thành lỗi nặng. |
| A03 | timeofday=dusk, weather=overcast; ảnh sáng nhưng có ánh chiều. | Chưa coi dusk là sai nếu chưa có tiêu chí/metadata rõ hơn. |
| A04 | weather=clear trong cảnh bầu trời nhiều mây, mặt đường khô. | Cân nhắc overcast theo guideline; hỏi coach nếu cần phân định, chưa cộng lỗi. |
| A03 | Checkpoint nhắc ca occluded nhưng cả hai lane đều occluded=0. | Coach chỉ đúng đoạn bị che trên ảnh để quyết định; không tự bật hàng loạt. |
| A06 | Đèn người đi bộ sáng hình người trắng, taxonomy chỉ có red/yellow/green/off/unknown. | Hỏi lead; có thể dùng unknown khi không thể ánh xạ, không tự quy ước trắng=xanh. |
| A01–A06 | Chưa có bảng nhóm label cần gán theo từng ảnh trên slide. | Chưa kết luận thiếu biển/đèn ở ảnh chưa gán nhóm đó. |

## Quyết định

Lỗi nặng xác định: **0**. Lỗi chính: **9 / 77 nhãn = 11,69%**. Lỗi nhẹ xác định: **0**.

Tôi quyết định **Rework** vì ghi nhận 9 lỗi chính trên 77 nhãn đã kiểm, tương đương **11,69%**, vượt ngưỡng 5% của phiếu QC1. Đề nghị bạn sửa các lỗi trong bảng trên rồi gửi lại để kiểm tra. Các ca mơ hồ và ngoại lệ thiếu L1/R1 cần được coach xác nhận trước khi kết luận Release.

Tôi không đưa cảnh báo ở A07–A12 vào kết quả vì nằm ngoài 6 ảnh được kiểm. Cảnh báo box A03 cao dưới 8 px chỉ dùng để tự kiểm, không tính là lỗi.

## Tài liệu và ảnh đối chiếu

- [Guideline](../../docs/guideline_road_v1.0.md)
- [Thang mức lỗi](../../docs/qc_severity_road_v1.0.md)
- [A01 overlay](A01-overlay.jpg), [A02 overlay](A02-overlay.jpg), [A03 overlay](A03-overlay.jpg)
- [A04 overlay](A04-overlay.jpg), [A05 overlay](A05-overlay.jpg), [A06 overlay](A06-overlay.jpg)

