# 2. BRD — Yêu cầu nghiệp vụ

> Mã yêu cầu do mình đặt khi tái cấu trúc tài liệu. Nguồn: hồ sơ bàn giao dự án.

## 2.1 Quy tắc nghiệp vụ (Business Rules)

| Mã | Quy tắc |
|---|---|
| BR-01 | Mỗi đơn được định danh bằng **Mã vận đơn**, hoặc **Mã đơn hàng** nếu đơn không có mã vận đơn (ví dụ đơn hỏa tốc). Đây là khoá liên kết xuyên suốt giữa nhập liệu, in tem, đóng gói. |
| BR-02 | Tên sản phẩm trên đơn phải được quy đổi về "Sản phẩm thật" theo **bảng phân loại chuẩn**. Ưu tiên khớp theo **SKU**; không có SKU thì khớp theo **Tên giỏ hàng + Phân loại**. Không khớp được thì **giữ tên gốc và gắn cảnh báo**. |
| BR-03 | Một dòng đơn có thể ra **nhiều sản phẩm** (combo). Số lượng thật = số lượng đơn × hệ số trong bảng phân loại. |
| BR-04 | Một dòng dữ liệu = **một sản phẩm thật trong một đơn**. Nếu cùng sản phẩm xuất hiện nhiều lần trong một đơn thì **cộng dồn số lượng** trước khi lưu. |
| BR-05 | **Chống trùng:** nhập lại cùng một đơn thì **cập nhật**, không tạo thêm dòng. Hai dòng được coi là trùng nếu trùng mã vận đơn **hoặc** mã đơn hàng, và cùng sản phẩm. |
| BR-06 | Trạng thái đóng gồm **Chưa đóng · Đã đóng · Đã hủy**. Hệ thống **không xoá dữ liệu**, chỉ đổi trạng thái; bảng tính chung là sổ cái. |
| BR-07 | Đơn **Đã hủy** bị loại khỏi danh sách soạn hàng và file xuất Excel; được đếm riêng. |
| BR-08 | Đơn **đã đóng** vẫn có thể chuyển sang **Đã hủy** (khách hủy sau khi hàng đã đóng). |
| BR-09 | Tem A4 gộp **6, 4 hoặc 2 tem/tờ**, mặc định 6. |
| BR-10 | Sau khi tạo file in, các đơn tương ứng được đánh dấu **Đã in**. |
| BR-11 | Hệ thống phải **đối soát**: đơn có dữ liệu nhưng chưa in tem, và tem đã in nhưng chưa có dữ liệu đơn. |
| BR-12 | **Phân quyền theo vai trò**; bên đóng gói **không nhìn thấy các cột tiền**. |
| BR-13 | Đơn đã đóng cũ hơn N ngày có thể **chuyển sang trang lưu trữ** (không xoá). |
| BR-14 | Danh sách hiển thị **đơn mới nhất lên trên**. |

## 2.2 Yêu cầu chức năng (Functional Requirements)

| Mã | Yêu cầu | Nhóm |
|---|---|---|
| FR-01 | Đọc được 2 định dạng Excel đơn hàng (Shopee, TikTok Shop) và chuẩn hoá về một cấu trúc dữ liệu chung | Nhập liệu |
| FR-02 | Quy đổi tên sản phẩm theo BR-02, BR-03; hiển thị cờ cảnh báo cho dòng chưa khớp | Nhập liệu |
| FR-03 | Đẩy đơn mới lên kho chung với cơ chế chống trùng theo BR-05 | Nhập liệu |
| FR-04 | Quản lý bảng phân loại sản phẩm dùng chung: thêm, sửa, xoá, nạp hàng loạt, không nhân đôi khi nạp lại | Nhập liệu |
| FR-05 | Đọc file PDF tem vận đơn, trích mã vận đơn và vùng cắt tem | In tem |
| FR-06 | Ghép tem lên A4 theo BR-09, giữ chất lượng mã vạch | In tem |
| FR-07 | Đánh dấu đã in (BR-10) và bảng đối soát (BR-11) | In tem |
| FR-08 | Xuất file Excel danh sách đơn chưa đóng | Đóng gói |
| FR-09 | Tổng hợp soạn hàng: cộng theo sản phẩm thật | Đóng gói |
| FR-10 | Xác nhận Đã đóng / Đã hủy theo từng đơn hoặc chọn nhiều (BR-06, 07, 08) | Đóng gói |
| FR-11 | Cảnh báo cho bên đóng gói khi tên sản phẩm không có trong bảng phân loại | Đóng gói |
| FR-12 | Trang chủ hiển thị thống kê trạng thái và dẫn vào 3 luồng | Chung |
| FR-13 | Gộp các dòng đơn trùng đã tồn tại và dọn lưu trữ theo số ngày chọn (BR-13) | Quản trị |
| FR-14 | Đăng nhập theo vai trò bằng mã PIN, mỗi vai trò chỉ thấy các trang được phép (BR-12) | Chung |

## 2.3 Yêu cầu phi chức năng (NFR)

| Mã | Yêu cầu |
|---|---|
| NFR-01 | Chạy hoàn toàn trên trình duyệt; triển khai được lên dịch vụ lưu trữ tĩnh. |
| NFR-02 | Dữ liệu dùng chung giữa các bên qua một bảng tính trực tuyến, thấy gần như tức thời. |
| NFR-03 | Chịu được kết nối chập chờn: tự thử lại tối đa 3 lần, quá 15 giây mỗi lần thì ngắt, các thao tác đều an toàn khi lặp lại. |
| NFR-04 | Thư viện xử lý PDF/Excel đóng gói kèm, không phụ thuộc mạng ngoài. |
| NFR-05 | Giao diện tiếng Việt. |

## 2.4 Ràng buộc & giả định

- **Ràng buộc:** không có máy chủ riêng; kho dữ liệu là bảng tính trực tuyến; phân quyền theo PIN là cổng nhẹ phía trình duyệt, **không phải bảo mật tuyệt đối**.
- **Giả định:** người dùng xuất file Excel từ sàn theo đúng định dạng; bảng phân loại được nhân viên duy trì.
- **Phụ thuộc:** thay đổi phía máy chủ bảng tính (script) phải được triển khai lại riêng, tách khỏi phần giao diện.

## 2.5 Chưa chốt / Rủi ro mở

- Chưa có file Excel TikTok loại "chờ đóng" thật để quyết định có lọc theo trạng thái đơn khi nhập hay không (mẫu hiện có là "đã vận chuyển").
- Đơn giao hàng nhanh hiện được gắn kênh SPX do chưa có kênh riêng; chỉ ảnh hưởng nhãn hiển thị.
