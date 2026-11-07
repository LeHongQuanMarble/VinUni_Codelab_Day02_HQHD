# 01 — Problem Scan: Vin Smart Future

> Bài làm cá nhân để nhóm review và lựa chọn. Bối cảnh doanh nghiệp lấy từ đề lab; các quy trình và con số dưới đây là giả định phục vụ scoping, chưa phải kết quả khảo sát nội bộ.

## Phase 1 — SCAN

| # | Đơn vị | Lens | Bài toán và người chịu ảnh hưởng |
|---|---|---|---|
| 1 | Xanh SM | Lặp lại; tốn thời gian | Điều phối viên tra vị trí, tìm trạm sạc và soạn hướng dẫn cho tài xế báo pin yếu. |
| 2 | VinFast | AI có thể tốt hơn | Tổng đài đọc mô tả lỗi xe bằng ngôn ngữ tự do để chuyển đúng nhóm dịch vụ. |
| 3 | Vinhomes | Pain từ người khác | Cư dân phải giải thích lại khi phản ánh bị chuyển nhầm đội kỹ thuật, vệ sinh hoặc an ninh. |
| 4 | Vinmec | Tốn thời gian | Nhân viên hành chính đọc yêu cầu đổi lịch khám và nhập lại thông tin; phạm vi chỉ là hành chính. |
| 5 | Vinpearl | Lặp lại | Nhân viên vận hành tổng hợp phản hồi nhiều kênh, gộp trùng và chuyển các vấn đề cần xử lý. |
| 6 | VinFast | Lặp lại | Kế toán đối chiếu mã giao dịch sạc với hóa đơn; ưu tiên rule khi dữ liệu đã có cấu trúc. |

## Phase 2 — QUICK-ASSESS

### Quick Problem Card #1 — Hỗ trợ điều phối sạc Xanh SM

- **Công ty thành viên:** Xanh SM.
- **Bài toán:** Rút ngắn thao tác tra cứu và soạn nháp hỗ trợ tài xế báo pin yếu.
- **Actor:** Điều phối viên ca trực; tài xế là người nhận hỗ trợ.
- **Workflow:** (1) Nhận sự cố → (2) xác minh xe, pin và vị trí → (3) tìm trạm tương thích còn chỗ → (4) soạn hướng dẫn → (5) duyệt, gửi hoặc liên hệ cứu hộ.
- **Bottleneck:** Bước 3–4, giả định 10/15 phút mỗi ca, vì phải chuyển giữa nhiều màn hình.
- **AI hỗ trợ:** LLM soạn nháp từ dữ liệu đã xác minh; rule quyết định nhánh an toàn. API và bộ lọc thực hiện tra cứu, không giao việc này cho LLM tự suy đoán.
- **Metric:** Mục tiêu ít nhất 90% ca đủ dữ liệu được xử lý trong 3 phút; 100% bản nháp phải qua người duyệt. Baseline 15 phút cần đo lại.
- **Architecture:** Rule + LLM Feature, không cần agent tự trị.
- **Boundary:** Không tự gửi, không tự điều xe, không bịa trạm. Ngưỡng pin dưới 5% dùng để đề xuất cứu hộ trong mô phỏng, chưa phải hướng dẫn vận hành thực tế.

### Quick Problem Card #2 — Phân luồng ticket dịch vụ VinFast

- **Công ty thành viên:** VinFast.
- **Bài toán:** Gợi ý nhóm tiếp nhận từ mô tả sự cố không thống nhất của khách hàng.
- **Actor:** Tổng đài và nhân viên tiếp nhận dịch vụ.
- **Workflow:** (1) Nhận ticket → (2) đọc mô tả → (3) tra danh mục → (4) gán nhóm → (5) chuyển người phụ trách.
- **Bottleneck:** Bước 2–3, giả định 8 phút/ticket.
- **AI hỗ trợ:** Chuẩn hóa mô tả và đề xuất nhóm từ danh mục đóng; chuyển người xử lý nếu thiếu thông tin.
- **Metric:** Mục tiêu macro-F1 ≥0,90 trên 200 ticket được hai người gán nhãn, thời gian tạo gợi ý p90 ≤30 giây.
- **Architecture:** Rule cho mã lỗi có sẵn; LLM cho mô tả tự do.
- **Boundary:** Không chẩn đoán kỹ thuật cuối cùng, không khuyên tiếp tục lái xe; nhân viên duyệt phân luồng.

### Quick Problem Card #3 — Phân loại phản ánh Vinhomes

- **Công ty thành viên:** Vinhomes.
- **Bài toán:** Giảm chuyển nhầm đội vận hành khi cư dân gửi phản ánh dài hoặc nhiều ý.
- **Actor:** Nhân viên CSKH tòa nhà.
- **Workflow:** (1) Nhận phản ánh → (2) đọc, tách ý → (3) tra trách nhiệm → (4) đề xuất đội xử lý → (5) nhân viên duyệt.
- **Bottleneck:** Bước 2–3, giả định 6 phút/phản ánh.
- **AI hỗ trợ:** Tóm tắt, tách nhiều vấn đề và gợi ý nhãn có dẫn chứng từ văn bản.
- **Metric:** ≥90% gợi ý đúng đội trên 200 phản ánh đã gán nhãn; thời gian xử lý có người duyệt p90 ≤2 phút.
- **Architecture:** LLM Feature + rule tra đội theo tòa nhà.
- **Boundary:** Không tự đóng yêu cầu, cam kết bồi thường hay quyết định mức độ an toàn; tình huống khẩn cấp chuyển người phụ trách.

## Ghi chú cá nhân để mang đi thảo luận

Ba thẻ trên là các phương án cá nhân, chưa chốt bài toán chung. Phần deep-dive, sơ đồ chi tiết và quyết định GO / NOT YET / NO-GO sẽ thực hiện khi nhóm thảo luận.

Các câu hỏi cần kiểm chứng cho từng thẻ:

- **Card #1:** Dữ liệu trạm và pin có đủ mới không? Tự động tra cứu bằng API + template có giải quyết phần lớn bottleneck không? Con số 15 phút phải đo lại trước khi tính hiệu quả.
- **Card #2:** Đã có danh mục nhóm dịch vụ và ticket được gán nhãn chưa? Với ticket có mã lỗi rõ, rule tra bảng phù hợp hơn LLM. Cần đo riêng chất lượng gợi ý và thời gian con người duyệt.
- **Card #3:** Đội nào chịu trách nhiệm cho phản ánh có nhiều vấn đề? Rule có thể xử lý định tuyến theo tòa; LLM chỉ cần cho phần đọc và tóm tắt nội dung tự do. Cần tránh bỏ sót ý khi tóm tắt.
