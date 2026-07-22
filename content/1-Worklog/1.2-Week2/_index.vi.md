---
title: "Worklog Tuần 2"
date: 2026-07-12
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

- Nắm vững cách thiết kế và triển khai môi trường mạng cô lập trong AWS, hiểu rõ cơ chế định tuyến, subnetting và kết nối Internet.
- Làm chủ hai công cụ tường lửa là Security Groups (Stateful) và Network ACLs (Stateless) để bảo vệ tài nguyên ở mức Instance và Subnet.
- Thực hành xây dựng các mô hình kết nối phức tạp: Site-to-Site VPN (Hybrid Cloud), VPC Peering (kết nối nội bộ giữa các VPC) và Transit Gateway.
- Tích hợp hệ thống DNS giữa môi trường On-premise giả lập (Managed AD) và AWS thông qua Route 53 Resolver (Inbound/Outbound Endpoints).

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                                                                                                                                                                                                                                                             | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                                                                                                   |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ---------------------------------------------------------------------------------------------------------------- |
| 2   | - Tìm hiểu tổng quan về Amazon VPC: kiến trúc mạng ảo tách biệt, dải địa chỉ IP (CIDR), cách phân đoạn mạng với Subnet, bảng định tuyến (Route Table) và Internet Gateway.<br>- Nghiên cứu cơ chế tường lửa trong VPC: Security Group (stateful) và Network ACLs (stateless) để bảo vệ tài nguyên.<br>- Khám phá kiến trúc Multi-AZ, NAT Gateway để cho phép truy cập Internet một chiều từ Private Subnet.                           | 27/04/2026   | 27/04/2026      | https://000003.awsstudygroup.com/vi/<br>https://www.youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i |
| 3   | - Thực hành tạo VPC & EC2:<br>+Khởi tạo VPC ASG (10.10.0.0/16), tạo 2 Public Subnet và 2 Private Subnet trên 2 AZ khác nhau.<br>+ Cấu hình Route Table: Public (kết nối IGW) và Private (kết nối NAT Gateway).<br>+ Triển khai 2 máy chủ EC2 Public (kết nối Internet trực tiếp) và EC2 Private (SSH thông qua EC2 Public).<br>+ Cấu hình Security Group cho phép SSH và ICMP, kiểm tra thông tuyến giữa 2 máy chủ.                   | 28/04/2026   | 28/04/2026      | https://000003.awsstudygroup.com/vi/<br>https://www.youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i |
| 4   | - Nghiên cứu mô hình Hybrid Cloud và AWS Site-to-Site VPN: Vai trò của Virtual Private Gateway (VGW) và Customer Gateway (CGW).<br>- Thực hành VPN:<br>+ Thiết lập kết nối VPN tunnel giữa 2 VPC (mô phỏng chi nhánh on-premise).<br>+ Cấu hình VPN thông qua thiết bị EC2 chạy phần mềm StrongSwan/Libreswan.<br>+ Thực hành cấu hình file ipsec.conf, ipsec.secrets và kiểm tra tunnel kết nối thành công qua lệnh Ping IP Private. | 29/04/2026   | 29/04/2026      | https://000003.awsstudygroup.com/vi/<br>https://www.youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i |
| 5   | - Thiết lập Hybrid DNS với Route 53:<br>+ Nghiên cứu cơ chế DNS Hybrid: Outbound/Inbound Endpoints và Resolver Rules.<br>+ Khởi tạo AWS Managed Microsoft AD để giả lập hệ thống DNS on-premise.<br>+ Cấu hình Outbound Endpoint và Resolver Rule để forward truy vấn onprem.example.com sang AD.<br>+ Cấu hình Inbound Endpoint để phân giải DNS ngược lại từ AD về AWS.<br>+ Kiểm thử DNS qua nslookup và Resolve-DnsName           | 30/04/2026   | 30/04/2026      | https://000010.awsstudygroup.com/vi/<br>https://www.youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i |
| 6   | - Thực hành VPC Peering & NACL:<br>+ Thiết lập VPC Peering giữa My VPC và HG VPC.<br>+ Cấu hình NACL cho subnet của HG VPC, giới hạn source IP chỉ cho phép traffic từ My VPC (172.31.0.0/16).<br>+ Kích hoạt tính năng Cross-Peer DNS để phân giải IP Private qua tên DNS khi peering.<br>+ Dọn dẹp: Terminate EC2, xóa Peering Connection, Security Groups và CloudFormation Stacks liên quan.                                      | 01/05/2026   | 01/05/2026      | https://000019.awsstudygroup.com/vi/<br>https://www.youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i |

### Kết quả đạt được tuần 2:

- Kiến thức VPC & Network:
  - Hiểu rõ cách thiết kế mạng theo tiêu chuẩn Well-Architected Framework: sử dụng đa vùng khả dụng (Multi-AZ) và phân tách Public/Private Subnet
  - Thành thạo quản lý tường lửa: Thiết lập Security Groups cho các tầng ứng dụng (Web server, Database) và áp dụng NACL để lọc traffic mức Subnet
  - Cấu hình thành công NAT Gateway và Internet Gateway để quản lý lưu lượng truy cập Internet cho các tài nguyên

- Kiến thức về Kết nối Hybrid & Peering:
  - Triển khai thành công Site-to-Site VPN với mô hình IPsec Tunnel (StrongSwan), cho phép giao tiếp an toàn giữa môi trường giả lập On-premise và AWS
  - Thiết lập VPC Peering, hiểu rõ hạn chế của transitive peering và cách kích hoạt Cross-Peer DNS để phân giải tên miền giữa các VPC
  - Nắm vững cách quản trị Routing Table và Route Propagation để điều hướng traffic nội bộ

- Kỹ năng Hệ thống & Công cụ:
  - Xây dựng hệ thống DNS Hybrid với Route 53 Resolver, kết nối hiệu quả với dịch vụ AWS Managed Microsoft AD
  - Làm quen với VPC Reachability Analyzer để kiểm tra đường đi của gói tin và VPC Flow Logs để giám sát/phát hiện các truy cập bất thường
  - Vận hành thành thạo Infrastructure as Code (CloudFormation) để triển khai hạ tầng mạng một cách nhất quán và có thể lặp lại
  - Thực hành dọn dẹp tài nguyên (Terminate EC2, Release EIP, Delete Gateway/Peering) nhằm tối ưu chi phí thực tập
