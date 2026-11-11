# Báo cáo thực hành Day 3 — Nguyễn Việt Anh

- Mã học viên theo lớp: 2A202603095.
- Ngày / CVAT local: 11–12/11/2026; CVAT local 2.74.1.
- Công cụ đã dùng: Polygon trong CVAT; không dùng SAM. Codex hỗ trợ thao tác, kiểm export và biên tập báo cáo.

## 1. Bài đã nộp

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

## 2. Một quyết định trước khi dùng gợi ý

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: người phía sau ô tô, trước cửa hàng trong ảnh `000000181542.jpg`.
- Class và quy tắc tôi dùng để chọn biên: `person`, đặt điểm quanh đầu và vai nhìn thấy. Tôi vẽ vật phía sau trước và dùng Z-order sắp lớp; khi kiểm lại, phần polygon bị che vẫn cần sửa.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: không áp dụng.
- Nếu không dùng gợi ý: không dùng; tự vẽ bằng Polygon.

## 3. Một lỗi tôi tìm thấy và sửa

- Task/ảnh/vùng: `hard_panoptic`, vùng trời trong `000000350023.jpg` và `000000460147.jpg`.
- Lỗi thuộc loại: khác — dùng Rectangle thay cho mask và còn khung thừa.
- Bằng chứng tôi nhìn thấy: export có `segmentation: []`; công cụ kiểm báo thiếu polygon/RLE.
- Quy tắc và hành động sửa: thay vùng trời bằng Polygon, xóa Rectangle thừa.
- Sau sửa đã Save và export lại chưa? Đã Save và export lại; đủ 2 ảnh, 105 polygon hợp lệ, kiểm cấu trúc `OK`.

Kết quả tự đánh giá bằng script với reference mentor gửi: Easy 19,8/20, Medium 9,3/32, Hard 7,8/30; tổng **36,9/82**, chưa gồm checkpoint và không phải điểm chính thức /100.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| Easy `7ee6d192-89e2408b.jpg`, dải phân cách | Gán `building` hoặc để ngoài nhãn | Công trình bê tông không mặc nhiên là tòa nhà | Đã bỏ nhãn `building` ở dải phân cách |
| Easy `81ae7cbb-6bc63a4a.jpg`, biển 30 và cột | Gộp vào vùng xung quanh hoặc để ngoài nhãn | Task không có `pole`/`traffic sign` | Để biển và cột không gán nhãn |
| Medium `000000181542.jpg`, người sau ô tô | Chỉ chỉnh Z-order hoặc sửa cả biên | Chỉ vẽ phần nhìn thấy; Z-order chỉ sắp lớp | Cần sửa phần chồng, chưa nhận là đã sửa |
