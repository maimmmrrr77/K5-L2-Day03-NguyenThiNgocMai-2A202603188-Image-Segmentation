# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202603188
- Ngày / CVAT local: 12/11/2026
- Công cụ đã dùng: Segformer-cityscape

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic |easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip| 3 / 3 | 32 |
| hard_panoptic | hard_paoptic | 2 / 2 | 30 |
| cp1_holes | … | … / 1 | 3 |
| cp2_slice | … | … / 1 | 3 |
| cp5_occlusion | … | … / 1 | 3 |
| cp3_thin | … | … / 1 | 3 |
| cp4_curb | … | … / 1 | 3 |
| cp6_coverage | … | … / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: 000000181542, car
- Class và quy tắc tôi dùng để chọn biên: Class `car`. Quy tắc chọn biên là vẽ ôm sát phần thân vỏ, bánh xe và gương chiếu hậu; loại bỏ phần bóng đổ dưới gầm xe trên mặt đường và cắt biên theo vật cản phía trước (nếu bị che khuất) chứ không vẽ đoán xuyên qua vật cản.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: các xe tiếp theo, vùng gợi ý đúng phần thân xe nhưng bị lem vào bóng đổ dưới gầm và lẹm mất phần gương chiếu hậu. Tôi đã dùng Brush/Eraser để gọt bỏ phần bóng đổ và bù thêm phần gương nhằm đảm bảo biên sát vật thể thực tế.
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: hard_panoptic ảnh 000000350023.jpg, vùng mặt đường `road` gần vỉa hè / dải phân cách
- Lỗi thuộc loại: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác: thủng lỗ
- Bằng chứng tôi nhìn thấy: mask của lớp `road` bị thủng nhiều lỗ nhỏ ở khu vực vạch kẻ đường hoặc bị răng cưa, lẹm sang phần bó vỉa
- Quy tắc và hành động sửa: Áp dụng quy tắc phủ kín bề mặt đường liền mạch (vạch kẻ đường vẫn tính thuộc `road`) và tách bạch ranh giới tại mép bó vỉa. Tôi đã dùng công cụ Brush để tô lấp các lỗ thủng bên trong mask và dùng Eraser gọt lại đường biên sát mép vỉa hè.
- Sau sửa đã Save và export lại chưa? Đã bấm Save trên CVAT và export lại file ZIP mới.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): … / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1 | cành cây mảnh | Các chi tiết quá mảnh tốn nhiều thời gian mà độ phủ pixel rất nhỏ | Nên vẽ các nhánh chính hay bao trùm lên các vật xung quanh? |
| 2 | … | … | … |
| 3 | … | … | … |
