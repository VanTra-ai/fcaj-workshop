---
title: "Module 2: Khởi tạo Máy chủ EC2"
date: 2026-07-15
weight: 3
chapter: false
pre: " <b> 5.3 </b> "
---

# MODULE 2: KHỞI TẠO MÁY CHỦ ỨNG DỤNG VỚI AMAZON EC2

### BƯỚC 1: Truy cập dịch vụ Amazon EC2
1. Tại ô tìm kiếm chính trên cùng (Search `[Alt+S]`), gõ: **EC2**.
2. Nhấp chọn dịch vụ **EC2 (Virtual Servers in the Cloud)** từ danh sách kết quả.

![Truy cập dịch vụ Amazon EC2](/images/5-Workshop/5.3-EC2-Server/image11.png)

---

### BƯỚC 2: Bắt đầu tạo Máy ảo (Launch Instance)
1. Tại giao diện **EC2 Dashboard**, nhấp vào nút màu cam **Launch instance**.

![Khởi tạo Launch Instance](/images/5-Workshop/5.3-EC2-Server/image4.png)

---

### BƯỚC 3: Cấu hình Thông số Máy chủ EC2

#### 1. Name and tags
- **Name**: Điền `wms-pro-server`

#### 2. Application and OS Images (Chọn hệ điều hành)
- Chọn **Ubuntu** (System provided).
- **AMI**: Chọn **Ubuntu Server 24.04 LTS (HVM), SSD Volume Type** (Bản 64-bit x86).

![Chọn Hệ điều hành Ubuntu](/images/5-Workshop/5.3-EC2-Server/image7.png)

#### 3. Instance type (Cấu hình phần cứng)
- Chọn `t3.micro` hoặc `t2.micro` (Thuộc diện **Free Tier** miễn phí).

#### 4. Key pair (Khóa SSH để đăng nhập)
1. Nhấp vào **Create new key pair** (nếu chưa có).
2. **Key pair name**: Điền `wms-server-key`
3. **Key pair type**: RSA
4. **Private key file format**: `.pem` (cho Linux/Mac/OpenSSH) hoặc `.ppk` (cho PuTTY).
5. Nhấp **Create key pair** (Tải file khóa về máy và lưu trữ an toàn).
6. Chọn lại Key pair vừa tạo trong danh sách thả xuống.

![Cấu hình Key Pair](/images/5-Workshop/5.3-EC2-Server/image3.png)
![Tạo Key Pair thành công](/images/5-Workshop/5.3-EC2-Server/image9.png)

#### 5. Network settings (Cấu hình Mạng & Firewall - CỰC KỲ QUAN TRỌNG)
- **VPC**: Chọn **Default VPC**.
- **Auto-assign public IP**: Chọn **Enable** (Bắt buộc bật để có IP Public truy cập từ Internet).
- **Firewall (Security group)**: Chọn **Create security group**.
- Tích chọn mở các cổng:
  - ☑ **Allow SSH traffic from**: Anywhere (`0.0.0.0/0`)
  - ☑ **Allow HTTP traffic from the internet**: Anywhere (`0.0.0.0/0`)
  - ☑ **Allow HTTPS traffic from the internet**: Anywhere (`0.0.0.0/0`)
- Nhấp **Add security group rule** để mở thêm cổng riêng cho Backend API:
  - **Type**: Custom TCP
  - **Port range**: `3333` (Cổng mặc định của NestJS Backend)
  - **Source**: Anywhere (`0.0.0.0/0`)

![Network Settings Security Group](/images/5-Workshop/5.3-EC2-Server/image2.png)
![Allow HTTP/HTTPS & Custom Port 3333](/images/5-Workshop/5.3-EC2-Server/image1.png)
![Cấu hình Chi tiết Inbound Rules](/images/5-Workshop/5.3-EC2-Server/image5.png)

#### 6. Configure storage (Cấu hình ổ đĩa)
- Giữ nguyên cấu hình mặc định: `8 GiB` hoặc `20 GiB` **gp3/gp2** (Nằm trong diện Free Tier 30GB).

---

### BƯỚC 4: Hoàn tất khởi tạo EC2
1. Nhìn sang cột bên phải màn hình, nhấp vào nút màu cam lớn **Launch instance**.
2. Hệ thống báo thành công (**Successfully initiated launch of instance**).
3. Nhấp vào mã Instance ID (ví dụ: `i-0123456789abcdef0`) để chuyển sang trang quản lý máy chủ.

![Bấm Launch Instance](/images/5-Workshop/5.3-EC2-Server/image10.png)
![Khởi tạo thành công](/images/5-Workshop/5.3-EC2-Server/image6.png)
![Xem danh sách EC2 Instances](/images/5-Workshop/5.3-EC2-Server/image8.png)
