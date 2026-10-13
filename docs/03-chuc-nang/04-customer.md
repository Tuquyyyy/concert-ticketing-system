[🏠 Trang chủ](../../README.md) › [03. Đặc tả chức năng](README.md) › **3.4 Khách hàng (CUSTOMER)**

# 3.4 Khách hàng (CUSTOMER)

> Người mua vé: tìm sự kiện, chờ trong phòng chờ ảo, chọn ghế theo thời gian thực, thanh toán và nhận vé QR.

**Nội dung:** [A. Tài khoản](#a-tài-khoản-cá-nhân) · [B. Tra cứu sự kiện](#b-tìm-kiếm--tra-cứu-sự-kiện) · [C. Phòng chờ ảo](#c-phòng-chờ-ảo-virtual-waiting-room) · [D. Chọn ghế](#d-chọn-ghế--đặt-vé) · [E. Thanh toán](#e-thanh-toán-giả-lập) · [F. Quản lý vé](#f-quản-lý-vé) · [G. Thông báo](#g-thông-báo)

---

## A. Tài khoản cá nhân

| Mã | Chức năng | Mô tả | Ưu tiên |
|----|-----------|-------|:-------:|
| `CUS-01` | Đăng ký | Đăng ký bằng email / số điện thoại, mật khẩu đủ mạnh. | 🔴 Must |
| `CUS-02` | Đăng nhập / đăng xuất | Đăng nhập bằng email hoặc SĐT; JWT + refresh token. | 🔴 Must |
| `CUS-03` | Quên / đổi mật khẩu | Đặt lại mật khẩu qua email, đổi mật khẩu khi đã đăng nhập. | 🔴 Must |
| `CUS-04` | Xác thực OTP | Xác thực email / SĐT bằng OTP; bắt buộc trước khi được mua vé. | 🔴 Must |
| `CUS-05` | Xác thực 2 lớp (2FA) | Bật/tắt 2FA bằng ứng dụng TOTP. | 🟢 Could |
| `CUS-06` | Hồ sơ & thiết bị | Cập nhật thông tin cá nhân; xem và đăng xuất các thiết bị đang đăng nhập. | 🟠 Should |

## B. Tìm kiếm & tra cứu sự kiện

| Mã | Chức năng | Mô tả | Ưu tiên |
|----|-----------|-------|:-------:|
| `CUS-07` | Tìm kiếm sự kiện | Theo tên, nghệ sĩ, thể loại, thành phố, ngày. | 🔴 Must |
| `CUS-08` | Xem chi tiết sự kiện | Mô tả, sơ đồ khu, bảng giá, thời điểm mở bán, chính sách hoàn vé. | 🔴 Must |
| `CUS-09` | Đăng ký nhận thông báo mở bán | Nhận email / thông báo khi phòng chờ sắp mở. | 🟠 Should |
| `CUS-10` | Sự kiện nổi bật | Danh sách sự kiện nổi bật, sắp diễn ra trên trang chủ. | 🟢 Could |

## C. Phòng chờ ảo (Virtual Waiting Room)

| Mã | Chức năng | Mô tả | Ưu tiên |
|----|-----------|-------|:-------:|
| `CUS-11` | Vào phòng chờ | Vào phòng chờ trước giờ mở bán; mọi người vào trước giờ mở bán được xếp vị trí ngẫu nhiên. | 🔴 Must |
| `CUS-12` | Xem vị trí & thời gian chờ | Vị trí trong hàng, số người phía trước, thời gian chờ dự kiến, cập nhật realtime. | 🔴 Must |
| `CUS-13` | Giữ lượt khi tải lại trang | Lượt gắn với tài khoản + phiên; tải lại trang hoặc mất mạng ngắn không mất vị trí. | 🔴 Must |
| `CUS-14` | Xác minh CAPTCHA | Hiển thị CAPTCHA khi risk score vượt ngưỡng. | 🔴 Must |
| `CUS-15` | Nhận lượt vào mua | Đến lượt: nhận access token có thời hạn để vào trang chọn ghế. | 🔴 Must |

## D. Chọn ghế & đặt vé

| Mã | Chức năng | Mô tả | Ưu tiên |
|----|-----------|-------|:-------:|
| `CUS-16` | Xem sơ đồ ghế realtime | Trạng thái ghế cập nhật qua WebSocket, phân màu theo hạng vé. | 🔴 Must |
| `CUS-17` | Chọn ghế thủ công | Chọn từng ghế trên sơ đồ, trong giới hạn số vé cho phép. | 🔴 Must |
| `CUS-18` | Chọn "ghế tốt nhất" | Hệ thống tự chọn ghế liền nhau tốt nhất còn trống theo hạng vé và số lượng. | 🟠 Should |
| `CUS-19` | Giữ ghế có đếm ngược | Ghế được giữ trong thời gian cố định (vd: 8 phút), hiển thị đồng hồ đếm ngược. | 🔴 Must |
| `CUS-20` | Nhả ghế | Ghế tự trả về khi khách hủy hoặc hết thời gian giữ. | 🔴 Must |

## E. Thanh toán (giả lập)

| Mã | Chức năng | Mô tả | Ưu tiên |
|----|-----------|-------|:-------:|
| `CUS-21` | Chọn phương thức thanh toán | Thẻ, ví điện tử, QR ngân hàng (đều giả lập). | 🔴 Must |
| `CUS-22` | Áp dụng mã giảm giá / presale | Kiểm tra hiệu lực, giới hạn lượt dùng. | 🟢 Could |
| `CUS-23` | Nhận kết quả thanh toán | Thành công / thất bại / quá hạn; thất bại hoặc quá hạn thì nhả ghế. | 🔴 Must |

## F. Quản lý vé

| Mã | Chức năng | Mô tả | Ưu tiên |
|----|-----------|-------|:-------:|
| `CUS-24` | Danh sách vé đã mua | Vé sắp diễn ra, vé đã sử dụng, vé đã hủy. | 🔴 Must |
| `CUS-25` | Chi tiết vé & QR động | Hiển thị sự kiện, ghế, cổng vào; QR thay đổi theo thời gian, chống chụp màn hình. | 🔴 Must |
| `CUS-26` | Chuyển nhượng vé | Chuyển vé cho tài khoản khác đã xác thực; giới hạn số lần, không bán qua hệ thống. | 🟢 Could |
| `CUS-27` | Yêu cầu hoàn vé | Gửi yêu cầu hoàn vé theo chính sách sự kiện, theo dõi trạng thái. | 🟠 Should |
| `CUS-28` | Lịch sử giao dịch | Danh sách đơn hàng, thanh toán, hoàn tiền. | 🟠 Should |

## G. Thông báo

| Mã | Chức năng | Mô tả | Ưu tiên |
|----|-----------|-------|:-------:|
| `CUS-29` | Thông báo qua email / dashboard | Mở bán, đến lượt trong hàng đợi, thanh toán thành công, vé đã chuyển nhượng. | 🟠 Should |
| `CUS-30` | Nhắc lịch sự kiện | Nhắc trước ngày diễn ra, kèm cổng vào và hướng dẫn. | 🟢 Could |

---

## Quy tắc nghiệp vụ liên quan

| Mã | Quy tắc |
|----|---------|
| `BR-40` | Chỉ tài khoản đã xác thực OTP mới được vào phòng chờ. |
| `BR-41` | Mỗi tài khoản chỉ có một vị trí trong hàng đợi của mỗi sự kiện; mở nhiều tab không tạo thêm lượt. |
| `BR-42` | Access token chỉ dùng được cho đúng tài khoản và thiết bị được cấp. |
| `BR-43` | Một tài khoản mua tối đa N vé / sự kiện (N do admin cấu hình, mặc định 4). |
| `BR-44` | Ghế đang giữ không hiển thị là trống với người khác cho đến khi hết hạn giữ. |

---

<div align="center">

[← 3.3 STAFF](03-checkin-staff.md) · [🏠 Mục lục](../../README.md) · [3.5 SYSTEM →](05-system.md)

</div>
