# Lab 02 — Problem Scan & Quick Cards

**Sinh viên:** Đỗ Hoàng Minh (MazzDh)  
**Dự án:** AI Product Scoping — Vin Smart Future  
**Đơn vị phối hợp:** Xanh SM (GSM), VinFast, Vinmec  

---

## 1. Mục tiêu

Tài liệu này ghi lại quá trình rà soát các quy trình thủ công tại các đơn vị thành viên Vingroup, đánh giá nhanh 3 bài toán tiềm năng và chọn ra bài toán phù hợp nhất để nhóm phân tích sâu.

---

## Phase 1 — SCAN: Bảng quét cơ hội vận hành (4 Lenses)

| # | Đơn vị | Lăng kính (Lens) | Quy trình thực tế | Điểm nghẽn vận hành |
|---|---|---|---|---|
| 1 | **Xanh SM** | Tốn thời gian | Điều phối viên hỗ trợ tài xế taxi điện gặp sự cố pin yếu hoặc cạn pin giữa đường. | Phải mở đồng thời 3 hệ thống (bản đồ xe, phần mềm trạm sạc VinFast, chat nội bộ) để tìm trụ trống rồi gõ tin nhắn chỉ đường thủ công. |
| 2 | **VinFast** | AI làm tốt hơn | Tiếp nhận mô tả lỗi hỏng hóc từ khách hàng khi đặt lịch bảo dưỡng. | Khách thường dùng từ ngữ đời thường (ví dụ: *"xe qua gờ giảm tốc kêu cọc cọc ở gầm trước"*). Cố vấn dịch vụ phải gọi lại hỏi nhiều lần mới xác định được mã lỗi OBD-II. |
| 3 | **Vinmec** | Tốn thời gian & Pain | Bác sĩ điều trị làm tóm tắt hồ sơ xuất viện (Discharge Summary). | Mất 20–30 phút cho mỗi ca để đọc lại xét nghiệm, diễn tiến bệnh và viết lại lời dặn bằng ngôn ngữ dễ hiểu cho người nhà. |
| 4 | **Xanh SM** | Lặp lại | Điều chuyển lại chuyến xe khi khách đổi điểm đến đột xuất trên đường đi. | Điều phối viên phải tính lại giá cước và kiểm tra thủ công xem lượng pin còn lại có đủ lộ trình mới không. |
| 5 | **Vinhomes** | Lặp lại | Phân loại phản ánh cư dân gửi qua app Vinhomes Resident. | Trực ban phải đọc từng phản ánh (mất nước, hỏng đèn, tiếng ồn) để gán việc thủ công cho đội kỹ thuật tòa nhà. |
| 6 | **Vinpearl** | Pain từ khách | Lọc đánh giá khách hàng trên Agoda, Booking.com, Google Maps. | Đọc thủ công hàng trăm phản hồi mỗi ngày để nhặt ra các khiếu nại gấp (phòng bẩn, hỏng máy lạnh) báo quản lý ca trực. |

---

## Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

---

### QUICK PROBLEM CARD #1: Xanh SM — Điều phối xử lý sự cố pin xe taxi điện

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                                       │
│                                                                             │
│ Bài toán (1 câu): Hỗ trợ điều phối viên tra cứu nhanh trụ sạc trống và điều │
│ xe sạc lưu động khi tài xế Xanh SM gặp sự cố cạn pin trên đường đón khách.  │
│ Đơn vị: [x] Xanh SM (GSM)     [ ] VinFast     [ ] Vinmec                    │
│                                                                             │
│ Ai đang đau (Actor)?                                                        │
│ - Tài xế taxi: Lo xe chết máy giữa đường, ảnh hưởng doanh thu ca chạy.      │
│ - Điều phối viên: Quá tải vì phải chuyển đổi liên tục giữa 3 màn hình.      │
│                                                                             │
│ Workflow thủ công hiện tại:                                                 │
│   1. Nhận cuộc gọi hoặc cảnh báo pin từ xe tài xế.                          │
│   → 2. Mở bản đồ GPS lấy tọa độ xe và phần trăm pin còn lại.                │
│   → 3. Mở cổng thông tin trạm sạc VinFast, tìm trụ sạc trống đúng chuẩn.     │
│   → 4. Gõ tin nhắn chỉ đường gửi qua ứng dụng cho tài xế.                   │
│   → 5. Nếu pin < 5%, liên hệ đội xe sạc pin lưu động đến cứu hộ.             │
│                                                                             │
│ Bước nào tốn thời gian/dễ lỗi nhất?                                         │
│ Bước 3 & Bước 4 (mất 10/15 phút). Dễ nhầm trạm đã đầy hoặc sai cổng sạc xe. │
│                                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                                       │
│ Bước 3 & 4: Tự động gom dữ liệu định vị, lọc trạm trống hợp lệ và soạn      │
│ sẵn bản nháp có thẻ [DRAFT_ONLY] cho điều phối viên duyệt trước khi gửi.    │
│                                                                             │
│ Đo thành công bằng gì (Metric có số)?                                       │
│ 1. Giảm thời gian xử lý sự cố từ 15 phút xuống khoảng 5 phút.               │
│ 2. 100% ca pin < 5% tự động kích hoạt điều xe sạc lưu động.                 │
│ 3. Tỷ lệ chỉ đúng trạm còn trụ trống đạt trên 98%.                          │
│                                                                             │
│ Quick Architecture: [x] LLM Feature (kèm Rule Guardrails)                   │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

### QUICK PROBLEM CARD #2: VinFast — Phân loại triệu chứng lỗi xe qua mô tả của khách

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                                       │
│                                                                             │
│ Bài toán (1 câu): Phân tích câu chữ mô tả hỏng hóc của chủ xe để gợi ý nhóm │
│ mã lỗi ban đầu, giúp cố vấn dịch vụ phân loại nhanh lịch sửa chữa.          │
│ Đơn vị: [ ] Xanh SM     [x] VinFast     [ ] Vinmec                          │
│                                                                             │
│ Ai đang đau (Actor)?                                                        │
│ - Chủ xe: Không rành kỹ thuật, diễn đạt khó hiểu.                           │
│ - Cố vấn xưởng VinFast: Mất thời gian gọi điện gặng hỏi lại từng chi tiết.  │
│                                                                             │
│ Workflow thủ công hiện tại:                                                 │
│   1. Khách gửi đoạn mô tả lỗi qua app VinFast hoặc hotline.                 │
│   → 2. Cố vấn gọi điện hỏi lại hoàn cảnh xuất hiện tiếng kêu hoặc lỗi.       │
│   → 3. Tra danh mục kỹ thuật để đoán bộ phận hỏng và ước lượng thời gian.   │
│   → 4. Lập phiếu tiếp nhận dịch vụ trên phần mềm xưởng.                     │
│                                                                             │
│ Bước nào tốn thời gian/dễ lỗi nhất?                                         │
│ Bước 2 & Bước 3 (mất 12–15 phút/lượt, dễ xếp nhầm nhóm thợ chuyên môn).     │
│                                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                                       │
│ Bước 1 & 2: Trích xuất các thực thể chính (vị trí kêu, điều kiện đường xá)  │
│ và tạo sẵn danh sách câu hỏi làm rõ để cố vấn kiểm tra nhanh.               │
│                                                                             │
│ Đo thành công bằng gì (Metric có số)?                                       │
│ - Giảm 50% thời gian tiếp nhận và lập phiếu dịch vụ ban đầu.                │
│ - Độ chính xác phân nhóm lỗi (gầm, điện, điều hòa, pin) đạt trên 85%.       │
│                                                                             │
│ Quick Architecture: [x] LLM Feature (Trích xuất thực thể & phân loại)      │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

### QUICK PROBLEM CARD #3: Vinmec — Tóm tắt hồ sơ bệnh án xuất viện

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                                       │
│                                                                             │
│ Bài toán (1 câu): Trích xuất dữ liệu lâm sàng từ phần mềm bệnh án để soạn   │
│ bản tóm tắt xuất viện bằng văn phong đại chúng cho người bệnh.              │
│ Đơn vị: [ ] Xanh SM     [ ] VinFast     [x] Vinmec                          │
│                                                                             │
│ Ai đang đau (Actor)?                                                        │
│ - Bác sĩ điều trị: Mất nhiều thời gian xử lý thủ tục giấy tờ cuối ca.       │
│ - Bệnh nhân/Người nhà: Không hiểu các thuật ngữ y khoa viết tắt trong hồ sơ.│
│                                                                             │
│ Workflow thủ công hiện tại:                                                 │
│   1. Bác sĩ mở bệnh án điện tử, rà soát kết quả xét nghiệm và đơn thuốc.    │
│   → 2. Tự tổng hợp lại diễn biến điều trị vào mẫu văn bản tóm tắt.          │
│   → 3. Viết thêm phần dặn dò ăn uống, kiêng khem và lịch tái khám.          │
│   → 4. In bản giấy và giải thích trực tiếp cho gia đình.                    │
│                                                                             │
│ Bước nào tốn thời gian/dễ lỗi nhất?                                         │
│ Bước 2 & Bước 3 (mất 20–25 phút/bệnh nhân).                                 │
│                                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                                       │
│ Bước 2 & 3: Tự trích xuất chẩn đoán chính, lọc danh sách thuốc và soạn bản   │
│ nháp giải thích ngắn gọn để bác sĩ kiểm tra và ký xác nhận.                 │
│                                                                             │
│ Đo thành công bằng gì (Metric có số)?                                       │
│ - Giảm thời gian chuẩn bị giấy xuất viện từ 25 phút xuống dưới 7 phút.      │
│ - 100% bản tóm tắt bắt buộc có chữ ký xác nhận của bác sĩ (HITL).           │
│                                                                             │
│ Quick Architecture: [x] LLM Feature (Tóm tắt tài liệu y khoa)              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Quyết định lựa chọn của nhóm

Nhóm chọn **Bài toán #1: Xanh SM — Điều phối xử lý sự cố pin xe taxi điện** để làm Deep-Dive.

### Lý do:
1. **Thiệt hại rõ ràng:** Mỗi xe dừng hoạt động vì cạn pin trực tiếp làm giảm doanh thu chạy xe của GSM và có thể gây cản trở giao thông nếu xe chết máy giữa đường.
2. **Ranh giới an toàn tường minh:**
   - Khi pin `< 5%`: Dừng ngay việc hướng dẫn đi trạm sạc xa quá 5 km; chuyển sang điều xe cứu hộ sạc pin lưu động tại chỗ.
   - Thẻ `[DRAFT_ONLY]`: Bắt buộc điều phối viên xem xét và bấm nút duyệt trước khi gửi cho tài xế, tránh gửi nhầm trạm đang lỗi hoặc lệch chuẩn sạc.
3. **Mức độ khả thi cao:** Bài toán giải quyết tốt bằng **LLM Feature kết hợp Rule Guardrails**, không cần dựng hệ thống Agent phức tạp tốn tài nguyên.
