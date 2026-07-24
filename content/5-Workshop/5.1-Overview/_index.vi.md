---
title: "Tổng quan Workshop"
date: 2026-07-15
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

# WMS Pro: Hướng dẫn Triển khai Hạ tầng AWS Cloud

### 1. Mục tiêu Workshop

Workshop này được thiết kế theo dạng **Hands-on Lab** chi tiết từng bước, hướng dẫn bạn khởi tạo và cấu hình hạ tầng đám mây **AWS Cloud** hoàn chỉnh phục vụ vận hành sản xuất hệ thống **WMS Pro (Comprehensive Warehouse & Transportation Management System)**:

* **Triển khai Cơ sở dữ liệu Cloud:** Khởi tạo cụm CSDL quan hệ **Amazon RDS PostgreSQL** quản lý toàn bộ dữ liệu đơn hàng, kho bãi, số dư ví tài xế và lịch sử hành trình.
* **Khởi tạo Máy chủ Ứng dụng:** Cấu hình máy chủ ảo **Amazon EC2 (Ubuntu 24.04 LTS)** đóng vai trò máy chủ trung tâm chạy Backend NestJS API và Web App Dashboard Next.js.
* **Cấu hình Kết nối & Bảo mật:** Thiết lập quy tắc tường lửa **VPC Security Groups** cô lập an toàn, cho phép EC2 giao tiếp thông suốt với CSDL RDS qua cổng 5432 và kích hoạt Swagger API trên cổng 3333.

{{% notice info %}}
**Hệ thống WMS Pro** sử dụng kiến trúc 3 lớp (3-Tier Cloud Architecture):
1. **Frontend Layer:** Web App (Next.js 15) & Mobile App (Flutter).
2. **Application Layer:** Backend API (NestJS, PM2 Process Manager, Socket.io) trên Amazon EC2.
3. **Database Layer:** Amazon RDS for PostgreSQL quản lý dữ liệu giao dịch khép kín (ACID).
{{% /notice %}}

---

### 2. Cấu trúc Các Bài Lab (Workshop Roadmap)

Nội dung Workshop được chia thành 3 Module thực hành độc lập nhưng kết nối liên hoàn:

* 🔹 **[Module 1: Triển khai CSDL Amazon RDS PostgreSQL](../5.2-rds-postgresql/):** Hướng dẫn tạo RDS Instance (`wms-pro-db`), chọn gói Free Tier, cấu hình Master Credentials và khởi tạo sẵn CSDL gốc `logistics`.
* 🔹 **[Module 2: Khởi tạo Máy chủ Ứng dụng Amazon EC2](../5.3-ec2-server/):** Hướng dẫn tạo EC2 Instance (`wms-pro-server`), gán IP Public, tạo khóa SSH (`wms-server-key`) và mở các cổng tường lửa Security Group (22, 80, 443, 3333).
* 🔹 **[Module 3: Cấu hình Kết nối Backend EC2 với RDS & Kích hoạt API](../5.4-connect-ec2-rds/):** Hướng dẫn trích xuất RDS Endpoint, mở Inbound Rule 5432 cho RDS, SSH vào EC2 cài đặt Node.js 20 LTS / PM2, bóc tách file `.env` và kích hoạt Swagger API Documentation.

---

### 3. Yêu cầu Tiền đề (Prerequisites)

Dụng cụ và kiến thức cần chuẩn bị trước khi bắt đầu thực hành:

1. **Tài khoản AWS (AWS Account):** Đã kích hoạt và còn hạn mức sử dụng (Khuyên dùng tài khoản trong thời gian **AWS Free Tier** 12 tháng đầu).
2. **Công cụ kết nối & Quản trị:**
   * Trình duyệt web hiện đại (Chrome, Edge, Firefox) để truy cập AWS Management Console.
   * Phần mềm Terminal/SSH trên máy tính cá nhân (MobaXterm, PuTTY, VS Code Terminal, hoặc Windows PowerShell).
3. **Kiến thức căn bản:** Nắm được các câu lệnh Linux cơ bản, khái niệm IP/Port và truy vấn CSDL quan hệ SQL.

{{% notice tip %}}
**Mẹo tiết kiệm chi phí (Cost Optimization):** Toàn bộ các bước hướng dẫn trong bài Workshop này đều tận dụng 100% định mức dịch vụ miễn phí thuộc gói **AWS Free Tier** (750 giờ EC2 `t2.micro`/`t3.micro`, 750 giờ RDS `db.t4g.micro`, 20GB SSD storage), giúp bạn thực hành hoàn toàn không phát sinh chi phí ngoài ý muốn.
{{% /notice %}}
