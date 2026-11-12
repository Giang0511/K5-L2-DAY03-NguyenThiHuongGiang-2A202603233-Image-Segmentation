# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

- Mã học viên theo lớp: 2A202603233
- Ngày / CVAT local: 11/11/2026 / CVAT online
- Công cụ đã dùng: CVAT, công cụ Brush (không dùng SAM hay gợi ý tự động)

## 1. Bài đã nộp

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 |  |
| medium_instance | medium_instance.zip | 3 / 3 |  |
| hard_panoptic | hard_panoptic.zip | 2 / 2 |  |
| cp1_holes | cp1_holes.zip | 1 / 1 |  |
| cp2_slice | cp2_slice.zip | 1 / 1 |  |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 |  |
| cp3_thin | cp3_thin.zip | 1 / 1 |  |
| cp4_curb | cp4_curb.zip | 1 / 1 |  |
| cp6_coverage | cp6_coverage.zip | 1 / 1 |  |
| **Tổng tối đa** | | |  |


## 2. Một quyết định trước khi dùng gợi ý

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: ảnh `000000373353.jpg`, người đi bộ ở giữa ảnh, phía trước xe taxi vàng.
- Class và quy tắc tôi dùng để chọn biên: class `person`; chỉ vẽ phần cơ thể nhìn thấy bằng Brush, mask dừng ở mép người, không vẽ phần bị che.
- Nếu dùng gợi ý sau đó: không dùng gợi ý tự động.
- Một quyết định gán nhãn của tôi: phía sau người này còn một người khác, chỉ thấy một phần chân (dưới 20% cơ thể nhìn thấy). Tôi quyết định không gán nhãn người đó vì phần nhìn thấy quá ít để xác định thành một instance đáng tin.

## 3. Một lỗi tôi tìm thấy và sửa

- Task/ảnh/vùng: hard_panoptic, ảnh `7daa6479-67988f3f.jpg`, các khe giữa những cột phía bên phải ảnh.
- Lỗi thuộc loại: biên / phủ vùng.
- Bằng chứng tôi nhìn thấy: khi tự QC trong CVAT, phần mask công trình (màu xanh lá) tô cả vào các khe giữa các cột, trong khi qua khe vẫn nhìn thấy đường phố phía sau (xe taxi vàng, người đi bộ). Vùng này không phải công trình.
- Quy tắc và hành động sửa: quy tắc là chỉ gán lớp cho phần nhìn thấy đúng với lớp đó, không tô ép vùng chưa chắc. Hành động sửa: dùng Brush ở chế độ Eraser xóa phần mask `building` lấn vào khe.
- Sau sửa đã Save và export lại chưa? 【Đã / Chưa — chỉ giữ "Đã" nếu bạn thật sự đã sửa, Save và export lại `hard_panoptic.zip`】

Kết quả tự đánh giá liên quan lỗi vừa sửa: chưa có điểm.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1. medium_instance, `000000373353.jpg`, người phía sau người ở giữa | Gán nhãn thành một `person` riêng, hoặc bỏ qua vì chỉ thấy phần chân | Phần nhìn thấy dưới 20% cơ thể; chỉ vẽ phần nhìn thấy, không vẽ phần bị che | Quyết định: không gán nhãn. Câu hỏi cho coach: ngưỡng nhìn thấy để một vật được tính là instance là bao nhiêu? |
| 2. easy_semantic, `7ee6d192-89e2408b.jpg`, các ô tô nhỏ ở xa trên đường cao tốc | Gán nhãn riêng cho từng ô tô, hoặc để thuộc vùng `road` / bỏ qua | Task semantic chỉ có 5 lớp (`road`, `sidewalk`, `building`, `vegetation`, `sky`), không có lớp xe | Quyết định: không gán nhãn xe. Câu hỏi cho coach: pixel của xe nhỏ có cần phủ bằng `road` không? |
| 3. hard_panoptic, `7daa6479-67988f3f.jpg`, người đi bộ nhỏ và taxi vàng ở giữa ảnh, sau xe buýt | Gán nhãn `person` / `car` cho từng vật nhỏ, hoặc bỏ qua vì quá nhỏ và bị che một phần | Chỉ vẽ phần nhìn thấy; vật nhỏ khó xác định biên | Câu hỏi cho coach: vật nhỏ nhìn thấy qua khe có cần là instance riêng trong panoptic không? |
