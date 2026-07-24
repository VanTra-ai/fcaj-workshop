---
title: "Workshop"
date: 2026-07-15
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Workshop: Triển khai Hệ thống WMS Pro trên Hạ tầng AWS Cloud

Tại phần này, tôi ghi lại toàn bộ quá trình thực hành thực tế (**Hands-on Lab**) triển khai hệ thống **WMS Pro (Comprehensive Warehouse & Transportation Management System)** lên nền tảng hạ tầng đám mây AWS. Mỗi bài lab đều có hướng dẫn từng bước chi tiết kèm hình ảnh chụp màn hình minh họa thực tế từ AWS Management Console và Terminal.

---

### Danh sách các Module thực hành (Hands-on Labs):

1. **[5.1 - Tổng quan Workshop](5.1-overview/):** Giới thiệu mục tiêu workshop, kiến trúc đám mây 3 lớp (3-Tier Architecture), các công cụ cần chuẩn bị và hướng dẫn tối ưu chi phí với gói AWS Free Tier.
2. **[5.2 - Module 1: Triển khai CSDL Amazon RDS PostgreSQL](5.2-rds-postgresql/):** Khởi tạo cụm CSDL quan hệ Amazon RDS PostgreSQL (`wms-pro-db`), tạo sẵn cơ sở dữ liệu gốc `logistics` và thiết lập nhóm bảo mật `wms-rds-sg`.
3. **[5.3 - Module 2: Khởi tạo Máy chủ Ứng dụng Amazon EC2](5.3-ec2-server/):** Khởi tạo máy chủ ảo EC2 Ubuntu 24.04 LTS (`wms-pro-server`), tạo khóa SSH `wms-server-key` và mở các cổng tường lửa Security Group (22, 80, 443, 3333).
4. **[5.4 - Module 3: Cấu hình Kết nối Backend EC2 với RDS & Kích hoạt API](5.4-connect-ec2-rds/):** Trích xuất RDS Endpoint, cấu hình quy tắc SG-to-SG Inbound 5432, SSH cài đặt Node.js 20 / PM2, khai báo biến môi trường `.env` và kích hoạt Swagger API Documentation.

---

{{% notice info %}}
💡 **Lưu ý:** Tất cả các thao tác hướng dẫn trong chuỗi bài Lab này đều tuân thủ các nguyên tắc bảo mật và tối ưu chi phí trong hạn mức miễn phí **AWS Free Tier**.
{{% /notice %}}
