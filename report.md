# Báo cáo cá nhân — Ngày 11

Họ tên: **Nguyễn Hồ Bắc** — Mã học viên: **2A202603351**.  
Guideline: **Road v1.0**. Bản bàn giao: **revision 2**, chuẩn bị sau Rework ngày **21/11/2026**.  
Phiên bản CVAT, thời điểm export trên CVAT: **chưa xác minh**; XML dùng định dạng 1.1.  
Bản sửa hiện được cập nhật trực tiếp trong zip; chưa đồng bộ/xác minh trạng thái completed trên CVAT. Đây là bản chuẩn bị gửi, chưa có kết quả tái kiểm Release.

## 1. Kiểm project

| Mục | Kết quả | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Có trong metadata export | lane/road_curb polyline, crosswalk/drivable polygon, traffic_light/traffic_sign box |
| Thuộc tính và giá trị | Đã đọc XML và chạy lint | Đã sửa camera B01/B05/B06, position=other cho B05–B08 |
| 4 tag ảnh | 20/20 ảnh có đủ | Camera phù hợp tên ảnh sau khi sửa |
| Trạng thái job | Chưa xác minh trên CVAT | Cần đồng bộ zip đã sửa và kiểm completed |

Thao tác theo tài liệu hướng dẫn của repo: kết thúc polyline bằng N; đặt tag qua công cụ Tag rồi mở Details để kiểm value. Chưa xác minh thao tác trên phiên bản CVAT đang dùng.

## 2. Số lượng đã gán

Đếm trực tiếp từ hai zip revision 2; A01–A12 và B01–B08 đầy đủ. Không có ảnh thêm.

| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 28 | 16 | 5 | 26 | 30 | 19 |
| fisheye | 8 | 17 | 7 | 8 | 13 | 0 | 0 |
| front-extra (0/4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye-extra (0/4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

## 3. Bảng ca khó

| Ảnh | Nhãn | Phân vân giữa | Đã chọn / hướng xử lý | Lý do |
| --- | --- | --- | --- | --- |
| A05, A06 | lane | Thiếu L1/R1 hay không có vạch | Không vẽ thêm; chờ coach xác nhận ngoại lệ | Không thấy rõ vạch sơn dọc tương ứng |
| A07, A08, A09 | lane | Thiếu vạch hay ranh giới không có sơn | Giữ phần thấy được; chờ coach | A07 thiếu L1 sát dải phân cách; A08 chưa chắc vạch trái; A09 phía phải là lề/vùng đỗ |
| A03 | occluded | Đoạn nào thực sự bị che | Chờ coach chỉ đoạn | Không tự bật cờ chỉ từ checkpoint |
| A06 | traffic_light pedestrian | Màu trắng / unknown | Tạm chọn unknown, hỏi lead | Đèn hình người trắng; taxonomy không có white |
| A03, A04 | weather/timeofday | dusk/overcast, clear/overcast | Giữ nguyên, chờ coach nếu cần | Phiếu nhận được chưa kết luận lỗi |
| B01/B02/B03/B06/B08 | Polyline ngắn | Ít điểm có thực sự sai cung không | Giữ cảnh báo để tái kiểm | Không thêm điểm nội suy chỉ để xóa lint; chưa có GT chứng nhận ≤5 px |

## 4. Phiếu QC 1 nhận được

Người kiểm: **Đào Bình An — 03264**. Phiếu `front-qc1-A01-A06.md` ngày 20/11/2026 kiểm `front.zip`, A01–A06: **53 shape + 24 tag = 77 nhãn**. Quyết định ban đầu **Rework**, **0 lỗi nặng; 9 lỗi chính/77 = 11,69%; 0 lỗi nhẹ**.

| Mã lỗi | Số lỗi nhận được | Đồng ý? | Xử lý trong zip revision 2 |
| --- | ---: | --- | --- |
| QC1-07 | 6 | Đồng ý theo ảnh và phiếu | Đổi A01 direct; cắt hai polygon A03 và polygon A05 theo mép capô; bỏ alternative ngược chiều A06; tách vùng alternative phải A06 quanh cột |
| QC1-08 | 1 | Đồng ý | Thêm box đèn người đi bộ A06, type=pedestrian, color=unknown tạm chờ lead |
| QC1-09 | 2 | Đồng ý | Đổi biển công trường A06 sang warning; đèn xe A06 sang vehicle |

Đã sửa hình/thuộc tính cho cả 9 mục trong bản zip và xem lại overlay A03/A05/A06. Các polygon vừa sửa không có cạnh tự cắt. Màu đèn người đi bộ vẫn cần lead xác nhận; chưa có tái kiểm để kết luận Release.

Bổ sung ngoài phiếu: sửa tag camera và position fisheye; bổ sung R1 A12 theo vạch đứt thấy được; đảo chiều polyline ngang A08; chỉnh cung curb dài B02. Bản gốc tại `submission_history/r1/`, bản trước lượt sửa hình học tại `submission_history/before-quality-pass/`. Chưa gửi thêm lần nào; giữ revision 2 cho bộ sửa hiện tại.

Phiếu tôi lập cho Daobinhan: `nguyenhobac-qc1-for-daobinhan.md`, quyết định Rework do hai tag camera sai. Ca occluded A03 được chuyển sang chờ coach vì chưa xác định chắc đoạn bị che, không cộng lỗi chính khi thiếu bằng chứng.

## 5. Kiểm file export

| File | Mở lại được? | Shape ảnh 1 (job / file) | Shape ảnh 2 (job / file) | Tag camera trong XML? |
| --- | --- | --- | --- | --- |
| nguyenhobac-front.zip | Có, XML 1.1 | Chưa xem job / 9 (A01) | Chưa xem job / 7 (A02) | Có, 12 ảnh |
| nguyenhobac-fisheye.zip | Có, XML 1.1 | Chưa xem job / 5 (B01) | Chưa xem job / 5 (B02) | Có, 8 ảnh |

Hai zip chỉ chứa `annotations.xml`; không có ảnh hay GT. Manifest revision 2 ghi hash SHA-256 và `contains_images=false`. Đã kiểm hash khớp file cuối.

Lint còn **7 cảnh báo nặng QC1-02**, **8 cảnh báo chính QC1-11** và **4 cảnh báo nhẹ box dưới 8 px**. Chi tiết ở `submission_history/lint-r2.txt`. Các cảnh báo nặng: A05 L1/R1, A06 L1/R1, A07 L1, A08 L1, A09 R1. Chưa có coach xác nhận ngoại lệ nên chưa thể tuyên bố hết lỗi nặng. Cảnh báo chính còn lại là số điểm ít trên các đoạn ngắn fisheye; không phải kết quả đo lệch GT. Lint không chấm chất lượng hình học.

## 6. Ảnh chụp màn hình

**Chưa có ảnh chụp CVAT thật**, cần bổ sung trước khi gửi: tab Labels, một ảnh front đủ nhãn, một ảnh fisheye phóng to đường cong, và đoạn XML lane. Overlay kiểm nội bộ A03/A05/A06 lưu tại `submission_history/qa-front.png`, không thay thế ảnh chụp CVAT và không đưa ảnh dữ liệu vào bộ 5 file.

## 7. Tự đánh giá

Lỗi nhiều nhất theo phiếu nhận được là **QC1-07, 6/9 lỗi chính**: sai area_type, polygon lấn capô và bao vùng ngược chiều/cột. Lần sau tôi kiểm biên mặt đường với thân xe và đảo/cột, rồi kiểm direct là làn đang đi, alternative là làn cùng chiều bên cạnh.

Nhãn drivable là mục tiêu cho model phân đoạn vùng lái được. Hai polygon A03 đã được cắt khỏi capô trong bản sửa; nếu giữ nhãn cũ, model có thể học nhận thân xe mình là mặt đường xe đi được. Ngoài ra, tôi kiểm lại thuộc tính sau khi tạo box để tránh nhầm biển warning hoặc đèn vehicle/pedestrian. Các thay đổi do trợ lý thực hiện trên XML cần được tôi kiểm lại trên CVAT trước khi nộp.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor

Chưa thực hiện hoạt động tùy chọn, không tính điểm. Chưa có cặp polyline của hai người để so sánh x tại y=720,680,640,600,560. Đảo thứ tự điểm không đổi giao điểm hình học; xử lý theo thứ tự điểm vẫn cần tuân thủ chiều gần ra xa.
