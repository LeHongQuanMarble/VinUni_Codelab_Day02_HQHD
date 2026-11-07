# 03 — AI Log & Reflection

---

## 1. Mục đích

Ghi lại trung thực quá trình sử dụng ChatGPT và Gemini làm **thought-partner** trong quá trình phân tích bài toán Xanh SM Intelligent EV Battery Emergency Support.

Tập trung vào việc AI đã hỗ trợ những công việc nào, những câu trả lời nào chưa đáng tin cậy, cách tôi kiểm tra thông tin và những điều chỉnh đã thực hiện để đảm bảo giải pháp phù hợp với nghiệp vụ và an toàn vận hành.

---

## 2. Nhật ký tương tác với AI

| # | Giai đoạn | Yêu cầu với AI | AI làm gì | Kiểm tra và quyết định | Kết quả |
|---|---|---|---|---|---|
| 1 | Problem Scan | Phân tích các cơ hội ứng dụng AI trong hệ sinh thái Vingroup | Đề xuất các bài toán liên quan đến vận hành Xanh SM, phản hồi khách hàng, phân loại dữ liệu và hỗ trợ nghiệp vụ | So sánh các bài toán theo actor, pain point, business impact và khả năng ứng dụng AI | Chọn bài toán hỗ trợ điều phối viên xử lý sự cố pin yếu |
| 2 | Problem Selection | So sánh các bài toán và chọn một vấn đề để phát triển | Giúp làm rõ vai trò của điều phối viên và các khó khăn khi tiếp nhận báo cáo pin yếu | Ưu tiên bài toán có quy trình rõ ràng, có thể xây dựng prototype và có ranh giới AI cụ thể | Chọn Intelligent EV Battery Emergency Support |
| 3 | Workflow Analysis | Mô tả quy trình xử lý sự cố pin yếu hiện tại | Chia quy trình thành các bước: tiếp nhận báo cáo, xác minh thông tin xe, tìm phương án hỗ trợ, phối hợp và phản hồi tài xế | Nhận thấy các bước và thời gian xử lý do AI đề xuất chưa có dữ liệu vận hành thực tế xác nhận | Xác định bước tìm kiếm và đối chiếu phương án hỗ trợ là bottleneck giả định cần kiểm chứng |
| 4 | Problem Statement | Hoàn thiện Problem Statement theo 6 trường thông tin | Hỗ trợ xác định actor, workflow, bottleneck, business impact, metrics và operational boundary | Phân biệt dữ liệu thực tế với mục tiêu pilot và giả định. Không sử dụng mục tiêu đề xuất như baseline đã đo | Hoàn thiện Problem Statement cho bài toán pin yếu |
| 5 | AI Fit | Xác định phần nào nên dùng LLM, Rule-based và Agentic AI | Đề xuất LLM để đọc hiểu báo cáo, trích xuất thông tin và tạo bản nháp; Rule-based để kiểm tra điều kiện an toàn | Kiểm tra xem quyết định liên quan đến ngưỡng pin và điều phối có nên giao cho LLM hay không | Chọn kết hợp LLM và Rule-based; không triển khai Agentic Loop trong prototype |
| 6 | Prompt & Prototype Design | Thiết kế System Prompt và prototype xử lý báo cáo sự cố | Hỗ trợ xây dựng vai trò AI, định dạng đầu ra JSON và các giới hạn xử lý | Rà soát các trường hợp thiếu GPS, thiếu phần trăm pin, dữ liệu không hợp lệ và yêu cầu vượt quyền | Bổ sung quy tắc không tự suy đoán dữ liệu và không tự thực hiện hành động bên ngoài |
| 7 | Adversarial Testing | Xây dựng các tình huống kiểm thử nhằm kiểm tra giới hạn AI | Hỗ trợ đề xuất các đầu vào có thông tin thiếu, nội dung yêu cầu bỏ qua quy tắc và tình huống pin nguy cấp | Đánh giá phản hồi theo System Prompt và kiểm tra xem AI có bịa dữ liệu hoặc vượt quyền hay không | Bổ sung các tình huống kiểm thử để đánh giá độ tin cậy của prototype |
| 8 | Readiness Assessment | Đánh giá khả năng triển khai thực tế | Hỗ trợ xây dựng checklist về dữ liệu, rủi ro, stakeholder và khả năng vận hành | Nhận thấy chưa có baseline, log vận hành, error rate và xác nhận từ stakeholder | Chọn NOT YET; tiếp tục prototype offline trước khi xem xét triển khai |

---

## 3. AI đã giúp gì?

- **Phân tích và cấu trúc vấn đề:** Giúp chuyển một tình huống nghiệp vụ tương đối rộng thành Problem Statement có actor, workflow, bottleneck và business impact rõ ràng.
- **Xây dựng workflow:** Chia quy trình xử lý sự cố thành các bước cụ thể, giúp nhận diện công đoạn có khả năng tiêu tốn nhiều thời gian nhất.
- **Định hướng kiến trúc AI:** Giúp phân biệt nhiệm vụ phù hợp với LLM và các quy tắc bắt buộc phải được kiểm soát bằng code.
- **Thiết kế prompt:** Hỗ trợ xây dựng System Prompt, JSON output và các giới hạn để giảm nguy cơ AI tự suy đoán thông tin.
- **Thiết kế kiểm thử:** Gợi ý các tình huống adversarial nhằm kiểm tra khả năng tuân thủ ranh giới của AI.
- **Đánh giá khả năng triển khai:** Giúp xây dựng checklist để nhận diện những điều kiện còn thiếu trước khi đưa prototype vào môi trường thực tế.

---

## 4. AI đã sai hoặc chưa đáng tin ở đâu?

- **Số liệu workflow chưa được xác minh:** AI đề xuất thời gian cho từng bước xử lý và tổng thời gian 22 phút mỗi sự cố. Đây chỉ là số liệu minh họa, không phải dữ liệu đo được tại Xanh SM. Tôi giữ chúng dưới dạng giả định và không dùng làm baseline thực tế.
- **Nguy cơ suy đoán dữ liệu:** Nếu báo cáo không có GPS hoặc phần trăm pin, LLM có thể tạo câu trả lời có vẻ hoàn chỉnh dù thiếu thông tin đầu vào. Điều này không thể chấp nhận trong quy trình hỗ trợ sự cố.
- **Đề xuất không phù hợp với tình trạng pin:** Nếu không có quy tắc kiểm soát, AI có thể đề xuất tìm trạm sạc ngay cả khi xe đang ở tình trạng pin nguy cấp.
- **Khả năng vượt giới hạn:** Prompt thông thường chưa đủ để đảm bảo AI không làm theo yêu cầu tự gửi tin nhắn, điều phối xe hoặc xác nhận hành động chưa được thực hiện.
- **Metrics chưa có baseline:** Các mục tiêu như tạo bản nháp dưới 2 phút, JSON hợp lệ từ 99% trở lên và chặn 100% đề xuất trạm sạc khi pin dưới 5% là mục tiêu thiết kế/pilot, không phải kết quả đã được kiểm chứng.
- **Khả năng phụ thuộc vào API:** Nếu model API lỗi, quá tải hoặc trả về dữ liệu không đúng schema, hệ thống có thể không xử lý được báo cáo theo cách mong muốn.

---

## 5. Tôi đã sửa gì?

- Xác định rõ AI chỉ là công cụ hỗ trợ điều phối viên, không thay thế người ra quyết định.
- Điều chỉnh System Prompt để AI chỉ trích xuất thông tin có trong đầu vào, không tự tạo GPS, mức pin hoặc trạng thái chuyến đi.
- Chuyển các điều kiện an toàn như ngưỡng pin dưới 5% sang Rule-based code thay vì phụ thuộc vào LLM.
- Bổ sung quy tắc khi pin dưới 5%: chặn đề xuất di chuyển đến trạm sạc và đưa ra quy trình hỗ trợ phù hợp để điều phối viên xem xét.
- Thiết lập Human-in-the-loop: mọi bản nháp phải được con người kiểm tra và phê duyệt trước khi sử dụng.
- Xác định fallback về quy trình thủ công khi thiếu dữ liệu, API gặp lỗi hoặc JSON không hợp lệ.
- Phân biệt rõ số liệu giả định, mục tiêu pilot và dữ liệu thực tế trong tài liệu.

---

## 6. Phản ánh cá nhân

- **AI giúp tôi nhanh nhất ở đâu:** Phân tích bài toán, cấu trúc workflow, xây dựng Problem Statement và thiết kế các tình huống kiểm thử.
- **AI làm tôi dễ tin nhầm ở đâu:** Những con số và đề xuất được diễn đạt tự tin nhưng chưa có dữ liệu thực tế chứng minh.
- **Tôi đã học được gì:** Một câu trả lời hợp lý về mặt ngôn ngữ không đồng nghĩa với một quyết định đúng về mặt nghiệp vụ. Đặc biệt với các tình huống liên quan đến an toàn xe điện, không thể để LLM tự quyết định.
- **Tôi sẽ thay đổi cách làm việc thế nào:** Yêu cầu nguồn cho các số liệu, phân biệt giả định với dữ liệu đã xác minh, kiểm tra đầu ra bằng code và thử các tình huống adversarial trước khi tin tưởng kết quả.
- **Điều tôi chưa chắc:** Chưa có dữ liệu vận hành thực tế và phản hồi từ điều phối viên Xanh SM để xác nhận bottleneck, baseline thời gian xử lý và hiệu quả thực sự của giải pháp.

**Kết luận:** Qua bài Lab, tôi nhận ra giá trị của AI không chỉ nằm ở khả năng tạo câu trả lời mà còn ở cách con người kiểm soát, xác minh và giới hạn nó. Với bài toán này, LLM phù hợp để hỗ trợ đọc hiểu và soạn thảo, trong khi các quyết định an toàn phải được kiểm soát bằng business rules và con người. Vì chưa đủ bằng chứng vận hành, tôi đánh giá dự án ở trạng thái **NOT YET** đối với triển khai thực tế.