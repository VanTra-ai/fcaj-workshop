---
title: "Event 2"
date: 2026-07-12
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

# Bài thu hoạch “FCAJ Community Day: Data Driven, AI Risen”

### Mục Đích Của Sự Kiện

- Chia sẻ các góc nhìn thực tế, bài toán thực tiễn từ môi trường doanh nghiệp về việc ứng dụng AI và Cloud.
- Cập nhật xu hướng phát triển của các thế hệ AI Agent (Voice AI, DevOps AI, Amazon Q) và cách AI đang định hình lại thị trường việc làm IT.
- Hướng dẫn giải pháp kiến trúc và kỹ thuật: từ việc chọn kiến trúc Single/Multi-Agent đến việc thiết lập bảo mật kết nối (Security) cho hệ thống AI của doanh nghiệp.

### Danh Sách Diễn Giả

- **Steve Trần** - CTO/Founder, Cloud Thinker
- **Danh Hiếu Nghị** - AI Engineer, Renova Cloud
- **Trần Tuấn Kiệt** - AI Engineer, AWS Student Builder Group
- **Vũ Quốc Trung** - CEO, Revve AI
- **Phan Thị Bảo & Nguyễn Đình Nguyên** - Cloud Engineers, Cloud Kinetics
- **Trần Nhật Trường (Wayne) & Đặng Thị Minh Anh** - Solution Sales, Noventiq
- **Nguyễn Tấn Toàn** - AWS Security Builder

### Nội Dung Nổi Bật

#### Sự chuyển dịch nghề nghiệp và giải pháp AI cho Vận hành Cloud (Aentic Platform)

- AI đang đẩy nhanh tốc độ code nhưng lại tạo ra "nút thắt cổ chai" ở khâu QA/QC và vận hành hạ tầng.
- Cloud Thinker giới thiệu giải pháp AI Agent giúp tự động hóa Incident Management, Code Review hạ tầng, FinOps và Security Testing.
- Single Agent vs Multi-Agent: Single Agent nếu thiết kế tốt có thể giải quyết 95% bài toán. Multi-Agent phức tạp hơn nhưng cần thiết để giải quyết bài toán Role-Based Access Control (RBAC) và giới hạn context window.

#### Xây dựng Voice AI Agent (Đại lý AI bằng giọng nói)

- Phân tích 2 kiến trúc: Speech-to-Speech trực tiếp vs Kiến trúc 3 thành phần (STT -> LLM -> TTS).
- Đối với Tiếng Việt (low resource), kiến trúc 3 thành phần tối ưu hơn giúp ngân hàng/doanh nghiệp kiểm soát nội dung AI nói và hỗ trợ thực thi tác vụ (Tool Calling) chính xác.
- Thách thức thực tế: Xử lý độ trễ (cần dùng Streaming), nhận diện giới tính để xưng hô (Anh/Chị), và ngữ cảnh ngắt lời (Interruption).

#### AWS DevOps AI Agent - Gỡ rối hệ thống tự động

- Giải quyết vấn đề "Fragmented telemetry" (Log bị phân mảnh) khiến kỹ sư mất nhiều thời gian tìm lỗi.
- Quy trình 4 bước của Agent: Triage (Phân loại) -> Investigation (Điều tra) -> Mitigation (Đề xuất giải quyết) -> Improvement (Cải thiện).
- Nhấn mạnh nguyên tắc an toàn: AI chỉ đưa ra đề xuất (recommend), con người là người phê duyệt và thực thi.

#### Ứng dụng Amazon Q Business trong Nhân sự (HR)

- Giải quyết bài toán tốn thời gian sàng lọc CV thủ công, dễ bỏ sót nhân tài và đánh giá cảm tính.
- Amazon Q giúp tự động hóa việc tạo Job Description (JD), trích xuất thông tin CV, chấm điểm đối chiếu và xuất báo cáo so sánh ứng viên cực kỳ nhanh chóng và bảo mật.

#### Bảo mật kết nối giữa Amazon Q và MCP Server

- Đưa AI vào doanh nghiệp không thể dùng Public Endpoint vì rủi ro DDoS và bắt gói tin (Man-in-the-Middle).
- Giải pháp: Đặt MCP Server trong Private Subnet. Dùng VPC Connection qua Interface Endpoint kết hợp Route53 Resolver và Application Load Balancer (ALB) để Amazon Q truy cập nội bộ một cách an toàn (Private Connection).

### Những Gì Học Được

#### Tư Duy Thiết Kế & Vận Hành

- **AI Support, Not Replace**: AI là công cụ hỗ trợ để tăng productivity, không thể thay thế quyết định của con người trong các môi trường Production có rủi ro cao.
- **Hiểu bản chất vấn đề**: Đừng chỉ dựa dẫm vào output của AI. Cần có kiến thức nền tảng vững chắc để validate lại kết quả mà AI trả về (Đặc biệt trong DevOps và Data).

#### Kiến Trúc Kỹ Thuật

- **Observability là xương sống**: DevOps AI Agent chỉ hoạt động tốt khi hệ thống có tính quan sát tốt (Ghi nhận đủ Log, Metric, Tracing).
- **Kiến trúc Voice AI**: Nắm được luồng xử lý Streaming từ Speech-to-Text qua LLM và Text-to-Speech để giảm thiểu Latency trong tương tác thời gian thực.
- **Zero Trust Security**: Bất kỳ kết nối nào từ SaaS (như Amazon Q) vào hệ thống nội bộ (MCP Server) đều phải được quy hoạch qua Private Network (VPC, Private Subnet).

#### Chiến Lược Tích Hợp AI

- Ứng dụng AI cần phải tính đến rủi ro "ảo giác" (Hallucination) bằng cách giới hạn Agent Space và cung cấp deterministic rules rõ ràng.

### Ứng Dụng Vào Công Việc / Học Tập

- **Nâng cấp Project cá nhân**: Thay vì chỉ làm ứng dụng CRUD thông thường, sẽ tìm hiểu và tích hợp thêm MCP (Model Context Protocol) để AI có thể chọc vào DB hoặc hệ thống bên ngoài.
- **Security First**: Áp dụng tư duy thiết kế mạng Private Subnet và VPC khi làm đồ án môn học liên quan đến Cloud, không mở Public Endpoint bừa bãi.
- **Cải thiện CV ứng tuyển**: Tối ưu hóa CV với các keyword rõ ràng vì hiện tại CV vòng đầu tiên thường được Screening bằng AI chứ không phải con người.

### Trải nghiệm trong event

Tham gia workshop **“FCAJ Community Day”** mở ra cho tôi một bức tranh hoàn toàn mới về cách AI đang thực sự được ứng dụng trong các hệ thống doanh nghiệp lớn (Enterprise), vượt xa việc chỉ dùng AI để "chat" thông thường. Một số trải nghiệm nổi bật:

#### Học hỏi từ chuyên gia hàng đầu

- Việc lắng nghe trực tiếp từ Founder/CTO và các Senior Engineer giúp tôi nhận ra các khoảng trống kiến thức (gap) giữa trường học và thực tế doanh nghiệp, đặc biệt là trong khâu vận hành, chi phí và bảo mật.

#### Trải nghiệm kỹ thuật thực tế

- Vô cùng ấn tượng với màn Live Demo Voice AI gọi hỏi đáp trực tiếp bằng giọng nói về sản phẩm MacBook. Nó giúp tôi hình dung rõ ràng độ khó của việc xử lý độ trễ (latency) và ngữ cảnh ngắt lời.
- Phiên Live Demo giả lập một cuộc tấn công DDoS và cách DevOps Agent phân tích Log để tìm ra Root Cause thực sự mang lại cảm giác của một môi trường Production thực chiến.

#### Ứng dụng công cụ hiện đại

- Thấy được sức mạnh thực sự của Amazon Q khi nó tự động phân tích hàng loạt CV ứng viên và tạo ra bảng chấm điểm chỉ trong vài chục giây.

#### Kết nối và trao đổi

- Sự kiện có rất nhiều câu hỏi hay từ người tham dự, giúp tôi hiểu thêm rằng trong thực tế, bên cạnh Tech thì Business Problem mới là bài toán gốc rễ cần giải quyết.

#### Bài học rút ra

- Tốc độ phát triển của AI là quá nhanh. Đừng dùng AI để giải những bài toán cũ bằng tay, hãy dùng AI để khuếch đại năng lực và giải quyết những bài toán phức tạp hơn.
- Công nghệ/Công cụ (Tool) có thể thay đổi, nhưng nguyên lý kiến trúc (Architecture) và bảo mật (Security) là những nền tảng không bao giờ lỗi thời.
- Cơ hội nghề nghiệp không giảm đi, nhưng tiêu chuẩn đang tăng lên rất cao (Cần Senior + AI). Sinh viên cần phải liên tục trau dồi và có những "Side Projects" thực tế chất lượng cao.

#### Một số hình ảnh khi tham gia sự kiện
