[🏠 Trang chủ](../README.md) › **05. Thuật ngữ**

# 05. Thuật ngữ

| Thuật ngữ | Giải thích |
|-----------|------------|
| **Phe vé (scalper)** | Cá nhân hoặc nhóm gom vé số lượng lớn để bán lại với giá cao hơn giá gốc. |
| **Virtual Waiting Room** | Phòng chờ ảo: trang đứng trước hệ thống bán vé, xếp hàng người dùng và chỉ cho vào theo tốc độ hệ thống chịu được. |
| **Access token** | Mã có chữ ký và thời hạn, cấp khi đến lượt, chứng minh người dùng đã qua hàng đợi. |
| **JWT** | JSON Web Token, định dạng token có chữ ký số dùng cho xác thực. |
| **Rate limiting** | Giới hạn số request trong một khoảng thời gian theo IP, thiết bị hoặc tài khoản. |
| **Token bucket** | Thuật toán rate limit: mỗi request tiêu một token, token được nạp lại theo tốc độ cố định. |
| **Device fingerprint** | Tập đặc điểm của trình duyệt / thiết bị dùng để nhận diện và phát hiện bất thường. |
| **Headless browser** | Trình duyệt chạy không giao diện, thường được bot sử dụng (Puppeteer, Selenium). |
| **Risk score** | Điểm rủi ro 0–100 tổng hợp từ các tín hiệu nghi bot. |
| **CAPTCHA** | Bài kiểm tra phân biệt người và máy. |
| **Distributed lock** | Khóa phân tán: đảm bảo chỉ một tiến trình trong nhiều máy chủ được thao tác một tài nguyên tại một thời điểm. |
| **Redlock** | Thuật toán khóa phân tán trên nhiều node Redis. |
| **TTL** | Time To Live: thời gian tồn tại của khóa / dữ liệu trước khi tự hết hạn. |
| **Idempotency** | Tính chất gọi lại nhiều lần cho cùng một kết quả, không tạo dữ liệu trùng. |
| **Race condition** | Lỗi xảy ra khi nhiều tiến trình đồng thời truy cập cùng dữ liệu và kết quả phụ thuộc thứ tự thực thi. |
| **WebSocket** | Kết nối hai chiều giữ liên tục giữa trình duyệt và máy chủ, dùng cập nhật trạng thái ghế realtime. |
| **TOTP** | Mã một lần dựa trên thời gian, dùng cho 2FA và QR động. |
| **Chữ ký số (Ed25519/ECDSA)** | Cơ chế ký bằng khóa riêng, xác thực bằng khóa công khai, chống làm giả vé. |
| **Load test / Spike test / Stress test** | Kiểm thử tải ổn định / tải tăng đột ngột / tải vượt ngưỡng để tìm điểm gãy. |
| **RPS** | Requests per second: số request mỗi giây. |
| **p95 / p99** | 95% / 99% request có độ trễ thấp hơn giá trị này. |
| **TP / FP / FN / TN** | Chặn đúng bot / chặn nhầm người thật / bỏ lọt bot / cho qua đúng người thật. |
| **IDOR** | Insecure Direct Object Reference: lỗ hổng truy cập dữ liệu của người khác bằng cách đổi ID. |
| **MoSCoW** | Phương pháp xếp ưu tiên: Must, Should, Could, Won't. |

---

<div align="center">

[← 04. Kiểm thử & chỉ số đo](04-kiem-thu-chi-so.md) · [🏠 Mục lục](../README.md)

</div>
