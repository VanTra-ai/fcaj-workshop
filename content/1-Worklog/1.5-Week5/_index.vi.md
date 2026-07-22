---
title: "Worklog Tuần 5"
date: 2026-07-12
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

- Nắm vững cách phân phối website tĩnh, sử dụng CDN để tăng tốc và bảo mật dữ liệu, đồng thời làm chủ các tính năng nâng cao như quản lý phiên bản (Versioning) để bảo vệ dữ liệu.
- Hiểu rõ phương pháp luận về dự phòng thảm họa (RPO/RTO) và cách tự động hóa quy trình sao lưu, phục hồi, gửi thông báo trạng thái cho toàn bộ hệ thống tài nguyên trên Cloud.
- Thành thạo quy trình di chuyển máy ảo (Migration) giữa môi trường ảo hóa on-premises (VMware) và đám mây Amazon EC2.
- Hiểu cách kết nối và đồng bộ dữ liệu mượt mà giữa ổ đĩa mạng nội bộ của doanh nghiệp với kho lưu trữ đám mây S3.
- Làm chủ giải pháp lưu trữ tệp tin dùng chung được quản lý toàn phần, tích hợp Windows Active Directory cho các ứng dụng doanh nghiệp lớn.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                       |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ------------------------------------ |
| 2   | - Nghiên cứu lý thuyết lưu trữ đối tượng (Object Storage) S3, các lớp lưu trữ (Storage Classes) và tính năng Access Points.<br>- Khởi tạo S3 Bucket tại Singapore, tải lên mã nguồn và cấu hình tính năng Static Website Hosting.<br>- Phân quyền truy cập công khai cho tệp tin trang web thông qua Block Public Access và Object ACLs.<br>- Tích hợp CDN Amazon CloudFront để tăng tốc tải trang web tĩnh và chặn quyền truy cập trực tiếp vào S3.<br>- Kích hoạt S3 Versioning để lưu trữ đa phiên bản, thực hành xóa và cứu hộ khôi phục dữ liệu gốc.<br>- Thực hiện di chuyển đối tượng (Move) sang bucket mới và tiến hành dọn dẹp xóa sạch tài nguyên lab. | 18/05/2026   | 18/05/2026      | https://000057.awsstudygroup.com/vi/ |
| 3   | - Nghiên cứu lý thuyết quản lý sao lưu tập trung, các chỉ số phục hồi RPO/RTO và các chiến lược Disaster Recovery.<br>- Triển khai nhanh hạ tầng Lab tự động (EC2, SNS, Lambda) bằng dịch vụ AWS CloudFormation.<br>- Khởi tạo Backup Vault và thiết lập Backup Plan cấu hình lịch trình sao lưu tự động dựa trên thẻ nhãn Tag.<br>- Tích hợp dịch vụ AWS SNS để tự động gửi thông báo qua Email khi trạng thái backup/restore hoàn tất.<br>- Thực hiện kiểm thử khôi phục dữ liệu từ bản sao lưu và theo dõi nhật ký hoạt động trên CloudWatch Logs.                                                                                                             | 19/05/2026   | 19/05/2026      | https://000013.awsstudygroup.com/vi/ |
| 4   | - Nghiên cứu lý thuyết dịch vụ VM Import/Export và quy trình chuyển dịch hệ thống (Migration) lên đám mây.<br>- Cấu hình máy ảo Ubuntu local trên VMware Workstation và xuất thành file đĩa ảo định dạng .ova/.vmdk.<br>- Tạo S3 Bucket và sử dụng AWS CLI để upload file đĩa ảo từ máy tính cá nhân lên Cloud lưu trữ.<br>- Thiết lập IAM Role (vmimport) và gán Trust Relationship cho phép dịch vụ truy xuất tệp tin trên S3.<br>- Sử dụng lệnh aws ec2 import-image để convert file đĩa ảo thành Custom AMI và theo dõi qua CLI.<br>- Khởi chạy EC2 mới từ AMI đã convert thành công, kiểm tra hệ thống và tiến hành xóa sạch tài nguyên lab.                 | 20/05/2026   | 20/05/2026      | https://000014.awsstudygroup.com/vi/ |
| 5   | - Nghiên cứu lý thuyết giải pháp lưu trữ lai (Hybrid Storage) và các loại AWS Storage Gateway.<br>- Khởi tạo S3 Bucket làm kho lưu trữ dữ liệu gốc cho cổng kết nối Storage Gateway.<br>- Khởi chạy máy chủ EC2 sử dụng ảnh đĩa Gateway AMI chuyên dụng và gắn thêm ổ EBS 150 GiB làm Cache.<br>- Cấu hình Storage Gateway, tạo SMB File Share liên kết với S3 Bucket và mở tính năng truy cập Guest.<br>- Thực hiện ánh xạ (mount) File Share thành ổ đĩa mạng Z: trên máy trạm Windows và kiểm tra đồng bộ lên S3.                                                                                                                                              | 21/05/2026   | 21/05/2026      | https://000024.awsstudygroup.com/vi/ |
| 6   | - Nghiên cứu lý thuyết Amazon FSx cho Windows File Server, giao thức SMB và tính năng chống trùng lặp dữ liệu.<br>- Triển khai hạ tầng mạng VPC và thiết lập dịch vụ Directory Service (AWS Managed Microsoft AD).<br>- Khởi tạo hệ thống tệp tin Amazon FSx, cấu hình dung lượng lưu trữ và tích hợp vào domain Active Directory.<br>- Khởi chạy máy chủ EC2 Windows Client và tiến hành thực hiện join domain AD để xác thực.<br>- Thực hiện mount ổ đĩa chia sẻ FSx trên máy Windows Client qua giao thức SMB và kiểm tra đọc/ghi dữ liệu.                                                                                                                     | 22/05/2026   | 22/05/2026      | https://000025.awsstudygroup.com/vi/ |

### Kết quả đạt được tuần 5:

- Làm chủ S3 Static Hosting và CDN CloudFront:
  - Triển khai thành công website du lịch tĩnh lên S3, cấu hình tăng tốc qua CloudFront giúp tối ưu độ trễ tải trang từ mốc ~600ms xuống mốc kinh ngạc ~13ms nhờ các Edge Location tại Việt Nam.
  - Bật tính năng S3 Versioning thành công, lưu trữ đa phiên bản của tệp tin giúp hệ thống có khả năng tự khôi phục dữ liệu nguyên vẹn kể cả khi bị Ransomware tấn công ghi đè.
  - Thực hiện thành công việc di chuyển (Move) toàn bộ object sang một bucket mới cùng vùng nhanh chóng.

- Tự động hóa data với AWS Backup:
  - Thiết lập thành công cụm hạ tầng tự động qua CloudFormation. Khởi tạo chính xác Backup Vault và Backup Plan tự động quét tài nguyên theo thẻ nhãn Tag.
  - Cấu hình thành công AWS SNS gửi email thông báo tự động cho đội Vận hành mỗi khi tiến hành tạo bản sao lưu hoặc khôi phục dữ liệu hoàn tất.

- Chuyển đổi máy ảo On-premise lên Cloud qua VM Import/Export:
  - Xây dựng thành công máy ảo Ubuntu local trên VMware Workstation, đóng gói xuất thành file đĩa ảo .vmdk và upload lên S3.
  - Tạo thành công IAM role vmimport và sử dụng AWS CLI convert file đĩa ảo thành Custom AMI, từ đó khởi chạy một EC2 Instance trên Cloud hoạt động ổn định.

- Triển khai ổ đĩa mạng lai với Storage Gateway:
  - Cấu hình thành công cụm máy chủ ảo Storage Gateway trên EC2 kết hợp bộ nhớ Cache đệm 150 GiB.
  - Tạo thành công cụm chia sẻ dữ liệu SMB File Share liên kết S3, mount thành công ổ đĩa mạng Z: trên máy tính local và đồng bộ dữ liệu trực tiếp lên đám mây.

- Vận hành File Server doanh nghiệp với Amazon FSx:
  - Triển khai thành công cụm quản lý thư mục AWS Managed Microsoft Active Directory và hệ thống tệp tin cậy cao Amazon FSx for Windows Multi-AZ.
  - Khởi chạy máy chủ EC2 Windows Client, thực hiện join domain AD và mount thành công ổ đĩa mạng FSx để đọc/ghi file chia sẻ an toàn.
