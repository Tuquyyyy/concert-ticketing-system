[🏠 Trang chủ](../README.md) › **01. Tổng quan dự án**

# 01. Tổng quan dự án

**Nội dung:** [Bối cảnh](#1-bối-cảnh) · [Vấn đề](#2-vấn-đề-cần-giải-quyết) · [Mục tiêu](#3-mục-tiêu-dự-án) · [Phạm vi](#4-phạm-vi) · [Các bên liên quan](#5-các-bên-liên-quan) · [Ràng buộc](#6-giả-định--ràng-buộc) · [Chỉ số thành công](#7-chỉ-số-thành-công)

---

## 1. Bối cảnh

Thị trường concert trong nước tăng mạnh, nhiều sự kiện bán hết vé chỉ trong vài phút. Tại thời điểm mở bán, hàng trăm nghìn người truy cập cùng lúc khiến hệ thống bán vé thường xuyên gặp sự cố. Song song đó, các nhóm "phe vé" dùng bot để gom vé ngay khi mở bán rồi bán lại với giá cao, gây thiệt hại cho khán giả và uy tín của ban tổ chức.

## 2. Vấn đề cần giải quyết

| # | Vấn đề | Hệ quả |
|---|--------|--------|
| P1 | Website sập do lưu lượng tăng đột biến khi mở bán | Người dùng không mua được vé, mất doanh thu, khủng hoảng truyền thông |
| P2 | Bot tự động gom vé | Người dùng thật không mua được, vé bị đẩy giá trên chợ đen |
| P3 | Bán trùng ghế khi nhiều người chọn cùng một ghế | Tranh chấp tại cổng, hoàn tiền, mất uy tín |
| P4 | Vé giả, vé bị sao chép (chụp màn hình QR) | Nhiều người vào bằng một vé, thất thoát doanh thu |

## 3. Mục tiêu dự án

- **G1 – Chịu tải cao:** hệ thống không sập khi lượng truy cập tăng đột biến nhờ phòng chờ ảo và điều tiết lưu lượng.
- **G2 – Chống phe vé:** phát hiện và chặn bot với tỉ lệ chặn đúng cao, hạn chế chặn nhầm người dùng thật.
- **G3 – Toàn vẹn dữ liệu:** tỉ lệ bán trùng ghế **bằng 0** trong mọi kịch bản tranh chấp.
- **G4 – Vé an toàn:** vé QR có chữ ký số, không làm giả được, mỗi vé chỉ dùng một lần.
- **G5 – Công bằng:** thứ tự vào mua được phân phối công bằng, người dùng biết rõ vị trí và thời gian chờ.

## 4. Phạm vi

### 4.1 Trong phạm vi

- Web chọn ghế theo thời gian thực.
- Phòng chờ ảo và hàng đợi phân tán.
- Cơ chế phát hiện và chặn bot.
- Khóa phân tán chống bán trùng ghế.
- Thanh toán **giả lập** (không kết nối cổng thanh toán thật).
- Vé QR chống làm giả và ứng dụng/trang soát vé.
- Trang quản trị cho Admin và Ban tổ chức.
- Bộ kịch bản load test và security test.

### 4.2 Ngoài phạm vi

- Tích hợp cổng thanh toán thật (VNPay, MoMo, thẻ quốc tế).
- Ứng dụng di động native (chỉ làm web responsive).
- Chợ bán lại vé (resale marketplace).
- Xuất hóa đơn điện tử.

## 5. Các bên liên quan

| Bên liên quan | Vai trò | Quan tâm chính |
|---------------|---------|----------------|
| Khách hàng | Mua vé | Mua được vé công bằng, nhanh, an toàn |
| Ban tổ chức | Tạo và bán sự kiện | Bán hết vé, đúng người, báo cáo minh bạch |
| Nhân viên soát vé | Kiểm soát cổng vào | Soát vé nhanh, phát hiện vé giả |
| Quản trị viên | Vận hành nền tảng | Ổn định, an toàn, chống gian lận |
| Giảng viên hướng dẫn | Đánh giá đồ án | Chất lượng kỹ thuật, số liệu đo kiểm |

## 6. Giả định & ràng buộc

- Thanh toán được giả lập, luôn trả kết quả thành công/thất bại/quá hạn theo cấu hình.
- Môi trường kiểm thử tải chạy trên hạ tầng giới hạn (máy cá nhân hoặc cloud gói sinh viên); kết quả được chuẩn hóa theo cấu hình phần cứng.
- Bot dùng để kiểm thử do nhóm tự xây dựng, không thử nghiệm trên hệ thống của bên thứ ba.
- Dữ liệu người dùng trong demo là dữ liệu giả.

## 7. Chỉ số thành công

| Chỉ số | Yêu cầu |
|--------|---------|
| Số request/giây chịu được | Đo và báo cáo ngưỡng tối đa |
| Tỉ lệ bán trùng ghế | **= 0** |
| Tỉ lệ chặn bot đúng | Đo và báo cáo (kèm tỉ lệ chặn nhầm) |
| Thời gian chờ trung bình | Đo và báo cáo trong kịch bản mở bán |

Chi tiết cách đo xem tại [04. Kiểm thử & chỉ số đo](04-kiem-thu-chi-so.md).

---

<div align="center">

[🏠 Mục lục](../README.md) · [Tiếp: 02. Vai trò & phân quyền →](02-vai-tro-phan-quyen.md)

</div>
