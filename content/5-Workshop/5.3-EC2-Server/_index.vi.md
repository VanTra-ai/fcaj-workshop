---
title: "Module 2: Khởi tạo Máy chủ Ứng dụng Amazon EC2"
date: 2026-07-15
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

### 1. Giới thiệu Module

{{% notice info %}}
**Amazon EC2 (Elastic Compute Cloud)** cung cấp năng lượng tính toán có thể co giãn linh hoạt trên hạ tầng đám mây của AWS. Trong hệ thống **Logistics WMS Pro**, máy chủ EC2 đóng vai trò là "trái tim" điều hành, chịu trách nhiệm chạy song song hai phân hệ quan trọng:
* **Backend API (NestJS):** Lõi xử lý logic nghiệp vụ, thuật toán điều phối TMS, kết nối CSDL Amazon RDS và giao tiếp thời gian thực qua WebSocket/Socket.io trên cổng `3333`.
* **Frontend Web App (Next.js):** Giao diện quản trị Web Dashboard phục vụ Điều phối viên và Admin vận hành hệ thống.
{{% /notice %}}

{{% notice tip %}}
**Pro Tip:** Sử dụng dòng máy `t2.micro` hoặc `t3.micro` kết hợp hệ điều hành Ubuntu Server 24.04 LTS, bạn sẽ tận dụng trọn vẹn 750 giờ/tháng chạy máy chủ cùng 30GB dung lượng đĩa cứng EBS miễn phí theo chính sách AWS Free Tier.
{{% /notice %}}

---

### 2. Quy trình Triển khai Chi tiết

#### Bước 1: Truy cập Dịch vụ Amazon EC2
1. Đăng nhập vào AWS Management Console.
2. Tại thanh tìm kiếm chính ở đầu trang (`[Alt+S]`), nhập từ khóa **EC2**.
3. Nhấp chọn dịch vụ **EC2 (Virtual Servers in the Cloud)** từ danh sách kết quả.

![Truy cập Dịch vụ Amazon EC2](/images/5-Workshop/5.3-EC2-Server/image7.png)

---

#### Bước 2: Bắt đầu Khởi tạo Máy ảo (Launch Instance)
1. Tại bảng điều khiển EC2 Dashboard, tìm mục **Launch instance**.
2. Nhấp vào nút màu cam **Launch instance** để mở trang cấu hình máy ảo.

![Bắt đầu Khởi tạo Máy ảo](/images/5-Workshop/5.3-EC2-Server/image8.png)

---

#### Bước 3: Cấu hình Chi tiết Thông số Máy chủ EC2

##### 2.1. Đặt tên Máy chủ (Name and tags)
* **Name**: Nhập `wms-pro-server`.

##### 2.2. Chọn Hệ điều hành (Application and OS Images - AMI)
1. Tại mục Quick Start, chọn thẻ **Ubuntu**.
2. **Amazon Machine Image (AMI)**: Chọn phiên bản **Ubuntu Server 24.04 LTS (HVM)**, SSD Volume Type (Bản 64-bit (x86) - Có nhãn *Free tier eligible*).

![Chọn Hệ điều hành Ubuntu](/images/5-Workshop/5.3-EC2-Server/image1.png)

##### 2.3. Cấu hình Phần cứng (Instance type)
* **Instance type**: Chọn gói `t2.micro` (hoặc `t3.micro` tùy theo Vùng khả dụng AZ) - Có nhãn *Free tier eligible*.

##### 2.4. Khởi tạo và Cấu hình Cặp khóa SSH (Key pair)
1. Tại mục **Key pair (login)**, nhấp vào liên kết **Create new key pair**.
2. Thiết lập các thông số trong cửa sổ bật lên:
   * **Key pair name**: Nhập `wms-server-key`.
   * **Key pair type**: Chọn **RSA**.
   * **Private key file format**: Chọn `.pem` (dành cho OpenSSH / MobaXterm / Termius / VS Code) hoặc `.ppk` (dành cho PuTTY).
3. Nhấp nút **Create key pair** để tải file khóa về máy tính cá nhân và lưu trữ an toàn.
4. Chọn lại khóa `wms-server-key` trong danh sách thả xuống.

![Tạo Cặp khóa SSH](/images/5-Workshop/5.3-EC2-Server/image11.png)
![Chọn Cặp khóa SSH](/images/5-Workshop/5.3-EC2-Server/image4.png)

##### 2.5. Cấu hình Mạng & Tường lửa (Network settings & Security Group)
1. Nhấp nút **Edit** ở góc phải mục **Network settings**.
2. **VPC**: Giữ nguyên **Default VPC**.
3. **Auto-assign public IP**: Chọn **Enable** (Bắt buộc bật để máy chủ sở hữu IP Public kết nối từ Internet).
4. **Firewall (security groups)**: Chọn **Create security group**.
5. **Security group name**: Nhập `wms-ec2-sg`.
6. Cấu hình danh sách các quy tắc Inbound Rules (Cho phép lưu lượng đi vào):

| Rule Type | Protocol | Port Range | Source Type | Source CIDR | Mục đích sử dụng |
| --- | --- | --- | --- | --- | --- |
| **SSH** | TCP | `22` | Anywhere | `0.0.0.0/0` | Quản trị máy chủ từ xa qua Terminal / MobaXterm |
| **HTTP** | TCP | `80` | Anywhere | `0.0.0.0/0` | Điều hướng Web App / Nginx Reverse Proxy |
| **HTTPS** | TCP | `443` | Anywhere | `0.0.0.0/0` | Cổng giao thức bảo mật SSL/TLS |
| **Custom TCP** | TCP | `3333` | Anywhere | `0.0.0.0/0` | Cổng API Backend NestJS & Socket.io |

![Security Group Configuration 1](/images/5-Workshop/5.3-EC2-Server/image10.png)
![Security Group Configuration 2](/images/5-Workshop/5.3-EC2-Server/image9.png)
![Security Group Rules](/images/5-Workshop/5.3-EC2-Server/image5.png)

{{% notice warning %}}
**Security Notice:** Quy tắc mở cổng 22 (SSH) và 3333 từ `0.0.0.0/0` (Anywhere) phục vụ mục đích kiểm thử và triển khai linh hoạt. Trong môi trường doanh nghiệp thực tế, cổng 22 nên được giới hạn chính xác theo IP Tĩnh của nhà mạng cá nhân (*My IP*).
{{% /notice %}}

##### 2.6. Cấu hình Dung lượng Lưu trữ (Configure storage)
* **Root volume**: Giữ nguyên cấu hình mặc định 8 GiB loại gp3 (SSD).

---

#### Bước 4: Khởi chạy và Trích xuất Địa chỉ IP Public
1. Kiểm tra lại toàn bộ thông số cấu hình tại bảng Summary ở cột bên phải.
2. Nhấp vào nút màu cam **Launch instance**.
3. Màn hình thông báo khởi tạo thành công (*Successfully initiated launch of instance*).
4. Nhấp chọn mã Instance ID để chuyển về trang chi tiết máy chủ.
5. Tại trang **Instance summary**, ghi lại thông số **Public IPv4 address** (Ví dụ thực tế: `54.169.12.125`). Đây là địa chỉ IP tĩnh dùng để cấu hình tệp `.env` cho Frontend Web App và Flutter Mobile App.

![Launch Instance Success](/images/5-Workshop/5.3-EC2-Server/image3.png)
![Instance Summary](/images/5-Workshop/5.3-EC2-Server/image2.png)
![Public IP Address](/images/5-Workshop/5.3-EC2-Server/image6.png)

---

### 3. Tổng kết Module 2

Trong Module này, bạn đã triển khai thành công:
* Máy chủ ảo **Amazon EC2 Ubuntu 24.04 LTS** (`wms-pro-server`) hoạt động ổn định trên hạ tầng Free Tier.
* Thiết lập cặp khóa SSH `wms-server-key` bảo mật để truy cập quản trị từ máy trạm.
* Cấu hình nhóm bảo mật Security Group mở trọn vẹn các cổng giao tiếp chuẩn (22, 80, 443) và cổng ứng dụng NestJS (`3333`).
* Sở hữu địa chỉ Public IPv4 Address sẵn sàng cho các bước đóng gói và kích hoạt ứng dụng ở Module tiếp theo.
