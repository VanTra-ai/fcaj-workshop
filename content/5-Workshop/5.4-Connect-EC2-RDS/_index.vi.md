---
title: "Module 3: Cấu hình Kết nối EC2 với CSDL RDS PostgreSQL & API"
date: 2026-07-15
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

### 1. Giới thiệu Module

{{% notice info %}}
Trong hệ thống **Logistics WMS Pro**, máy chủ Backend NestJS chạy trên Amazon EC2 (`wms-pro-server`) cần giao tiếp thông suốt với cơ sở dữ liệu Amazon RDS PostgreSQL (`wms-pro-db`).

Module này hướng dẫn bạn bóc tách Endpoint kết nối, cấu hình mở cổng tường lửa Security Group (Port `5432`) cho RDS, SSH vào EC2 để cài đặt môi trường vận hành sản xuất (Node.js 20 LTS, PM2 Process Manager) và kích hoạt API dịch vụ.
{{% /notice %}}

{{% notice tip %}}
**Pro Tip:** Mã nguồn Backend NestJS được tích hợp cờ `synchronize: true` trong TypeORM. Ngay khi Backend kết nối thành công tới RDS, toàn bộ cấu trúc bảng (Entities: `users`, `orders`, `shipments`, `locations`, `wallets`, v.v.) sẽ được tự động khởi tạo trên cơ sở dữ liệu `logistics` mà không cần chạy migration thủ công.
{{% /notice %}}

---

### 2. Quy trình Triển khai Chi tiết

#### Bước 1: Trích xuất Endpoint Kết nối của Amazon RDS
1. Đăng nhập vào AWS Management Console.
2. Tại thanh tìm kiếm chính ở đầu trang (`[Alt+S]`), nhập từ khóa **RDS** và nhấp chọn **Aurora and RDS**.
3. Tại menu điều hướng bên trái, chọn **Databases**.
4. Nhấp chọn vào tên CSDL `wms-pro-db` vừa khởi tạo từ Module 1.
5. Ở tab **Connectivity & security**, chọn mục **Endpoints**.
6. Sao chép và lưu lại chuỗi địa chỉ tại mục **Endpoint** (Ví dụ thực tế: `wms-pro-db.c7asq8i066d6.ap-southeast-1.rds.amazonaws.com`). Chuỗi này sẽ được sử dụng làm giá trị cho biến `DB_HOST` trong file `.env` của Backend.

![RDS Endpoint Step 1](/images/5-Workshop/5.4-Connect-EC2-RDS/image12.png)
![RDS Endpoint Step 2](/images/5-Workshop/5.4-Connect-EC2-RDS/image2.png)
![RDS Endpoint Step 3](/images/5-Workshop/5.4-Connect-EC2-RDS/image11.png)

---

#### Bước 2: Cấu hình Quy tắc Tường lửa (Security Group) cho RDS
Để máy chủ EC2 có thể gửi truy vấn dữ liệu tới Database RDS, chúng ta cần mở cổng `5432` trên Security Group của RDS:
1. Ngay tại tab **Connectivity & security** của `wms-pro-db`, tìm mục **Security**.
2. Nhấp chọn vào tên nhóm bảo mật `wms-rds-sg`.
3. Hệ thống chuyển hướng sang giao diện quản lý Security Groups của dịch vụ EC2/VPC.
4. Nhấp chọn dòng `wms-rds-sg` trong danh sách.
5. Ở khung chi tiết bên dưới, chọn tab **Inbound rules** $
ightarrow$ Nhấp vào nút **Edit inbound rules**.
6. Nhấp vào nút **Add rule** và cấu hình thông số quy tắc mới:
   * **Type**: Chọn **PostgreSQL** (Hệ thống tự động điền Protocol TCP và Port Range `5432`).
   * **Source**: Chọn **Custom** $
ightarrow$ Nhập địa chỉ IP Public của EC2 (Ví dụ: `54.169.12.125/32`) hoặc chọn ID nhóm bảo mật của EC2 (`wms-ec2-sg`).
   * **Description**: Nhập `Allow EC2 to access RDS`.
7. Nhấp nút màu cam **Save rules** để áp dụng thay đổi.

![RDS Security Group Edit 1](/images/5-Workshop/5.4-Connect-EC2-RDS/image3.png)
![RDS Security Group Edit 2](/images/5-Workshop/5.4-Connect-EC2-RDS/image15.png)
![RDS Security Group Edit 3](/images/5-Workshop/5.4-Connect-EC2-RDS/image4.png)
![RDS Security Group Edit 4](/images/5-Workshop/5.4-Connect-EC2-RDS/image13.png)

---

#### Bước 3: Kết nối SSH vào Máy chủ EC2 và Cài đặt Môi trường Runtime
1. Mở phần mềm Terminal/SSH trên máy tính cá nhân (MobaXterm, PuTTY, hoặc VS Code Terminal).
2. Kết nối tới máy chủ EC2 bằng cặp khóa `wms-server-key` đã tải về ở Module 2:
   ```bash
   ssh -i "wms-server-key.pem" ubuntu@54.169.12.125
   ```

![SSH to EC2](/images/5-Workshop/5.4-Connect-EC2-RDS/image7.png)

3. Cập nhật danh sách gói hệ thống Ubuntu:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

![Ubuntu Update](/images/5-Workshop/5.4-Connect-EC2-RDS/image5.png)

4. Cài đặt môi trường Node.js 20 LTS, Git, và trình quản lý tiến trình PM2:
   ```bash
   # Tải và cài đặt NodeSource Node.js 20.x
   curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
   sudo apt-get install -y nodejs git build-essential

   # Kiểm tra phiên bản Node.js và npm
   node -v
   npm -v
   ```

![Nodejs Install](/images/5-Workshop/5.4-Connect-EC2-RDS/image14.png)

5. Cài đặt PM2 toàn cục (Global):
   ```bash
   sudo npm install -g pm2
   ```

![PM2 Install](/images/5-Workshop/5.4-Connect-EC2-RDS/image10.png)

---

#### Bước 4: Triển khai Mã nguồn Backend NestJS và Cấu hình Biến Môi trường (.env)
1. Tải mã nguồn `logistics-backend` từ GitHub repository về máy chủ EC2:
   ```bash
   git clone https://github.com/vantra-ai/logistics-backend.git
   cd logistics-backend
   ```

![Git Clone Backend](/images/5-Workshop/5.4-Connect-EC2-RDS/image9.png)

2. Cài đặt toàn bộ gói phụ thuộc (Dependencies):
   ```bash
   npm install
   ```

![NPM Install](/images/5-Workshop/5.4-Connect-EC2-RDS/image1.png)

3. Tạo và chỉnh sửa file cấu hình biến môi trường `.env`:
   ```bash
   nano .env
   ```
   Dán bộ thông số cấu hình kết nối chuẩn vào file `.env` (Thay thế `DB_HOST` bằng Endpoint thực tế thu được ở Bước 1):
   ```env
   # --- DATABASE CONFIGURATION (Amazon RDS) ---
   DB_HOST=<YOUR_RDS_ENDPOINT> # Ví dụ: wms-pro-db.xxxxxx.ap-southeast-1.rds.amazonaws.com
   DB_PORT=5432
   DB_USER=postgres
   DB_PASS=<YOUR_MASTER_PASSWORD>
   DB_NAME=logistics
   DB_SSL=false

   # --- SECURITY CONFIGURATION ---
   JWT_SECRET=<YOUR_JWT_SECRET_KEY>

   # --- MAIL SERVICE (Nodemailer OTP) ---
   MAIL_HOST=smtp.gmail.com
   MAIL_PORT=587
   MAIL_USER=<YOUR_EMAIL_ADDRESS>
   MAIL_PASS=<YOUR_GMAIL_APP_PASSWORD>
   MAIL_FROM="WMS Logistics Pro" <<YOUR_EMAIL_ADDRESS>>
   ```

   {{% notice warning %}}
   ⚠️ **Cảnh báo Bảo mật (Security Notice):** Khi công khai tài liệu hoặc mã nguồn lên GitHub, **tuyệt đối KHÔNG hardcode** các thông tin nhạy cảm như Mật khẩu Database thực tế, JWT Secret Key, hoặc Mật khẩu ứng dụng Email. Hãy sử dụng các giá trị giữ chỗ (Placeholder) như mẫu trên và đảm bảo tệp `.env` chứa thông tin thật trên máy chủ EC2 luôn được bảo mật.
   {{% /notice %}}
   *(Nhấn `Ctrl + O` $
ightarrow$ `Enter` để lưu, sau đó nhấn `Ctrl + X` để thoát editor Nano).*

4. Thực hiện biên dịch mã nguồn NestJS sang JavaScript sản xuất:
   ```bash
   npm run build
   ```

![NPM Run Build](/images/5-Workshop/5.4-Connect-EC2-RDS/image8.png)

5. Khởi chạy ứng dụng Backend dưới dạng dịch vụ ngầm với PM2:
   ```bash
   pm2 start dist/main.js --name wms-api

   # Thiết lập PM2 tự động khởi động cùng hệ điều hành
   pm2 save
   pm2 startup
   ```

![PM2 Start](/images/5-Workshop/5.4-Connect-EC2-RDS/image6.png)

---

#### Bước 5: Kiểm thử API và Swagger Documentation
1. Kiểm tra trạng thái tiến trình chạy ngầm của PM2:
   ```bash
   pm2 status
   ```
   *(Đảm bảo tiến trình `wms-api` hiển thị trạng thái `online` màu xanh).*
2. Mở trình duyệt web trên máy tính cá nhân và truy cập vào đường dẫn Swagger UI:
   `http://54.169.12.125:3333/api`
3. Màn hình giao diện **Logistics API - Swagger Documentation** hiển thị danh sách toàn bộ các danh mục Endpoints (`auth`, `orders`, `shipments`, `locations`, `wallets`, v.v.) chứng tỏ hệ thống đã kết nối Database thành công và vận hành ổn định.

---

### 3. Tổng kết Module 3

Sau khi hoàn thành Module 3, bạn đã đạt được:
* Trích xuất thành công RDS Endpoint chính xác và cấu hình phân quyền truy cập cổng `5432` trên Security Group.
* Chuẩn bị môi trường vận hành tiêu chuẩn trên máy chủ Ubuntu EC2 với Node.js 20, Git và PM2.
* Cấu hình biến môi trường kết nối mượt mà giữa ứng dụng Backend NestJS và CSDL Cloud RDS PostgreSQL.
* Kích hoạt dịch vụ Backend API chạy liên tục 24/7 trên cổng `3333` sẵn sàng phục vụ cho Web App (Next.js) và Mobile App (Flutter).
