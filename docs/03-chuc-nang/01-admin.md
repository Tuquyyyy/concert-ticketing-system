[🏠 Trang chủ](../../README.md) › [03. Đặc tả chức năng](README.md) › **3.1 Quản trị viên (ADMIN)**

# 3.1 Quản trị viên (ADMIN)

> Người vận hành toàn bộ nền tảng: quản lý tài khoản, dữ liệu dùng chung, cấu hình cơ chế chống phe vé và chịu tải, xử lý gian lận và theo dõi báo cáo.

**Nội dung:** [A. Tài khoản & phân quyền](#a-quản-lý-tài-khoản--phân-quyền) · [B. Danh mục dữ liệu](#b-quản-lý-danh-mục-dữ-liệu) · [C. Cấu hình chống phe vé & chịu tải](#c-cấu-hình-chống-phe-vé--chịu-tải) · [D. Giám sát gian lận](#d-giám-sát--xử-lý-gian-lận) · [E. Thống kê & báo cáo](#e-thống-kê--báo-cáo)

---

## A. Quản lý tài khoản & phân quyền

| Mã | Chức năng | Mô tả | Ưu tiên |
|----|-----------|-------|:-------:|
| `ADM-01` | CRUD tài khoản người dùng | Tạo, xem, sửa, xóa mềm tài khoản khách hàng, ban tổ chức, nhân viên soát vé. Tìm kiếm, lọc theo vai trò, trạng thái. | 🔴 Must |
| `ADM-02` | Gán quyền theo vai trò | Gán vai trò `admin / organizer / staff / customer` cho tài khoản. | 🔴 Must |
| `ADM-03` | Reset mật khẩu, khóa/mở tài khoản | Gửi link đặt lại mật khẩu, khóa/mở tài khoản kèm lý do. | 🔴 Must |
| `ADM-04` | Buộc đăng xuất mọi phiên | Thu hồi toàn bộ token của một tài khoản (khi nghi bị chiếm quyền). | 🟠 Should |
| `ADM-05` | Duyệt hồ sơ ban tổ chức | Xem thông tin, giấy tờ, duyệt hoặc từ chối đăng ký làm ban tổ chức. | 🟠 Should |

## B. Quản lý danh mục dữ liệu

| Mã | Chức năng | Mô tả | Ưu tiên |
|----|-----------|-------|:-------:|
| `ADM-06` | Quản lý danh mục | CRUD thể loại sự kiện, nghệ sĩ, địa điểm (venue). | 🔴 Must |
| `ADM-07` | Quản lý sơ đồ địa điểm | Định nghĩa khu (zone), hàng, ghế, tọa độ hiển thị; nhập sơ đồ từ file JSON/CSV. | 🔴 Must |
| `ADM-08` | Duyệt sự kiện | Duyệt / từ chối sự kiện do ban tổ chức tạo trước khi công khai. | 🟠 Should |

## C. Cấu hình chống phe vé & chịu tải

| Mã | Chức năng | Mô tả | Ưu tiên |
|----|-----------|-------|:-------:|
| `ADM-09` | Cấu hình phòng chờ ảo | Thời điểm mở phòng chờ, tốc độ cho vào (người/phút), sức chứa tối đa của trang mua, thời hạn access token. | 🔴 Must |
| `ADM-10` | Cấu hình giới hạn mua | Số vé tối đa / tài khoản / số điện thoại / thẻ thanh toán cho từng sự kiện. | 🔴 Must |
| `ADM-11` | Cấu hình rate limit | Ngưỡng request theo IP, thiết bị, tài khoản cho từng nhóm API. | 🔴 Must |
| `ADM-12` | Quản lý blacklist / whitelist | Thêm, gỡ IP, dải IP, thiết bị, tài khoản; đặt thời hạn chặn. | 🟠 Should |
| `ADM-13` | Cấu hình bot detection | Bật/tắt CAPTCHA, ngưỡng risk score để yêu cầu CAPTCHA hoặc chặn. | 🔴 Must |

## D. Giám sát & xử lý gian lận

| Mã | Chức năng | Mô tả | Ưu tiên |
|----|-----------|-------|:-------:|
| `ADM-14` | Danh sách phiên nghi bot | Xem phiên bị gắn cờ, risk score, các tín hiệu dẫn đến gắn cờ. | 🔴 Must |
| `ADM-15` | Xử lý phiên / đơn gian lận | Xác nhận hoặc gỡ cờ; hủy đơn gian lận và trả ghế về kho. | 🟠 Should |
| `ADM-16` | Phát hiện cụm tài khoản | Nhóm các tài khoản dùng chung IP, thiết bị, thẻ, địa chỉ để phát hiện phe vé. | 🟢 Could |

## E. Thống kê & báo cáo

| Mã | Chức năng | Mô tả | Ưu tiên |
|----|-----------|-------|:-------:|
| `ADM-17` | Dashboard thời gian thực | Số người trong hàng đợi, request/giây, đơn hàng/phút, tỉ lệ lỗi. | 🔴 Must |
| `ADM-18` | Thống kê bán vé | Vé bán theo sự kiện, khu, hạng vé; tỉ lệ lấp đầy. | 🔴 Must |
| `ADM-19` | Thống kê chống bot | Số phiên bị chặn, tỉ lệ chặn đúng / chặn nhầm (dựa trên kết quả xác minh). | 🔴 Must |
| `ADM-20` | Báo cáo doanh thu | Doanh thu, hoàn tiền theo sự kiện / theo tháng; xuất Excel/PDF. | 🟠 Should |
| `ADM-21` | Audit log | Tra cứu nhật ký mọi thao tác quản trị: ai, làm gì, lúc nào, trên đối tượng nào. | 🟠 Should |

---

## Quy tắc nghiệp vụ liên quan

| Mã | Quy tắc |
|----|---------|
| `BR-10` | Không thay đổi cấu hình giới hạn mua của sự kiện khi đợt mở bán đang diễn ra. |
| `BR-11` | Thay đổi tốc độ cho vào của phòng chờ có hiệu lực ngay, không làm mất vị trí người đang chờ. |
| `BR-12` | Hủy đơn gian lận phải ghi lý do và hoàn tiền (giả lập) cho đơn đó. |

---

<div align="center">

[← 03. Đặc tả chức năng](README.md) · [🏠 Mục lục](../../README.md) · [3.2 ORGANIZER →](02-organizer.md)

</div>
