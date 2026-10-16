# 6. Quyết định đã chốt

Mỗi quyết định ghi: **chốt gì · lý do · trước đó là gì**.
Chỗ nào hồ sơ dự án **không ghi lại lý do** thì ghi rõ như vậy, không suy đoán.

| # | Quyết định | Lý do (theo hồ sơ) | Trước đó / phương án thay thế |
|---|---|---|---|
| D-01 | **Quy đổi tên sản phẩm kiểu hybrid:** ưu tiên SKU, dự phòng theo tên + phân loại; không khớp thì giữ tên gốc và cảnh báo | Không được để sai mà không báo (xem D-10) | — |
| D-02 | **Dùng cột trạng thái, không xoá dòng** | Giữ triết lý "bảng tính là sổ cái" | Ban đầu 3 mức trạng thái (xem D-12) |
| D-03 | **Có trang Đóng gói trong hệ thống để bên đóng gói tự đánh dấu "đã đóng"** | Cả nhóm cần nắm tình hình chung | — |
| D-04 | **Tách thành trang/URL riêng cho từng luồng** | Hồ sơ không ghi lại lý do | Trước đó có một bản gộp một trang (đã lưu trữ, không còn dùng) |
| D-05 | **Bảng tính là sổ cái vĩnh viễn, ứng dụng không xoá** | Là triết lý đã có từ bản đầu | — |
| D-06 | **Dữ liệu sản phẩm lấy 100% từ Excel, không đọc từ PDF tem** | Hồ sơ không ghi lại lý do | Trước đó có thử đọc sản phẩm từ PDF |
| D-07 | **Bảng phân loại đầy đủ (58 dòng) đặt trên bảng tính dùng chung**, nhân viên tự thêm/sửa | Thiết kế trước (chỉ SKU, 5 cột) không dùng được: 39/58 dòng không có SKU, cột SKU trùng/sai | Bảng chỉ-SKU 5 cột; file Excel kèm sẵn |
| D-08 | **Không mở rộng danh sách mã cứng trong mã nguồn** | Mã cứng **đè lên** bảng dùng chung nên sửa trên bảng không có tác dụng, và mỗi lần thêm SKU phải sửa mã + triển khai lại | Thêm mã mới vào mã nguồn |
| D-09 | **SKU thắng "gán nhanh theo tên"** khi mâu thuẫn | Một máy lỡ gán nhầm theo tên sẽ kéo sai mọi đơn cùng tên dù SKU đúng | Gán nhanh theo tên đứng trên bước SKU |
| D-10 | **Mọi nhánh không chắc chắn phải dẫn tới cảnh báo** | Khi hoà điểm, hệ thống từng lặng lẽ lấy dòng đầu → sai mà không báo | Lấy dòng đầu khi hoà điểm |
| D-11 | **Thêm trạng thái "Đã hủy"** do bên đóng gói tự đánh dấu, và cho hủy cả đơn đã đóng | Thực tế có khi đóng hàng xong mới biết khách hủy | Chỉ có Chưa đóng / Đã đóng |
| D-12 | **Rút từ 3 mức còn Chưa đóng / Đã đóng (bỏ "Đã xuất")** rồi sau đó thêm "Đã hủy" | Hồ sơ không ghi lại lý do | 3 mức: Chưa đóng → Đã xuất → Đã đóng |
| D-13 | **Phân quyền theo PIN phía trình duyệt, chấp nhận không phải bảo mật tuyệt đối** | Hệ thống chạy hoàn toàn trên trình duyệt, không có máy chủ; ghi nhận rõ giới hạn này | — |
| D-14 | **Trang Dữ liệu không tự đồng bộ khi mở, chỉ đồng bộ khi bấm** | Là yêu cầu của người dùng, không phải lỗi | — |
