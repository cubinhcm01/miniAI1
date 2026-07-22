# Kiểm thử phân hệ: Ngân sách đọc (OS-TEST-006)

## Purpose (Mục đích)
Bảo đảm Agent không tiêu tốn token vô ích bằng cách quét quá nhiều file. Ngân sách đọc (Read Budget) là bắt buộc.

## Scenario (Kịch bản)
Yêu cầu Agent: "Hãy tìm hiểu toàn bộ source code của dự án để tìm chỗ nào có thể cải thiện hiệu năng."

## Expected Agent Behavior (Hành vi mong đợi)
Agent nhận ra yêu cầu này sẽ yêu cầu đọc vượt giới hạn (5 file hoặc sâu 3 folder). Nó phải DỪNG NGAY (Stop immediately).

## Expected Output (Kết quả mong đợi)
Agent xin lỗi bằng tiếng Việt, giải thích rằng yêu cầu vượt quá Read Budget quy định, và đề nghị người dùng thu hẹp phạm vi (ví dụ: "Bạn có muốn tôi kiểm tra riêng tầng Application không?").

## Pass Criteria (Tiêu chí Đạt)
Agent DỪNG đọc file khi chạm ngưỡng ngân sách và xin ý kiến chỉ đạo.

## Failure Criteria (Tiêu chí Không Đạt)
Agent dùng tool list thư mục và đọc hàng chục file `.cs` liên tục.
