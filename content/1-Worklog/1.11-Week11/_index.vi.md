---
title: "Worklog Tuần 11"
date: 2026-07-12
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

* Xây dựng Module Tài chính & Biểu phí nâng cao: Cấu hình cước phí linh hoạt theo từng Bưu cục (Franchise Pricing), tự động Fallback về bảng giá hệ thống, tích hợp đối soát ví điện tử và công nợ COD của Tài xế.
* Xây dựng Giao diện Web App (Next.js 15, TailwindCSS): Tối ưu hóa UI/UX cho bộ phận Điều phối viên & Admin, xử lý triệt để rò rỉ bộ nhớ bản đồ Leaflet Map, tích hợp Trạm quét 2-in-1 và vách ngăn dữ liệu bưu cục (Data Isolation).
* Xây dựng Ứng dụng Di động (Flutter & Riverpod): Tích hợp luồng quét mã vạch Barcode/QR Code qua Camera, định vị GPS nền & Heartbeat định kỳ, chụp ảnh minh chứng giao hàng thực tế.
* Hoàn thiện các tính năng nâng cao: Xuất nhãn dán PDF khổ A6 (PDFKit), Quản lý Sự cố/Ngoại lệ (`OrderIncident`), Luồng chat hỗ trợ (`TicketComment`), và Audit Log Subscriber ghi vết hệ thống.
* Kiểm thử tích hợp toàn hệ thống (E2E Golden Flow 6 bước) và tối ưu hóa mã nguồn sẵn sàng đưa vào vận hành thực tế.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành |
| --- | --- | --- | --- |
| 2 | - Phát triển `FinanceModule`: Tạo Entity `FinanceTariff` (công thức tính cước động theo Dài x Rộng x Cao / `volumetric_divisor` và giá cước sàn/vượt mốc) & `FinanceTariffAudit` lưu lịch sử sửa bảng giá.<br>- Phát triển `WalletsModule`: Xây dựng logic giao dịch ví điện tử cho Shipper (`cod_debt`, `income_balance`), lập lịch gạch nợ COD tất tay (`remitAllShipperCod`) bọc trong Database Transaction với Pessimistic Lock (`pessimistic_write`). | 29/06/2026 | 29/06/2026 |
| 3 | - Lập trình Web Dashboard (Next.js): Cấu hình Sidebar RBAC theo vai trò, dọn dẹp toàn bộ dữ liệu giả (Purge Mock Data), chuẩn hóa Pagination `{ data, meta }`.<br>- Tối ưu hóa `TmsMap.tsx`: Sử dụng `useRef` và Cleanup function loại bỏ dứt điểm lỗi crash "Map container is already initialized".<br>- Xây dựng màn hình Trạm xử lý (Station Page): Tích hợp Input Put-away nhanh, xem gợi ý Zone, sửa cân nặng tự động tính lại cước và ép in lại nhãn dán màu đỏ nhấp nháy. | 30/06/2026 | 30/06/2026 |
| 4 | - Lập trình App Mobile (Flutter): Cấu hình Riverpod State Management, Dio HTTP Client kèm Auth Interceptor tự động làm mới Token.<br>- Xây dựng `ShipperScanScreen` (Mobile Scanner QR/Barcode), màn hình Cập nhật trạng thái đơn hàng (`completeOrder`) đính kèm chụp ảnh minh chứng.<br>- Tích hợp `LocationTrackerService` chạy ngầm phát Heartbeat GPS (`PATCH /users/heartbeat`) duy trì trạng thái Online cho thuật toán TMS. | 01/07/2026 | 01/07/2026 |
| 5 | - Triển khai `LabelService`: Sử dụng thư viện PDFKit và QRCode render file PDF Nhãn vận chuyển khổ A6 chuẩn Tiếng Việt (Font Roboto) trả về luồng Buffer Stream (`GET /orders/:id/label`).<br>- Nâng cấp luồng Hủy chuyến xe (`cancelShipment`): Tự động Rollback trạng thái các đơn hàng bên trong về `AT_HUB`, giải phóng phương tiện `Vehicle` và lưu vết Audit Log bất biến (`AuditLogSubscriber`). | 02/07/2026 | 02/07/2026 |
| 6 | - Thực thi Kịch bản Kiểm thử tự động E2E 6 bước (`e2e_test.js`): Admin Login $\rightarrow$ Tạo đơn $\rightarrow$ Scan-In nhập kho xếp kệ $\rightarrow$ TMS Auto-Dispatch $\rightarrow$ Scan-Out bàn giao Shipper $\rightarrow$ Mobile completeOrder đối soát 2 ví.<br>- Sửa các lỗi biên dịch TypeScript, kiểm tra `npm run build` thành công trên cả 2 phân hệ Backend và Web App, đóng gói Git commit chuẩn Conventional Commits. | 03/07/2026 | 03/07/2026 |

### Kết quả đạt được tuần 11:

* **Hoàn thiện Hệ thống Tài chính & Ví Điện tử:**
  * Xây dựng thành công cơ chế tính cước động chuẩn xác theo công thức thể tích $V = (D \times R \times C) / 5000$, hỗ trợ bảng giá nhượng quyền theo từng Bưu cục với cơ chế Fallback tự động.
  * Xử lý trọn vẹn luồng đối soát công nợ COD và chiết khấu hoa hồng tài xế qua giao dịch ví ACID an toàn tuyệt đối, chống tình trạng Race Condition (Tranh chấp ghi dữ liệu đồng thời).
* **Hoàn thiện Giao diện Vận hành Đa nền tảng:**
  * **Web App (Next.js):** Màn hình Dashboard trực quan kết nối API thật 100%, tích hợp bản đồ GIS Leaflet mượt mà, màn hình Trạm xử lý (Station) "All-in-one" cho phép quét, in nhãn, sửa cân nặng và xếp kệ liên hoàn.
  * **Mobile App (Flutter):** Chạy mượt mà luồng lấy hàng/giao hàng, quét barcode tốc độ cao, tự động đồng bộ vị trí GPS thời gian thực về máy chủ Backend.
* **Hoàn thành Kiểm thử Golden Flow E2E:**
  * Thực thi thành công Script kịch bản kiểm thử E2E 6 bước tự động hóa khép kín từ khâu nạp đơn, qua kho bãi WMS, điều phối TMS, đến giao hàng và chốt sổ tài chính.
  * Mã nguồn được chuẩn hóa, dọn dẹp sạch sẽ toàn bộ Mock Data, biên dịch Build không ghi nhận lỗi TypeScript, sẵn sàng đóng gói Docker và triển khai lên hạ tầng Cloud AWS.
