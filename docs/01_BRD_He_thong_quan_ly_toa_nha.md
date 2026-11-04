# BRD – Hệ thống quản lý toà nhà (Building Management System)

**Ngày:** 03/11/2026 · **Tác giả:** Nguyễn Huy Hoàng

**Dự án:** Smart Building Management System – hệ thống quản lý vận hành toà nhà


## 1. TỔNG QUAN DỰ ÁN VÀ MỤC TIÊU KINH DOANH

### 1.1. Bối cảnh dự án

Ban quản lý toà nhà vận hành theo mô hình quản lý tập trung nhiều toà, nguồn thu chính là phí dịch vụ, tiền thuê và phí gửi xe.

Khi quản lý bằng sổ sách và các file rời rạc, thường gặp các vấn đề quản trị:

**Ảo ảnh doanh thu:** hoá đơn xuất đủ nhưng tiền thu thực tế thấp, công nợ khó theo dõi và nợ quá hạn kéo dài.

**Dữ liệu phân mảnh:** thông tin cư dân, hợp đồng, chỉ số công tơ nằm ở nhiều file, số của kế toán và ban quản lý lệch nhau.

**Sự cố xử lý theo trí nhớ:** báo qua điện thoại hoặc Zalo, không rõ ai chịu trách nhiệm, không có lịch sử để rút kinh nghiệm.

**Bảo trì thiết bị không có lịch:** thang máy, PCCC, máy bơm bị bỏ lỡ hạn bảo trì và kiểm định.

**Cư dân thiếu kênh minh bạch:** không biết phí được tính thế nào, không biết sự cố của mình đang ở đâu.

### 1.2. Mục tiêu kinh doanh (Business Goals – SMART)

| Mã | Mục tiêu |
| --- | --- |
| G1 | Kiểm soát doanh thu thực thu và dòng tiền: chuyển từ theo dõi tổng hoá đơn sang theo dõi số tiền đã thu và công nợ |
| G2 | Tính phí chính xác, minh bạch: loại bỏ tính tay và khiếu nại do sai phí |
| G3 | Rút ngắn thời gian xử lý sự cố bằng quy trình có người chịu trách nhiệm và SLA |
| G4 | Bảo trì chủ động, giảm hỏng đột xuất |
| G5 | Ra quyết định điều hành trong 90 giây, không cần mở Excel: dashboard trả lời 3 câu hỏi (thu phí, công nợ, sự cố) ngay ở màn hình chính |

## 2. CÁC BÊN LIÊN QUAN VÀ CHÂN DUNG NGƯỜI DÙNG (STAKEHOLDERS)

| Vai trò | Đại diện | Nhu cầu kinh doanh cốt lõi | Điểm đau được giải quyết |
| --- | --- | --- | --- |
| Executive / Chủ đầu tư | Giám đốc vận hành, ban giám đốc | Xem trong 90 giây: tỷ lệ thu phí, công nợ, sự cố đang mở, tỷ lệ lấp đầy để ra quyết định đầu tư và nhân sự | Hết cảnh "xuất hoá đơn đủ nhưng thu thiếu"; báo cáo không còn làm tay từ nhiều file |
| Ban quản lý (Admin) | Trưởng ban, phó ban | Điều hành tập trung nhiều toà, giao việc, duyệt hoá đơn, theo dõi tiến độ | Dữ liệu rời rạc, không biết ai đang xử lý việc gì |
| Kế toán / Thu phí | Nhân viên kế toán | Tính phí tự động theo bảng giá, ghi nhận thanh toán, đối soát, nhắc nợ | Tính tay dễ sai; công nợ thiếu minh bạch, khó đối soát |
| Kỹ thuật và Vận hành | Kỹ thuật điện nước, thang máy, bảo vệ, vệ sinh | Nhận việc rõ ràng, xem lịch bảo trì và lịch sử thiết bị, cập nhật trạng thái nhanh | Bỏ sót sự cố; bảo trì theo trí nhớ; không có lịch sử sửa chữa |
| Cư dân / Khách thuê | Chủ hộ, người thuê | Xem hoá đơn, báo sự cố, theo dõi tiến độ xử lý, nhận thông báo | Không rõ cách tính phí; báo sự cố xong không ai phản hồi |
| Đội phát triển / BA | Nguyễn Huy Hoàng | Mô hình dữ liệu, quy trình và quy tắc nghiệp vụ rõ ràng để làm SRS | Yêu cầu mơ hồ làm lệch phạm vi và phải làm lại |

## 3. PHẠM VI DỰ ÁN (PROJECT SCOPE)

### 3.1. Trong phạm vi (In-Scope)

**Quản trị và làm sạch dữ liệu (Data Cleaning và Import):**

Nhập danh sách toà, căn hộ, cư dân, chỉ số công tơ từ file Excel hoặc CSV.

Chuẩn hoá mã căn, số điện thoại, ngày tháng, tiền tệ.

Tách rõ **Master Data** (toà, căn, cư dân, thiết bị, bảng giá) và **Transactional Data** (hợp đồng, chỉ số công tơ, hoá đơn, thanh toán, sự cố, công việc bảo trì).

**Động cơ nghiệp vụ:**

**Billing Engine:** tính phí theo bảng giá và bậc thang, tạo hoá đơn theo kỳ.

**Debt Engine:** theo dõi công nợ, tính phạt chậm, phân khúc hành vi thanh toán, nhắc nợ.

**SLA Engine:** phân loại ưu tiên sự cố, đo thời hạn tiếp nhận và xử lý, cảnh báo quá hạn.

**Maintenance Scheduler:** sinh công việc bảo trì định kỳ và nhắc hạn kiểm định.

**Giao diện web theo 3 tầng:**

Tầng 1: Executive 90-Second Cockpit (tỷ lệ thu phí, công nợ quá hạn, sự cố mở, tỷ lệ lấp đầy).

Tầng 2: Vận hành (căn hộ, cư dân, hợp đồng, hoá đơn, sự cố, bảo trì).

Tầng 3: Cổng cư dân (xem hoá đơn, báo sự cố, nhận thông báo).

**Phân quyền theo vai trò và theo toà, kèm nhật ký thao tác (audit log).**

### 3.2. Ngoài phạm vi (Out-of-Scope)

Tích hợp thiết bị IoT thời gian thực (công tơ thông minh, camera, kiểm soát ra vào). Giai đoạn này chỉ nhập chỉ số thủ công hoặc theo lô.

Cổng thanh toán trực tuyến. Giai đoạn đầu ghi nhận thanh toán thủ công hoặc đối soát theo sao kê.

Kế toán đầy đủ (sổ cái, thuế). Hệ thống chỉ ghi nhận phải thu và đã thu.

Ứng dụng di động native. Giai đoạn đầu dùng web responsive.

Đặt tiện ích chung và marketplace nội khu.

Thuật toán AI phức tạp (nhận diện hình ảnh, dự đoán hỏng hóc). Có thể làm ở giai đoạn sau.

## 4. QUY TRÌNH NGHIỆP VỤ: HIỆN TẠI (AS-IS) VÀ TƯƠNG LAI (TO-BE)

### 4.1. Chu kỳ thu phí hằng tháng

chu kỳ thu phí · 5 bước thủ công so với 5 bước tự động

Mỗi bước thủ công ở cột trái có một bước tương ứng do hệ thống đảm nhiệm ở cột phải; kế toán chỉ còn việc duyệt hoá đơn trước khi phát hành.

### 4.2. Sự cố, bảo trì, báo cáo và thông báo

| Quy trình | As-Is (hiện tại) | To-Be (tương lai) |
| --- | --- | --- |
| Báo và xử lý sự cố | Cư dân gọi điện hoặc nhắn Zalo; nhân viên nhớ và tự đi xử lý; không có lịch sử | Cư dân gửi yêu cầu trên hệ thống; tự phân loại ưu tiên và giao việc; theo dõi theo SLA; cư dân đánh giá khi xong |
| Bảo trì thiết bị | Theo trí nhớ hoặc sổ tay; dễ lỡ hạn kiểm định | Lịch định kỳ tự sinh việc và nhắc trước hạn; lịch sử và chi phí lưu theo từng thiết bị |
| Báo cáo điều hành | Tổng hợp tay từ nhiều file Excel, mất nhiều giờ | Dashboard 90 giây, xuất Excel hoặc PDF khi cần |
| Thông báo cho cư dân | Dán bảng tin, nhắn nhóm chat rời rạc | Thông báo theo toà, tầng hoặc cá nhân, có trạng thái đã đọc |

## 5. YÊU CẦU NGHIỆP VỤ CHI TIẾT (BUSINESS REQUIREMENTS)

### 5.1. Nhóm BR-01: Chuẩn hoá và Quản trị Dữ liệu (Data Governance và Import)

**BR-01.1: Phân tách mô hình dữ liệu (Data Separation):**

**Dữ liệu danh mục (Master Data):** buildings (toà), units (căn hoặc phòng, mã duy nhất), residents (cư dân), equipment (thiết bị), fee_rules (bảng giá có hiệu lực theo thời gian).

**Dữ liệu giao dịch (Transactional Data):** contracts, meter_readings (chỉ số công tơ), invoices và invoice_items, payments, tickets (sự cố), maintenance_tasks.

**BR-01.2: Tiêu chuẩn hoá định dạng (Normalization):**

Ngày tháng quy về YYYY-MM-DD.

Tiền tệ chuyển các dạng như 1.250.000, 1,250,000, 1250k thành số nguyên VNĐ.

Mã căn quy về dạng chữ hoa không dấu, ví dụ A1-1205 (toà A1, tầng 12, căn 05).

Số điện thoại quy về một định dạng thống nhất.

Trạng thái chuẩn: căn hộ VACANT, OCCUPIED, MAINTENANCE; hoá đơn DRAFT, ISSUED, PARTIAL, PAID, OVERDUE, CANCELLED; sự cố NEW, ACCEPTED, IN_PROGRESS, RESOLVED, CLOSED.

**BR-01.3: Khoá toàn vẹn (Integrity Key):**

Không được trùng unit_code, invoice_no, ticket_no. Bản ghi vi phạm phải bị gắn cờ chất lượng dữ liệu (*Data Quality Flag*).

**BR-01.4: Import có kiểm tra:**

Import từ Excel phải báo lỗi theo từng dòng (dòng nào, cột nào, lỗi gì). Không import một phần âm thầm.

### 5.2. Nhóm BR-02: Chỉ số Tài chính, Vận hành và Billing Engine

**BR-02.1: Công thức tính toán minh bạch:**

**Tiền điện, nước bậc thang:** tiêu thụ trong kỳ = chỉ số cuối kỳ − chỉ số đầu kỳ; mỗi bậc nhân với đơn giá của bậc đó rồi cộng lại.

**Phí quản lý:** đơn giá trên mỗi m² nhân diện tích căn.

**Phí gửi xe:** theo loại phương tiện đã đăng ký.

\text{Tổng hoá đơn} = \text{Phí quản lý} + \text{Điện} + \text{Nước} + \text{Gửi xe} + \text{Phí khác} - \text{Giảm trừ} + \text{Phạt chậm}

\text{Tỷ lệ thu phí} = \frac{\text{Số tiền đã thu}}{\text{Số tiền phải thu}} \times 100\%

\text{Tỷ lệ lấp đầy} = \frac{\text{Số căn OCCUPIED}}{\text{Tổng số căn khai thác}} \times 100\%

\text{Thời gian xử lý trung bình} = \frac{\sum (\text{Thời điểm RESOLVED} - \text{Thời điểm NEW})}{\text{Số sự cố đã xử lý}}

**BR-02.2: Quy trình tạo hoá đơn 5 bước (Billing Pipeline):**

Đọc chỉ số công tơ hợp lệ của kỳ (chỉ số cuối kỳ không nhỏ hơn đầu kỳ).

Tính từng khoản theo bảng giá có hiệu lực tại kỳ tính phí.

Áp dụng giảm trừ và phạt chậm của kỳ trước (nếu có).

Kiểm tra bất thường: gắn cờ căn có mức tiêu thụ tăng đột biến so với các kỳ gần nhất để kiểm tra rò rỉ hoặc ghi sai chỉ số.

Tạo hoá đơn DRAFT chờ kế toán duyệt và phát hành.

**BR-02.3: Nguyên tắc thiết kế 90 giây của Ban điều hành:**

Góc trên bên trái màn hình chính phải có 3 thẻ KPI:

**Tỷ lệ thu phí kỳ hiện tại**.

**Công nợ quá hạn** (tổng tiền và số căn).

**Sự cố đang mở** (kèm số sự cố vượt SLA).

Màn hình chính không quá 4 biểu đồ để tránh quá tải nhận thức (*Cognitive Load*): lấp đầy theo toà, thu phí theo tháng, sự cố theo loại, thiết bị sắp đến hạn bảo trì.

### 5.3. Nhóm BR-03: Cư dân, Hợp đồng và Phân khúc Hành vi Thanh toán (Debt Engine)

**BR-03.1: Vòng đời hợp đồng:**

Trạng thái: DRAFT → ACTIVE → EXPIRING (sắp hết hạn) → EXPIRED hoặc TERMINATED.

Hệ thống cảnh báo Ban quản lý khi hợp đồng chuyển sang EXPIRING.

**BR-03.2: Một căn, một hợp đồng hiệu lực** tại một thời điểm; hợp đồng gắn với cư dân chính, thành viên đi cùng và phương tiện đăng ký.

**BR-03.3: Phân khúc hành vi thanh toán** dựa trên lịch sử thanh toán các kỳ hoá đơn. Ngưỡng cụ thể của từng phân khúc do Ban quản lý cấu hình:

| Phân khúc | Đặc điểm | Hành vi thực tế | Hành động đề xuất |
| --- | --- | --- | --- |
| Đúng hạn | Luôn thanh toán trước hạn | Cư dân ổn định, ít cần nhắc | Chỉ gửi thông báo hoá đơn; không nhắc nợ để tránh phiền |
| Trễ thỉnh thoảng | Thỉnh thoảng trễ hạn, mỗi lần trễ ngắn | Thường quên hạn | Nhắc trước hạn qua thông báo |
| Trễ thường xuyên | Thường xuyên thanh toán trễ hạn | Chưa có thói quen thanh toán đúng hạn | Liên hệ trực tiếp, đề xuất thanh toán định kỳ |
| Nợ kéo dài | Còn nợ qua nhiều kỳ | Rủi ro mất doanh thu | Gửi thông báo chính thức, tính phạt theo hợp đồng, cảnh báo trước khi áp dụng biện pháp theo hợp đồng |
| Người thuê mới | Chưa có đủ lịch sử thanh toán | Chưa quen cách tính phí và kênh thanh toán | Gửi hướng dẫn cách tính phí, kênh thanh toán, kênh báo sự cố |

### 5.4. Nhóm BR-04: Sự cố và SLA Engine

**BR-04.1: Tiếp nhận và phân loại:**

Cư dân gửi yêu cầu kèm mô tả, hình ảnh và nhóm sự cố (điện, nước, thang máy, vệ sinh, an ninh, khác). Lễ tân hoặc bảo vệ có thể nhập hộ qua điện thoại.

**BR-04.2: Ma trận ưu tiên và SLA** (thời hạn tiếp nhận và xử lý do Ban quản lý cấu hình):

| Mức ưu tiên | Ví dụ |
| --- | --- |
| Khẩn cấp | Cháy, thang máy kẹt người, vỡ ống chính |
| Cao | Mất điện hoặc nước cả tầng, rò rỉ nước |
| Trung bình | Hỏng đèn hành lang, điều hoà khu chung |
| Thấp | Hỏi thông tin, góp ý |

**BR-04.3: Vòng đời và đánh giá:**

NEW → ACCEPTED → IN_PROGRESS → RESOLVED → CLOSED; cư dân theo dõi được từng bước.

Sau RESOLVED, cư dân xác nhận và chấm điểm 1 đến 5.

**BR-04.4: Cảnh báo vi phạm SLA:** sự cố quá hạn tiếp nhận hoặc xử lý được leo thang lên Trưởng ban và hiển thị đỏ trên dashboard.

### 5.5. Nhóm BR-05: Thiết bị và Bảo trì (Maintenance Scheduler)

**BR-05.1: Danh mục thiết bị:** mỗi thiết bị (thang máy, PCCC, máy bơm, điều hoà trung tâm, máy phát điện) gắn với toà, vị trí, nhà cung cấp và ngày đưa vào sử dụng.

**BR-05.2: Lịch bảo trì định kỳ:** khai báo chu kỳ theo ngày hoặc tháng; hệ thống tự sinh công việc trước hạn và nhắc người phụ trách.

**BR-05.3: Lịch sử và chi phí:** mỗi lần bảo trì hoặc sửa chữa ghi nhận người thực hiện, nội dung, chi phí và biên bản đính kèm; sau khi hoàn thành, hệ thống tính ngày bảo trì kế tiếp.

**BR-05.4: Bài toán cụ thể, thiết bị hỏng lặp lại:** thiết bị có nhiều sự cố lặp lại trong thời gian ngắn bị gắn cờ "cân nhắc thay thế" trên dashboard, kèm tổng chi phí sửa chữa luỹ kế để Ban quản lý so sánh với chi phí thay mới.

### 5.6. Nhóm BR-06: Thông báo, Kể chuyện bằng Dữ liệu và Tiêu chuẩn Trình bày (CCR)

**BR-06.1: Thông báo:**

Thông báo chung (toàn toà, theo tầng, theo nhóm) và thông báo cá nhân (hoá đơn, trạng thái sự cố, nhắc hạn).

Lưu lịch sử gửi và trạng thái đã đọc.

**BR-06.2: Ứng dụng công thức CCR (Context – Complication – Resolution):** mọi biểu đồ quan trọng phải có chú giải gồm 3 phần:

**Bối cảnh (Context):** tình hình thực tế.

**Xung đột (Complication):** điểm nghẽn trong dữ liệu.

**Hành động giải quyết (Resolution):** khuyến nghị.

**BR-06.3: Tiêu chuẩn kiểm thử im lặng (Blind Test Ready):** người dùng lần đầu nhìn dashboard, không cần người hướng dẫn, phải hiểu được thông điệp chính.

### 5.7. Nhóm BR-07: Phân quyền và Nhật ký (Access Control và Audit)

**BR-07.1: Phân quyền theo vai trò (RBAC):** Admin, Manager, Accountant, Technician, Resident; mỗi vai trò chỉ thấy và làm những thao tác được phép.

**BR-07.2: Phân quyền theo phạm vi toà:** người dùng chỉ truy cập dữ liệu của các toà được giao; cư dân chỉ thấy hoá đơn và sự cố của căn mình.

**BR-07.3: Nhật ký (audit log)** cho các thao tác quan trọng: sửa hoá đơn, đổi trạng thái hợp đồng, đổi bảng giá, đổi phân quyền; mỗi bản ghi có người thực hiện, thời điểm, giá trị trước và sau.

## 6. QUY TẮC NGHIỆP VỤ (BUSINESS RULES)

**BR-RULE-01 (Doanh thu thực thu):** chỉ số tiền đã ghi nhận của hoá đơn PAID hoặc PARTIAL mới tính vào doanh thu thực thu; hoá đơn DRAFT và CANCELLED không tính.

**BR-RULE-02 (Một hợp đồng hiệu lực):** mỗi căn chỉ có một hợp đồng ACTIVE tại một thời điểm.

**BR-RULE-03 (Chỉ số công tơ):** chỉ số kỳ sau không nhỏ hơn kỳ trước; ngoại lệ khi thay công tơ phải có ghi chú và chỉ số chốt của công tơ cũ.

**BR-RULE-04 (Bất biến hoá đơn):** hoá đơn đã phát hành không được xoá; chỉ điều chỉnh bằng bút toán điều chỉnh có lý do và người duyệt.

**BR-RULE-05 (Bảng giá theo hiệu lực):** hoá đơn dùng bảng giá có hiệu lực tại kỳ tính phí, không dùng bảng giá mới cho kỳ cũ.

**BR-RULE-06 (Phạt chậm):** chỉ tính sau ngày quá hạn, theo tỷ lệ cấu hình trong hợp đồng và không vượt mức pháp luật cho phép.

**BR-RULE-07 (Đóng sự cố):** sự cố khẩn cấp và mức cao chỉ được chuyển RESOLVED khi người xử lý ghi kết quả và đính kèm hình ảnh hoặc biên bản.

**BR-RULE-09 (Phạm vi dữ liệu):** người dùng chỉ truy cập các toà được phân quyền; cư dân chỉ thấy dữ liệu căn của mình.

## 7. YÊU CẦU PHI CHỨC NĂNG (NON-FUNCTIONAL REQUIREMENTS)

**NFR-01 (Dễ dùng):** giao diện tiếng Việt, dùng tốt trên điện thoại; nhân viên kỹ thuật cập nhật trạng thái sự cố nhanh, ít thao tác.

**NFR-02 (Bảo mật):** mật khẩu được băm, phiên đăng nhập có thời hạn, truyền dữ liệu qua HTTPS; dữ liệu cá nhân cư dân được bảo vệ theo quy định pháp luật Việt Nam hiện hành về dữ liệu cá nhân.

**NFR-03 (Toàn vẹn và sao lưu):** sao lưu dữ liệu định kỳ; nhật ký thao tác không cho sửa hoặc xoá.

**NFR-04 (Mở rộng):** thêm toà nhà mới bằng cấu hình và nhập dữ liệu, không phải sửa mã nguồn.

## 8. TIÊU CHÍ NGHIỆM THU NGHIỆP VỤ (BUSINESS ACCEPTANCE CRITERIA)

Dự án được coi là hoàn thành giai đoạn yêu cầu nghiệp vụ khi thoả mãn các tiêu chí sau:

**AC-1:** import thành công danh sách căn hộ và cư dân từ file Excel mẫu; mã căn, ngày, tiền tệ đúng chuẩn; dòng lỗi được báo rõ vị trí.

**AC-2:** chạy trọn một chu kỳ thu phí (ghi chỉ số, tạo hoá đơn, duyệt, phát hành, ghi nhận thanh toán, báo cáo công nợ) trên dữ liệu mẫu, kết quả khớp phép tính tay.

**AC-3:** dashboard hiển thị đúng 3 chỉ số chính (tỷ lệ thu phí, công nợ quá hạn, sự cố đang mở) ngay ở màn hình đầu.

**AC-4:** một sự cố đi hết vòng đời có lịch sử đầy đủ, SLA tính đúng theo ma trận ưu tiên và có cảnh báo khi quá hạn.

**AC-5:** lịch bảo trì tự sinh công việc trước hạn và tự tính ngày kế tiếp sau khi hoàn thành.

**AC-6:** phân quyền đúng: mỗi vai trò và mỗi toà chỉ thấy và làm những gì được phép.

**AC-7:** đạt Blind Test: người ngoài dự án đọc dashboard và chỉ ra được việc cần làm mà không cần hướng dẫn.

*Tài liệu này là căn cứ để xây dựng Tài liệu Đặc tả Yêu cầu Phần mềm (SRS) và thiết kế kỹ thuật ở bước tiếp theo.*
