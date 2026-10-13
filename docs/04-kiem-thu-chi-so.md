[🏠 Trang chủ](../README.md) › **04. Kiểm thử & chỉ số đo**

# 04. Kiểm thử & chỉ số đo (Capstone III)

**Nội dung:** [KPI](#1-chỉ-số-đo-kpi) · [Môi trường](#2-môi-trường-kiểm-thử) · [Load test](#3-load-test) · [Tranh chấp ghế](#4-kiểm-thử-tranh-chấp-ghế) · [Security test](#5-security-test) · [Trải nghiệm người dùng](#6-trải-nghiệm-người-dùng) · [Mẫu báo cáo](#7-mẫu-báo-cáo-kết-quả)

---

## 1. Chỉ số đo (KPI)

| Mã | Chỉ số | Cách tính | Mục tiêu |
|----|--------|-----------|----------|
| `KPI-01` | Throughput tối đa | Số request/giây cao nhất khi tỉ lệ lỗi còn < 1% và p95 < 1 giây | Đo và báo cáo |
| `KPI-02` | Độ trễ | p50 / p95 / p99 của API chọn ghế và thanh toán | p95 < 500 ms ở tải mục tiêu |
| `KPI-03` | Tỉ lệ bán trùng ghế | Số ghế có > 1 vé hợp lệ / tổng số ghế đã bán | **= 0** |
| `KPI-04` | Tỉ lệ chặn bot đúng | Số phiên bot bị chặn / tổng số phiên bot | ≥ 90% |
| `KPI-05` | Tỉ lệ chặn nhầm | Số phiên người thật bị chặn / tổng số phiên người thật | ≤ 2% |
| `KPI-06` | Thời gian chờ trung bình | Trung bình (lúc nhận token − lúc vào hàng đợi) | Đo và báo cáo |
| `KPI-07` | Tỉ lệ mua thành công | Số người thật mua được vé / số người thật vào hàng đợi (khi còn vé) | Đo và báo cáo |

> Các mục tiêu là đề xuất ban đầu, sẽ điều chỉnh theo hạ tầng thực tế.

## 2. Môi trường kiểm thử

| Thành phần | Mô tả |
|------------|-------|
| Hệ thống đích | Docker Compose / Kubernetes, ghi rõ CPU, RAM, số bản sao mỗi service |
| Máy sinh tải | Tách riêng với hệ thống đích để kết quả không bị ảnh hưởng |
| Công cụ | k6 (chính), JMeter hoặc Locust (đối chiếu), Selenium / Puppeteer / Playwright (bot) |
| Giám sát | Prometheus + Grafana, lưu ảnh chụp dashboard cho từng lần chạy |
| Dữ liệu | Sự kiện mẫu 5.000 – 20.000 ghế, 50.000+ tài khoản giả |

## 3. Load test

| Mã | Kịch bản | Mô tả | Chỉ số |
|----|----------|-------|--------|
| `TST-01` | Baseline | Tải ổn định thấp để lấy mốc độ trễ | KPI-02 |
| `TST-02` | Load | Tăng dần đến tải mục tiêu, giữ 10 phút | KPI-01, KPI-02 |
| `TST-03` | Spike (mở bán) | 10.000+ người vào phòng chờ trong 1 phút | KPI-01, KPI-06 |
| `TST-04` | Stress | Tăng tải đến khi hệ thống gãy, xác định điểm gãy | KPI-01 |
| `TST-05` | So sánh có / không phòng chờ | Chạy cùng tải với phòng chờ bật và tắt | KPI-01, KPI-02 |

## 4. Kiểm thử tranh chấp ghế

| Mã | Kịch bản | Kết quả mong đợi |
|----|----------|------------------|
| `TST-10` | 1.000 request đồng thời cùng giữ một ghế | Đúng 1 request thành công |
| `TST-11` | Nhiều người giữ các nhóm ghế chồng lấn | Không ai giữ được một phần nhóm ghế |
| `TST-12` | Hết TTL giữ ghế đúng lúc đang thanh toán | Không phát hành vé cho ghế đã bị người khác giữ |
| `TST-13` | Gửi lại request thanh toán nhiều lần | Chỉ một đơn, một vé (idempotency) |
| `TST-14` | Tắt Redis giữa chừng | Ràng buộc CSDL vẫn chặn trùng ghế |

Sau mỗi lần chạy, truy vấn kiểm tra:

```sql
SELECT show_id, seat_id, COUNT(*) AS so_ve
FROM tickets
WHERE status = 'VALID'
GROUP BY show_id, seat_id
HAVING COUNT(*) > 1;   -- kết quả phải rỗng
```

## 5. Security test

| Mã | Kịch bản | Kết quả mong đợi |
|----|----------|------------------|
| `TST-20` | Bot gọi API trực tiếp bằng script | Bị rate limit / không có token nên bị từ chối |
| `TST-21` | Bot dùng Selenium / Puppeteer headless | Bị phát hiện, yêu cầu CAPTCHA hoặc chặn |
| `TST-22` | Nhiều tài khoản từ cùng thiết bị / IP | Bị giới hạn và gắn cờ cụm tài khoản |
| `TST-23` | Giả mạo / dùng lại access token | Bị từ chối |
| `TST-24` | Làm giả QR, sửa payload | Thiết bị soát vé báo vé giả |
| `TST-25` | Dùng ảnh chụp QR cũ, quét một vé hai lần | Báo QR hết hạn / vé đã sử dụng |
| `TST-26` | OWASP Top 10 | Không có lỗ hổng SQL injection, XSS, IDOR, broken authentication |

Đo KPI-04 và KPI-05 bằng tập dữ liệu có nhãn: trộn phiên bot (do nhóm tạo) và phiên người thật (tình nguyện viên hoặc script mô phỏng hành vi người thật), sau đó tính ma trận nhầm lẫn.

|  | Hệ thống chặn | Hệ thống cho qua |
|--|:-------------:|:----------------:|
| **Bot thật** | TP | FN |
| **Người thật** | FP | TN |

## 6. Trải nghiệm người dùng

| Mã | Kịch bản | Chỉ số |
|----|----------|--------|
| `TST-30` | Đo thời gian chờ ở nhiều mức tải và tốc độ cho vào | KPI-06 |
| `TST-31` | Đo tỉ lệ mua thành công của người thật khi có bot cạnh tranh | KPI-07 |
| `TST-32` | Độ chính xác thời gian chờ dự kiến so với thực tế | Sai số trung bình |

## 7. Mẫu báo cáo kết quả

| Lần chạy | Kịch bản | Cấu hình | RPS max | p95 (ms) | Lỗi (%) | Trùng ghế | Ghi chú |
|----------|----------|----------|--------:|---------:|--------:|:---------:|---------|
| R01 | TST-02 | 2 bản sao | | | | | |
| R02 | TST-03 | 4 bản sao | | | | | |

---

<div align="center">

[← 3.5 SYSTEM](03-chuc-nang/05-system.md) · [🏠 Mục lục](../README.md) · [05. Thuật ngữ →](05-thuat-ngu.md)

</div>
