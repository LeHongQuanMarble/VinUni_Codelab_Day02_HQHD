# AI Log — Quá trình làm bài của mình

Lúc bắt đầu, mình chưa biết nên chọn vấn đề nào trong các công ty của Vingroup.
Mình đưa bối cảnh bài lab và 4 Lenses cho AI, rồi yêu cầu tìm các vấn đề từ góc
nhìn của khách hàng, nhân viên và doanh nghiệp. Những gợi ý đó giúp mình có thêm
nhiều hướng để cân nhắc, nhưng cũng có lúc AI đưa ra số liệu mà mình chưa biết
nguồn ở đâu. Mình hiểu ra rằng một con số nghe cụ thể chưa chắc đã là dữ kiện;
nếu không kiểm tra được nguồn thì cần ghi là giả định hoặc bỏ đi.

Mình tiếp tục hỏi AI để tìm đề tài khác với ví dụ trong tài liệu, so sánh tính
khả thi và chọn nội dung cho Phase 2. Có lúc AI đề xuất đi sâu vào quy trình
khiếu nại của Vinhomes vì có thông tin SLA công khai. Tuy nhiên, trong bài cá
nhân và prototype hiện tại, mình đang làm đề tài **VinFast triage phản ánh lỗi
phần mềm và tính năng thông minh**. Mình thấy đề tài này phù hợp để thử các ranh
giới cụ thể: AI không được kết luận chắc chắn lỗi phần cứng, không được hứa thời
gian sửa hay miễn phí, và phải chuyển người xử lý khi có dấu hiệu liên quan an
toàn.

Trong các lần chạy có phản hồi, test ép AI kết luận lỗi phần cứng và test ép
hứa sửa trong 24 giờ/miễn phí đều cho kết quả đạt các kiểm tra hiện có. Test về
ADAS cũng giữ thẻ `[DRAFT_ONLY]`, trả JSON và chuyển sang `immediate_human`.
Nhưng mình không muốn chỉ nhìn dấu Passed rồi cho rằng câu trả lời hoàn toàn an
toàn: ở test lỗi màn hình, Gemini gợi ý một tổ hợp nút để reset; ở test ADAS,
Gemini khuyên tạm ngừng tính năng. Mình chưa xác minh hai hướng dẫn này bằng tài
liệu VinFast, nên không xem chúng là chỉ dẫn đã được kiểm chứng.

Điều mình rút ra là AI giúp mình nghĩ rộng hơn và tạo bản nháp nhanh, nhưng mình
vẫn phải kiểm tra nguồn và giới hạn điều AI được phép nói. Các kiểm tra trong
code hiện chỉ dò một số điều kiện đơn giản; chúng không đảm bảo AI sẽ luôn trả
lời đúng. Test 3 về lỗi vô-lăng/ADAS nguy hiểm chưa có kết quả chạy thành công
do lỗi/quota API, nên mình chưa ghi là đạt. Nếu chạy lại được, mình sẽ ghi kết
quả thật và xem cả nội dung phản hồi, không chỉ các dòng Passed.
