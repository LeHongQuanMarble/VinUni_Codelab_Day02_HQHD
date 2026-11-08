# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)
Quy trình xử lý phản ánh lỗi phần mềm / tính năng thông minh hiện tại của CSKH & kỹ thuật viên hỗ trợ từ xa VinFast:
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Tiếp nhận    │     │ Hỏi thêm     │     │ Tra cứu thủ  │     │ Đưa hướng    │
│ phản ánh     │ ──→ │ thông tin    │ ──→ │ công kiến    │ ──→ │ xử lý /      │
│ từ App /     │     │ từ chủ xe    │     │ thức & case  │     │ chuyển xưởng │
│ Tổng đài /   │     │              │     │ tương tự     │     │              │
│ Diễn đàn     │     │              │     │              │     │              │
│              │     │              │     │              │     │              │
│ Ai: CSKH     │     │ Ai: CSKH     │     │ Ai: CSKH /   │     │ Ai: CSKH /   │
│ ⏱ 1-2 phút  │     │ ⏱ 3-5 phút  │     │ Kỹ thuật     │     │ Kỹ thuật     │
│              │     │              │     │ ⏱ 5-8 phút 🔴│     │ ⏱ 2-3 phút  │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
* 🔴 **Bottleneck:**: Bước 3 (tra cứu thủ công kiến thức + case tương tự) — mất nhiều thời gian nhất và dễ đưa hướng xử lý chưa tối ưu.
* 🔄 **Handoff:** Từ CSKH → Kỹ thuật viên hỗ trợ từ xa (khi lỗi phức tạp hoặc liên quan an toàn).
* Tổng thời gian trung bình ước tính: 12–18 phút/lượt (giả định dựa trên quan sát cộng đồng và mô tả quy trình hỗ trợ hiện tại).



## 3.2. Problem Statement (6-field) & Metrics (15 min)
Điền đầy đủ 6 trường thông tin của bài toán:

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Nhân viên Chăm sóc khách hàng (CSKH) và kỹ thuật viên hỗ trợ từ xa của VinFast. |
| **2. Current Workflow** | Chủ xe gửi phản ánh lỗi phần mềm/tính năng thông minh qua App, tổng đài hoặc diễn đàn → CSKH hỏi thêm thông tin → tra cứu thủ công kiến thức và case tương tự → đưa hướng xử lý (reset, kiểm tra kết nối, đề xuất OTA, hoặc hẹn xưởng). Quy trình hoàn toàn thủ công, mất trung bình 12–18 phút/lượt. |
| **3. Bottleneck** | Bước tra cứu kiến thức và case tương tự (Bước 3). Nhân viên phải nhớ hoặc tìm kiếm nhiều nguồn thông tin, dễ bỏ sót case đã biết hoặc đưa hướng xử lý chưa phù hợp, đặc biệt với các lỗi ADAS / kết nối / tài khoản. |
| **4. Business Impact** | Tăng thời gian xử lý mỗi ticket → tăng tải cho đội ngũ CSKH và kỹ thuật. Chủ xe phải chờ lâu hơn, dẫn đến trải nghiệm hậu mãi giảm và tăng tỉ lệ leo thang khiếu nại không cần thiết. |
| **5. Success Metric** | 1. Giảm thời gian triage trung bình từ ~15 phút xuống dưới 3 phút.
2. Tỉ lệ đề xuất bước xử lý đầu tiên đúng hướng ≥ 85% (đo trên mẫu ticket được kỹ thuật viên gắn nhãn). |
| **6. Operational Boundary** | AI được phép: Phân loại mức độ nghiêm trọng, nhóm lỗi, đề xuất bước xử lý đầu tiên, soạn tin nhắn nháp gửi chủ xe.
AI tuyệt đối không được: Kết luận chắc chắn là lỗi phần cứng; hứa thời gian sửa chữa hoặc miễn phí; tự ý đưa hướng dẫn sửa chữa kỹ thuật sâu với lỗi liên quan an toàn (phanh, lái, ADAS bất thường, mất kiểm soát…). Các trường hợp an toàn phải được đánh dấu escalate ngay cho người. Mọi output phải ở dạng nháp ([DRAFT_ONLY]) để con người duyệt trước khi gửi. |

## 3.3. Future-State Flow & AI Fit (25 min)
* **AI Fit (AI-Fit Matrix):** LLM Feature.
* **Quy trình tương lai (Future-State):**
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Tiếp nhận    │     │ 🔵 AI Triage │     │ 🟢 Human     │     │ Gửi hướng    │
│ phản ánh     │ ──→ │ (phân loại + │ ──→ │ Review &     │ ──→ │ dẫn đã được  │
│              │     │ đề xuất +    │     │ chỉnh sửa    │     │ duyệt        │
│              │     │ soạn nháp)   │     │ (HITL)       │     │              │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                              │
                                              ▼
                                       ↩️ Fallback:
                                       Nếu AI trả về
                                       kết quả không
                                       tự tin hoặc
                                       vi phạm ranh giới
                                       → CSKH/Kỹ thuật
                                       xử lý hoàn toàn
                                       thủ công như cũ.
  * 🔵 **AI Step:** Phân loại severity + category, đề xuất bước đầu, soạn draft_message_to_customer.
  * 🟢 **Human Step (HITL):** Nhân viên kiểm tra, chỉnh sửa nếu cần, rồi mới gửi hoặc chuyển xưởng.
  * ↩️ **Fallback:** hi AI đánh dấu escalation = immediate_human hoặc độ tin cậy thấp → chuyển ngay cho kỹ thuật viên xử lý thủ công.

---


# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [ ] **Chưa đủ dữ liệu mẫu/logs sạch để đánh giá.** Trong workspace hiện chưa có bộ ticket VinFast đã khử định danh và được kỹ thuật viên gắn nhãn. Thời gian xử lý 12–18 phút/lượt ở phần workflow đang là ước tính, chưa phải baseline đo từ dữ liệu vận hành.
2. [ ] **Đang kiểm soát một phần, chưa xác nhận đầy đủ.** Quy trình yêu cầu `[DRAFT_ONLY]`, người thật duyệt, chuyển lỗi an toàn cho người và có fallback thủ công. Tuy vậy, bộ test hiện chưa hoàn tất; các kiểm tra tự động chủ yếu dò định dạng/cụm từ, và một số hướng dẫn kỹ thuật của mô hình vẫn cần đối chiếu tài liệu VinFast.
3. [ ] **Chưa xác nhận mức sẵn sàng của các bên liên quan.** Chưa có ghi nhận phỏng vấn hoặc xác nhận từ CSKH, kỹ thuật viên và bộ phận phụ trách dữ liệu về quy trình, quyền truy cập dữ liệu và cách dùng bản nháp AI.

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[ ] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[x] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Chuẩn bị dữ liệu và xác minh quy trình trước khi thử nghiệm với ticket thật.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> Chọn **NOT YET** vì vấn đề có phạm vi phù hợp để thử một LLM Feature: đọc mô tả tự do, phân loại lỗi và soạn bản nháp cho CSKH/kỹ thuật viên. Ranh giới đề xuất cũng giữ quyền quyết định ở con người và chuyển các tình huống an toàn sang xử lý trực tiếp. Tuy nhiên, chưa có ticket đã khử định danh để kiểm tra độ chính xác, chưa đo baseline thời gian triage, và chưa xác nhận quy trình với người vận hành. Các con số 12–18 phút/lượt, mục tiêu dưới 3 phút và độ chính xác 85% hiện là ước tính/mục tiêu đề xuất, chưa phải kết quả đã chứng minh. Prototype cũng chưa hoàn tất kiểm chứng tất cả test và đầu ra kỹ thuật cần được rà soát với tài liệu chính hãng. Chưa có dữ liệu về chi phí API, tích hợp hoặc lợi ích định lượng để kết luận hiệu quả tài chính.
>
> **Điều kiện để xem xét GO cho pilot hẹp:** (1) đội CSKH/kỹ thuật cung cấp bộ ticket mẫu đã khử định danh và gắn nhãn; (2) đo thời gian xử lý hiện tại làm baseline; (3) kỹ thuật viên rà soát hướng dẫn và danh sách ca phải escalation; (4) chạy đủ test an toàn trên dữ liệu giả lập/được phép sử dụng, không gửi dữ liệu cá nhân hoặc thông tin xe nhạy cảm lên API khi chưa được phê duyệt; (5) thống nhất cách đo độ chính xác, thời gian tiết kiệm, chi phí và cơ chế duyệt bản nháp. Nếu không đạt các điều kiện này, tiếp tục xử lý thủ công và chưa đưa AI vào quy trình thật.

---
