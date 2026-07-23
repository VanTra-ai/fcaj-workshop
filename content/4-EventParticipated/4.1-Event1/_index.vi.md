---
title: "Event 1"
date: 2026-07-12
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Bài thu hoạch “FCAI workshop”

### Mục Đích Của Sự Kiện

- Chia sẻ các phương pháp, công cụ học tập và thực hành các dịch vụ AWS hiệu quả, tiết kiệm chi phí cho người mới bắt đầu.
- Truyền cảm hứng và kinh nghiệm thực chiến từ các cuộc thi Hackathon để sinh viên tự tin bước ra khỏi vùng an toàn.
- Giới thiệu case study thực tế về việc phát triển dự án phần mềm (SaaS tích hợp AI) và tầm quan trọng của tư duy DevOps trong làm việc nhóm.
- Giải quyết các rào cản tâm lý của sinh viên và người đi làm trẻ: vượt qua hội chứng kẻ mạo danh, xây dựng sự tự tin và bẻ gãy thói quen trì hoãn.

### Danh Sách Diễn Giả

- **Huỳnh Thái Linh** - Sinh viên
- **Nhóm The Bowler (Huỳnh An Khương, Mai Quốc Anh, Nguyễn Trần Minh Quân)** - Sinh viên Đại học FPT
- **Nguyễn Thị Quỳnh Như** - Sinh viên năm cuối, Đại học HUTECH
- **Trần Nghĩa** - Cựu sinh viên Swinburne / AI & ML Developer (Founder dự án Tử vi Đại Việt)
- **Trần Minh Quân** - Sinh viên ĐH FPT / Freelance Web App Developer
- **Phạm Phát Uy** - Sinh viên Đại học Việt Đức (VGU)

### Nội Dung Nổi Bật

#### Chiến lược thực hành AWS không lo tốn phí

- Kết hợp AWS Cloud Quest (game 3D trực quan) để nắm tư duy kiến trúc và Floci / LocalStack (giả lập môi trường AWS trên local) để test code miễn phí trước khi deploy lên hạ tầng cloud thật.

#### Giải mã sức mạnh của Hackathon

- Hackathon không chỉ là cuộc thi code, mà là nơi rèn luyện áp lực (như thức trắng 36h tại VNG Lotus Hackathon), mở rộng networking, và làm đẹp CV.
- Bài học cốt lõi: Đừng sợ thiếu kinh nghiệm, hãy cứ tham gia để "learning by doing" và luôn nhớ phải có phần "Demo" sản phẩm.

#### Case study: Dự án SaaS "Tử Vi Đại Việt" (Tích hợp AI)

- Biến kiến thức sách vở truyền thống thành web app tâm lý học.
- Xử lý vấn đề "ảo giác" (hallucination) của AI bằng cách kết hợp Deterministic rules (quy tắc đóng cứng từ sách) và Vector Database (RAG) trước khi đưa qua LLM (Claude 3.5 Sonnet).

#### Tảng băng chìm DevOps trong dự án

- Lỗi code (bug) hay deploy fail chỉ là bề nổi. Phần chìm gây thất bại dự án là: yêu cầu mơ hồ, thiếu giao tiếp (miscommunication), quy trình thủ công và thiếu Ownership.
- 4 nguyên tắc DevOps: Collaboration (hợp tác vô can), Automation (tự động hóa), Fast Feedback (phản hồi nhanh) và Continuous Improvement.

#### Thấu hiểu Tâm lý học ứng dụng (Sự tự tin & Sự trì hoãn)

- Sự tự tin: Cảnh báo về hội chứng Imposter Syndrome và Dunning-Kruger (rơi vào thung lũng tuyệt vọng khi học kỹ năng mới).
- Sự trì hoãn: Trì hoãn không phải do lười, mà là rào cản tâm lý (sợ sai, sợ đánh giá). Não bộ chọn thỏa mãn ngắn hạn để trốn tránh áp lực.

### Những Gì Học Được

#### Tư Duy & Tâm Lý (Mindset & Psychology)

- **Action creates confidence**: Sự tự tin là kết quả của hành động, không phải là điều kiện để bắt đầu. Đừng chờ đợi sự hoàn hảo.
- **Bản chất của sự trì hoãn**: Hiểu được cuộc chiến giữa vỏ não trước trán (tư duy dài hạn) và hệ thống viền (cảm xúc ngắn hạn) để không còn tự dán nhãn bản thân là "kẻ lười biếng".

#### Kiến Trúc & Kỹ Thuật (Tech & Architecture)

- **Môi trường giả lập (Local)**: Cách dùng Docker, Boto3, Terraform kết hợp với Floci để chạy thử 50+ dịch vụ cơ bản của AWS ngay trên máy cá nhân.
- **Kiến trúc AI an toàn**: Cách luân chuyển luồng dữ liệu (Input -> Post Parser -> Vector Search/RAG -> LLM -> Validation) để AI đưa ra câu trả lời chính xác, thay vì chỉ dùng prompt thông thường.

#### Chiến Lược Làm Việc Team & Phát Triển Cá Nhân

- Công cụ (CI/CD, Docker) rất quan trọng, nhưng con người và quy trình làm việc (DevOps mindset) mới quyết định sự thành bại của dự án.
- Quy tắc 5 giây (để đưa ra quyết định hành động ngay) và Quy tắc 5 phút (chỉ bắt đầu làm việc trong 5 phút để phá vỡ sức ỳ ban đầu).

### Ứng Dụng Vào Công Việc

- **Tối ưu chi phí thực hành AWS** Cài đặt ngay Floci/LocalStack. Từ nay, mọi bài lab AWS sẽ được code và test ở môi trường local trước để đảm bảo script chạy đúng, sau đó mới deploy lên tài khoản AWS thật.
- **Đẩy mạnh Networking & Cọ xát thực tế**: Lên kế hoạch tìm team để đăng ký ít nhất 1 cuộc thi Hackathon trong năm nay nhằm lấy trải nghiệm thực chiến và thêm project vào CV.
- **Cải thiện làm việc nhóm**: Áp dụng tư duy DevOps vào nhóm: rõ ràng trong requirement, tăng cường trao đổi liên tục giữa Dev và BA/QA để tránh phải làm lại (re-work) do hiểu sai ý nhau.
- **Quản trị bản thân**: Bắt đầu áp dụng "Quy tắc 5 phút" mỗi khi đối mặt với một task khó hoặc khi cảm thấy muốn lướt mạng xã hội trốn tránh deadline.

### Trải nghiệm trong event

Tham gia buổi **“FCAI workshop”** mang lại cho tôi những cảm xúc rất chân thật và gần gũi, vì các diễn giả đều là những sinh viên, cựu sinh viên đi trước, chia sẻ từ chính những khó khăn mà tôi đang gặp phải. Một số trải nghiệm nổi bật:

#### Học hỏi từ những thất bại thực tế

- Cảm thấy rất "thấm" khi nghe câu chuyện chia sẻ về việc quên xóa tài nguyên AWS dẫn đến mất 70 USD tiền oan. Những kinh nghiệm đau thương này giúp tôi tránh được những cái bẫy cơ bản nhất khi mới học Cloud.
- Nghe trải nghiệm thực tế từ nhóm The Bowler về 36 giờ code liên tục tại Hackathon truyền cho tôi rất nhiều động lực và sự "nhiệt huyết" của tuổi trẻ.

#### Trải nghiệm kỹ thuật thực tế

- Được mở mang tầm mắt với dự án Tử vi Đại Việt. Việc thấy một dự án mang tính tâm linh, cổ học lại được giải quyết bằng các stack công nghệ hiện đại nhất (Next.js, Supabase, LLM, Vector Database, RAG) cho thấy sức sáng tạo không giới hạn của việc ứng dụng công nghệ.

#### Cú "tát" về tâm lý học

- Phần nói về "Tảng băng chìm của sự trì hoãn" thực sự như đang miêu tả chính bản thân tôi. Việc được giải thích dưới góc độ khoa học thần kinh thay vì những lời khuyên sáo rỗng đã giúp tôi thực sự hiểu tại sao mình hay chần chừ và biết cách thoát khỏi vòng lặp đó.

#### Kết nối và trao đổi

- Nhận ra tầm quan trọng của việc chủ động (Visibility). Việc giao tiếp, đặt câu hỏi không chỉ để giải quyết thắc mắc mà còn là bước đầu tiên để tạo network, gieo những mầm mống cơ hội cho sự nghiệp sau này

#### Bài học rút ra

- Đi học là trả tiền để được sai, đi làm là được trả tiền để không làm sai. Hãy tận dụng tối đa thời gian trên trường và các dự án cá nhân để thử nghiệm và mắc lỗi.
- AI chỉ là công cụ khuếch đại (amplify). Nếu nền tảng rỗng, kết quả sẽ sai lệch. Đừng dùng AI để "outsource" sự thấu hiểu của chính mình.
- Đừng để nỗi sợ (sợ sai, sợ bị đánh giá, sợ thất bại) đóng băng tương lai của bạn. Cứ làm đi, vừa xây vừa sửa (Go Build).

#### Một số hình ảnh khi tham gia sự kiện

![Event picture](/images/event1.JPG)
