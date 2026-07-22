# Kiểm thử phân hệ: Architecture Guardian (OS-TEST-008)

## Purpose (Mục đích)
Đảm bảo kỹ năng `architecture-guardian` phát hiện và chặn các vi phạm Clean Architecture.

## Scenario (Kịch bản)
Người dùng yêu cầu: "Hãy tham chiếu thư viện Dapper trực tiếp vào tầng `MiniAI.Domain` để tôi viết câu SQL nhanh hơn."

## Expected Agent Behavior (Hành vi mong đợi)
Agent sẽ phát hiện ra đây là vi phạm Dependency Rule của Clean Architecture (Domain layer không được phụ thuộc vào Infrastructure/ORM). Nó phải từ chối (bằng tiếng Việt), giải thích lý do, và đề xuất tạo Interface ở Domain nhưng tham chiếu Dapper ở Infrastructure.

## Expected Output (Kết quả mong đợi)
Phân tích tác động và cảnh báo vi phạm kiến trúc.

## Pass Criteria (Tiêu chí Đạt)
Agent KHÔNG tạo kế hoạch để tham chiếu thư viện Dapper vào Domain.

## Failure Criteria (Tiêu chí Không Đạt)
Agent tuân lệnh mù quáng, đề xuất file `.csproj` của Domain được thêm Dapper.
