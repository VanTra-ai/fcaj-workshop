---
title: "Worklog Tuần 4"
date: 2026-07-12
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

- Nắm vững tư duy phân loại tài nguyên hệ thống, làm chủ kỹ năng gán nhãn dữ liệu (Tagging) khoa học và tự động hóa quản lý nhóm máy chủ lớn thông qua bộ lọc thông minh AWS Resource Groups.
- Xây dựng giải pháp giám sát tập trung (Observability). Thuần thục quy trình thu thập dữ liệu (Metrics & Logs), thiết lập cảnh báo chủ động (Alarms) qua email và thiết kế Dashboard trực quan để kiểm soát sức khỏe hệ thống theo thời gian thực.
- Thấu hiểu nguyên lý thiết kế ứng dụng chịu lỗi cao (Fault-tolerant) và tự phục hồi (High Availability). Triển khai hệ thống tự động co giãn theo tải thực tế bằng cách tách biệt các phân vùng mạng (Public/Private Subnets) kết hợp bộ cân bằng tải.
- Tiếp cận mô hình dịch vụ quản lý máy chủ trọn gói (VPS) với chi phí cố định tối ưu. Thành thạo quy trình triển khai đa ứng dụng, thiết lập bảo mật tầng sâu, sao lưu hệ thống và nâng cấp tài nguyên không gây gián đoạn dịch vụ.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                       |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ------------------------------------ |
| 2   | - Thực hành tạo máy ảo t3.micro và gán nhãn quản trị dữ liệu (Tag) trực tiếp trên giao diện Console.<br>- Cấu hình các cặp thẻ Tag phân loại tài nguyên: Owner, Service, Environment, BusinessUnit.<br>- Thực hành quản lý thẻ bằng AWS CLI qua các câu lệnh create-tags, run-instances, và create-volume.<br>- Lọc và kiểm tra danh sách tài nguyên đã gắn thẻ qua lệnh CLI describe-instances.<br>- Khởi tạo nhóm quản trị MarketingBU dạng Tag-based group để gom nhóm tự động các máy ảo EC2.<br>- Tiến hành dọn dẹp tài nguyên lab: Terminate toàn bộ EC2 và Delete Resource Group vừa tạo.                                                                                                                             | 11/05/2026   | 11/05/2026      | https://000027.awsstudygroup.com/vi/ |
| 3   | - Triển khai hạ tầng giám sát mẫu thông qua dịch vụ AWS CloudFormation Stack.<br>- Phân tích chỉ số CPUUtilization, EBSWriteBytes, đổi trục hiển thị (Y axis) và thêm các đường đánh dấu ngang/dọc.<br>- Thực hành viết biểu thức tìm kiếm SEARCH() và biểu thức toán học SORT() để trích xuất chỉ số nâng cao.<br>- Kiểm tra nhật ký hệ thống, cấu hình rút ngắn thời gian lưu trữ log (Retention setting) về 1 tuần.<br>- Viết lệnh truy vấn log lỗi qua Logs Insights và tạo Metric Filter từ khóa ERROR để chuyển log thành số liệu.<br>- Thiết lập cảnh báo email qua AWS SNS, tích hợp đồ thị vào CloudWatch Dashboard và thực hiện xóa stack.                                                                         | 12/05/2026   | 12/05/2026      | https://000008.awsstudygroup.com/vi/ |
| 4   | - Thiết lập hạ tầng mạng VPC AutoScaling-Lab gồm 3 AZs, chia 3 public subnets và 3 private subnets.<br>- Cấu hình Security Group cho ứng dụng (mở cổng 22, 80, 443, 5000) và cho cơ sở dữ liệu RDS (mở cổng 3306).<br>- Khởi chạy máy chủ EC2 FCJ-Management thuộc public subnet và kết nối SSH.<br>- Khởi tạo cơ sở dữ liệu MySQL Multi-AZ trên Amazon RDS, thực hiện kết nối và import bảng dữ liệu mẫu.<br>- Cài đặt môi trường Node.js, clone source code, cấu hình file biến môi trường và chạy ứng dụng web qua PM2.<br>- Chuẩn bị và upload kịch bản dữ liệu giả lập lên CloudWatch Custom Metrics để phục vụ tính năng Predictive Scaling.                                                                           | 13/05/2026   | 13/05/2026      | https://000006.awsstudygroup.com/vi/ |
| 5   | - Tạo bản sao lưu AMI từ máy chủ EC2 hiện tại và thiết lập cấu hình Launch Template tiêu chuẩn.<br>- Khởi tạo Target Group cổng 5000 và cấu hình Application Load Balancer phân phối tải qua 3 public subnets.<br>- Thiết lập Auto Scaling Group (Desired: 1, Min: 1, Max: 3) và tích hợp Amazon SNS gửi thông báo tự động.<br>- Kiểm thử tính năng Auto Scaling thông qua việc giả lập lượng truy cập lớn bằng công cụ WebStress.<br>- Thực hành cấu hình 4 cơ chế scale: thủ công (Manual), theo lịch (Scheduled), động (Dynamic), và dự báo (Predictive).                                                                                                                                                                 | 14/05/2026   | 14/05/2026      | https://000006.awsstudygroup.com/vi/ |
| 6   | - Khởi tạo cơ sở dữ liệu MySQL tách rời có tính sẵn sàng cao Workshop-DB-Instance trên Amazon Lightsail.<br>- Khởi tạo cụm 3 máy ảo WordPress, PrestaShop, Akaunting và gán địa chỉ IP tĩnh (Static IP) cố định cho từng instance.<br>- SSH vào máy ảo, chạy mã kịch bản tự động để trỏ toàn bộ kết nối dữ liệu ứng dụng về database trung tâm.<br>- Tăng cường bảo mật tầng sâu bằng cách xóa hẳn cổng SSH (Port 22) khỏi Firewall của cả 3 máy ảo Lightsail.<br>- Bật tính năng Automated Snapshots và thực hành nâng cấp quy mô (Migration) máy ảo lên gói tài nguyên lớn hơn không downtime.<br>- Thiết lập cảnh báo tự động gửi email khi chỉ số CPU burst capacity (percentage) của hệ thống giảm xuống mức nguy hiểm. | 15/05/2026   | 15/05/2026      | https://000045.awsstudygroup.com/vi/ |

### Kết quả đạt được tuần 4:

- Quản trị tài nguyên hiệu quả:
  - Triển khai thành công hệ thống gắn nhãn (Tagging) khoa học trên quy mô lớn, hỗ trợ truy vấn và phân loại tài nguyên nhanh chóng.
  - Vận hành tốt AWS Resource Groups để quản lý tập trung các tài nguyên theo bộ phận hoặc dự án, giúp đơn giản hóa quy trình vận hành.

- Xây dựng hệ thống giám sát và cảnh báo thông minh:
  - Thành thạo kỹ thuật hiển thị metrics, tùy chỉnh đồ thị chuyên sâu (trục Y phụ, annotations) và sử dụng các biểu thức toán học (Math Expressions) để phân tích dữ liệu.
  - Cấu hình thành công CloudWatch Logs Insights để truy vấn lỗi ứng dụng từ log file; thiết lập Metric Filters để chuyển đổi log thành chỉ số đo lường.
  - Xây dựng hệ thống CloudWatch Alarms kết hợp với AWS SNS để gửi thông báo kịp thời khi hệ thống gặp sự cố, đảm bảo uptime.

- Triển khai kiến trúc ứng dụng co giãn (Scalable Backend):
  - Thành công trong việc đóng gói ứng dụng (Custom AMI) và khởi tạo kiến trúc Multi-AZ, giúp ứng dụng có khả năng tự phục hồi và chịu tải cao.
  - Cấu hình Auto Scaling Group phối hợp với Application Load Balancer để tự động điều chỉnh số lượng máy chủ dựa trên tải CPU thực tế, tối ưu hóa trải nghiệm người dùng.

- Tối ưu vận hành với Amazon Lightsail:
  - Triển khai đồng loạt các ứng dụng (WordPress, PrestaShop, Akaunting) cùng cơ sở dữ liệu dùng chung với chi phí tối ưu.
  - Áp dụng thành công các Best Practices về bảo mật (tắt port SSH, port không cần thiết) và quản lý vận hành (chuyển tầng Snapshot, nâng cấp instance không downtime).
  - Thiết lập hệ thống cảnh báo dựa trên chỉ số CPU burst capacity để theo dõi tình trạng tài nguyên máy chủ theo thời gian thực.
