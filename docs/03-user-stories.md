# 3. User stories

> Tiêu chí chấp nhận được rút từ hành vi của hệ thống đã chạy.

## Vai trò và quyền truy cập

| Vai trò | Trang được phép | Ghi chú |
|---|---|---|
| Quản trị | Tất cả | Cấu hình, gộp đơn trùng, dọn lưu trữ |
| Nhập liệu | Trang chủ, Nhập liệu | |
| Đóng gói | Trang chủ, In tem, Đóng gói | Không thấy các cột tiền (BR-12) |

---

## Epic A — Nhập liệu

### US-01 Nhập đơn từ Excel của sàn
**Với vai trò** nhân viên nhập liệu, **tôi muốn** kéo thả file Excel đơn hàng của Shopee hoặc TikTok Shop, **để** hệ thống tự đọc được mà không phải xử lý định dạng thủ công.

**Tiêu chí chấp nhận**
- Nhận được cả hai định dạng; tải nhiều file một lần được.
- Dòng mô tả của file (không phải đơn) bị loại.

*Liên kết:* BR-01 · FR-01

### US-02 Tự quy đổi tên sản phẩm chuẩn
**Với vai trò** nhân viên nhập liệu, **tôi muốn** hệ thống đổi tên dài của sàn thành tên sản phẩm chuẩn và tách combo, **để** bên đóng gói đọc là hiểu.

**Tiêu chí chấp nhận**
- Khớp theo SKU trước; không có SKU thì khớp theo tên + phân loại.
- Combo ra nhiều dòng, số lượng nhân theo hệ số.
- Dòng không khớp được hiển thị cờ cảnh báo, kèm nút để gán nhanh.
- Không bao giờ để một dòng sai tên mà không có cảnh báo.

*Liên kết:* BR-02, BR-03 · FR-02

### US-03 Đẩy đơn mới, không trùng
**Với vai trò** nhân viên nhập liệu, **tôi muốn** đẩy đơn lên kho chung mà không sợ nhân đôi khi đẩy lại, **để** dữ liệu luôn sạch.

**Tiêu chí chấp nhận**
- Đẩy lại cùng đơn thì cập nhật, giữ nguyên trạng thái đã in/đã đóng.
- Cùng sản phẩm xuất hiện nhiều lần trong một đơn thì được cộng dồn số lượng.
- Khớp trùng theo mã vận đơn hoặc mã đơn hàng.

*Liên kết:* BR-04, BR-05 · FR-03

### US-04 Quản lý bảng phân loại sản phẩm
**Với vai trò** nhân viên, **tôi muốn** tự thêm, sửa, xoá sản phẩm trong bảng phân loại, **để** không phải nhờ lập trình viên mỗi khi có sản phẩm mới.

**Tiêu chí chấp nhận**
- Thay đổi dùng chung cho cả nhóm.
- Nạp hàng loạt bấm lại không nhân đôi.

*Liên kết:* BR-02, BR-03 · FR-04

---

## Epic B — In tem

### US-05 Gộp tem lên A4
**Với vai trò** người in tem, **tôi muốn** gộp nhiều tem vận đơn lên một tờ A4, **để** tiết kiệm giấy và thời gian.

**Tiêu chí chấp nhận**
- Chọn 6, 4 hoặc 2 tem/tờ, mặc định 6.
- Mã vạch vẫn nét sau khi in.
- Có dấu cắt.

*Liên kết:* BR-09 · FR-05, FR-06

### US-06 Đánh dấu đã in và đối soát
**Với vai trò** người in tem, **tôi muốn** hệ thống tự đánh dấu các đơn đã in và chỉ ra chỗ lệch, **để** không bỏ sót đơn nào.

**Tiêu chí chấp nhận**
- Tạo file in xong thì các đơn tương ứng được đánh dấu **Đã in**.
- Bảng đối soát liệt kê: đơn có dữ liệu nhưng chưa in; tem đã in nhưng chưa có dữ liệu.

*Liên kết:* BR-10, BR-11 · FR-07

---

## Epic C — Đóng gói

### US-07 Xem và xuất đơn chưa đóng
**Với vai trò** nhân viên đóng gói, **tôi muốn** xuất Excel đơn chưa đóng, **để** mang đi soạn hàng.

**Tiêu chí chấp nhận**
- Chỉ gồm đơn **Chưa đóng**; đơn **Đã hủy** bị loại.
- Danh sách mới nhất ở trên.

*Liên kết:* BR-06, BR-07, BR-14 · FR-08

### US-08 Tổng hợp soạn hàng
**Với vai trò** nhân viên đóng gói, **tôi muốn** thấy tổng số lượng theo từng sản phẩm, **để** nhặt hàng theo lô thay vì từng đơn.

**Tiêu chí chấp nhận**
- Cộng theo sản phẩm thật.
- Không tính đơn đã hủy.

*Liên kết:* BR-03, BR-07 · FR-09

### US-09 Xác nhận đã đóng / đã hủy
**Với vai trò** nhân viên đóng gói, **tôi muốn** đánh dấu đơn đã đóng hoặc đã hủy, **để** cả nhóm thấy tình hình chung.

**Tiêu chí chấp nhận**
- Làm được từng đơn hoặc chọn nhiều đơn.
- Đơn đã đóng vẫn hủy được nếu khách hủy sau; bỏ hủy đưa về **Chưa đóng**.
- Ghi lại người đóng và thời điểm.

*Liên kết:* BR-06, BR-08 · FR-10

### US-10 Cảnh báo tên sản phẩm lạ
**Với vai trò** nhân viên đóng gói, **tôi muốn** được cảnh báo khi tên sản phẩm không có trong bảng phân loại, **để** không soạn nhầm hàng.

**Tiêu chí chấp nhận**
- Dòng và dòng tổng hợp có nhãn cảnh báo; có ô thống kê số đơn cảnh báo, tự ẩn khi bằng 0.
- Nếu không tải được bảng phân loại thì **không** gắn cảnh báo bừa.

*Liên kết:* BR-02 · FR-11

---

## Epic D — Quản trị

### US-11 Gộp đơn trùng và dọn lưu trữ
**Với vai trò** quản trị, **tôi muốn** gộp các dòng trùng đã tồn tại và dọn đơn cũ đã đóng sang trang lưu trữ, **để** dữ liệu gọn và nhanh.

**Tiêu chí chấp nhận**
- Gộp giữ lại mã đầy đủ, trạng thái cao nhất (Đã hủy > Đã đóng > Chưa đóng) và cờ đã in.
- Dọn lưu trữ cho chọn số ngày; **chuyển** chứ không xoá; không đụng đơn chưa đóng hoặc đã hủy.
- Vai trò đóng gói không dùng được chức năng này.

*Liên kết:* BR-05, BR-13 · FR-13

### US-12 Phân quyền theo vai trò
**Với vai trò** quản trị, **tôi muốn** mỗi vai trò chỉ thấy các trang cần dùng, **để** giảm sai sót và bảo vệ dữ liệu tiền.

**Tiêu chí chấp nhận**
- Mỗi PIN gắn một vai trò và danh sách trang.
- Bên đóng gói không thấy cột tiền.

*Liên kết:* BR-12 · FR-14
