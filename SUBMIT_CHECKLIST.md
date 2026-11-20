# Chuẩn bị nộp — Nguyễn Hồ Bắc

Bộ 5 file trong `submission/` đã cập nhật sau lượt kiểm chất lượng ngày 21/11/2026, revision 2. Chưa xác nhận đủ điều kiện gửi vì còn việc trên CVAT và ngoại lệ cần coach.

- [x] Đúng 5 file; zip chỉ chứa annotations.xml, không kèm ảnh/GT.
- [x] Đủ 12 ảnh front và 8 ảnh fisheye, đủ bốn tag mỗi ảnh.
- [x] Sửa camera B01/B05/B06 và position camera hai bên B05–B08.
- [x] Sửa A01 direct, group/type A06.
- [x] Sửa polygon capô A03/A05, bỏ vùng ngược chiều A06, tách vùng phải quanh cột.
- [x] Thêm đèn người đi bộ A06 (unknown, chờ lead xác nhận màu).
- [x] Thêm R1 A12 thấy được; sửa chiều polyline A08; chỉnh curb dài B02.
- [x] Kiểm polygon vừa sửa không tự cắt; xem overlay A03/A05/A06.
- [x] Tạo lại manifest revision 2; kiểm SHA-256 khớp zip cuối.
- [x] Cập nhật report.md và bản nộp; soát phiếu QC, chuyển occluded A03 chưa đủ bằng chứng sang ca hỏi coach.
- [ ] Coach xác nhận ngoại lệ QC1-02: A05 L1/R1, A06 L1/R1, A07 L1, A08 L1, A09 R1. Danh sách/lý do đã ghi trong report và phụ lục phiếu QC; chưa tự xác nhận được miễn.
- [ ] Lead xác nhận dùng unknown cho đèn người đi bộ trắng A06.
- [ ] Xem lại 8 cảnh báo ít điểm fisheye B01/B02/B03/B06/B08 trên CVAT; chưa có GT chứng nhận sai lệch ≤5 px.
- [ ] Import hai zip sửa về CVAT hoặc sửa tương ứng; tự kiểm và đặt mọi job completed.
- [ ] Bổ sung Help → About, thời điểm export thật, đối chiếu shape job/file và 4 ảnh chụp yêu cầu vào báo cáo.
- [ ] Tái kiểm lô sau sửa trước khi kết luận Release.
- [ ] Gửi đúng 5 file trong submission lên kênh coach chỉ định khi hoàn tất các mục trên.

## Sau khi cập nhật lại zip từ CVAT

Chạy từ gốc repo để tạo lại hash manifest và đồng bộ báo cáo:

```powershell
$env:PYTHONPATH = 'src'
$env:PYTHONUTF8 = '1'
python -m road_lab.road_check lint submission/nguyenhobac-front.zip submission/nguyenhobac-fisheye.zip --manifest submission/nguyenhobac-manifest.json --name nguyenhobac --revision 2
Copy-Item report.md submission/nguyenhobac-report.md
```

Bản gốc giữ ở `submission_history/r1/`; bản trước lượt sửa hình học ở `submission_history/before-quality-pass/`. Log hiện tại: `submission_history/lint-r2.txt` (7 nặng QC1-02, 8 chính QC1-11, 4 nhẹ box nhỏ). Không gửi checklist, lịch sử, ảnh hoặc log kèm bộ 5 file.
