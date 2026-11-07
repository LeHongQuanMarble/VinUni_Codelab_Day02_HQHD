# Lab 02 — Worksheet: AI Product Scoping

---

## 🏛️ Bối cảnh: Tôi là ai?

Tôi là **Hoàng**, Sinh viên tại **VinUniversity**. Nhóm chúng tôi được giao nhiệm vụ phối hợp với Khối Vận Hành của **Xanh SM (GSM)** để tìm kiếm các cơ hội tối ưu hóa bằng trí tuệ nhân tạo. 

Thông qua quá trình tìm hiểu quy trình hỗ trợ xe điện tại Xanh SM, tôi nhận thấy khi tài xế gặp tình trạng pin yếu hoặc pin nguy cấp, các điều phối viên (Dispatchers) phải mất nhiều thời gian tiếp nhận thông tin, xác minh dữ liệu xe, kiểm tra vị trí GPS, tìm kiếm trạm sạc và phối hợp với bộ phận hỗ trợ. Quy trình xử lý còn phụ thuộc nhiều vào thao tác thủ công và việc trao đổi thông tin giữa các bộ phận.

Điều này có thể làm kéo dài thời gian xử lý sự cố, tăng áp lực cho đội ngũ điều phối và khiến xe phải gián đoạn hoạt động lâu hơn. Vì vậy, bài toán tôi mang đến buổi Lab hôm nay là Xây dựng hệ thống AI hỗ trợ điều phối viên xử lý sự cố xe điện pin yếu tại Xanh SM (Intelligent EV Battery Emergency Support).

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội (Cá nhân)

| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | Xanh SM | Repetitive, Time-consuming | Điều phối viên phải đọc thông tin pin, vị trí, trạng thái chuyến đi và tìm phương án hỗ trợ cho xe điện pin yếu. |
| 2 | Xanh SM | AI-upgrade, Stakeholder Pain | Soạn phản hồi cho tài xế/khách hàng khi có sự cố như xe hết pin, trễ chuyến, điểm đón sai; nội dung hiện có thể chậm hoặc thiếu nhất quán. |
| 3 | Xanh SM | Repetitive, Time-consuming | Phân loại phản ánh của khách hàng theo nhóm: thái độ tài xế, vệ sinh xe, trễ chuyến, thanh toán, an toàn. |
| 4 | VinFast | Repetitive, Time-consuming | Tổng hợp mô tả lỗi xe từ đại lý/call center và phân loại để chuyển đúng bộ phận kỹ thuật.
| 5 | Vinhomes | Time-consuming, Stakeholder Pain | Phân loại phản ánh cư dân và soạn bản nháp phản hồi cho ban quản lý theo loại sự cố và mức độ ưu tiên. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards (Cá nhân)

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1 - Hỗ trợ xe điện pin nguy cấp         │
│                                                             │
│ Bài toán (1 câu): Điều phối viên cần nhanh chóng xác định   |
| hướng xử lý an toàn khi tài xế Xanh SM báo xe có mức pin    |
| rất thấp.                                                   │
|                                                             |
│ Công ty thành viên: [ ] VinFast  [X] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Điều phối viên, tài xế                 │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Nhận cuộc gọi/tin nhắn báo pin yếu                     |
|   2. Hỏi hoặc tra cứu mức pin, vị trí GPS, mã xe            |
|   và trạng thái chuyến.                                     |
|   3. Kiểm tra phương án hỗ trợ và khoảng cách               |
|   trạm sạc/đội hỗ trợ.                                      |
|   4. Trao đổi với bộ phận điều phối hoặc cứu hộ.            |
|   5. Soạn phản hồi và thông báo cho tài xế.                 |
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? 3 (⏱ 5-10 phút/lượt)       │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Tóm tắt nội dung báo  | 
| sự cố, trích xuất thông tin có trong yêu cầu và tạo         |
| bản nháp phản hồi.                                          │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       |
|  1. Giảm thời gian tạo bản nháp từ baseline giả định 5–10   |
| phút xuống dưới 2 phút                                      |
|  2. 100% trường hợp pin dưới 5% không được gợi ý trạm sạc   | 
|  3. 100% hành động cần người duyệt.                         │
│                                                             │
│                                                             │
│ Quick Architecture: [ ] No AI  [X] Rule  [X] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2 - Phân loại phản ánh khách hàng       │
│                                                             │
│ Bài toán (1 câu): Tự động phân loại phản ánh khách hàng     |
| để chuyển đúng nhóm xử lý.                                  |
|                                                             |
│ Công ty thành viên: [ ] VinFast  [X] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên chăm sóc khách hàng và       |
| trưởng nhóm vận hành.                                       │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Nhận phản ánh từ ứng dụng/call center.                 |
|   2. Đọc nội dung và xác định chủ đề.                       |
|   3. Xác định mức độ ưu tiên.                               |
|   4. Chuyển ticket đến nhóm phụ trách.                      |
|   5. Theo dõi trạng thái xử lý.                             │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? 2 (⏱ 10-15 phút/lượt)      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Gợi ý category,       |
| priority và tóm tắt ticket; nhân viên xác nhận trước        |
| khi chuyển.                                                 │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       |
|  1. Ít nhất 90% ticket được gợi ý đúng category trong       |
| tập kiểm thử được gán nhãn                                  |
|  2. thời gian phân loại trung vị dưới 30 giây.              │
│                                                             │
│                                                             │
│ Quick Architecture: [ ] No AI  [X] Rule  [X] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3 - Soạn phản hồi sự cố cho tài xế      │
│                                                             │
│ Bài toán (1 câu): Tạo bản nháp phản hồi ngắn gọn, nhất quán |
| cho tài xế khi phát sinh sự cố vận hành.                    |
|                                                             |
│ Công ty thành viên: [ ] VinFast  [X] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên điều phối và chăm sóc tài xế.│
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Nhận thông tin sự cố.                                  |
|   2. Kiểm tra dữ liệu liên quan.                            |
|   3. Tìm mẫu phản hồi phù hợp.                              |
|   4. Chỉnh sửa nội dung theo tình huống.                    |
|   5. Gửi sau khi được duyệt.                                │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Viết lại nội dung và       |
| bảo đảm không đưa ra cam kết hoặc thông tin chưa xác minh.  │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Soạn bản nháp dựa     |
| trên dữ liệu đã xác minh, không tự gửi.                     │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       |
|  1. 90% bản nháp được nhân viên chấp nhận sau tối đa        |
| một lần chỉnh sửa                                           |
|  2. Không có bản nháp nào tự động được gửi.                 │
│                                                             │
│                                                             │
│ Quick Architecture: [ ] No AI  [X] Rule  [X] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

