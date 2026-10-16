# 7. Truy vết yêu cầu

Ma trận nối **quy tắc nghiệp vụ → user story → yêu cầu chức năng → trang → bằng chứng kiểm thử**.

Cột bằng chứng chỉ ghi những gì **hồ sơ dự án có ghi lại**. Chỗ nào ghi "Chưa có ghi nhận" nghĩa là hồ sơ không lưu kết quả kiểm thử riêng cho yêu cầu đó — đây là **khoảng trống** cần bổ sung nếu dự án tiếp tục.

| Quy tắc | User story | FR | Trang | Bằng chứng kiểm thử đã ghi nhận |
|---|---|---|---|---|
| BR-01 Khoá đơn = mã vận đơn hoặc mã đơn hàng | US-01, US-03 | FR-01, FR-03 | Nhập liệu | Chưa có ghi nhận kiểm thử riêng; có thay đổi thiết kế để hỗ trợ đơn không có mã vận đơn |
| BR-02 Quy đổi theo SKU, dự phòng theo tên, cảnh báo khi không khớp | US-02, US-10 | FR-02, FR-11 | Nhập liệu, Đóng gói | Chạy thử 31 đơn mẫu của 2 sàn: 0 cảnh báo thừa. Bộ kiểm thử chốt chặn: 8/8 đạt |
| BR-03 Combo, số lượng = đơn × hệ số | US-02 | FR-02 | Nhập liệu | Kiểm thử combo, nhiều mùi, combo khác món: đúng. Ca đơn 3 món thành 3 sản phẩm riêng: đúng |
| BR-04 Cộng dồn số lượng cùng sản phẩm trong 1 đơn | US-03 | FR-03 | Nhập liệu | Chưa có ghi nhận kiểm thử riêng |
| BR-05 Chống trùng theo 1 trong 2 mã | US-03, US-11 | FR-03, FR-13 | Nhập liệu, Quản trị | 12/12 ca đạt (nhập 2 mã + gộp đơn trùng). Trước khi sửa, đo được 38 đơn trùng |
| BR-06 Trạng thái đóng, không xoá dòng | US-09 | FR-10 | Đóng gói | Mô phỏng vòng nhập → lưu → cập nhật: đạt |
| BR-07 Đơn hủy loại khỏi soạn hàng và xuất Excel | US-07, US-08 | FR-08, FR-09 | Đóng gói | Chưa có ghi nhận kiểm thử riêng |
| BR-08 Đơn đã đóng vẫn hủy được | US-09 | FR-10 | Đóng gói | Kiểm thử giả lập: đơn đã đóng chỉ có nút hủy, bấm xong chuyển Đã hủy |
| BR-09 Tem 6/4/2 mỗi tờ A4 | US-05 | FR-06 | In tem | Chưa có ghi nhận kiểm thử riêng |
| BR-10 Đánh dấu Đã in | US-06 | FR-07 | In tem | Chưa có ghi nhận kiểm thử riêng |
| BR-11 Đối soát in / dữ liệu | US-06 | FR-07 | In tem | Chưa có ghi nhận kiểm thử riêng |
| BR-12 Phân quyền, ẩn cột tiền với bên đóng gói | US-12 | FR-14 | Tất cả | Chưa có ghi nhận kiểm thử riêng |
| BR-13 Dọn lưu trữ chuyển, không xoá | US-11 | FR-13 | Quản trị | Kiểm thử giả lập: dọn 186 đơn quá 7 ngày; mặc định 7 ngày |
| BR-14 Mới nhất lên trên | US-07 | FR-08 | Đóng gói, Dữ liệu | 426 đơn sắp xếp giảm dần theo ngày: đạt |

## Nhận xét

- **Mức độ bao phủ kiểm thử không đều:** phần lõi quy đổi sản phẩm (BR-02, BR-03, BR-05) có kiểm thử tự động và số liệu; phần in tem và phân quyền chưa có ghi nhận riêng.
- Đề xuất nếu tiếp tục: bổ sung ca kiểm thử chấp nhận cho BR-09 → BR-12 và lưu kết quả cùng tài liệu.
