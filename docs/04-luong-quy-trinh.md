# 4. Luồng quy trình

## 4.1 Quy trình tổng thể

```mermaid
flowchart TD
    A([Bắt đầu: có đơn mới trên sàn]) --> B[Nhân viên xuất file Excel từ sàn]
    B --> C[Trang Nhập liệu: kéo thả file]
    C --> D{Quy đổi tên<br/>sản phẩm khớp?}
    D -- Khớp --> F[Chuẩn bị đẩy lên kho chung]
    D -- Không khớp --> E[Gắn cảnh báo<br/>nhân viên gán nhanh]
    E --> F
    F --> G[(Kho dữ liệu chung)]
    G --> H[Trang In tem: kéo thả PDF vận đơn]
    H --> I[Gộp tem lên A4 và in]
    I --> J[Đánh dấu Đã in]
    J --> G
    G --> K[Trang Đóng gói: xuất Excel đơn chưa đóng]
    K --> L[Soạn hàng theo tổng hợp sản phẩm]
    L --> M{Khách hủy?}
    M -- Không --> N[Đánh dấu Đã đóng]
    M -- Có --> O[Đánh dấu Đã hủy]
    N --> G
    O --> G
    N --> P{Khách hủy sau khi đóng?}
    P -- Có --> O
    P -- Không --> Q([Kết thúc])
```

## 4.2 Vòng đời trạng thái đơn

```mermaid
stateDiagram-v2
    [*] --> ChuaDong: Đẩy đơn lên kho chung
    ChuaDong --> DaDong: Xác nhận đã đóng
    ChuaDong --> DaHuy: Đánh dấu hủy
    DaDong --> DaHuy: Khách hủy sau khi đóng
    DaHuy --> ChuaDong: Bỏ hủy
    DaDong --> LuuTru: Dọn lưu trữ quá N ngày
    LuuTru --> [*]

    note right of ChuaDong
        Hiển thị: Chưa đóng
    end note
    note right of DaHuy
        Hiển thị: Đã hủy
        Loại khỏi soạn hàng và xuất Excel
    end note
```

Song song với trạng thái đóng, mỗi đơn có cờ **Đã in** (trống → ✓) được đặt khi in tem.
Quy tắc: không xoá dòng; chỉ đổi trạng thái hoặc chuyển sang trang lưu trữ.

## 4.3 Trình tự giữa các bên

```mermaid
sequenceDiagram
    actor NV as Nhân viên nhập liệu
    participant N as Trang Nhập liệu
    participant K as Kho dữ liệu chung
    actor DG as Bên đóng gói
    actor IT as Người in tem
    participant T as Trang In tem
    participant G as Trang Đóng gói

    NV->>N: Thả file Excel đơn hàng
    N->>N: Quy đổi tên sản phẩm theo bảng phân loại
    N->>K: Đẩy đơn mới (chống trùng)
    IT->>T: Thả PDF tem vận đơn
    T->>K: Đánh dấu Đã in theo mã vận đơn
    T-->>IT: Báo đối soát (chưa in / chưa có dữ liệu)
    DG->>G: Mở danh sách đơn chưa đóng
    G->>K: Lấy đơn Chưa đóng
    K-->>G: Danh sách đơn
    DG->>G: Xác nhận Đã đóng hoặc Đã hủy
    G->>K: Cập nhật trạng thái, người đóng, thời điểm
```

## 4.4 Logic quy đổi tên sản phẩm (quy tắc quyết định)

Đây là phần quan trọng nhất của hệ thống: sai ở đây thì bên đóng gói soạn nhầm hàng.

```mermaid
flowchart TD
    S([Một dòng đơn từ sàn]) --> A{Đã có gán nhanh<br/>theo đúng SKU?}
    A -- Có --> R1[Dùng kết quả gán nhanh]
    A -- Không --> B{SKU có trong<br/>bảng phân loại?}
    B -- Có --> R2[Dùng theo SKU]
    B -- Không --> C{Đã có gán nhanh<br/>theo tên?}
    C -- Có --> R3[Dùng gán nhanh theo tên]
    C -- Không --> D[Khớp theo tên + phân loại<br/>phân loại chấm điểm cao hơn tên]
    D --> E{Dòng có điền SKU<br/>nhưng SKU không có trong bảng?}
    E -- Có --> W1[⚠ Gắn cảnh báo]
    E -- Không --> F{Hai lựa chọn hoà điểm?}
    F -- Có --> W2[⚠ Gắn cảnh báo thay vì lấy bừa]
    F -- Không --> OK[Kết quả khớp]
    D -- Không khớp được --> W3[Giữ tên gốc + ⚠]
```

**Nguyên tắc rút ra:** thà **cảnh báo** còn hơn **lặng lẽ sai**. Mọi nhánh không chắc chắn đều dẫn tới cảnh báo.
