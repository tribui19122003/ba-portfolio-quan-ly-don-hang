# 1. Bối cảnh & mục tiêu

## 1.1 Bối cảnh nghiệp vụ

- Doanh nghiệp bán hàng trên **Shopee** (giao qua **SPX Express**) và **TikTok Shop** (giao qua **J&T Express**).
- Mỗi sàn xuất **file Excel đơn hàng** theo định dạng riêng. Đây là **nguồn dữ liệu chính** của hệ thống.
- Hàng được **bên đóng gói (đối tác bên ngoài)** soạn và đóng. Hai bên cần nhìn chung một tình trạng đơn.
- Tên sản phẩm hiển thị trên sàn rất dài, khó hiểu → cần quy đổi về **tên sản phẩm chuẩn** ("Sản phẩm thật") để người đóng gói soạn đúng món.
- Tem vận đơn khổ A6 được **gộp nhiều tem lên một tờ A4** để in.

## 1.2 Các bên liên quan

> Cột "Quan tâm chính" do mình tổng hợp từ yêu cầu.

| Bên | Vai trò | Quan tâm chính |
|---|---|---|
| Doanh nghiệp (chủ hệ thống) | Nhập liệu, in tem, theo dõi | Không sót đơn, không trùng đơn, thấy tổng quan |
| Bên đóng gói (đối tác) | Soạn hàng, xác nhận đã đóng | Danh sách đơn chưa đóng, tên sản phẩm rõ ràng |
| Quản trị | Cấu hình, quản lý bảng phân loại | Kiểm soát dữ liệu và quyền |

## 1.3 Nhu cầu và vấn đề

Theo hồ sơ dự án, nhu cầu nghiệp vụ ban đầu gồm:

1. Bên đóng gói cần **một danh sách đơn chưa đóng** (Excel) để soạn hàng.
2. Bên đóng gói cần thấy **tên sản phẩm rõ ràng, đúng món**, không phải tên listing dài dòng của sàn.
3. Cần **đánh dấu "đã đóng"** để cả nhóm nắm tình hình chung.
4. Hai sàn xuất Excel theo **hai định dạng khác nhau**.

Các vấn đề phát sinh khi vận hành thực tế được ghi ở [Rủi ro & bài học](08-rui-ro-va-bai-hoc.md) (đơn trùng, đơn thiếu sản phẩm, quy đổi sai tên).
## 1.4 Mục tiêu (To-Be)

> Mục tiêu và cách đo do mình đề xuất khi tái cấu trúc tài liệu, **không phải KPI chính thức** của dự án.


| # | Mục tiêu | Cách đo |
|---|---|---|
| G1 | Một nơi chung để cả hai bên theo dõi trạng thái đơn | Mọi đơn có trạng thái in/đóng nhìn được realtime |
| G2 | Tên sản phẩm trên đơn nhất quán với bảng phân loại chuẩn | Tỷ lệ dòng đơn bị gắn cảnh báo "chưa map" |
| G3 | Không nhân đôi đơn khi nhập lại | Số đơn trùng sau khi nhập lại = 0 |
| G4 | Đối soát được giữa dữ liệu đơn và tem đã in | Báo cáo đơn chưa in / tem chưa có dữ liệu |
| G5 | Không phụ thuộc hạ tầng máy chủ riêng | Chạy hoàn toàn trên trình duyệt |

## 1.5 Phạm vi

**Trong phạm vi**
- Nhập liệu từ Excel của 2 sàn, quy đổi tên sản phẩm, đẩy lên kho chung.
- In tem: gộp tem A6 lên A4, đánh dấu đã in, đối soát.
- Đóng gói: danh sách đơn chưa đóng, tổng hợp soạn hàng, xác nhận đã đóng/đã hủy, xuất Excel.
- Quản lý bảng phân loại sản phẩm (SKU) dùng chung.
- Phân quyền theo vai trò.

**Ngoài phạm vi**
- Đọc thông tin sản phẩm từ file PDF tem (chỉ lấy mã vận đơn và vùng cắt tem).
- Xoá dữ liệu đơn hàng (hệ thống chỉ đổi trạng thái).
- Tích hợp API trực tiếp với sàn: hiện nguồn dữ liệu là file Excel xuất tay, chưa làm.
- Máy chủ ứng dụng riêng: hệ thống chạy hoàn toàn trên trình duyệt, không có backend.
