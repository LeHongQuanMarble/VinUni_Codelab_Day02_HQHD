# AI Log — Cách mình dùng AI khi làm Lab 02

Mình bắt đầu bằng cách đưa cho AI bối cảnh Vin Smart Future, 4 Lenses và yêu
cầu tìm các vấn đề vận hành có ảnh hưởng đến khách hàng hoặc doanh nghiệp. Khi
các gợi ý đầu tiên còn gần với ví dụ trong tài liệu, mình nói rõ hơn rằng mình
muốn tìm đề tài mới, nhìn từ nhiều phía và có tìm kiếm thông tin tham khảo. Sau
đó, mình nhờ AI so sánh các lựa chọn theo mức độ khả thi và khả năng hoàn thành
các phần của lab, rồi hỏi cách triển khai Phase 2 cho đề tài đã chọn.

Nhìn lại, các yêu cầu mình đặt cho AI có thể tóm tắt như sau:

- Dựa vào bối cảnh và 4 Lenses, gợi ý các pain point thực tế cho khách hàng,
  nhân viên và doanh nghiệp.
- Tìm thêm hướng khác với ví dụ có sẵn; nêu nguồn và phân biệt thông tin có
  bằng chứng với giả thuyết.
- So sánh đề tài theo dữ liệu cần có, khả năng làm prototype, rủi ro và khả năng
  hoàn thành yêu cầu của lab.
- Giúp mình hiểu `prompt_prototype.py` cần thay đổi gì để khớp đề tài cá nhân,
  rồi hỗ trợ rà checklist Phase 5 theo những gì đã biết và chưa biết.

AI giúp mình mở rộng danh sách và chia một đề tài lớn thành các phần có thể làm
được. Nhưng mình cũng thấy AI có thể đưa ra số liệu cụ thể mà nguồn chưa rõ, hoặc
đề xuất một đề tài cho Deep-Dive khác với đề tài mình đang theo trong các file
cá nhân. Mình phải đối chiếu gợi ý với `01-problem-scan.md` và prototype trước
khi quyết định tiếp tục với **VinFast triage phản ánh lỗi phần mềm/tính năng
thông minh**. Những con số chưa kiểm chứng mình giữ ở dạng giả định/mục tiêu,
không xem là dữ liệu vận hành đã được xác nhận.

Khi chuyển sang code, mình hỏi AI cách sửa starter code theo bài toán VinFast.
AI giúp nhận ra phần kiểm tra ban đầu còn mang quy tắc Xanh SM về pin và trạm
sạc, nên mình đổi hướng kiểm tra sang các ranh giới của bài mình: không chẩn
đoán chắc chắn lỗi phần cứng, không hứa thời gian sửa hay miễn phí, và chuyển
vấn đề an toàn cho người xử lý. Mình cũng gặp lỗi model ID/API trong lúc chạy;
điều đó khiến mình phải phân biệt lỗi dịch vụ với lỗi trong prompt, thay vì kết
luận ngay rằng mô hình đã vượt qua hoặc thất bại.

Một điểm mình cần giữ cảnh giác là Gemini có thể đưa ra chỉ dẫn kỹ thuật nghe
hợp lý nhưng mình chưa xác minh được, như cách reset màn hình hoặc tạm ngừng
ADAS. Vì thế, mình không lấy câu trả lời của AI làm hướng dẫn chính thức. Mình
cần kiểm tra các thao tác đó với tài liệu VinFast và giữ bước CSKH/kỹ thuật viên
duyệt nội dung trước khi gửi khách.

Khi nhờ AI hoàn thiện Phase 5 trong `02-deep-dive-report.md`, mình yêu cầu đánh
giá dựa trên dữ liệu hiện có, không tự giả định rằng đã có ticket sạch hay ý
kiến của đội vận hành. Việc này giúp mình chọn **NOT YET**: workflow và metric
hiện vẫn có phần ước tính, chưa có bộ ticket được gắn nhãn, baseline đo thực tế
hay xác nhận từ CSKH/kỹ thuật viên. Đây là quyết định dựa trên những khoảng
trống cần giải quyết trước khi thử với ticket thật.

AI cũng từng viết AI Log quá giống bản tổng hợp test và dùng giọng không giống
mình. Mình yêu cầu viết lại ở ngôi “mình”, tập trung vào quá trình sử dụng AI,
điều mình phải kiểm tra và cách mình điều chỉnh, thay vì chép kết quả console.
Qua bài này, mình thấy AI hữu ích để brainstorm và sắp xếp suy nghĩ, nhưng mình
vẫn phải kiểm tra nguồn, đối chiếu đúng đề tài và chịu trách nhiệm với quyết
định cuối cùng.
