---
title: "Module 3: Kết nối EC2 với RDS PostgreSQL"
date: 2026-07-15
weight: 4
chapter: false
pre: " <b> 5.4 </b> "
---

# MODULE 3: CẤU HÌNH KẾT NỐI BACKEND EC2 VỚI DATABASE RDS POSTGRESQL

### BƯỚC 1: Lấy Endpoint của Database RDS
1. Tại thanh tìm kiếm trên cùng, gõ **RDS** và chọn dịch vụ RDS.
2. Nhấp vào tên CSDL `wms-pro-db` vừa tạo ở Module 1.
3. Ở tab **Connectivity & security**, sao chép chuỗi địa chỉ tại mục **Endpoint** (dạng `wms-pro-db.c7asq8i066d6.ap-southeast-1.rds.amazonaws.com`).
*(Lưu lại Endpoint này để điền giá trị `DB_HOST` cho Backend NestJS).*

![Xem thông tin RDS Database](/images/5-Workshop/5.4-Connect-EC2-RDS/image6.png)
![Copy Endpoint CSDL](/images/5-Workshop/5.4-Connect-EC2-RDS/image3.png)
![Connectivity & Security Details](/images/5-Workshop/5.4-Connect-EC2-RDS/image5.png)

---

### BƯỚC 2: Cấu hình Firewall (Security Group) cho RDS
Để máy chủ EC2 (`wms-pro-server`) có quyền kết nối vào Database RDS, chúng ta phải mở cổng `5432` cho Security Group của RDS:

1. Tại trang chi tiết `wms-pro-db`, chọn tab **Connectivity & security**, tìm mục **VPC security groups** và nhấp vào tên Security Group của RDS (`wms-rds-sg`).
2. Hệ thống chuyển hướng sang trang **Security Groups** của VPC.
3. Chọn Security Group của RDS ➔ Chọn tab **Inbound rules** ở khung bên dưới ➔ Nhấp **Edit inbound rules**.
4. Nhấp **Add rule**:
   - **Type**: Chọn **PostgreSQL** (Port `5432`).
   - **Source**: Chọn **Custom** ➔ Nhập Security Group ID của `wms-pro-server` (dạng `sg-xxxxxxxxxxxxxxxxx`) hoặc chọn IP Public của EC2.
   - **Description**: `Allow EC2 backend to access PostgreSQL`.
5. Nhấp **Save rules**.

![Chuyển hướng trang Security Group](/images/5-Workshop/5.4-Connect-EC2-RDS/image1.png)
![Danh sách Security Groups](/images/5-Workshop/5.4-Connect-EC2-RDS/image7.png)
![Chỉnh sửa Inbound Rules cho RDS](/images/5-Workshop/5.4-Connect-EC2-RDS/image4.png)
![Lưu Inbound Rules thành công](/images/5-Workshop/5.4-Connect-EC2-RDS/image2.png)
