---
title: "Worklog Tuần 10"
date: 2026-07-12
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

* Phân tích nghiệp vụ toàn diện hệ thống Chuỗi cung ứng & Logistics (WMS/TMS), chuyển đổi yêu cầu bài toán thành mô hình kiến trúc phần mềm chuẩn Enterprise.
* Thiết kế mô hình CSDL quan hệ (ERD) trên PostgreSQL, định nghĩa các Entity TypeORM với đầy đủ ràng buộc khóa ngoại, chỉ mục (Index) và bộ chuyển đổi kiểu dữ liệu (Transformers).
* Xây dựng bộ lõi Backend bằng NestJS: Thiết lập cấu trúc Modular Monolith, tích hợp JWT Authentication, mã hóa mật khẩu bcrypt và cơ chế phân quyền dựa trên vai trò (RBAC Guard).
* Xây dựng phân hệ WMS (Quản lý kho bãi) lõi: Quản lý vị trí lưu trữ đa tầng (Zone/Aisle/Shelf/Bin), thuật toán gợi ý Put-away theo tải trọng, quản lý vật tư đóng gói và quy trình kiểm kê kho (Audits).
* Phát triển phân hệ TMS (Quản lý vận tải) lõi: Mô hình hóa Hạm đội (Bikes & Trucks), thuật toán Auto-Dispatch gom nhóm tự động theo khoảng cách GPS (Haversine Formula) và giới hạn tải trọng xe.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành |
| --- | --- | --- | --- |
| 2 | - Phân tích yêu cầu nghiệp vụ hệ thống Logistics B2B: Luồng chuyển dịch hàng hóa, phân quyền 3 vai trò (ADMIN, HUB_COORDINATOR, SHIPPER).<br>- Phân tích kiến trúc hệ thống 3 lớp: Máy chủ Backend (NestJS/TypeORM), Web Dashboard (Next.js/TailwindCSS) và Mobile App (Flutter/Riverpod).<br>- Thiết kế Sơ đồ quan hệ CSDL (ERD) trên PostgreSQL gồm các bảng lõi: `users`, `hubs`, `orders`, `shipments`, `locations`, `vehicles`, `materials`, `wallets`, `incidents`, `tracking_history`. | 22/06/2026 | 22/06/2026 |
| 3 | - Khởi tạo dự án NestJS backend, cấu hình tệp môi trường `.env` và kết nối PostgreSQL qua TypeORM (`AppModule`).<br>- Định nghĩa `User` Entity (kèm mã nhân viên tự động NV/TX, tọa độ GPS, heartbeat thời gian thực) và `Hub` Entity.<br>- Triển khai `AuthModule`: Xây dựng API `/auth/login`, `/auth/refresh`, mã hóa Bcrypt, cấp phát cặp Access Token / Refresh Token và lớp bảo mật `RolesGuard`. | 23/06/2026 | 23/06/2026 |
| 4 | - Triển khai `Order` Entity và `OrdersService`: Xây dựng Cổng kiểm soát trạng thái (`validateStatus` State Machine) bảo vệ vòng đời đơn hàng (`PENDING` $\rightarrow$ `AT_HUB` $\rightarrow$ `DELIVERING` $\rightarrow$ `FINISHED`).<br>- Tích hợp `EventEmitter2` bắn sự kiện `order.status.changed` ghi nhật ký hành trình tự động vào `TrackingHistory`.<br>- Triển khai `OrdersExcelService` hỗ trợ Import/Export đơn hàng hàng loạt từ file Excel qua tệp đệm Buffer và Database Transaction. | 24/06/2026 | 24/06/2026 |
| 5 | - Phát triển Module Kho bãi (WMS): Tạo Entity `Location` cấu hình mã vạch kệ (`LOC-Zone-Aisle-Shelf-Bin`).<br>- Viết hàm `putaway()` khóa dữ liệu bi quan (`pessimistic_write`) xếp đơn hàng lên kệ và tự động cập nhật sức chứa kho (`EMPTY` / `OCCUPIED` / `FULL`).<br>- Xây dựng `MaterialsModule` quản lý vật tư đóng gói và `AuditsModule` phục vụ kiểm kê, đối soát lệch vị trí hàng hóa trên kệ. | 25/06/2026 | 25/06/2026 |
| 6 | - Phát triển Module Vận tải (TMS): Khởi tạo `Shipment` Entity phân loại rõ Hạm đội giao hàng chặng cuối (`BIKE`) và Luân chuyển liên trạm (`TRUCK`).<br>- Xây dựng `TmsService` và `RouteOptimizationService`: Lập thuật toán Auto-Dispatch quét Shipper rảnh (online trong 10 phút, không vướng chuyến `IN_TRANSIT`), tính khoảng cách GPS bằng công thức Haversine để gợi ý chuyến xe ảo (`virtualShipments`). | 26/06/2026 | 26/06/2026 |

### Kết quả đạt được tuần 10:

* **Kiến trúc & CSDL Vững chắc:**
  * Hoàn thành 100% bản vẽ kiến trúc ERD và triển khai thành công 20+ TypeORM Entities đồng bộ xuống PostgreSQL Database.
  * Tích hợp cơ chế mã hóa mật khẩu bảo mật, cấp phát JWT Token hai tầng (Access/Refresh) và bảo vệ toàn bộ Endpoints bằng AuthGuard & RolesGuard.
* **Bộ Lõi Vận hành WMS & TMS:**
  * Xây dựng thành công Ma trận trạng thái (Logistics State Machine) khép kín, chặn đứng mọi thao tác cập nhật trạng thái nhảy cóc từ phía Client.
  * Phát triển thuật toán WMS Put-away tự động gợi ý Khu vực A (<5kg) / Khu vực B ($\ge$5kg) và tự động tính toán tỷ lệ lấp đầy kho.
  * Lập trình thuật toán TMS Auto-Dispatch tự động tối ưu hóa tuyến đường giao hàng theo thuật toán Láng giềng gần nhất (Nearest Neighbor) kết hợp khóa tải trọng phương tiện.
