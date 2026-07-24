---
title: "Module 1: Triển khai CSDL Amazon RDS PostgreSQL"
date: 2026-07-15
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

### 1. Giới thiệu Module

{{% notice info %}}
**Amazon RDS (Relational Database Service)** là dịch vụ cơ sở dữ liệu quan hệ được AWS quản lý toàn phần (Managed Service). RDS tự động hóa các tác vụ quản trị tốn thời gian như cấp phát hạ tầng, sao lưu (backup), vá lỗi phần mềm (patching) và khôi phục khi gặp sự cố.

Trong hệ thống **Logistics WMS Pro**, tầng Cơ sở dữ liệu đóng vai trò lưu trữ toàn bộ dữ liệu quan trọng: đơn hàng, thông tin kho bãi, số dư ví tài xế, lịch sử theo dõi và mã vận đơn. Chúng ta sẽ sử dụng PostgreSQL để đảm bảo tính toàn vẹn giao dịch (ACID) và tương thích hoàn hảo với ORM (TypeORM) trên máy chủ Backend NestJS.
{{% /notice %}}

{{% notice tip %}}
**Pro Tip:** Tận dụng AWS Free Tier, bạn được cung cấp 750 giờ/tháng chạy Amazon RDS (với các dòng instance `db.t2.micro` hoặc `db.t4g.micro`) cùng 20GB dung lượng lưu trữ General Purpose SSD (`gp2`/`gp3`) hoàn toàn miễn phí trong 12 tháng đầu tiên.
{{% /notice %}}

---

### 2. Quy trình Triển khai Chi tiết

#### Bước 1: Truy cập Dịch vụ Amazon RDS
1. Đăng nhập vào AWS Management Console.
2. Trên thanh tìm kiếm chính ở đầu trang (`[Alt+S]`), nhập từ khóa **RDS** hoặc **Aurora and RDS**.
3. Nhấp chọn dịch vụ **Aurora and RDS (Managed Relational Database Service)** từ danh sách kết quả.

![Truy cập Dịch vụ Amazon RDS](/images/5-Workshop/5.2-RDS-PostgreSQL/image4.png)

---

#### Bước 2: Chuyển đến Trang Khởi tạo Cơ sở Dữ liệu
1. Tại bảng điều khiển RDS Dashboard, ở menu điều hướng bên trái, chọn **Databases**.
2. Nhấp vào nút **Create database** màu cam ở góc trên bên phải.
3. Chọn chế độ cấu hình **Full configuration** để tùy chỉnh toàn bộ các tham số mạng và bảo mật.

![Chuyển đến Trang Khởi tạo Cơ sở Dữ liệu](/images/5-Workshop/5.2-RDS-PostgreSQL/image9.png)

---

#### Bước 3: Cấu hình Chi tiết Thông số Database

##### 2.1. Engine Options & Creation Method
* **Engine type**: Chọn **PostgreSQL**.
* **Choose a database creation method**: Chọn **Full configuration** (đảm bảo kiểm soát được VPC và Database Name).

![Engine Options](/images/5-Workshop/5.2-RDS-PostgreSQL/image6.png)

##### 2.2. Templates & Availability
* **Templates**: Chọn gói **Free tier** (Hệ thống sẽ tự động tối ưu các tùy chọn để không phát sinh chi phí).
* **Availability and durability**: Hệ thống mặc định chọn **Single-AZ DB instance deployment** (1 instance) giúp tiết kiệm tài nguyên Free Tier.

![Templates Free Tier](/images/5-Workshop/5.2-RDS-PostgreSQL/image3.png)

##### 2.3. Cấu hình Định danh & Thông tin Xác thực (Settings & Credentials)
* **Engine version**: Giữ nguyên phiên bản mặc định mới nhất (ví dụ: PostgreSQL 18.3-R2 hoặc tương đương).
* **DB instance identifier**: Nhập `wms-pro-db`.
* **Master username**: Nhập `postgres`.
* **Credentials management**: Chọn **Self managed**.
* **Master password**: Nhập mật khẩu quản trị (Ví dụ: `WmsPro2026Password!`).
* **Confirm master password**: Nhập lại mật khẩu để xác nhận.

![Settings and Credentials](/images/5-Workshop/5.2-RDS-PostgreSQL/image10.png)
![Master Password Setup](/images/5-Workshop/5.2-RDS-PostgreSQL/image1.png)

{{% notice warning %}}
⚠️ **Lưu ý quan trọng:** Hãy lưu lại Master Username (`postgres`) và Master Password ở nơi an toàn. Đây là thông tin bắt buộc để khai báo vào biến môi trường `DB_USER` và `DB_PASS` trong file `.env` của Backend NestJS.
{{% /notice %}}

##### 2.4. Cấu hình Máy chủ & Lưu trữ (Instance & Storage)
* **DB instance class**: Chọn lớp máy chủ **Burstable classes (includes t classes)** $
ightarrow$ Chọn `db.t4g.micro` hoặc `db.t2.micro` (Có nhãn *Free tier eligible*).
* **Storage type**: Chọn **General Purpose SSD (gp2)**.
* **Allocated storage**: Nhập `20` (GiB) - Định mức tối đa chuẩn Free Tier.

![Instance and Storage](/images/5-Workshop/5.2-RDS-PostgreSQL/image7.png)

##### 2.5. Cấu hình Mạng & Kết nối (Connectivity)
* **Compute resource**: Chọn **Don’t connect to an EC2 compute resource** (Chúng ta sẽ tự kết nối thủ công qua Security Group sau).
* **Virtual private cloud (VPC)**: Chọn **Default VPC**.
* **Public access**: Chọn **Yes**.

{{% notice note %}}
**Security Note:** Việc bật `Public access = Yes` ở bước này phục vụ cho việc kiểm thử, chạy lệnh Seed dữ liệu địa giới hành chính (Vietnam Provinces/Wards) và truy vấn trực tiếp từ máy trạm tính cá nhân. Ở Module 3, chúng ta sẽ siết chặt chốt chặn Inbound Rule của Security Group chỉ cho phép duy nhất IP của EC2 truy cập.
{{% /notice %}}

* **VPC security group (firewall)**: Chọn **Create new**.
* **New VPC security group name**: Nhập `wms-rds-sg`.

![Connectivity Configuration](/images/5-Workshop/5.2-RDS-PostgreSQL/image2.png)
![Public Access and Security Group](/images/5-Workshop/5.2-RDS-PostgreSQL/image11.png)

##### 2.6. Cấu hình Tên Cơ sở Dữ liệu Ban đầu (Additional Configuration)
1. Cuộn xuống cuối trang, mở rộng mục **Additional configuration**.
2. Tại mục **Database options** $
ightarrow$ **Initial database name**: Nhập chính xác là `logistics`.

![Initial Database Name](/images/5-Workshop/5.2-RDS-PostgreSQL/image5.png)

{{% notice warning %}}
CRITICAL: Nếu bỏ trống mục **Initial database name**, Amazon RDS sẽ chỉ khởi tạo Instance rỗng mà không tạo sẵn Database schema. Backend NestJS khi khởi chạy sẽ báo lỗi database `"logistics" does not exist`. Bắt buộc phải điền `logistics` tại bước này!
{{% /notice %}}

---

#### Bước 4: Khởi chạy và Kiểm tra Trạng thái
1. Rà soát lại toàn bộ thông số cấu hình.
2. Nhấp vào nút **Create database** màu cam ở cuối trang.
3. Hệ thống sẽ chuyển về danh sách Databases. Trạng thái của `wms-pro-db` ban đầu sẽ là `Creating`. Quá trình này thường mất từ 5 - 10 phút để AWS khởi tạo phần cứng và gán IP.
4. Sau khi trạng thái chuyển sang `Available`, nhấp vào tên `wms-pro-db` để lấy thông tin **Endpoint** (Đường dẫn kết nối) và **Port** (`5432`).

![Create Database Complete](/images/5-Workshop/5.2-RDS-PostgreSQL/image8.png)

---

### 3. Tổng kết Module 1

Trong Module này, bạn đã triển khai thành công:
* Cụm cơ sở dữ liệu quan hệ **Amazon RDS for PostgreSQL** (`wms-pro-db`) chạy trên hạ tầng Free Tier tối ưu chi phí.
* Tạo sẵn cơ sở dữ liệu gốc `logistics` tương thích 100% với TypeORM Entity của mã nguồn Backend.
* Thiết lập nhóm bảo mật `wms-rds-sg` chuẩn bị cho việc phân quyền SG-to-SG với máy chủ EC2.
