[🏠 Trang chủ](../../README.md) › [03. Đặc tả chức năng](README.md) › **3.2 Ban tổ chức (ORGANIZER)**

# 3.2 Ban tổ chức sự kiện (ORGANIZER)

> Đơn vị tổ chức concert: tạo sự kiện, thiết lập vé và đợt mở bán, theo dõi đơn hàng và kết quả bán vé của sự kiện mình.

**Nội dung:** [A. Sự kiện](#a-quản-lý-sự-kiện) · [B. Vé & ghế](#b-quản-lý-vé--ghế) · [C. Đơn hàng](#c-quản-lý-đơn-hàng) · [D. Nhân viên soát vé](#d-quản-lý-nhân-viên-soát-vé) · [E. Báo cáo sự kiện](#e-báo-cáo-sự-kiện)

---

## A. Quản lý sự kiện

| Mã | Chức năng | Mô tả | Ưu tiên |
|----|-----------|-------|:-------:|
| `ORG-01` | Tạo / sửa / hủy sự kiện | Tên, nghệ sĩ, thời gian, địa điểm, mô tả, poster; hủy sự kiện kèm hoàn tiền hàng loạt. | 🔴 Must |
| `ORG-02` | Thiết lập hạng vé & giá | Chọn sơ đồ địa điểm, gán hạng vé (VVIP, VIP, GA…) và giá cho từng khu. | 🔴 Must |
| `ORG-03` | Thiết lập đợt mở bán | Tạo đợt presale, mở bán chung; thời gian bắt đầu/kết thúc, số lượng vé mỗi đợt. | 🔴 Must |
| `ORG-04` | Giữ ghế dành riêng | Đánh dấu ghế khách mời, tài trợ, báo chí; không mở bán. | 🟠 Should |

## B. Quản lý vé & ghế

| Mã | Chức năng | Mô tả | Ưu tiên |
|----|-----------|-------|:-------:|
| `ORG-05` | Theo dõi ghế thời gian thực | Sơ đồ ghế với trạng thái trống / đang giữ / đã bán, cập nhật qua WebSocket. | 🔴 Must |
| `ORG-06` | Khóa / mở ghế thủ công | Khóa ghế hỏng, ghế bị che tầm nhìn; mở lại khi cần. | 🟠 Should |
| `ORG-07` | Mã ưu đãi & mã presale | Phát hành mã giảm giá, mã presale cho fan club (giới hạn lượt dùng, thời hạn). | 🟢 Could |

## C. Quản lý đơn hàng

| Mã | Chức năng | Mô tả | Ưu tiên |
|----|-----------|-------|:-------:|
| `ORG-08` | Danh sách đơn hàng | Tra cứu theo mã đơn, email, số điện thoại; lọc theo trạng thái. | 🔴 Must |
| `ORG-09` | Xử lý hoàn / đổi vé | Duyệt hoặc từ chối yêu cầu hoàn vé theo chính sách sự kiện. | 🟠 Should |
| `ORG-10` | Xuất danh sách khán giả | Xuất Excel/CSV danh sách vé đã bán. | 🟢 Could |

## D. Quản lý nhân viên soát vé

| Mã | Chức năng | Mô tả | Ưu tiên |
|----|-----------|-------|:-------:|
| `ORG-11` | Tạo tài khoản soát vé | Tạo tài khoản STAFF cho sự kiện, có hiệu lực trong khung giờ sự kiện. | 🔴 Must |
| `ORG-12` | Phân cổng | Gán nhân viên vào cổng (gate) và các khu tương ứng. | 🟠 Should |

## E. Báo cáo sự kiện

| Mã | Chức năng | Mô tả | Ưu tiên |
|----|-----------|-------|:-------:|
| `ORG-13` | Báo cáo bán vé | Doanh thu, số vé bán theo đợt / khu / hạng vé. | 🔴 Must |
| `ORG-14` | Báo cáo hàng đợi | Thời gian chờ trung bình, số người vào phòng chờ, tỉ lệ bỏ hàng đợi. | 🟠 Should |
| `ORG-15` | Báo cáo check-in | Số vé check-in theo cổng, theo khung giờ; vé chưa sử dụng. | 🟠 Should |

---

## Quy tắc nghiệp vụ liên quan

| Mã | Quy tắc |
|----|---------|
| `BR-20` | Không sửa giá, sơ đồ ghế của sự kiện sau khi đã có vé bán ra. |
| `BR-21` | Tổng số vé các đợt mở bán không vượt quá số ghế khả dụng. |
| `BR-22` | Hủy sự kiện kéo theo hủy toàn bộ vé và hoàn tiền (giả lập) cho mọi đơn hàng. |

---

<div align="center">

[← 3.1 ADMIN](01-admin.md) · [🏠 Mục lục](../../README.md) · [3.3 STAFF →](03-checkin-staff.md)

</div>
