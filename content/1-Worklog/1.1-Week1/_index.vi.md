---
title: "Worklog Tuần 1"
date: 2026-07-12
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Mục tiêu tuần 1:

- Làm quen với các thành viên trong First Cloud AI Journey (FCAJ); thấu hiểu lộ trình học tập, tiêu chuẩn dự án thực tế và quy định tại đơn vị thực tập.
- Tiếp cận tư duy Cloud Computing, hạ tầng toàn cầu (Region, AZ, Edge Location) và các phương thức tương tác tài nguyên (Console, CLI, SDK).
- Nắm vững kiến thức định danh IAM, phân quyền nhóm quản trị và tuân thủ các nguyên tắc bảo mật cơ bản (MFA, Access Key).
- Làm quen với môi trường Free Tier kết hợp các công cụ Budget để giám sát chi phí, hiểu quy trình vận hành hệ thống support case của AWS.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                                                                                                                                           |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2   | - Gia nhập mạng lưới cộng đồng (WhatsApp, Facebook, LinkedIn) phục vụ học tập và trao đổi.<br>- Kết nối, giao lưu với các thành viên chương trình FCAJ.<br>- Đọc và ghi nhận các nội quy làm việc, tìm hiểu yêu cầu tốt nghiệp.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | 20/04/2026   | 20/04/2026      |                                                                                                                                                          |
| 3   | - Tìm hiểu định nghĩa và 4 lợi ích lớn của Điện toán đám mây (Cloud Computing).<br>- Phân tích hạ tầng AWS: Cấu trúc Data Center, Region, AZ (tính sẵn sàng cao với tối thiểu 3 AZ/Region) và Local Zone tại Việt Nam kết nối sang Singapore.<br>- Làm quen giao diện AWS Management Console, tìm hiểu tổng quan CLI phục vụ tự động hóa và vai trò Serialization/Retrying của AWS SDK.<br>- Nghiên cứu công cụ phát triển phần mềm bằng trợ lý AI – AWS Kiro (Kiro IDE, Agent Hook, Steering files, Rollback checkpoint).                                                                                                                                                                                                                                                                                                                                                                                                                                                       | 21/04/2026   | 21/04/2026      | https://www.youtube.com/playlist?list=PLahN4TLWtox3TSYFbN1DNX7NZgTVXNj3x                                                                                 |
| 4   | - Nghiên cứu tài liệu phân biệt Free Plan vs Paid Plan và chiến lược nhận 200 USD Credit.<br>- Khởi tạo tài khoản AWS Free Tier và thiết lập thiết bị xác thực đa yếu tố ảo (Virtual MFA Device).<br>- Thực hành IAM Console: Khởi tạo admin-group (gán Policy AdministratorAccess) và admin-user (bật chính sách đổi mật khẩu lần đầu), tải và lưu trữ an toàn file credential .csv.<br>- Kiểm tra đăng nhập ẩn danh qua Sign-in Link, thực hành tạo Access Key cho CLI và các thao tác quản trị vòng đời key (Deactivate/Delete).<br>- Nghiên cứu sơ lược về IAM Role và cấu trúc phân quyền hệ thống.                                                                                                                                                                                                                                                                                                                                                                         | 22/04/2026   | 22/04/2026      | https://000001.awsstudygroup.com/vi/<br>https://www.youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i                                         |
| 5   | - Triển khai chiến dịch thực hành chuỗi 5 nhiệm vụ tích lũy Credit từ widget Explore AWS tại trang chủ console.<br>+ Task 1 (EC2): Khởi tạo thành công máy ảo Test Instance, cấu hình key pair first-kp (.pem), Security Group và thực hiện Terminate sau khi hoàn thành.<br>+ Task 2 (Bedrock): Thử nghiệm chat playground với mô hình Claude 3 Haiku, thực hiện mở case hỗ trợ Bedrock Allowlisting với AWS Support khi gặp lỗi Authorization.<br>+ Task 3 (Budgets): Thiết lập ngân sách chi phí hàng tháng My Monthly Cost Budget ($100) đính kèm email nhận cảnh báo tự động ở các ngưỡng 85% và 100%. <br>+ Task 4 (Lambda): Xây dựng serverless web application chạy Node.js bằng Blueprint mẫu, kích hoạt Public Function URL và tiến hành Delete function an toàn.<br>+ Task 5 (RDS): Khởi tạo nhanh cụm database quan hệ mẫu Aurora (PostgreSQL Compatible) cho môi trường Dev/Test và thực hiện đúng quy trình xóa cụm cluster sau khi đổi trạng thái sang Available. | 23/04/2026   | 23/04/2026      | https://000001.awsstudygroup.com/vi/<br>https://www.youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i                                         |
| 6   | - Nghiên cứu cấu trúc vận hành của AWS Support qua 4 gói dịch vụ (Basic, Business Support+, Enterprise, Unified Operations).<br>- Tìm hiểu quy trình quản lý support case và 3 nhóm trường hợp lỗi phổ biến (Thanh toán, Nâng hạn mức, Hỗ trợ kỹ thuật).<br>- Mở rộng lý thuyết AWS Budgets (Cost, Usage, RI, Savings Plans Budget) và thực hành tạo Custom ngân sách nâng cao kết hợp dọn dẹp (Clean up) tài nguyên lab.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | 24/04/2026   | 24/04/2026      | https://000007.awsstudygroup.com/vi/<br>https://000009.awsstudygroup.com/vi/<br>https://www.youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i |

### Kết quả đạt được tuần 1:

- Hiểu AWS là gì, nắm vững kiến thức hạ tầng toàn cầu (Region, AZ, Local Zone) và các nhóm dịch vụ cơ bản:
  - Compute (EC2, Lambda)
  - Database (RDS - Aurora PostgreSQL)
  - Management & Governance (Budgets, AWS Support)
  - Artificial Intelligence (Amazon Bedrock, AWS Kiro)

- Đã tạo và cấu hình AWS Free Tier account thành công, đi kèm các thiết lập bảo mật chuẩn:
  - Bật Virtual MFA cho tài khoản Root
  - Tạo IAM Group và IAM User phân quyền quản trị

- Làm quen với AWS Management Console và biết cách tìm, truy cập, sử dụng dịch vụ từ giao diện web.

- Thực hành cấu hình, quản lý danh tính và khóa truy cập bao gồm:
  - Access Key
  - Secret Key
  - Quản lý vòng đời Key (Khởi tạo, Deactivate, Delete)

- Sử dụng AWS Console để thực hiện các thao tác cơ bản và hoàn thành chuỗi nhiệm vụ nhận 200$ Credit:
  - Tạo, kết nối và xóa máy chủ ảo EC2
  - Tạo và quản lý key pair (định dạng .pem cho SSH)
  - Gửi Support Case yêu cầu cấp quyền truy cập mô hình AI
  - Thiết lập các Budget (Ngân sách) cảnh báo chi phí và mức sử dụng qua Email
  - Khởi tạo hàm Serverless Lambda và cụm Cơ sở dữ liệu RDS

- Có khả năng kết nối giữa lý thuyết hạ tầng mạng và thao tác trên giao diện web để quản lý tài nguyên AWS song song, ý thức được tầm quan trọng của việc dọn dẹp (Clean up) tài nguyên sau khi thực hành

- Nắm rõ văn hóa làm việc nhóm và lộ trình phát triển của chương trình FCAJ
