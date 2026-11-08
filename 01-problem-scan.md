# Họ tên: Đào Huy Hoàng
# MSHV: 2A202603451

# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng [Chọn một: VinFast / Xanh SM / Vinhomes / Vinmec]. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

### 📝 List bài toán của tôi:
| # | Subsidiary              | Lens                          | Mô tả ngắn bài toán |
|---|-------------------------|-------------------------------|---------------------|
| 1 | VinFast                 | Tốn thời gian + Pain từ người khác | Theo dõi và thúc đẩy các khoản hoàn trả chi phí sau dịch vụ/cứu hộ (ví dụ tiền cẩu xe) đang bị kéo dài nhiều tháng. |
| 2 | VinFast                 | Lặp lại + AI-upgrade          | Phân loại và triage phản ánh lỗi phần mềm / tính năng thông minh (điều khiển từ xa, ADAS, liên kết tài khoản…) để đề xuất bước xử lý đầu. |
| 3 | Green SM (Xanh SM)      | Tốn thời gian + Pain từ người khác | Giải thích và tính toán quyền lợi phúc lợi cho tài xế khi nhiều chương trình chồng chéo (chia sẻ doanh thu, miễn phí sạc, bảo hiểm, thưởng…). |
| 4 | Vinhomes                | Pain từ người khác + AI-upgrade | Hỗ trợ cư dân lớn tuổi / không rành công nghệ sử dụng App Vinhomes Resident và tiện ích Smart City. |
| 5 | VinWonders / Vinpearl   | AI-upgrade + Tốn thời gian    | Hỗ trợ lập lịch trình trong ngày + gợi ý Fastpass, đồng thời cảnh báo lỗi chọn sai ngày vé trên app. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

**Chọn 3 đề tài cho Quick Cards:** #1, #2, #3.

** QUICK PROBLEM CARD #1 - VinFast Triage lỗi phần mềm thông minh**
```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): Phân loại và triage các phản ánh lỗi      │
│ phần mềm / tính năng thông minh của xe VinFast để đề xuất   │
│ bước xử lý đầu tiên phù hợp.                                │
│ Công ty thành viên: [x] VinFast                             │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên CSKH / kỹ thuật viên hỗ trợ  │
│ từ xa và chủ xe đang gặp lỗi.                               │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Chủ xe gửi phản ánh qua App / tổng đài / diễn đàn      │
│   → 2. CSKH đọc mô tả lỗi và hỏi thêm thông tin             │
│   → 3. Tra cứu thủ công kiến thức / case tương tự           │
│   → 4. Đưa hướng xử lý (reset / OTA / hẹn xưởng)            │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2-3 (⏱ 8–12 phút/lượt)│
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-3              │
│ (Tự động phân loại mức độ + gợi ý bước xử lý đầu)           │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian triage trung bình từ 10 phút → dưới 2 phút,  │
│ đồng thời tỉ lệ đề xuất đúng hướng xử lý ≥ 85% trên mẫu     │
│ được người kỹ thuật gắn nhãn.                               │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
└─────────────────────────────────────────────────────────────┘
```

** QUICK PROBLEM CARD #2 - VinFast Theo dõi hoàn trả chi phí sau dịch vụ**
```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu): Theo dõi và thúc đẩy các khoản hoàn trả   │
│ chi phí sau dịch vụ / cứu hộ đang bị kéo dài nhiều tháng.   │
│ Công ty thành viên: [x] VinFast                             │
│                                                             │
│ Ai đang đau (Actor)? Chủ xe (chờ tiền) và nhân viên CSKH    │
│ phải theo dõi + nhắc nhiều lần.                             │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Chủ xe gửi yêu cầu hoàn trả (email / tổng đài)         │
│   → 2. CSKH tạo ticket và chuyển bộ phận Tài chính          │
│   → 3. Tài chính kiểm tra chứng từ thủ công                 │
│   → 4. CSKH phải gọi/email nhắc nhiều lần khi quá hạn       │
│   → 5. Hoàn tiền và thông báo lại cho khách                 │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3-4 (⏱ kéo dài        │
│ hàng tuần đến vài tháng, mỗi lần nhắc ~5–8 phút)            │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 và 4           │
│ (Tự động theo dõi hạn + soạn nháp email nhắc + cảnh báo     │
│ ticket quá hạn)                                             │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm tỉ lệ ticket hoàn trả quá 30 ngày từ mức hiện tại      │
│ xuống dưới 15%, và giảm số lần CSKH phải nhắc thủ công      │
│ trung bình từ 4 lần → ≤ 1 lần/ticket.                       │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
└─────────────────────────────────────────────────────────────┘
```

** QUICK PROBLEM CARD #3 - Green SM Giải thích phúc lợi tài xế chồng chéo**
```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): Giải thích và tính toán quyền lợi phúc    │
│ lợi cho tài xế Green SM khi nhiều chương trình chồng chéo.  │
│ Công ty thành viên: [x] Xanh SM (Green SM)                  │
│                                                             │
│ Ai đang đau (Actor)? Tài xế (không hiểu mình được hưởng     │
│ gì) và nhân viên hỗ trợ tài xế phải giải thích lặp lại.     │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Tài xế hỏi về quyền lợi (App / tổng đài / nhóm)        │
│   → 2. Nhân viên hỏi thêm điều kiện tham gia của tài xế     │
│   → 3. Tra cứu thủ công nhiều chương trình đang chạy        │
│   → 4. Giải thích + ước tính số tiền / quyền lợi            │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3-4 (⏱ 7–10 phút/lượt)│
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-4              │
│ (Hỏi thông tin cần thiết → đối chiếu điều kiện → giải thích │
│ rõ ràng + ước tính)                                         │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian giải thích trung bình từ 8 phút → dưới 2 phút│
│ và tỉ lệ tài xế hiểu đúng quyền lợi sau 1 lần giải thích    │
│ ≥ 90% (đo bằng câu hỏi xác nhận ngắn).                      │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
└─────────────────────────────────────────────────────────────┘
```
> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

---