# Báo cáo cá nhân — Ngày 11

Họ tên: **Nguyễn Hồ Bắc**    Mã học viên: **2A202603351** (theo tên thư mục dự án)  
Phiên bản CVAT (Help → About): **Chưa xác minh trong Help → About; 1.1 là phiên bản định dạng XML export**  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): **2**  
Thời điểm export (ngày giờ trên CVAT): **Chưa xác minh**    Số lần nộp lại sau Rework: **Đang chuẩn bị bản sửa lần 1 (revision 2), chưa gửi**



## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Có trong metadata XML | Các nhãn/kiểu khai báo khớp cấu trúc cần có; đã đối chiếu metadata trong export cá nhân front/fisheye. |
| Thuộc tính và giá trị | Có trong metadata XML | Đã đọc metadata và chạy lint trên hai zip bàn giao; chưa xác minh trạng thái completed trên CVAT. |
| 4 tag ảnh | Có đủ trên A01–A06 của bài tôi theo phiếu nhận được | 24 tag đã kiểm; không ghi nhận lỗi xác định QC1-01. Kết quả camera sai ở lô Daobinhan thuộc phiếu QC tôi lập cho bạn, không áp dụng cho bài tôi. |
Cách kết thúc polyline trên bản CVAT này: **Chưa có thông tin từ thao tác trực tiếp trên CVAT.**  
Cách đặt tag ảnh trên bản CVAT này: **Chưa có thông tin từ thao tác trực tiếp trên CVAT.**

## 2. Số lượng đã gán

Thống kê từ hai zip bàn giao revision 2; không làm ảnh thêm. Mọi ảnh trong hai file có đủ bốn tag và có shape.

| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 27 | 16 | 5 | 26 | 29 | 19 |
| front-extra (0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye | 8 | 17 | 7 | 8 | 13 | 0 | 0 |
| fisheye-extra (0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

## 3. Bảng ca khó

| Ảnh | Nhãn | Phân vân giữa | Đã chọn / hướng xử lý | Lý do |
| --- | --- | --- | --- | --- |
| A05, A06 | lane L1/R1 | Thiếu nhãn hay không có vạch nhìn thấy | Nhờ coach xác nhận ngoại lệ QC1-02; chưa vẽ thêm | Người kiểm không thấy rõ vạch sơn; chưa tính lỗi nặng. |
| A03 | lane / occluded | Đoạn nào thực sự bị che | Nhờ coach chỉ đoạn; chưa bật hàng loạt | Checkpoint nhắc occluded nhưng hai lane trong bài đều có occluded=0; phiếu chưa kết luận lỗi. |
| A03 | timeofday, weather | dusk/overcast so với điều kiện ảnh | Chờ xác nhận | Phiếu chưa coi dusk là sai khi thiếu tiêu chí/metadata rõ hơn. |
| A04 | weather | clear / overcast | Kiểm lại cùng coach | Nhiều mây, đường khô; phiếu chưa cộng lỗi. |
| A06 | traffic_light pedestrian | Màu trắng / unknown trong taxonomy | Hỏi lead trước khi chọn màu | Taxonomy không có white; không tự quy ước trắng thành green. |

## 4. Phiếu QC 1 nhận được

Bạn kiểm lô của tôi: **Đào Bình An — mã học viên 03264**.  
Nguồn: `front-qc1-A01-A06.md` (phiếu lưu trong repo), ngày **20/11/2026**, lô `front.zip`, mẫu **A01–A06**.  
Quyết định nhận được: **Rework** — **0 lỗi nặng, 9 lỗi chính / 77 nhãn = 11,69%, 0 lỗi nhẹ**. Tỷ lệ lỗi chính vượt ngưỡng 5%.

| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-07 | 6 | Ghi nhận theo phiếu | Đã sửa area_type A01 trong zip revision 2; 5 lỗi hình học còn cần sửa |
| QC1-08 | 1 | Ghi nhận đèn người đi bộ bị thiếu; màu cần hỏi lead | Chưa bổ sung |
| QC1-09 | 2 | Đồng ý theo ảnh và thuộc tính trong XML | Đã sửa group và type ở A06 trong zip revision 2 |

Các việc cần sửa theo phiếu:

1. **A01, drivable #7:** đổi vùng giữa L1/R1 từ alternative sang direct.
2. **A03, drivable #5 và #6:** cắt hai polygon theo mép capô, loại phần thân xe mình.
3. **A05, drivable #3:** chỉnh biên dưới chạy theo đường cong mép capô.
4. **A06, traffic_sign #5:** đổi group từ prohibitory sang warning cho biển công trường màu cam.
5. **A06, traffic_light #7:** đổi type từ pedestrian sang vehicle; giữ màu xanh đang sáng.
6. **A06:** bổ sung box đèn người đi bộ quanh x≈948–967, y≈337–367; hỏi lead về màu trắng trong taxonomy.
7. **A06, drivable #9:** loại vùng làn ngược chiều khỏi alternative.
8. **A06, drivable #8:** loại chân cột/đảo và phần sau cột khỏi vùng lái được.

Số thứ tự # là thứ tự phần tử con trong XML theo phiếu, không phải ID CVAT. Mục A03 gồm hai lỗi trên hai polygon, nên tổng danh sách trên là **9 lỗi**. Đã lưu bản gốc và manifest revision 1 tại `submission_history/r1/`, sửa trực tiếp thuộc tính trong zip bàn giao và tạo manifest revision 2. Chưa đồng bộ các thay đổi này về CVAT; cần import lại bản nhãn đã sửa hoặc sửa tương ứng trên CVAT trước khi xác nhận completed. Năm lỗi hình học và một lỗi thiếu đèn vẫn cần xử lý. Ngoài phiếu nhận được, đã sửa tag camera B01/B05/B06 và position=other cho lane B05–B08 trong bản bàn giao.

Phiếu QC tôi lập cho lô Daobinhan: [nguyenhobac-qc1-for-daobinhan.md](nguyenhobac-qc1-for-daobinhan.md), quyết định Rework. Đây là phiếu gửi cho bạn, độc lập với phiếu tôi nhận được ở trên.

## 5. Kiểm file export

Đã mở cả hai zip, đọc XML 1.1 và chạy `road_check lint` sau khi sửa thuộc tính. Mỗi zip chỉ chứa `annotations.xml`, không có ảnh. Manifest revision 2 ghi SHA-256, thống kê ảnh/shape và `contains_images=false` cho cả hai file.

| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| nguyenhobac-front.zip | Có | Chưa xem job / 9 (A01) | Chưa xem job / 7 (A02) | Có; 12 ảnh |
| nguyenhobac-fisheye.zip | Có | Chưa xem job / 5 (B01) | Chưa xem job / 5 (B02) | Có; 8 ảnh, đã sửa B01/B05/B06 |

**Chưa đủ điều kiện kết luận sẵn sàng nộp:** lint còn 8 cảnh báo nặng QC1-02: A05 L1/R1, A06 L1/R1, A07 L1, A08 L1, A09 R1, A12 R1. Cần xem ảnh để bổ sung vạch thực sự thấy được, hoặc coach xác nhận ngoại lệ và ghi mã ảnh/lý do. Không vẽ thêm vạch chỉ để hết cảnh báo.

Còn 10 cảnh báo chính: một cảnh báo chiều polyline A08 và chín cảnh báo ít điểm ở các polyline fisheye B01/B02/B03/B06/B08. Cần xem hình vẽ để quyết định sửa; số điểm ít chưa đủ để kết luận lệch quá 5 px. Bốn cảnh báo nhẹ là box dưới 8 px, chỉ gợi ý tự kiểm. Chi tiết lưu tại `submission_history/lint-r2.txt` trong repo. Lint không thay thế QC hình học và không xác nhận đã sửa xong 9 lỗi trong phiếu nhận được.

## 6. Ảnh chụp màn hình

Chưa có ảnh chụp màn hình CVAT cá nhân trong workspace; cần bổ sung các ảnh yêu cầu:

1. Tab Labels của project.
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển).
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong.
4. Một đoạn XML có `<polyline label="lane">`.

## 7. Tự đánh giá

Theo phiếu nhận được, lỗi tôi mắc nhiều nhất là **QC1-07: 6/9 lỗi chính**, chủ yếu ở phạm vi và loại vùng lái: vùng direct bị gán alternative, polygon lấn capô, vùng alternative bao làn ngược chiều hoặc chân cột/đảo. Ở Ngày 20, tôi cần kiểm ranh giới mặt đường với thân xe và đảo/cột trước khi lưu, rồi kiểm riêng area_type: direct là làn đang đi, alternative là làn cùng chiều bên cạnh.

Nhãn drivable cung cấp vùng mục tiêu cho model phân đoạn vùng lái được. Ví dụ A03 có polygon phủ capô: nếu đưa vào huấn luyện, model có thể học nhận thân xe mình là mặt đường xe đi được. Hướng sửa là cắt polygon theo mép capô. **Chưa có xác nhận lỗi này đã sửa trên CVAT**, nên chưa ghi là ca đã sửa hoàn tất.

Ngoài ra, tôi cần kiểm thuộc tính sau khi vẽ box: biển công trường A06 thuộc warning; cụm đèn ba màu điều khiển xe phải có type=vehicle. Những ca chưa có quy ước rõ như màu trắng của đèn người đi bộ cần hỏi lead và lưu lời đáp.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor

Phiếu QC không cung cấp đủ tọa độ polyline của hai người để so sánh row-anchor, nên chưa điền số x.

| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi | — | — | — | — | — |
| x của bạn kia | — | — | — | — | — |

1. Nếu dừng polyline sớm 40 px, hàng nào đổi thành "không có làn" phụ thuộc vào giao điểm polyline với các hàng; cần hai polyline cụ thể để xác định.
2. Chưa thể tính độ lệch tại y=720 và y=560 nếu chưa có hai polyline.
3. Đảo thứ tự các điểm không đổi giao điểm hình học, nhưng script xử lý theo thứ tự điểm có thể gặp khó; chưa chạy row-anchor vì chưa có zip phù hợp.
