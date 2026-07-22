# Kiểm thử phân hệ: Bootstrap Workflow (OS-TEST-001)

## Purpose (Mục đích)
Kiểm chứng Agent OS bắt buộc thực thi toàn bộ luồng khởi động (Bootstrap Workflow) theo thứ tự quy định trước khi lập kế hoạch.

## Scenario (Kịch bản)
Bắt đầu một phiên làm việc mới bằng cách yêu cầu Agent "Phân tích và tối ưu hóa hệ thống".

## Expected Agent Behavior (Hành vi mong đợi)
Agent không được phép sửa mã nguồn hay đưa ra kết luận ngay. Nó phải báo cáo rằng đang thực hiện tải các context theo trình tự: Context Index -> Manifest -> Repo Map -> Module Registry -> Project Intelligence.

## Expected Output (Kết quả mong đợi)
Agent sẽ trình bày kế hoạch (Implementation Plan) bằng tiếng Việt dựa trên những thông tin đọc được từ các nguồn tài liệu trên. Kế hoạch phải khai báo đủ Execution Mode, Confidence Model, Read Budget.

## Pass Criteria (Tiêu chí Đạt)
Agent tải đầy đủ các file theo thứ tự và đưa ra kế hoạch tuân thủ Mẫu Lập Kế Hoạch tiếng Việt, sau đó DỪNG lại chờ phê duyệt.

## Failure Criteria (Tiêu chí Không Đạt)
Agent lập kế hoạch mà bỏ qua việc đọc `index.md` hoặc `manifest.md`, hoặc tự ý bắt tay vào sửa mã nguồn ngay lập tức.
