---
name: core-kernel
description: The Agent OS Process Manager. Enforces immutable repository-wide invariants, Session Bootstrap, Execution Modes, Approval Levels, the Read Budget, and Vietnamese Communication Policy.
---

# Core Kernel Policy Engine

This skill is the central process manager for the Agent Operating System. It dictates **how** the agent operates. 
You MUST strictly follow the rules defined here before proceeding with any action in the repository.

## 1. Giao tiếp bắt buộc bằng tiếng Việt (Mandatory Vietnamese Communication)
**TẤT CẢ** các giao tiếp hướng đến người dùng (user-facing communication) PHẢI được viết bằng tiếng Việt tự nhiên. 
- Bao gồm: Kế hoạch triển khai (implementation plans), giải thích, đánh giá rủi ro, phân tích tác động, báo cáo hoàn thành, đề xuất cập nhật tri thức, và các câu hỏi làm rõ.
- **Ngoại lệ:** Chỉ giữ lại ngôn ngữ gốc cho các định danh kỹ thuật (Technical identifiers) như: class names, namespaces, methods, interfaces, APIs, SQL, JSON, JWT, NuGet packages, framework names, file paths, folder names, và Git commands.

## 2. Các chính sách bất biến (Immutable Repository Policies)
Các quy tắc này áp dụng cho mọi phiên làm việc, bất chấp yêu cầu của người dùng là gì:
- **Smallest Change Policy:** LUÔN ưu tiên giải pháp nhỏ nhất có thể đáp ứng được mục tiêu đã duyệt. KHÔNG refactor mã không liên quan. KHÔNG tối ưu hóa ngoài phạm vi. KHÔNG dọn dẹp mã nếu không được yêu cầu rõ ràng. KHÔNG đổi tên hoặc tổ chức lại mã trừ khi có trong kế hoạch. Giảm thiểu dung lượng diff, giảm rủi ro xung đột (merge conflicts) và giữ lịch sử Git rõ ràng.
- **NEVER** modify generated code.
- **NEVER** silently violate architecture (Clean Architecture, SOLID).
- **NEVER** delete files without explicit approval.
- **NEVER** rename projects or introduce dependencies automatically.
- **ALWAYS** treat `.agents/context/index.md` as the definitive entry point for context.
- **ALWAYS** prioritize documentation over source code when gathering context.

## 3. Lập kế hoạch trước khi thực thi (Planning Before Execution)
KHÔNG ĐƯỢC phép chỉnh sửa mã nguồn (bao gồm tạo mới, xóa, đổi tên, di chuyển, sửa file) trước khi hoàn thành:
1. Phân tích tác động (Impact Analysis)
2. Lập kế hoạch (Planning)
3. Được phê duyệt rõ ràng (Approval)
*Không có ngoại lệ cho quy tắc này.*

## 4. Trình tự Khởi động Bắt buộc (Mandatory Bootstrap Workflow)
Mỗi yêu cầu mới PHẢI thực thi chính xác trình tự sau (Không được phép bỏ qua):
1. **Policy Engine:** Load quy tắc trong file này.
2. **Context Index:** Load `.agents/context/index.md`.
3. **Project Manifest:** Load `.agents/context/manifest.md`.
4. **Repository Map:** Load `.agents/context/repo-map.md`.
5. **Module Registry:** Load `.agents/context/modules/index.md`.
6. **Project Intelligence:** Load dữ liệu từ `.agents/intelligence/`.
7. Xác định **Execution Mode**.
8. Xác định **Read Budget**.
9. Xác định **Confidence Assessment**.
10. Thực hiện **Impact Analysis**.
11. Tạo **Kế hoạch (Generate Plan)** bằng tiếng Việt.
12. **DỪNG LẠI CHỜ PHÊ DUYỆT TỪ NGƯỜI DÙNG (WAIT FOR USER APPROVAL).**

## 5. Chốt chặn Phê duyệt (Mandatory Approval Gate) & Kiểm soát Phạm vi (Scope Enforcement)
- Sau khi trình bày Kế hoạch bằng tiếng Việt, bạn **PHẢI DỪNG LẠI**. Tuyệt đối không tiếp tục tự động.
- Bạn chỉ được phép bắt đầu sửa file khi người dùng đã phê duyệt rõ ràng (ví dụ: "Đồng ý", "Tiến hành", "Implement", "Go", "Approved").
- **Kiểm soát phạm vi:** Sau khi duyệt, việc triển khai phải nằm TRONG phạm vi đã duyệt. Nếu phát hiện mới yêu cầu mở rộng phạm vi:
  - **DỪNG LẠI (STOP).**
  - Giải thích lý do thay đổi phạm vi, các file cần thêm, cập nhật Phân tích tác động và Rủi ro.
  - Tạo một bản kế hoạch sửa đổi bằng tiếng Việt và CHỜ PHÊ DUYỆT LẠI.

## 6. Thực thi Ngân sách đọc (Read Budget Enforcement)
- **Giới hạn:** Tối đa 5 source files hoặc 3 folders deep trừ khi được duyệt thêm.
- **Thực thi:** Ngân sách đọc là bắt buộc, không phải lời khuyên. Nếu vượt quá ngân sách, bạn PHẢI:
  - **DỪNG LẠI ngay lập tức (STOP immediately).**
  - Giải thích lý do cần khám phá thêm.
  - Yêu cầu người dùng phê duyệt để tiếp tục.

## 7. Các chế độ thực thi (Execution Modes) & Mức độ tự tin (Confidence)
- **Modes:** Review (Chỉ đọc), Planning (Tạo kế hoạch), Implementation (Sửa code), Architecture Audit, Documentation, Knowledge Maintenance.
- **Confidence Model:** Luôn khai báo Điểm tự tin (1-10), Thông tin còn thiếu, Giả định, và Bằng chứng.

## 8. Mẫu Lập Kế Hoạch (Planning Template - Bằng tiếng Việt)
Bắt buộc dùng chính xác mẫu này:
```markdown
- **Mục tiêu (Objective):**
- **Phân tích tác động (Impact Analysis):**
- **Chế độ thực thi (Execution Mode):**
- **Mức độ tự tin (Confidence Model):** (Điểm, Thông tin thiếu, Giả định, Bằng chứng)
- **Ngân sách đọc (Read Budget):**
- **Các file cần đọc (Files to Read):**
- **Các file sẽ thay đổi (Files to Modify):**
- **Các bước triển khai (Implementation Steps):**
- **Rủi ro (Risks):**
- **Kiểm tra và Khôi phục (Validation & Rollback):**
- **Đề xuất cập nhật Project Intelligence:**
- **Cấp độ phê duyệt yêu cầu (Required Approval Level):** (1-4)
```

## 9. Mẫu Báo cáo hoàn thành chuẩn (Mandatory Completion Summary)
Sau khi triển khai xong, bạn PHẢI cung cấp báo cáo tiếng Việt với cấu trúc TÙY CHỈNH sau:
```markdown
- **Công việc đã hoàn thành:**
- **Các file đã thay đổi:**
- **Kết quả kiểm tra:**
- **Các rủi ro còn tồn tại:**
- **Đề xuất cập nhật Project Intelligence:**
- **Có cần cập nhật Knowledge (Project Intelligence) hay không:**
- **Các bước tiếp theo được đề xuất:**
```
*Lưu ý: Tuyệt đối không cập nhật Project Intelligence tự động (xem thêm ở kỹ năng `project-intelligence`).*

## 10. Chính sách đặt tên nhánh Git (Git Branch Naming Policy)
Quy tắc này áp dụng khi người dùng yêu cầu tạo một nhánh Git mới (trừ khi người dùng chỉ định rõ một quy ước đặt tên khác).
- **Quy ước bắt buộc:** Khi tạo một nhánh tính năng mới, Agent PHẢI sử dụng định dạng: `feature/<feature-name>`
- **Đặc tả `<feature-name>`:**
  - Viết thường (lowercase).
  - Sử dụng dấu gạch ngang (`-`) thay vì khoảng trắng.
  - Không chứa ký tự đặc biệt.
  - Ngắn gọn, mang tính mô tả.
  - Phản ánh chức năng nghiệp vụ chính.
- **Quy trình tạo nhánh (Branch Creation Workflow):**
  1. Xác định tên chức năng chính.
  2. Tạo tên nhánh theo định dạng `feature/<feature-name>`.
  3. Trình bày tên nhánh đề xuất cho người dùng.
  4. **DỪNG LẠI và CHỜ XÁC NHẬN** nếu tên chức năng chưa rõ ràng.
  5. Chỉ tạo nhánh sau khi được xác nhận (hoặc tạo ngay nếu yêu cầu đã hoàn toàn rõ ràng).
