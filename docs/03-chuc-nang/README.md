[🏠 Trang chủ](../../README.md) › **03. Đặc tả chức năng**

# 03. Đặc tả chức năng

Danh mục chức năng được chia theo vai trò. Mỗi chức năng có mã định danh, mô tả và mức ưu tiên MoSCoW (🔴 Must · 🟠 Should · 🟢 Could).

---

## 📑 Mục lục

| #   | Tài liệu | Nhóm chức năng | Số chức năng |
|-----|----------|----------------|:------------:|
| 3.1 | [Quản trị viên (ADMIN)](01-admin.md) | Tài khoản & phân quyền · Danh mục dữ liệu · Cấu hình chống phe vé & chịu tải · Giám sát gian lận · Thống kê & báo cáo | 21 |
| 3.2 | [Ban tổ chức (ORGANIZER)](02-organizer.md) | Sự kiện · Vé & ghế · Đơn hàng · Nhân viên soát vé · Báo cáo | 15 |
| 3.3 | [Nhân viên soát vé (STAFF)](03-checkin-staff.md) | Soát vé · Hoạt động ngoại tuyến · Thống kê nhanh | 7 |
| 3.4 | [Khách hàng (CUSTOMER)](04-customer.md) | Tài khoản · Tra cứu sự kiện · Phòng chờ ảo · Chọn ghế · Thanh toán · Quản lý vé · Thông báo | 30 |
| 3.5 | [Hệ thống (SYSTEM)](05-system.md) | Phòng chờ & điều phối tải · Chống bán trùng ghế · Chống bot · Bảo mật vé · Giám sát & vận hành | 20 |

---

## 🗺️ Bản đồ chức năng

```mermaid
mindmap
  root((Concert<br/>Ticketing))
    ADMIN
      Tài khoản & phân quyền
      Danh mục dữ liệu
      Cấu hình chống bot
      Giám sát gian lận
      Báo cáo
    ORGANIZER
      Sự kiện
      Vé & ghế
      Đơn hàng
      Nhân viên soát vé
      Báo cáo sự kiện
    STAFF
      Quét QR
      Soát vé ngoại tuyến
    CUSTOMER
      Tài khoản
      Tra cứu sự kiện
      Phòng chờ ảo
      Chọn ghế
      Thanh toán giả lập
      Vé QR
    SYSTEM
      Hàng đợi
      Khóa phân tán
      Chống bot
      Bảo mật vé
      Giám sát
```

---

## 🔄 Luồng nghiệp vụ chính: mua vé

```mermaid
sequenceDiagram
    autonumber
    actor KH as Khách hàng
    participant WR as Phòng chờ ảo
    participant GW as API Gateway
    participant SEAT as Seat Service
    participant R as Redis
    participant PAY as Thanh toán (giả lập)
    participant TIX as Ticket Service

    KH->>WR: Vào phòng chờ trước giờ mở bán
    WR->>WR: Chấm điểm rủi ro bot, CAPTCHA nếu cần
    WR-->>KH: Vị trí ngẫu nhiên + thời gian chờ dự kiến
    WR-->>KH: Đến lượt: cấp access token (có hạn)
    KH->>GW: Chọn ghế (kèm token)
    GW->>SEAT: Kiểm tra token, rate limit
    SEAT->>R: SET seat:{id} NX PX 480000
    alt Giữ ghế thành công
        R-->>SEAT: OK
        SEAT-->>KH: Ghế được giữ 8 phút
        KH->>PAY: Thanh toán (idempotency key)
        PAY-->>SEAT: Thành công
        SEAT->>SEAT: Ghi DB (ràng buộc UNIQUE ghế–suất diễn)
        SEAT->>TIX: Phát hành vé
        TIX-->>KH: Vé QR có chữ ký số
    else Ghế đã bị giữ
        R-->>SEAT: nil
        SEAT-->>KH: Ghế không còn trống, chọn ghế khác
    end
```

---

<div align="center">

[← 02. Vai trò & phân quyền](../02-vai-tro-phan-quyen.md) · [🏠 Mục lục](../../README.md) · [3.1 ADMIN →](01-admin.md)

</div>
