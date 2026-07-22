---
title: "Worklog Tuần 3"
date: 2026-07-12
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

- Hiểu và cấu hình định tuyến thủ công trên TGW để kết nối mạng tập trung cho nhiều VPC, thay thế hoàn toàn mô hình VPC Peering phức tạp.
- Quản lý và kết nối an toàn đến máy chủ Private/Public không cần Bastion Host, SSH Key hay mở các cổng nhạy cảm (22, 3389).
- Thành thạo quản trị máy chủ (đổi cấu hình, tạo Snapshot, đóng gói Custom AMI), xử lý sự cố mất Key Pair và triển khai thực tế ứng dụng Node.js CRUD.
- Áp dụng IAM Policies (JSON) để phân quyền theo nguyên tắc đặc quyền tối thiểu, kiểm soát chặt chẽ khu vực, dòng máy và quyền xóa tài nguyên.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                       |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ------------------------------------ |
| 2   | - Khởi tạo kiến trúc kết nối 4 VPC thông qua hub trung tâm AWS Transit Gateway.<br>- Tạo Transit Gateway và cấu hình các Transit Gateway Attachments cho 4 VPC.<br>- Thiết lập Transit Gateway Route Tables (cấu hình Associations và Propagations).<br>- Thêm các route trỏ về Transit Gateway vào bảng định tuyến (Route Tables) của từng VPC để thông luồng mạng.                                                                                                                   | 04/05/2026   | 04/05/2026      | https://000020.awsstudygroup.com/vi/ |
| 3   | - Chuẩn bị hạ tầng VPC, Security Group, khởi tạo Public Linux EC2 và Private Windows EC2.<br>- Tạo IAM Role cấp quyền AmazonSSMManagedInstanceCore và AmazonS3FullAccess cho EC2.<br>- Tạo các VPC Interface Endpoints (ssm, ssmmessages, ec2messages) và S3 Gateway Endpoint để Private EC2 có thể giao tiếp với Systems Manager mà không cần Internet.<br>- Cấu hình lưu trữ Session logs trên S3 bucket.<br>- Thực hiện Port Forwarding qua Session Manager để kết nối RDP an toàn. | 05/05/2026   | 05/05/2026      | https://000058.awsstudygroup.com/vi/ |
| 4   | - Nghiên cứu kiến trúc phân lớp EC2, các loại Instance, lưu trữ (EBS, Instance Store), và cơ chế Key Pair.<br>- Chuẩn bị VPC, Subnet (Auto-assign public IP) và Security Group riêng biệt cho môi trường Linux và Windows.<br>- Khởi tạo máy chủ Amazon Linux và kết nối thông qua SSH (sử dụng MobaXterm hoặc PuTTY).<br>- Khởi tạo máy chủ Microsoft Windows Server và kết nối thông qua RDP.                                                                                        | 06/05/2026   | 06/05/2026      | https://000004.awsstudygroup.com/vi/ |
| 5   | - Thay đổi cấu hình Instance Type.<br>- Tạo và quản lý EBS Snapshots, khởi tạo Custom AMI (sử dụng Sysprep cho Windows).<br>- Xử lý sự cố mất Key Pair: Khôi phục quyền truy cập EC2 Windows bằng AWS Systems Manager (Run Command) và khôi phục EC2 Linux bằng EC2 User Data.<br>- Triển khai ứng dụng Node.js (CRUD) trên Amazon Linux: Cài đặt LAMP stack, phpMyAdmin, Node.js qua nvm và cấu hình database.                                                                        | 07/05/2026   | 07/05/2026      | https://000004.awsstudygroup.com/vi/ |
| 6   | - Viết các IAM Policy (JSON) để giới hạn sử dụng tài nguyên nhằm tối ưu hóa chi phí (Cost Governance).<br>- Phân quyền cho phép người dùng chỉ được khởi tạo EC2 tại một Region cụ thể (Singapore).<br>- Giới hạn khởi tạo EC2 theo Instance Family (t3, t4g, m5), Instance type (t3.small, t3.large) và loại ổ cứng EBS (gp3).<br>- Giới hạn quyền xóa (Terminate) EC2 theo địa chỉ IP của doanh nghiệp và theo khoảng thời gian chỉ định.                                            | 08/05/2026   | 08/05/2026      | https://000004.awsstudygroup.com/vi/ |

### Kết quả đạt được tuần 3:

- Kiến thức và Triển khai Mạng tập trung (TGW):
  - Khởi tạo thành công Transit Gateway đóng vai trò "Cloud Router" trung tâm, thay thế hoàn toàn cấu trúc VPC Peering phức tạp khi mở rộng hệ thống.
  - Kết nối thành công 4 VPC độc lập vào bộ định tuyến trung tâm và cấu hình chính xác các bảng định tuyến của từng VPC để kích hoạt giao tiếp liên VPC.
  - Thiết lập thành công Transit Gateway Route Tables thông qua việc cấu hình thủ công các cơ chế Associations và Propagations để kiểm soát chặt chẽ luồng lưu lượng.

- Kiểm soát truy cập bảo mật (Systems Manager):
  - Kết nối an toàn đến Public Linux EC2 qua Session Manager mà không cần mở cổng 22, đảm bảo lưu lượng mạng chỉ đi qua HTTPS (port 443).
  - Thiết lập các VPC Interface Endpoints (ssm, ssmmessages, ec2messages) và S3 Gateway Endpoint để quản lý máy chủ Windows hoàn toàn không có Internet.
  - Tự động hóa việc đẩy Session logs ghi lại lịch sử câu lệnh về S3 bucket, đồng thời thực hiện Port Forwarding qua SSM để Remote Desktop (RDP) vào máy chủ Windows Private.

- Vận hành EC2 nâng cao và triển khai ứng dụng:
  - Thực hiện nâng cấp tài nguyên (Instance Type), tạo bản sao lưu EBS Snapshots và đóng gói Custom AMI chuẩn (sử dụng Sysprep trên Windows) để khởi chạy máy chủ mới không bị lỗi.
  - Cứu hộ thành công máy chủ Windows bị mất Key Pair bằng SSM Run Command (EC2Rescue) và khôi phục quyền truy cập máy chủ Linux bằng cách ghi đè Public Key qua EC2 User Data.
  - Cấu hình thành công môi trường Web Server (LAMP trên Linux, XAMPP trên Windows), cài đặt phpMyAdmin và triển khai chạy thực tế ứng dụng Node.js CRUD kết nối cơ sở dữ liệu.

- Quản trị chi phí và bảo mật tầng sâu (IAM):
  - Xây dựng chính sách JSON ép buộc người dùng chỉ được thao tác dịch vụ EC2 tại Singapore (ap-southeast-1) và tự động từ chối (Deny) khi thao tác ở các vùng khác.
  - Cấu hình điều kiện StringNotLike để giới hạn người dùng chỉ được chọn các dòng máy giá rẻ (t3, t4g, m5), loại máy nhỏ (t3.small, t3.large) và bắt buộc sử dụng ổ cứng thế hệ mới gp3.
  - Ngăn chặn quyền xóa máy chủ (ec2:TerminateInstances) và chỉ cho phép thực hiện khi thỏa mãn đồng thời hai điều kiện: truy cập từ IP tĩnh của văn phòng và nằm ngoài khung giờ đóng băng hệ thống.
  - Vận hành quy trình dọn dẹp triệt để toàn bộ tài nguyên thực hành (EC2, AMI, Snapshot, Key Pair, VPC, IAM) để tránh phát sinh chi phí ngoài ý muốn.
