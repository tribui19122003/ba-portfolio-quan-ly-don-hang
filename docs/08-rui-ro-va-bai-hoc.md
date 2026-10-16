# 8. Rủi ro & bài học

Các sự cố thực tế trong quá trình vận hành, kèm nguyên nhân gốc và cách xử lý. Tên sản phẩm, mã đơn và mã SKU của khách hàng đã được ẩn.

| # | Sự cố | Nguyên nhân gốc | Xử lý | Bài học cho BA |
|---|---|---|---|---|
| L-01 | Một số đơn có **số lượng sai** (ví dụ một số bất thường, ví dụ 123 thay vì 2); đơn combo nhỏ bị **gộp thành một sản phẩm** | Tên và số lượng được **ghi cứng lúc đẩy lên**. Bảng phân loại sửa về sau **không** tự cập nhật các dòng đã ghi | Sửa tay các dòng cũ hoặc xoá rồi đẩy lại; bảng phân loại mới tách đúng từng sản phẩm | Dữ liệu tham chiếu thay đổi cần **quy tắc hồi tố** rõ ràng. Phải nêu trong yêu cầu: dữ liệu cũ có được cập nhật theo không? |
| L-02 | Đơn bị hiển thị **sai dung tích** mà không có cảnh báo | Khi bước SKU không tra được, hệ thống rơi về khớp theo tên; tên chứa **cả hai dung tích** nên hoà điểm và lặng lẽ lấy dòng đầu | Đổi thứ tự ưu tiên, chấm điểm phân loại cao hơn tên, và **hoà điểm hoặc SKU lạ đều phải cảnh báo**. Thêm chốt chặn thứ hai cho bên đóng gói | **Sai im lặng nguy hiểm hơn sai có cảnh báo.** Khi viết quy tắc quyết định, phải định nghĩa rõ "không chắc chắn" thì làm gì |
| L-03 | Khoảng 31 sản phẩm bị **gom thành một "đơn" vô danh** ở trang Đóng gói | Đơn nhiều món **dán tay** vào bảng tính chỉ có dòng đầu có mã; các dòng phụ trống mã nên cùng một khoá | Tự điền mã cho dòng phụ nếu cùng người nhận và tỉnh với dòng có mã ngay trên; khoá dự phòng không bao giờ gộp cục | Đừng chỉ thiết kế cho luồng chuẩn. Cần tính cả **dữ liệu nhập tay** và quy tắc tự phục hồi |
| L-04 | **38 đơn trùng** trong kho dữ liệu | Lần đẩy đầu có đủ 2 mã, lần sau mất mã vận đơn chỉ còn mã đơn hàng nên khoá khác nhau | Khớp theo **một trong hai mã**, chỉ ghi đè mã khi lần này có mã; thêm chức năng gộp đơn trùng cũ | Khoá định danh phải xét cả trường hợp **thiếu một phần** |
| L-05 | **Đơn của một hãng giao nhanh bị rơi** khỏi hệ thống | Mẫu nhận diện mã vận đơn quá chặt, mã ngắn không khớp nên cả đơn bị bỏ qua | Nới mẫu nhận diện. Thử lại: từ 7 lên 8 đơn, không ảnh hưởng file của sàn còn lại | Quy tắc **loại bỏ** dữ liệu cần kiểm thử kỹ hơn quy tắc chấp nhận, vì lỗi ở đây là mất đơn |
| L-06 | Tính năng mới **không có tác dụng** dù đã triển khai | Phần giao diện và phần máy chủ bảng tính triển khai **riêng**; người dùng hay quên triển khai lại phần máy chủ | Thêm cảnh báo trong giao diện khi phát hiện máy chủ còn bản cũ | Yêu cầu phi chức năng về **triển khai và tương thích phiên bản** cần viết ra từ đầu |
| L-07 | Bên đóng gói **thấy trang trống** dù có đơn chưa đóng | Bảng tính lớn dần, tải chậm và chập chờn; không có bản lưu trên máy mới | Tự thử lại tối đa 3 lần, quá 15 giây thì ngắt; các thao tác an toàn khi lặp | NFR về **hiệu năng và độ bền kết nối** nên có từ đầu, không chỉ khi sự cố |
| L-08 | Nút "Dọn lưu trữ" **dọn ra 0 đơn** nên tưởng hỏng | Ngưỡng cố định 60 ngày trong khi hệ thống mới chạy chưa tới 60 ngày; hộp xác nhận còn bị che bởi hộp cấu hình | Cho chọn số ngày (mặc định 7); sửa thứ tự hiển thị hộp thoại | Giá trị mặc định phải hợp với **dữ liệu thực tế**; kiểm thử với dữ liệu thật |

## Điều rút ra chung

1. **Thà cảnh báo còn hơn sai im lặng.** Mọi nhánh không chắc chắn phải để lại dấu vết cho con người thấy.
2. **Dữ liệu tham chiếu thay đổi theo thời gian** — cần nêu rõ trong yêu cầu việc có hồi tố hay không.
3. **Thiết kế cho cả luồng ngoại lệ:** dữ liệu nhập tay, mã thiếu, đơn nhiều món, khách hủy muộn.
4. **Ghi bằng chứng kiểm thử gắn với yêu cầu** để thấy được chỗ nào chưa được kiểm (xem [Truy vết yêu cầu](07-truy-vet-yeu-cau.md)).
