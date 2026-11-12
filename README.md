# 🏠 Rental Property Management System

Công cụ quản lý phòng trọ và nhà cho thuê – hỗ trợ chủ nhà quản lý tập trung nhiều khu trọ, tính phí dịch vụ, tạo hoá đơn và theo dõi công nợ trên nền tảng web.

## Giới thiệu

Hệ thống giúp chủ nhà và người quản lý số hoá toàn bộ quy trình vận hành phòng trọ / nhà cho thuê, giải quyết việc ghi chép sổ sách và tính toán thủ công:

- **Quản lý khu trọ & phòng:** quản lý danh sách phòng, trạng thái phòng (trống, đang thuê, bảo trì). Hỗ trợ cả 2 dạng: quản lý theo số người ở hoặc không quản lý số người (phòng cho công ty thuê/khoán trọn gói).
- **Hợp đồng & tiền cọc:** theo dõi vòng đời hợp đồng, thông tin người thuê, ghi nhận đặt cọc và đối trừ khi thanh lý.
- **Tính tiền điện theo số thực tế:** ghi nhận ngày đo và chỉ số cũ/mới (Ví dụ: 1.000 $\rightarrow$ 1.030 = 30 số $\times$ 4.000 VNĐ/số).
- **Tính tiền nước linh hoạt theo 3 hình thức:**
  - Theo chỉ số đồng hồ nước thực tế.
  - Theo số người ở trong phòng (mô hình phòng trọ: số người $\times$ đơn giá/người).
  - Khoán cố định theo tháng (mô hình công ty/văn phòng thuê).
- **Hoá đơn & Công nợ:** tạo hoá đơn tự động theo kỳ, ghi nhận thanh toán, theo dõi công nợ theo từng phòng.
- **Lịch sử sửa chữa thiết bị:** theo dõi lịch sử và chi phí sửa chữa máy bơm, bình nóng lạnh, hệ thống điện...
- **Phân quyền 2 vai trò:** Chủ nhà (Owner - toàn quyền) và Nhân viên thu phí (Staff - chỉ ghi chỉ số, thu tiền theo khu trọ được giao).

## Tài liệu dự án

| Tài liệu | Mô tả |
|-----------|-------|
| [BRD](docs/01_BRD_He_thong_quan_ly_toa_nha.md) | Yêu cầu nghiệp vụ (Business Requirements Document) |
| [SRS](docs/02_SRS_He_thong_quan_ly_toa_nha.md) | Đặc tả yêu cầu phần mềm (Software Requirements Specification - Phiên bản 2.0) |
| [Detailed Design](docs/03_Detailed_Design_He_thong_quan_ly_nha_cho_thue.md) | Tài liệu thiết kế chi tiết hệ thống Microservices (Angular + Python FastAPI) |
| [Prototype Screens](docs/stitch_screens/index.html) | Bộ mã HTML & ảnh giao diện tương tác từ Google Stitch |

## Tác giả

**Nguyễn Huy Hoàng**
