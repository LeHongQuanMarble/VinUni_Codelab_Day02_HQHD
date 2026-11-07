# 02 — Deep Dive: Trợ lý điều phối sạc Xanh SM

> Đề xuất cá nhân cho nhóm lựa chọn. Đây là mô hình bài tập theo bối cảnh đề lab, không mô tả một hệ thống Xanh SM đã được khảo sát. Tất cả thời gian, lưu lượng và mục tiêu là giả định cần kiểm chứng.

## Phạm vi và lựa chọn cá nhân

Bản này phân tích Card #1 từ Problem Scan để hoàn thiện bộ đề xuất riêng theo README. Mọi lựa chọn kiến trúc, mục tiêu và quyết định đánh giá là ý kiến cá nhân, chưa phải quyết định của nhóm.

## 3.1 Current-State Workflow Mapping

| Bước | Người/công cụ | Thao tác | Phút/ca giả định | Handoff |
|---|---|---|---:|---|
| 1 | Tài xế → điều phối viên | Báo sự cố qua cuộc gọi/ứng dụng | 1 | Thông tin ban đầu từ thực địa |
| 2 | Điều phối viên ↔ hồ sơ xe/map | Xác minh xe, pin, vị trí và thời điểm cập nhật | 2 | Tra thông tin giữa người và hệ thống |
| 3 | Điều phối viên ↔ dashboard trạm | Tra tương thích, tình trạng, khoảng cách | 6 | Chuyển sang hệ thống trạm; bottleneck |
| 4 | Điều phối viên | Tổng hợp và viết hướng dẫn | 4 | Bottleneck do sao chép thủ công |
| 5 | Điều phối viên → tài xế/đội cứu hộ | Kiểm tra, gửi hoặc liên hệ cứu hộ | 2 | Bàn giao phương án đã duyệt |
| **Tổng** | | | **15** | Thời gian tác nghiệp giả định, chưa gồm chờ cứu hộ |

Sơ đồ: [04-workflow-diagram.png](04-workflow-diagram.png). Điểm nghẽn bước 3–4 chiếm 10/15 phút. Cần quan sát ít nhất 50 ca, ghi thời điểm nhận, đủ dữ liệu, có phương án, duyệt và gửi để kiểm tra giả thuyết này.

## 3.2 Problem Statement — 6 trường

| Field | Nội dung |
|---|---|
| 1. Actor / Operator | Điều phối viên xử lý yêu cầu hỗ trợ pin yếu; tài xế cung cấp thông tin và nhận phương án đã duyệt. |
| 2. Current Workflow | Năm bước trên, qua cuộc gọi, hồ sơ xe, map và dashboard trạm; có thao tác nhập lại thông tin. |
| 3. Bottleneck | Tra dữ liệu và soạn hướng dẫn phân tán, giả định 10 phút/ca, dễ nhầm vị trí hoặc dùng thông tin cũ. |
| 4. Business Impact | Với giả định 60 ca/ngày và 15 phút/ca: 15 giờ tác nghiệp/ngày. Nếu trung bình còn 3 phút/ca, trần tiết kiệm lý thuyết 12 giờ/ngày trước chi phí kiểm tra và ca ngoại lệ. Chưa có chứng cứ về doanh thu hoặc ROI thực tế. |
| 5. Success Metric | Pilot: ≥90% ca đủ dữ liệu có phương án được duyệt trong 3 phút; 100% đề xuất qua HITL; 0 chỉ dẫn dùng trạm bịa/không tương thích trong tập kiểm thử; tỷ lệ phải viết lại toàn bộ ≤20%. |
| 6. Operational Boundary | AI chỉ soạn nháp. Không gửi tin, điều xe hay thay đổi dữ liệu vận hành. Dưới 5% pin: rule chuyển đề xuất cứu hộ cho người duyệt. Dữ liệu thiếu/mâu thuẫn, API lỗi hoặc JSON sai: manual_review. Ngưỡng 5%/5km của bài lab không phải mô hình xác nhận tầm hoạt động xe. |

**Cách đo:** Thời gian tính từ tiếp nhận tới duyệt; báo cáo riêng nhóm đủ dữ liệu và tất cả ca để tránh loại ca khó làm đẹp số. Đối chiếu cùng loại sự cố, ca trực và khu vực. Người vận hành gán nhãn đúng/sai phương án. Các mục tiêu trên chưa phải kết quả đã đạt.

## 3.3 AI Fit & Future-State Flow

| Phương án | Phù hợp | Hạn chế / quyết định |
|---|---|---|
| Rule / state machine | Kiểm tra pin, dữ liệu, danh sách trạm, quyền gửi và schema | Bắt buộc cho kiểm soát xác định; template là baseline để so sánh |
| LLM Feature | Tổng hợp mô tả tự do, soạn nháp ngắn theo dữ liệu đã xác minh | Chỉ thêm nếu giúp giảm thời gian sửa so với template mà không giảm chất lượng |
| Agentic Loop | Có thể chủ động gọi nhiều công cụ | Chưa cần vì luồng cố định và quyền tác động cần người duyệt; tăng chi phí và khó kiểm soát |

**Luồng đề xuất:** Nhân viên nhận ca → dịch vụ đọc telemetry/trạm theo quyền được cấp → rule kiểm tra độ mới, tương thích và tính đầy đủ → nhánh an toàn hoặc LLM soạn JSON nháp → kiểm tra schema và đối chiếu dữ liệu nguồn → **điều phối viên duyệt** → hệ thống nghiệp vụ hiện có gửi/lập yêu cầu cứu hộ theo quyền của nhân viên.

**Fallback:** API lỗi, dữ liệu quá hạn, pin không rõ/mâu thuẫn, không có trạm phù hợp, model lỗi hoặc output không đạt kiểm tra → dừng đề xuất tự động, tạo manual_review, giữ nguyên quy trình thủ công. Không lặp gọi vô hạn và không gửi trực tiếp từ LLM.

**Phạm vi code hiện tại:** Chưa tích hợp telemetry, map hay API trạm. Vì vậy code không xuất chỉ dẫn di chuyển: chỉ trả đề xuất cứu hộ khi phát hiện pin dưới 5%, hoặc chuyển người xác minh. Chọn mức pin thấp nhất trong các phần trăm xuất hiện để kiểm thử theo hướng thận trọng; cách đọc tự do này không thay được trường telemetry đáng tin cậy.

## Phase 4 — Prompt Prototype & Boundary Tests

Chạy kiểm thử offline, không cần key:

```powershell
$env:PROTOTYPE_OFFLINE="1"
.venv/Scripts/python.exe starter-code/prompt_prototype.py
.venv/Scripts/python.exe autograder/autograder.py
```

Hiện môi trường chưa có GEMINI_API_KEY hoặc GOOGLE_API_KEY nên chưa chạy được thử nghiệm model thật; yêu cầu này còn cần bổ sung bằng chứng live. Để gọi Gemini thật, bỏ PROTOTYPE_OFFLINE và thiết lập GEMINI_API_KEY trong môi trường, rồi chạy lại script. Code dùng model được đề chỉ định: gemini-2.5-flash. Không lưu key vào repo.

Sáu input gồm: phần trăm pin mâu thuẫn; yêu cầu bịa trạm khi thiếu GPS; pin thập phân 4,9%; pin đúng ngưỡng 5%; yêu cầu bỏ prefix và gửi ngay; pin 2% và trạm 8km. Assertions kiểm tra prefix ở đầu, JSON hợp lệ, action nằm trong tập cho phép và nhánh cứu hộ cho pin tới hạn. Kiểm tra bổ sung bao gồm model trả JSON hỏng, action lạ và trường message không được xác minh.

Kết quả offline xác nhận lớp bảo vệ trong ứng dụng; không chứng minh Gemini tự tuân thủ prompt. Khi chạy live cần lưu riêng raw output và output sau guardrail, thời gian, số token và lỗi; không được lấy output đã sửa làm bằng chứng model không vi phạm.

## Phase 5 — EVALUATE

- [ ] Có dữ liệu vận hành sạch: chưa có log nội bộ; hiện chỉ có input tổng hợp.
- [x] Rủi ro trong demo được giới hạn: không có công cụ gửi/điều xe, có rule và manual_review.
- [ ] Stakeholder sẵn sàng: chưa phỏng vấn điều phối viên và chủ hệ thống.

**Đánh giá cá nhân: NOT YET cho pilot dữ liệu thực; tiếp tục prototype offline trong scope lab.**

Điều kiện chuyển GO: chủ nghiệp vụ xác nhận workflow/ngưỡng an toàn; có quyền truy cập dữ liệu; 50 ca đo baseline và 200 ca gán nhãn để đánh giá; kiểm thử live thành công; quy trình HITL/fallback được người vận hành chấp nhận. Tập đánh giá phải có ca thiếu/mâu thuẫn dữ liệu, API trễ, trạm không tương thích và prompt injection.

Kế hoạch pilot hai tuần sau khi đủ điều kiện: tuần đầu đo baseline và chạy shadow không gửi; tuần hai nhân viên dùng draft, so với template và đo thời gian sửa. Dừng pilot nếu có đề xuất chưa duyệt được gửi hoặc đề xuất không có căn cứ nguồn. Chưa đủ dữ liệu để kết luận hòa vốn: chi phí phải gồm API, tích hợp, bảo trì, duyệt và xử lý ngoại lệ; chỉ giữ LLM khi lợi ích đo được vượt baseline rule/template.
