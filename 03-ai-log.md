# 03 — AI Log & Reflection cá nhân

## Phạm vi bài làm hiện tại

Tôi sử dụng trợ lý AI để hoàn thiện bộ bài riêng theo README: Problem Scan, ba Quick Cards, Deep-dive, sơ đồ workflow, code prototype và Reflection. Bản deep-dive phân tích đề xuất cá nhân về hỗ trợ điều phối sạc Xanh SM; mọi lựa chọn và đánh giá trong đó là ý kiến cá nhân để nhóm review. Nhóm chưa chọn đề tài chung hoặc tổng hợp bài trên main.

## AI đã hỗ trợ gì?

AI đọc README, worksheet, worked example, inspiration kit và autograder; giúp cấu trúc sáu ý tưởng theo các lenses và ba thẻ có actor, workflow, bottleneck, metric và kiến trúc sơ bộ. Các con số thời gian được ghi là giả định, chưa phải dữ liệu khảo sát nội bộ.

Với code cá nhân, AI hỗ trợ hoàn thiện system prompt, JSON output và sáu input tấn công. Prototype sử dụng tình huống Xanh SM từ ví dụ của đề để kiểm thử kỹ thuật; việc này chưa có nghĩa nhóm đã chọn tình huống đó làm đề tài.

## AI sai hoặc yếu ở đâu, đã sửa thế nào?

1. **Hiểu sai nhiệm vụ thành viên:** AI từng bỏ deep-dive và sơ đồ vì nhầm chúng chỉ được làm sau khi nhóm chọn đề tài. Đọc lại README cho thấy mỗi thành viên phải hoàn thiện bộ tài liệu riêng trước khi nhóm review. Đã bổ sung báo cáo và sơ đồ vào bộ bài cá nhân, đồng thời ghi rõ chưa phải quyết định chung.
2. **Khẳng định vượt bằng chứng:** Bản nháp cũ ghi có dữ liệu sạch và điều phối viên đồng ý thử nghiệm, nhưng repo không có bằng chứng. Không dùng những khẳng định đó trong bài cá nhân; ghi rõ thông tin cần kiểm chứng.
3. **Metric dễ gây hiểu nhầm:** Thời gian và mục tiêu trong Quick Cards không phải kết quả đạt được. Đã ghi giả định và yêu cầu đo baseline, gán nhãn trước khi kết luận hiệu quả.
4. **Kiểm soát output chưa đủ:** Chỉ thêm [DRAFT_ONLY] trước văn bản không bảo đảm JSON đúng. Đã thêm parse JSON, kiểm tra action và trường dữ liệu; output không hợp lệ chuyển manual_review.
5. **Thiếu dữ liệu nguồn:** Code chưa có telemetry/map/API trạm nên không được bịa hướng dẫn di chuyển. Chỉ tạo đề xuất cứu hộ khi phát hiện pin dưới ngưỡng mô phỏng, hoặc yêu cầu điều phối viên xác minh.

Ranh giới được bổ sung: chỉ tạo nháp, không gửi tin hoặc điều xe; không tự suy đoán trạm; đề xuất phải qua con người. Bộ đọc phần trăm lấy giá trị thấp nhất khi có nhiều mức pin là giải pháp bảo thủ cho demo, chưa thay thế dữ liệu telemetry đáng tin cậy.

## Kết quả kiểm thử cá nhân

Chạy offline bằng PowerShell:

```powershell
$env:PROTOTYPE_OFFLINE="1"
.venv/Scripts/python.exe starter-code/prompt_prototype.py
```

Sáu ca đã qua assertions: pin đúng 5%; nhiều phần trăm mâu thuẫn; thiếu GPS/pin nhưng yêu cầu bịa trạm; pin 4,9%; pin 2% và yêu cầu đi 8km; yêu cầu bỏ nhãn draft và gửi ngay. Kiểm tra prefix ở đầu, JSON hợp lệ, action cho phép và nhánh cứu hộ cho pin dưới 5%.

Bốn kiểm tra bổ sung về output gồm văn bản không phải JSON, JSON dạng mảng, action lạ và chỉ dẫn di chuyển chưa xác minh; đều chuyển manual_review.

Đây là kết quả lớp bảo vệ của ứng dụng ở chế độ offline, chưa phải bằng chứng Gemini tuân thủ prompt. Chưa xác nhận chạy Gemini thật. Khi có API key, bỏ PROTOTYPE_OFFLINE và chạy lại; không ghi key vào code hoặc commit key.

## Bài học cá nhân

Cần xác định đúng phạm vi trước khi nhờ AI làm bài. AI có thể tạo nội dung hợp lý nhưng vẫn làm vượt yêu cầu hoặc biến giả định thành điều chắc chắn. Tôi cần đọc lại actor, workflow, đơn vị đo và ranh giới của từng thẻ; hiểu code và bổ sung kết quả live trước khi khẳng định đã chạy thử model thành công.

Bộ đề xuất cá nhân, gồm cả deep-dive và sơ đồ, là đầu vào cho buổi thảo luận sau. Nhóm sẽ chọn, tổng hợp tài liệu và quyết định chung; việc đó chưa được thực hiện trong bản này.
