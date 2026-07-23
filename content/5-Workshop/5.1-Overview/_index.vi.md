---
title: "Tổng quan Workshop"
date: 2026-07-15
weight: 1
chapter: false
pre: " <b> 5.1 </b> "
---

# WMS Pro: Hướng dẫn Triển khai Hạ tầng AWS Cloud

### Mục tiêu Workshop
Workshop này hướng dẫn chi tiết từng bước khởi tạo hạ tầng chuẩn **AWS Cloud** để vận hành hệ thống **WMS Pro**:
- Triển khai Cơ sở dữ liệu quan hệ **Amazon RDS PostgreSQL** quản lý dữ liệu vận đơn & tài chính.
- Khởi tạo Máy chủ ảo **Amazon EC2 (Ubuntu 24.04 LTS)** phục vụ ứng dụng Backend NestJS và Web Frontend Next.js.
- Cấu hình mạng & tường lửa **Security Groups** cho phép EC2 giao tiếp an toàn với CSDL RDS.

### Yêu cầu tiền đề (Prerequisites)
1. Tài khoản **AWS Account** còn hiệu lực (ưu tiên tài khoản thuộc diện AWS Free Tier).
2. Trình duyệt web hiện đại (Chrome/Edge/Firefox) để truy cập **AWS Management Console**.
3. Kiến thức cơ bản về Linux, SSH và CSDL PostgreSQL.
