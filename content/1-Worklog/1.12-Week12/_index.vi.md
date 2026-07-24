---
title: "Worklog Tuần 12"
date: 2026-07-12
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Mục tiêu tuần 12:

* Khởi tạo và đóng gói toàn bộ hạ tầng Cloud AWS phục vụ triển khai hệ thống Logistics (WMS Pro) với chi phí tối ưu theo mô hình Free Tier (<10$/tháng).
* Triển khai thành công Cơ sở dữ liệu Amazon RDS PostgreSQL, cấu hình Security Group cô lập an toàn và kết nối thông suốt với máy chủ ứng dụng Amazon EC2.
* Cấu hình môi trường vận hành sản xuất (Node.js 20, PM2, Nginx Reverse Proxy) trên EC2 Ubuntu; triển khai thành công Backend NestJS API và Frontend Next.js Web App.
* Tích hợp kho lưu trữ đối tượng Amazon S3 chứa ảnh minh chứng giao hàng/sự cố, ứng dụng IAM Role Instance Profile cho EC2 để truy cập S3 không cần hardcode Access Key.
* Cấu hình địa chỉ IP máy chủ Cloud cho ứng dụng di động Flutter (Mobile App), đóng gói file APK, thực thi nghiệm thu E2E toàn bộ luồng nghiệp vụ thực tế trên thiết bị thật.
* Chuẩn hóa bảo mật theo tiêu chuẩn AWS Well-Architected Framework: Cấu hình quy tắc Inbound SG-to-SG giữa EC2 và RDS, kiểm tra mã hóa dữ liệu KMS.
* Quay Video Demo hệ thống, đóng gói tài liệu kỹ thuật, hoàn thiện trang thông tin Workshop/Báo cáo thực tập trên nền tảng Hugo Site và nghiệm thu dự án tốt nghiệp.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành |
| --- | --- | --- | --- |
| 2 | - Phân tích tham số hệ thống và chuẩn bị tệp biến môi trường `.env` cho 3 phân hệ (Backend NestJS, Web Next.js, Mobile Flutter).<br>- Khởi tạo cơ sở dữ liệu Amazon RDS for PostgreSQL (gói `db.t3.micro`, 20GB SSD, Single-AZ), thiết lập Master User `postgres` và cấu hình VPC Security Group.<br>- Khởi tạo máy chủ Amazon EC2 (Ubuntu 24.04 LTS, gói `t3.micro`), gán Elastic IP và mở các cổng Security Group: 22 (SSH), 80 (HTTP), 443 (HTTPS), 3333 (NestJS API).<br>- SSH vào EC2 qua MobaXterm, tiến hành cài đặt môi trường vận hành: Node.js 20 LTS, Git, PM2 Process Manager và Web Server Nginx. | 06/07/2026 | 06/07/2026 |
| 3 | - Clone mã nguồn `logistics-backend` từ GitHub về EC2, cấu hình file `.env` trỏ biến `DB_HOST` về Endpoint của Amazon RDS PostgreSQL.<br>- Thực hiện biên dịch mã nguồn (`npm install`, `npm run build`), kích hoạt tính năng tự động tạo bảng TypeORM (`synchronize: true`) và quản lý tiến trình bằng PM2 (`pm2 start dist/main.js --name wms-api`).<br>- Kiểm thử kết nối API công khai và giao diện Swagger UI tại đường dẫn `http://<EC2-Public-IP>:3333/api`.<br>- Triển khai `logistics-web-app` (Next.js): Cấu hình `NEXT_PUBLIC_API_URL`, build bản sản xuất và cấu hình Nginx Reverse Proxy điều hướng cổng 80 vào Web App (port 3000) và API (port 3333). | 07/07/2026 | 07/07/2026 |
| 4 | - Khởi tạo Amazon S3 Bucket public để lưu trữ hình ảnh minh chứng giao hàng và ảnh báo cáo sự cố tải lên từ ứng dụng di động.<br>- Cấu hình chỉnh sửa tệp `lib/core/network/api_client.dart` trên mã nguồn Flutter, cập nhật địa chỉ `_baseUrl` trỏ trực tiếp về IP Public của EC2 Server.<br>- Tiến hành đóng gói ứng dụng di động thành file cài đặt thực tế (`flutter build apk`) và cài đặt lên thiết bị Android thật.<br>- Thực thi kiểm thử luồng giao vận thực địa: Đăng nhập App Shipper $\rightarrow$ Quét mã Barcode $\rightarrow$ Chụp ảnh minh chứng $\rightarrow$ Tải ảnh lên S3 $\rightarrow$ Đồng bộ dữ liệu Real-time lên Web Dashboard. | 08/07/2026 | 08/07/2026 |
| 5 | - Áp dụng các nguyên tắc bảo mật chuẩn AWS Well-Architected Framework:<br>&emsp; + Thiết lập chốt chặn Security Group cho RDS theo mô hình SG-to-SG: Chỉ chấp nhận Inbound traffic port 5432 từ chính Security Group ID của máy chủ EC2.<br>&emsp; + Khởi tạo IAM Role với chính sách `AmazonS3FullAccess`, gán vào EC2 dưới dạng Instance Profile để Backend NestJS truy cập S3 an toàn mà không cần lưu Access Key/Secret Key trong code.<br>&emsp; + Rà soát thuộc tính mã hóa dữ liệu KMS (Encryption Enabled) trên Amazon S3 Bucket và Amazon RDS Instance.<br>- Đóng gói toàn bộ mã nguồn trên GitHub, dọn dẹp các tệp tin tạm và hoàn thiện kiểm thử an ninh. | 09/07/2026 | 09/07/2026 |
| 6 | - Tiến hành quay và biên tập Video Demo kịch bản vận hành E2E khép kín của hệ thống WMS Pro (từ lúc tạo đơn, lưu kho bãi, điều phối xe tải/xe máy, giao hàng di động đến đối soát ví tài chính).<br>- Tổng hợp toàn bộ tài liệu kỹ thuật, kiến trúc hạ tầng Cloud, hướng dẫn triển khai và cập nhật lên website tài liệu Workshop (`vantra-ai.github.io/fcaj-workshop/vi/`).<br>- Biên tập, rà soát văn phong và hoàn thiện toàn bộ nội dung Báo cáo Thực tập Tốt nghiệp theo đúng quy định của đơn vị thực tập AWS và Nhà trường (HUTECH). | 10/07/2026 | 10/07/2026 |

### Kết quả đạt được tuần 12:

* **Triển khai thành công Hạ tầng Cloud AWS Sản xuất (Production Infrastructure):**
  * Khởi tạo và vận hành ổn định Amazon RDS PostgreSQL tương thích 100% với TypeORM, tối ưu chi phí trong định mức Free Tier.
  * Cấu hình máy chủ Amazon EC2 Ubuntu chạy song song Backend NestJS (port 3333) và Frontend Next.js (port 3000) qua trình quản lý tiến trình PM2 và Nginx Reverse Proxy.
  * Tích hợp thành công kho lưu trữ đối tượng Amazon S3 phục vụ lưu trữ tài nguyên đa phương tiện (ảnh minh chứng giao hàng, bằng chứng sự cố).
* **Đóng gói và Nghiệm thu Hệ thống Đa nền tảng (Full-Stack Logistics Platform):**
  * Cấu hình và build thành công file APK ứng dụng di động Flutter, kết nối mượt mà với API Cloud qua địa chỉ IP Public của EC2.
  * Nghiệm thu thành công chuỗi luồng nghiệp vụ E2E thời gian thực (Real-time): Shipper quét mã vạch và chụp ảnh giao hàng trên điện thoại, dữ liệu lập tức nhảy trạng thái và cập nhật số dư ví COD trên Web Dashboard Admin/Coordinator.
* **Tuân thủ Tiêu chuẩn Bảo mật AWS Well-Architected Framework:**
  * Loại bỏ hoàn toàn việc hardcode Access Key/Secret Key nhờ việc áp dụng IAM Role Instance Profile cho EC2.
  * Cô lập hoàn toàn Cơ sở dữ liệu RDS khỏi Internet công cộng bằng quy tắc phân quyền theo Security Group ID (SG-to-SG Inbound Rule).
  * Đảm bảo tính toàn vẹn và an toàn dữ liệu thông qua cơ chế mã hóa KMS phía máy chủ (Server-Side Encryption).
* **Hoàn thiện Sản phẩm Báo cáo & Tài liệu Nghiệm thu:**
  * Hoàn thành Video Demo chuyên nghiệp ghi lại toàn bộ hoạt động của hệ thống WMS Pro.
  * Tổng hợp toàn bộ tài liệu triển khai Workshop và hoàn thiện Báo cáo Thực tập Tốt nghiệp.
