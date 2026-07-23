---
title: "Module 1: Triển khai CSDL RDS PostgreSQL"
date: 2026-07-15
weight: 2
chapter: false
pre: " <b> 5.2 </b> "
---

# MODULE 1: TRIỂN KHAI CƠ SỞ DỮ LIỆU AMAZON RDS POSTGRESQL

### BƯỚC 1: Truy cập dịch vụ Amazon RDS
1. Tại ô tìm kiếm chính trên cùng (Search `[Alt+S]`), gõ từ khóa: **RDS** hoặc click trực tiếp vào **Aurora and RDS** trong mục Recently visited.
2. Nhấp chọn dịch vụ **RDS (Managed Relational Database Service)** từ danh sách kết quả.

![Truy cập dịch vụ Amazon RDS](/images/5-Workshop/5.2-RDS-PostgreSQL/image2.png)

---

### BƯỚC 2: Điều hướng đến trang Khởi tạo Database
1. Tại giao diện RDS Dashboard, ở menu điều hướng bên trái, nhấp chọn **Databases**.
2. Nhấp vào nút màu cam **Create database** ở góc trên bên phải.
3. Chọn tùy chọn **Full configuration**.

![Trang khởi tạo Database](/images/5-Workshop/5.2-RDS-PostgreSQL/image9.png)

---

### BƯỚC 3: Thiết lập Thông số Chi tiết (Create database)

#### 1. Engine options (Chọn hệ quản trị CSDL)
- **Engine type**: Chọn **PostgreSQL**
- **Database creation method**: Tích chọn ô **Full configuration**

![Chọn PostgreSQL](/images/5-Workshop/5.2-RDS-PostgreSQL/image4.png)
![Cấu hình Engine](/images/5-Workshop/5.2-RDS-PostgreSQL/image8.png)

#### 2. Settings & Credentials
- **Engine version**: Giữ nguyên phiên bản PostgreSQL mới nhất có sẵn (ví dụ: PostgreSQL 16/18).
- **DB instance identifier**: Điền `wms-pro-db`.
- **Master username**: `postgres`.
- **Credentials management**: Chọn **Self managed**.
- **Master password & Confirm master password**: Nhập mật khẩu quản trị (ví dụ: `WmsPro2026Password!`).

![Cấu hình Settings](/images/5-Workshop/5.2-RDS-PostgreSQL/image7.png)
![Thiết lập Mật khẩu Master](/images/5-Workshop/5.2-RDS-PostgreSQL/image12.png)

#### 3. Instance configuration & Storage
- **DB instance class**: Chọn dòng có chữ micro (ví dụ: `db.t4g.micro` hoặc `db.t3.micro`) thuộc diện **Free Tier**.
- **Storage type**: Giữ nguyên **General Purpose SSD (gp2)** hoặc **gp3**.
- **Allocated storage**: Nhập `20` (GiB).

![Instance Configuration & Storage](/images/5-Workshop/5.2-RDS-PostgreSQL/image1.png)

#### 4. Connectivity
- **Compute resource**: Chọn **Don't connect to an EC2 compute resource**.
- **Virtual private cloud (VPC)**: Chọn **Default VPC**.
- **Public access**: **RẤT QUAN TRỌNG**: Chuyển từ **No** sang **Yes** (Để có thể kết nối từ máy tính cá nhân chạy script khởi tạo dữ liệu địa giới).
- **VPC security group (firewall)**: Chọn **Create new**, đặt tên Security Group là `wms-rds-sg`.

![Cấu hình Connectivity](/images/5-Workshop/5.2-RDS-PostgreSQL/image6.png)
![Cấu hình Public Access & Security Group](/images/5-Workshop/5.2-RDS-PostgreSQL/image5.png)

#### 5. Monitoring & Additional configuration
- **Monitoring**: Giữ nguyên mặc định.
- Nhấp mở rộng mục **Additional configuration** ở sát dưới cùng.
- **Initial database name**: Điền chính xác chữ `logistics` (Bắt buộc điền để đồng bộ với mã nguồn backend NestJS).
- Các mục còn lại như Backup, Encryption, Maintenance: Giữ nguyên mặc định.

![Điền Initial Database Name](/images/5-Workshop/5.2-RDS-PostgreSQL/image3.png)

---

### BƯỚC CUỐI CÙNG: Khởi tạo Database
Sau khi điền xong ô **Initial database name** là `logistics`, kéo xuống dưới cùng của trang và nhấp nút màu cam **Create database**.

![Hoàn tất khởi tạo Database](/images/5-Workshop/5.2-RDS-PostgreSQL/image10.png)
![Kiểm tra danh sách Databases](/images/5-Workshop/5.2-RDS-PostgreSQL/image11.png)
