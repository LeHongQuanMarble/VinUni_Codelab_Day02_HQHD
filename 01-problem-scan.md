# 01 — Problem Scan & Quick Problem Cards (VinUniversity)
---

## 🏛️ Bối cảnh: Tôi là ai?

Tôi là sinh viên đóng vai **AI Product Engineer** tại **Vin Smart Future**, khảo sát các quy trình học vụ và học tập có thể tối ưu bằng AI. Tôi chọn phạm vi VinUniversity vì tôi là người học, nên tôi thấy trực tiếp đầu ra của quy trình chấm bài lab: điểm số có, nhưng lời góp ý để hiểu lỗi thì thường không đủ.

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội (Cá nhân)

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **VinUniversity** | Lặp lại + Tốn thời gian | Hàng trăm email/ticket mỗi tuần hỏi lặp lại về đăng ký môn, tài khoản LMS, lịch thi. Nhân viên đọc, phân loại, rồi soạn trả lời thủ công. |
| 2 | **VinUniversity** | Tốn thời gian + Stakeholder Pain | Nhân viên Phòng Tuyển sinh đối chiếu thủ công hồ sơ (bảng điểm, giấy tờ, CCCD) với checklist. Thí sinh chờ lâu mới biết hồ sơ thiếu gì. |
| 3 | **VinUniversity** | Lặp lại | Phòng Đào tạo xếp phòng học bằng bảng tính, dễ trùng lịch khi nhiều khoa cùng đặt. Ràng buộc (sức chứa, thiết bị) đã rõ. |
| 4 | **VinUniversity** | Tốn thời gian + AI-upgrade | Hàng nghìn phản hồi tự luận khảo sát sau môn học mỗi học kỳ; giảng viên không đọc hết, chỉ nhận điểm trung bình. |
| 5 | **VinUniversity** | Stakeholder Pain + Lặp lại | Sinh viên hỏi lặp lại về hạn đóng và mức học phí sau giảm. Thông tin nằm ở nhiều file, mỗi kỳ phải soạn lại thông báo. |
| 6 | **VinUniversity** | Lặp lại + Tốn thời gian + Stakeholder Pain | **Chấm bài lab và giải thích lỗi cho sinh viên.** Autograder chấm được đúng/sai, nhưng sinh viên nhận được một dòng `[FAIL]` và không biết sửa ở đâu. Trợ giảng phải đọc log và code, rồi viết góp ý tay. |

> **Ghi nhận:** VinUniversity thuộc hệ sinh thái Vingroup. `03-inspiration-kit.md` (mục 3, "Mảng Y Tế & Giáo Dục") đưa VinUni vào cùng bảng với các công ty thành viên, nên phạm vi scan vẫn hợp lệ.

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards (Cá nhân)

Chọn top 3: **#6 (chấm bài và giải thích lỗi)** là bài chính; **#1 (ticket sinh viên)** để đối chiếu, cùng kiểu LLM + HITL; **#3 (xếp phòng)** để đối chiếu, không cần AI.

## 🃏 Card #6 — Chẩn đoán lỗi và gợi ý học tập cho bài lab (CHỌN)

```text
┌──────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #6                                                │
│                                                                      │
│ Bài toán (1 câu): Từ kết quả autograder, giúp sinh viên tự tìm và    │
│ sửa lỗi qua gợi ý nhiều cấp trên máy tính; trợ giảng chỉ duyệt nháp  │
│ phản hồi, không phải viết lại từ đầu.                                │
│                                                                      │
│ Công ty thành viên: [ ] VinFast [ ] Xanh SM [ ] Vinhomes [ ] Vinmec  │
│                     [x] Khác: VinUniversity                          │
│                                                                      │
│ Ai đang đau (Actor)?                                                 │
│   Sinh viên (nhận [FAIL] mà không biết sửa đâu);                     │
│   trợ giảng (đọc log và viết góp ý tay).                             │
│                                                                      │
│ Workflow thủ công hiện tại (4–5 bước):                               │
│   1. Autograder chấm ──> 2. Trợ giảng đọc log và code tìm nguyên     │
│   nhân ──> 3. Đối chiếu rubric, viết góp ý ──> 4. Ghi điểm, gửi      │
│   ──> 5. Sinh viên hỏi lại qua kênh khác khi chưa hiểu               │
│                                                                      │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3–4 (⏱ ~10 phút/bài, giả định) │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                                │
│   (a) Agent đọc log và code bằng tool hạn chế, chẩn đoán loại lỗi;   │
│   (b) LLM soạn nháp theo gợi ý cấp 1 → 2 → 3;                        │
│   (c) Sinh viên hỏi đáp trên máy tính, gợi ý tăng dần để tự sửa.     │
│   Điểm do rule autograder quyết định; trợ giảng duyệt trước khi gửi. │
│                                                                      │
│ Đo thành công bằng gì (Metric có số)?                                │
│   (1) Thời gian viết góp ý giảm ≥ 24% so với baseline (mốc TA Buddy) │
│   (2) ≥ 85% loại lỗi gắn đúng trên 50 bài mẫu có nhãn                │
│   (3) 0 phản hồi gửi sinh viên mà không có người duyệt               │
│   (4) ≥ 70% sinh viên tự sửa được sau gợi ý cấp 2 (buổi thử 20 SV,   │
│       giả định)                                                      │
│                                                                      │
│ Quick Architecture: [x] Rule (điểm) [x] LLM (soạn nháp, gợi ý)       │
│                     [x] Agent (chẩn đoán, tool hạn chế) [ ] Agent tự │
│                     trị                                              │
└──────────────────────────────────────────────────────────────────────┘
```

## 🃏 Card #1 — Phân loại và soạn nháp trả lời ticket sinh viên (đối chiếu)

```text
┌──────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                                │
│                                                                      │
│ Bài toán (1 câu): Phân loại và soạn nháp trả lời ticket về đăng ký   │
│ môn, LMS và lịch thi để nhân viên duyệt và gửi.                      │
│                                                                      │
│ Công ty thành viên: [x] Khác: VinUniversity                          │
│                                                                      │
│ Ai đang đau (Actor)? Nhân viên Phòng Hỗ trợ sinh viên; sinh viên     │
│ chờ trả lời.                                                         │
│                                                                      │
│ Workflow thủ công hiện tại (4 bước):                                 │
│   1. Nhận ticket ──> 2. Phân loại ──> 3. Tra quy định trong nhiều    │
│   file ──> 4. Soạn và gửi                                            │
│                                                                      │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 (⏱ ~8 phút/ticket, lỗi ~1/20,│
│ giả định)                                                            │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 và 4, từ knowledge base │
│ đã duyệt; có HITL.                                                   │
│                                                                      │
│ Đo thành công bằng gì (Metric có số)?                                │
│   Thời gian ~8 phút ──> dưới 2 phút/ticket; phân loại đúng ≥ 90%     │
│   trên 200 ticket mẫu.                                               │
│                                                                      │
│ Quick Architecture: [ ] No AI [ ] Rule [x] LLM [ ] Agent             │
└──────────────────────────────────────────────────────────────────────┘
```

**Lý do không chọn làm bài chính:** cùng kiểu LLM + HITL với #6, nhưng #6 có sẵn autograder làm nền rule, và có lợi ích học tập trực tiếp cho sinh viên.

## 🃏 Card #3 — Xếp lịch phòng học và phòng hội thảo (đối chiếu, không AI)

```text
┌──────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                                │
│                                                                      │
│ Bài toán (1 câu): Xếp phòng không trùng lịch, đúng sức chứa và thiết │
│ bị khi nhiều khoa cùng đặt.                                          │
│                                                                      │
│ Công ty thành viên: [x] Khác: VinUniversity                          │
│                                                                      │
│ Ai đang đau (Actor)? Phòng Đào tạo; khoa và giảng viên khi bị trùng  │
│ phòng.                                                               │
│                                                                      │
│ Workflow thủ công hiện tại (4 bước):                                 │
│   1. Khoa gửi yêu cầu ──> 2. Mở bảng tính ──> 3. Dò xung đột thủ công│
│   ──> 4. Xác nhận hoặc đổi phòng                                     │
│                                                                      │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 (⏱ ~5 phút/yêu cầu, giả định)│
│ AI có thể nhảy vào hỗ trợ ở bước nào? Không cần AI. Ràng buộc rõ,    │
│ một rule kiểm tra trùng là đủ.                                       │
│                                                                      │
│ Đo thành công bằng gì (Metric có số)?                                │
│   0 trường hợp trùng lịch được xác nhận; dưới 1 phút/yêu cầu.        │
│                                                                      │
│ Quick Architecture: [x] No AI [x] Rule [ ] LLM [ ] Agent             │
└──────────────────────────────────────────────────────────────────────┘
```

---

# 🗳️ Quyết định lựa chọn của nhóm

Chọn **Card #6 — Chẩn đoán lỗi và gợi ý học tập cho bài lab** để thực hiện Deep-Dive. Bài này có autograder làm nền rule đáng tin cậy, và tạo ra giá trị học tập trực tiếp: sinh viên hiểu lỗi thay vì chỉ thấy `[FAIL]`. Card #3 chỉ để đối chiếu: không phải mọi bài toán đều cần AI.

---
