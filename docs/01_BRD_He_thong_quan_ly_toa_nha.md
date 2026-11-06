# BRD – Hệ thống quản lý nhà cho thuê (Rental Property Management System)

**Ngày:** 06/11/2026 · **Tác giả:** Nguyễn Huy Hoàng

**Dự án:** Rental Property Management System – công cụ quản lý phòng trọ và nhà cho thuê dành cho chủ nhà


## 1. TỔNG QUAN DỰ ÁN VÀ MỤC TIÊU KINH DOANH

### 1.1. Bối cảnh dự án

Chủ nhà cho thuê phòng trọ hoặc nhà nguyên căn, có thể quản lý một hoặc nhiều khu trọ tại các địa chỉ khác nhau. Nguồn thu chính là tiền thuê phòng, tiền điện, nước và phí dịch vụ khác (internet, gửi xe, rác...).

Khi quản lý bằng sổ sách và các file rời rạc, thường gặp các vấn đề quản trị:

**Ảo ảnh doanh thu:** ghi hoá đơn đủ nhưng tiền thu thực tế thấp, công nợ khó theo dõi và nợ quá hạn kéo dài, đặc biệt khi quản lý nhiều khu trọ cùng lúc.

**Dữ liệu phân mảnh:** thông tin người thuê, hợp đồng, chỉ số điện nước nằm ở nhiều sổ tay và file khác nhau, dễ sai lệch giữa các nguồn.

**Tính phí dễ sai:** ghi chỉ số điện nước bằng tay, tính nhẩm hoặc bấm máy tính, thường sai sót dẫn đến khiếu nại hoặc mất tiền.

**Bảo trì thiết bị không có lịch sử:** máy bơm nước, bình nóng lạnh, hệ thống điện hỏng đột xuất, chủ nhà không nhớ đã sửa lần nào, tốn bao nhiêu, có nên thay mới hay không.

### 1.2. Mục tiêu kinh doanh (Business Goals)

| Mã | Mục tiêu |
| --- | --- |
| G1 | Kiểm soát doanh thu thực thu và dòng tiền: chuyển từ theo dõi tổng hoá đơn sang theo dõi số tiền đã thu và công nợ theo từng phòng, từng khu trọ |
| G2 | Tính phí chính xác, minh bạch: loại bỏ tính tay và khiếu nại do sai phí điện nước |
| G3 | Quản lý phòng và người thuê tập trung: không còn dữ liệu rải rác ở sổ tay và nhiều file |
| G4 | Ghi nhận lịch sử sửa chữa thiết bị: biết thiết bị nào đã sửa bao nhiêu lần, tốn bao nhiêu tiền để quyết định thay mới hay tiếp tục sửa |

## 2. CÁC BÊN LIÊN QUAN VÀ CHÂN DUNG NGƯỜI DÙNG (STAKEHOLDERS)

| Vai trò | Đại diện | Nhu cầu kinh doanh cốt lõi | Điểm đau được giải quyết |
| --- | --- | --- | --- |
| Chủ nhà / Chủ trọ | Chủ sở hữu một hoặc nhiều khu trọ | Quản lý toàn bộ: phòng, người thuê, hợp đồng, tính phí, thu tiền, công nợ, sửa chữa | Dữ liệu phân mảnh ở nhiều sổ; tính phí sai; không biết ai còn nợ bao nhiêu |
| Nhân viên thu phí | Người được chủ nhà giao đi ghi chỉ số và thu tiền | Ghi chỉ số điện nước, ghi nhận thanh toán, xem danh sách phòng cần thu | Ghi sổ tay dễ mất; phải báo lại chủ nhà bằng tin nhắn |
| Đội phát triển / BA | Nguyễn Huy Hoàng | Mô hình dữ liệu, quy trình và quy tắc nghiệp vụ rõ ràng để làm SRS | Yêu cầu mơ hồ làm lệch phạm vi và phải làm lại |

> **Lưu ý:** Người thuê không phải là người dùng hệ thống. Thông tin người thuê chỉ được lưu dưới dạng dữ liệu để phục vụ quản lý hợp đồng và hoá đơn.

## 3. PHẠM VI DỰ ÁN (PROJECT SCOPE)

### 3.1. Trong phạm vi (In-Scope)

**Quản trị và làm sạch dữ liệu (Data Cleaning và Import):**

Nhập danh sách khu trọ, phòng, người thuê, chỉ số công tơ từ file Excel hoặc CSV.

Chuẩn hoá mã phòng, số điện thoại, ngày tháng, tiền tệ.

Tách rõ **Master Data** (khu trọ, phòng, người thuê, thiết bị, bảng giá) và **Transactional Data** (hợp đồng, chỉ số công tơ, hoá đơn, thanh toán, lịch sử sửa chữa).

**Động cơ nghiệp vụ:**

**Billing Engine:** tính phí theo bảng giá:
- **Tiền điện:** tính theo số thực tế tiêu thụ giữa 2 kỳ đo (chỉ số mới − chỉ số cũ) nhân với đơn giá cố định trên 1 số điện (ví dụ: 4.000 VNĐ/số).
- **Tiền nước:** hỗ trợ linh hoạt 3 hình thức tính (theo chỉ số đồng hồ thực tế, theo số người ở trong phòng, hoặc khoán cố định theo tháng cho phòng trọ / công ty thuê).
- **Tiền thuê phòng & phí dịch vụ khác:** tiền thuê cố định theo hợp đồng, phí dịch vụ (internet, rác, gửi xe...), tạo hoá đơn theo kỳ.

**Debt Engine:** theo dõi công nợ, phân khúc hành vi thanh toán, nhắc nợ.

**Phân quyền theo 2 vai trò** (Chủ nhà và Nhân viên thu phí), kèm nhật ký thao tác cơ bản.

### 3.2. Ngoài phạm vi (Out-of-Scope)

Cổng dành cho người thuê (người thuê không phải là user hệ thống).

Dashboard điều hành 90 giây (có thể bổ sung ở giai đoạn sau).

Quản lý sự cố và SLA.

Lịch bảo trì tự sinh công việc (chỉ ghi nhận lịch sử sửa chữa).

Thông báo cho người thuê.

Tích hợp thiết bị IoT thời gian thực (công tơ thông minh, camera).

Cổng thanh toán trực tuyến. Giai đoạn đầu ghi nhận thanh toán thủ công hoặc đối soát theo sao kê.

Kế toán đầy đủ (sổ cái, thuế). Hệ thống chỉ ghi nhận phải thu và đã thu.

Ứng dụng di động native. Giai đoạn đầu dùng web responsive.

## 4. QUY TRÌNH NGHIỆP VỤ: HIỆN TẠI (AS-IS) VÀ TƯƠNG LAI (TO-BE)

### 4.1. Chu kỳ thu phí hằng tháng

| Bước | As-Is (hiện tại) | To-Be (tương lai) |
| --- | --- | --- |
| 1. Ghi chỉ số | Chủ nhà đi ghi chỉ số điện nước từng phòng vào sổ tay | Nhập chỉ số vào hệ thống hoặc import theo lô; hệ thống validate tự động |
| 2. Tính phí | Tính tay bằng máy tính hoặc Excel: điện, nước, tiền thuê, dịch vụ | Hệ thống tự tính theo bảng giá có hiệu lực, gắn cờ bất thường |
| 3. Xuất hoá đơn | Viết tay hoặc in từ Excel, dễ sai sót | Tạo hoá đơn DRAFT, chủ nhà duyệt rồi phát hành |
| 4. Thu tiền | Thu tiền mặt hoặc chuyển khoản, ghi sổ tay | Ghi nhận thanh toán trên hệ thống, tự cập nhật công nợ |
| 5. Đối soát | Cuối tháng tổng hợp tay, dễ thiếu sót | Báo cáo tự động: thu phí, công nợ, phòng trống |

### 4.2. Quản lý phòng và hợp đồng

| Quy trình | As-Is (hiện tại) | To-Be (tương lai) |
| --- | --- | --- |
| Quản lý phòng | Nhớ trong đầu hoặc ghi sổ phòng nào trống, phòng nào có người | Danh sách phòng có trạng thái rõ ràng, lọc theo khu trọ |
| Hợp đồng | Bản giấy, dễ quên hạn, không biết khi nào hết hợp đồng | Hệ thống cảnh báo hợp đồng sắp hết hạn, ghi nhận tiền cọc |
| Sửa chữa | Gọi thợ, trả tiền, không ghi lại | Ghi nhận mỗi lần sửa: thiết bị nào, chi phí bao nhiêu, ai sửa |

## 5. YÊU CẦU NGHIỆP VỤ CHI TIẾT (BUSINESS REQUIREMENTS)

### 5.1. Nhóm BR-01: Chuẩn hoá và Quản trị Dữ liệu (Data Governance và Import)

**BR-01.1: Phân tách mô hình dữ liệu (Data Separation):**

**Dữ liệu danh mục (Master Data):** properties (khu trọ hoặc nhà cho thuê), rooms (phòng, mã duy nhất), tenants (người thuê), equipment (thiết bị), fee_rules (bảng giá có hiệu lực theo thời gian).

**Dữ liệu giao dịch (Transactional Data):** contracts (hợp đồng), meter_readings (chỉ số công tơ), invoices và invoice_items (hoá đơn), payments (thanh toán), repair_records (lịch sử sửa chữa).

**BR-01.2: Tiêu chuẩn hoá định dạng (Normalization):**

Ngày tháng quy về YYYY-MM-DD.

Tiền tệ chuyển các dạng như 1.250.000, 1,250,000, 1250k thành số nguyên VNĐ.

Mã phòng quy về dạng chữ hoa không dấu, ví dụ KT01-P03 (khu trọ 01, phòng 03) hoặc tuỳ quy ước của chủ nhà.

Số điện thoại quy về một định dạng thống nhất.

Trạng thái chuẩn: phòng VACANT, OCCUPIED, MAINTENANCE; hoá đơn DRAFT, ISSUED, PARTIAL, PAID, OVERDUE, CANCELLED.

**BR-01.3: Khoá toàn vẹn (Integrity Key):**

Không được trùng room_code, invoice_no. Bản ghi vi phạm phải bị gắn cờ chất lượng dữ liệu (*Data Quality Flag*).

**BR-01.4: Import có kiểm tra:**

Import từ Excel phải báo lỗi theo từng dòng (dòng nào, cột nào, lỗi gì). Không import một phần âm thầm.

### 5.2. Nhóm BR-02: Chỉ số Tài chính và Billing Engine

**BR-02.1: Công thức tính toán minh bạch:**

**Tiền điện (tính theo số điện tiêu thụ thực tế):**
- Quản lý theo mốc thời gian ghi nhận: Ngày đo tháng trước (chỉ số cũ) và ngày đo kỳ hiện tại (chỉ số mới).
- $\text{Số điện tiêu thụ} = \text{Chỉ số mới} - \text{Chỉ số cũ}$.
- $\text{Tiền điện} = \text{Số điện tiêu thụ} \times \text{Đơn giá 1 số điện}$.
- *Ví dụ thực tế:* Ngày chốt tháng trước chỉ số điện là 1.000, ngày đo hôm nay là 1.030 $\rightarrow$ Tiêu thụ = $1.030 - 1.000 = 30$ số. Với đơn giá 4.000 VNĐ/số thì tiền điện = $30 \times 4.000 = 120.000$ VNĐ.

**Tiền nước (hỗ trợ linh hoạt 3 hình thức tính tuỳ cấu hình từng phòng/hợp đồng):**
- **Hình thức 1 – Theo chỉ số đồng hồ nước:** $\text{Tiền nước} = (\text{Chỉ số mới} - \text{Chỉ số cũ}) \times \text{Đơn giá/khối}$ (tương tự cách tính tiền điện).
- **Hình thức 2 – Theo số lượng người ở (mô hình phòng trọ):** Áp dụng cho phòng có quản lý số người: $\text{Tiền nước} = \text{Số người trong phòng} \times \text{Đơn giá nước/người/tháng}$ (Ví dụ: Phòng trọ ở 3 người, đơn giá nước 100.000 VNĐ/người/tháng $\rightarrow$ Tiền nước = $3 \times 100.000 = 300.000$ VNĐ/tháng).
- **Hình thức 3 – Khoán cố định theo tháng (mô hình công ty/văn phòng thuê hoặc khoán gói):** Không cần đo chỉ số hay theo số người, áp dụng mức phí cố định thoả thuận trong hợp đồng (Ví dụ: Phòng cho công ty thuê văn phòng khoán cố định 500.000 VNĐ/tháng).

**Tiền thuê phòng:** số tiền cố định theo hợp đồng. Trường hợp vào/ra giữa tháng thì tính theo số ngày thực tế hoặc theo thoả thuận trong hợp đồng.

**Phí dịch vụ khác:** internet, gửi xe, rác, vệ sinh chung... theo bảng giá cấu hình (tính theo phòng, theo đầu xe hoặc theo đầu người).

$$\text{Tổng hoá đơn} = \text{Tiền thuê} + \text{Điện} + \text{Nước} + \text{Dịch vụ khác} - \text{Giảm trừ} + \text{Phạt chậm (nếu có)}$$

$$\text{Tỷ lệ thu phí} = \frac{\text{Số tiền đã thu}}{\text{Số tiền phải thu}} \times 100\%$$

$$\text{Tỷ lệ lấp đầy} = \frac{\text{Số phòng OCCUPIED}}{\text{Tổng số phòng khai thác}} \times 100\%$$

**BR-02.2: Quy trình tạo hoá đơn (Billing Pipeline):**

Đọc chỉ số công tơ hợp lệ của kỳ (chỉ số cuối kỳ không nhỏ hơn đầu kỳ).

Tính từng khoản theo bảng giá có hiệu lực tại kỳ tính phí, cộng tiền thuê phòng.

Áp dụng giảm trừ và phạt chậm của kỳ trước (nếu có).

Kiểm tra bất thường: gắn cờ phòng có mức tiêu thụ tăng đột biến so với các kỳ gần nhất để kiểm tra rò rỉ hoặc ghi sai chỉ số.

Tạo hoá đơn DRAFT chờ chủ nhà duyệt và phát hành.

### 5.3. Nhóm BR-03: Người thuê, Hợp đồng và Công nợ (Debt Engine)

**BR-03.1: Thông tin người thuê:**

Người thuê là dữ liệu quản lý, không phải người dùng hệ thống. Lưu họ tên, số điện thoại, CCCD và thông tin liên hệ cần thiết.

**BR-03.2: Vòng đời hợp đồng:**

Trạng thái: DRAFT → ACTIVE → EXPIRING (sắp hết hạn) → EXPIRED hoặc TERMINATED.

Hệ thống cảnh báo chủ nhà khi hợp đồng chuyển sang EXPIRING.

**BR-03.3: Quản lý số người trong phòng & hợp đồng:**
- Hệ thống hỗ trợ 2 dạng quản lý phòng tuỳ theo nhu cầu thực tế:
  - **Có quản lý số người (mô hình phòng trọ):** Quản lý số lượng người ở thực tế trong phòng. Số người này được dùng làm căn cứ tính tiền nước theo đầu người (BR-02.1) và quản lý người ở thực tế.
  - **Không quản lý số người (mô hình công ty/văn phòng thuê hoặc khoán trọn gói):** Không cần đếm số người; tiền nước và các khoản phí dịch vụ được tính khoán theo mức cố định hàng tháng thoả thuận trong hợp đồng.
- **Ràng buộc:** Mỗi phòng chỉ có một hợp đồng ACTIVE tại một thời điểm; hợp đồng gắn với người thuê chính (hoặc đại diện công ty), danh sách người ở cùng (nếu có) và số người đăng ký lưu trú.

**BR-03.4: Tiền cọc:** hợp đồng ghi nhận số tiền đặt cọc. Khi kết thúc hợp đồng, tiền cọc được đối trừ công nợ còn lại hoặc hoàn trả theo thoả thuận.

**BR-03.5: Phân khúc hành vi thanh toán** dựa trên lịch sử thanh toán các kỳ hoá đơn. Ngưỡng cụ thể của từng phân khúc do chủ nhà cấu hình:

| Phân khúc | Đặc điểm | Hành động đề xuất |
| --- | --- | --- |
| Đúng hạn | Luôn thanh toán trước hạn | Không cần nhắc |
| Trễ thỉnh thoảng | Thỉnh thoảng trễ hạn, mỗi lần trễ ngắn | Nhắc trước hạn |
| Trễ thường xuyên | Thường xuyên thanh toán trễ hạn | Liên hệ trực tiếp |
| Nợ kéo dài | Còn nợ qua nhiều kỳ | Cảnh báo chủ nhà, tính phạt theo hợp đồng |
| Người thuê mới | Chưa có đủ lịch sử thanh toán | Theo dõi |

### 5.4. Nhóm BR-04: Thiết bị và Lịch sử Sửa chữa

**BR-04.1: Danh mục thiết bị:** mỗi thiết bị (máy bơm nước, bình nóng lạnh, hệ thống điện, đường ống nước, bồn chứa nước, cửa cuốn) gắn với khu trọ và vị trí (khu chung hoặc phòng cụ thể).

**BR-04.2: Ghi nhận lịch sử sửa chữa:** mỗi lần sửa chữa ghi nhận thiết bị, người thực hiện (thợ nào), nội dung sửa, chi phí và ngày sửa.

**BR-04.3: Thiết bị hỏng lặp lại:** thiết bị có nhiều lần sửa chữa được hiển thị kèm tổng chi phí luỹ kế để chủ nhà so sánh với chi phí thay mới.

### 5.5. Nhóm BR-05: Phân quyền và Nhật ký (Access Control và Audit)

**BR-05.1: Phân quyền theo 2 vai trò:**

**Chủ nhà (Owner):** toàn quyền quản lý tất cả khu trọ của mình – phòng, người thuê, hợp đồng, bảng giá, hoá đơn, thanh toán, công nợ, thiết bị, báo cáo, quản lý tài khoản nhân viên.

**Nhân viên thu phí (Staff):** chỉ thao tác trên các khu trọ được chủ nhà giao – ghi chỉ số công tơ, ghi nhận thanh toán, xem danh sách phòng và hoá đơn. Không được sửa bảng giá, xoá hoá đơn hay thay đổi hợp đồng.

**BR-05.2: Phân quyền theo phạm vi khu trọ:** nhân viên chỉ truy cập dữ liệu của các khu trọ được chủ nhà giao.

**BR-05.3: Nhật ký (audit log)** cho các thao tác quan trọng: sửa hoá đơn, đổi trạng thái hợp đồng, đổi bảng giá; mỗi bản ghi có người thực hiện, thời điểm, giá trị trước và sau.

## 6. QUY TẮC NGHIỆP VỤ (BUSINESS RULES)

**BR-RULE-01 (Doanh thu thực thu):** chỉ số tiền đã ghi nhận của hoá đơn PAID hoặc PARTIAL mới tính vào doanh thu thực thu; hoá đơn DRAFT và CANCELLED không tính.

**BR-RULE-02 (Một hợp đồng hiệu lực):** mỗi phòng chỉ có một hợp đồng ACTIVE tại một thời điểm.

**BR-RULE-03 (Chỉ số công tơ và ngày đo):** chỉ số kỳ sau không nhỏ hơn kỳ trước (ngoại lệ khi thay công tơ phải có ghi chú và chỉ số chốt của công tơ cũ). Mỗi lần chốt chỉ số điện/nước phải lưu ngày đo cụ thể để xác định chính xác số tiêu thụ giữa 2 kỳ đo liên tiếp.

**BR-RULE-04 (Bất biến hoá đơn):** hoá đơn đã phát hành không được xoá; chỉ điều chỉnh bằng bút toán điều chỉnh có lý do và người duyệt.

**BR-RULE-05 (Bảng giá theo hiệu lực):** hoá đơn dùng bảng giá có hiệu lực tại kỳ tính phí, không dùng bảng giá mới cho kỳ cũ.

**BR-RULE-06 (Phạt chậm):** chỉ tính sau ngày quá hạn, theo tỷ lệ cấu hình trong hợp đồng và không vượt mức pháp luật cho phép.

**BR-RULE-07 (Tiền cọc):** tiền cọc được ghi nhận khi tạo hợp đồng. Khi kết thúc hợp đồng, tiền cọc được đối trừ công nợ còn lại hoặc hoàn trả; mọi thao tác liên quan đến cọc phải có nhật ký.

**BR-RULE-08 (Phạm vi dữ liệu):** chủ nhà chỉ thấy dữ liệu khu trọ của mình; nhân viên chỉ truy cập khu trọ được giao.

## 7. YÊU CẦU PHI CHỨC NĂNG (NON-FUNCTIONAL REQUIREMENTS)

**NFR-01 (Dễ dùng):** giao diện tiếng Việt, dùng tốt trên điện thoại; chủ nhà và nhân viên thao tác nhanh, ít bước. Ưu tiên trải nghiệm trên mobile vì chủ nhà thường ghi chỉ số tại khu trọ.

**NFR-02 (Bảo mật):** mật khẩu được băm, phiên đăng nhập có thời hạn, truyền dữ liệu qua HTTPS; dữ liệu cá nhân người thuê được bảo vệ theo quy định pháp luật Việt Nam hiện hành về dữ liệu cá nhân.

**NFR-03 (Toàn vẹn và sao lưu):** sao lưu dữ liệu định kỳ; nhật ký thao tác không cho sửa hoặc xoá.

**NFR-04 (Mở rộng):** thêm khu trọ mới bằng cấu hình và nhập dữ liệu, không phải sửa mã nguồn.

## 8. TIÊU CHÍ NGHIỆM THU NGHIỆP VỤ (BUSINESS ACCEPTANCE CRITERIA)

Dự án được coi là hoàn thành giai đoạn yêu cầu nghiệp vụ khi thoả mãn các tiêu chí sau:

**AC-1:** import thành công danh sách phòng và người thuê từ file Excel mẫu; mã phòng, ngày, tiền tệ đúng chuẩn; dòng lỗi được báo rõ vị trí.

**AC-2:** chạy trọn một chu kỳ thu phí (ghi chỉ số, tạo hoá đơn, duyệt, phát hành, ghi nhận thanh toán, báo cáo công nợ) trên dữ liệu mẫu, kết quả khớp phép tính tay.

**AC-3:** hợp đồng đi hết vòng đời (tạo, kích hoạt, cảnh báo sắp hết hạn, hết hạn), tiền cọc được ghi nhận và đối trừ đúng.

**AC-4:** ghi nhận lịch sử sửa chữa thiết bị, hiển thị chi phí luỹ kế theo thiết bị.

**AC-5:** phân quyền đúng: chủ nhà thấy tất cả khu trọ của mình; nhân viên chỉ thấy khu trọ được giao và chỉ thao tác trong phạm vi cho phép.

*Tài liệu này là căn cứ để xây dựng Tài liệu Đặc tả Yêu cầu Phần mềm (SRS) và thiết kế kỹ thuật ở bước tiếp theo.*
