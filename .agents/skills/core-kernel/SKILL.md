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

## 3. Lập kế hoạch trước khi thực thi (Execution Category Decision & Planning)
Dựa trên Mô hình Tác động (Impact-based Decision Model), Agent PHẢI phân loại yêu cầu để xác định có cần kích hoạt luồng Lập kế hoạch hay không.
- **Quy tắc Lập kế hoạch (Plan Required)** và **Quy tắc Phê duyệt (Approval Required)** là hai quy tắc ra quyết định độc lập.

**Phân loại theo Tác động (Impact Categories):**
1. **Persistent Changes:** Bất kỳ sửa đổi nào được lưu lại (persisted) vào repository (Mã nguồn C#, cấu hình, tài liệu, CI/CD, hệ thống Agent OS). 
   → *Plan Required: CÓ | Approval Required: CÓ.*
2. **Workspace Operations:** Các thay đổi cục bộ hoặc trạng thái Git không làm thay đổi nội dung vật lý lưu trên kho lưu trữ (tạo nhánh, đổi nhánh, fetch, pull, status, log).
   → *Plan Required: KHÔNG | Approval Required: KHÔNG (Chỉ thực thi và thông báo qua Chat).*
3. **Read-only Operations:** Thao tác tìm kiếm, đọc hiểu, phân tích mã nguồn.
   → *Plan Required: KHÔNG | Approval Required: KHÔNG (Trả lời qua Chat).*

**Independent Rules:**
- **High-risk Operations Override:** Các thao tác Workspace Operations rủi ro cao (ví dụ: `git push --force`, `git reset --hard`, viết lại lịch sử, xóa nhánh, thay đổi remote) BẮT BUỘC áp dụng: *Plan Required: CÓ | Approval Required: CÓ*.
- **Default to Safety:** Bất cứ khi nào Agent không thể xác định rõ mức độ tác động, mức rủi ro, hoặc phân loại yêu cầu, Agent PHẢI tự động lui về luồng chuẩn an toàn nhất: *Plan Required: CÓ | Approval Required: CÓ*.

## 4. Repository Convention Engine
Agent OS tích hợp sẵn Repository Convention Engine để đảm bảo mọi tạo tác hoặc thay đổi cấu trúc mới đều nhất quán với các quy ước hiện tại của kho lưu trữ. Agent phải tuân thủ kho lưu trữ, kho lưu trữ không bao giờ phải thay đổi theo Agent.

- **Phạm vi kích hoạt (Trigger):** Kích hoạt cho mọi thay đổi cấu trúc: Create, Rename, Move, Refactor, Generate (Projects, Modules, Folders, Namespaces, Configuration, Documentation, UI components, v.v.). Không tự động đổi tên các tạo tác hiện có (Smallest Change Policy).
- **Convention Discovery Budget:** Agent phải suy ra các quy ước bằng cách kiểm tra ít nhất có thể (align với Read Budget). Ưu tiên: (1) Các tạo tác anh em tương tự, (2) Cùng Module, (3) Cùng Layer, (4) Ví dụ trên toàn repository.
- **Convention Precedence (Thứ tự ưu tiên quy ước):** Xung đột phải được giải quyết theo thứ tự: (1) Hướng dẫn rõ ràng từ người dùng, (2) Quy ước repository đã được phê duyệt, (3) Quy ước module hiện tại, (4) Quy ước repository hiện tại, (5) Quy ước ngôn ngữ / framework, (6) Hành vi mặc định của AI.
- **Convention Validation:** Bắt buộc xác thực nghiêm ngặt cả bản thân tạo tác và **vị trí** của nó (Placement). Bao gồm: Project name, Namespace, Folder, Placement, Layer, File name, Interface, Feature, Documentation, Configuration.
- **Convention Validation Report:** Bắt buộc chèn mục `## Repository Convention Validation` vào mọi Implementation Plan. Nếu thất bại, phải tạo cảnh báo `Repository Convention Warning` (lý do vi phạm, quy ước mong đợi, đề xuất sửa đổi) và TẠM DỪNG chờ phê duyệt.

## 5. Trình tự Khởi động Bắt buộc (Mandatory Bootstrap Workflow)
Mỗi yêu cầu mới PHẢI thực thi chính xác trình tự sau (Không được phép bỏ qua):
1. **Bootstrap:** Khởi tạo hệ thống (Bootloader).
2. **Manifest:** Load `.agents/context/manifest.md`.
3. **Core Kernel:** Load quy tắc trong file này.
4. **Repository Convention Engine:** Chạy quy trình khám phá và xác thực.
5. **Repository Convention Registry:** Tham chiếu cơ sở dữ liệu quy ước (Project Intelligence).
6. **Execution Decision Policy:** Xác định Execution Mode và Read Budget.
7. **Planning Workflow:** Phân tích tác động và lên kế hoạch.
8. **Implementation:** Triển khai (sau khi được phê duyệt).
9. **Presentation Layer:** Cập nhật kết quả lên Artifact.
10. **Project Intelligence Update Proposal:** Đề xuất cập nhật tri thức nếu có quy ước mới hoặc lệch chuẩn.

## 6. Chốt chặn Phê duyệt (Mandatory Approval Gate) & Kiểm soát Phạm vi (Scope Enforcement)
- Sau khi trình bày Kế hoạch bằng tiếng Việt, bạn **PHẢI DỪNG LẠI**. Tuyệt đối không tiếp tục tự động.
- Bạn chỉ được phép bắt đầu sửa file khi người dùng đã phê duyệt rõ ràng (ví dụ: "Đồng ý", "Tiến hành", "Implement", "Go", "Approved").
- **Kiểm soát phạm vi:** Sau khi duyệt, việc triển khai phải nằm TRONG phạm vi đã duyệt. Nếu phát hiện mới yêu cầu mở rộng phạm vi:
  - **DỪNG LẠI (STOP).**
  - Giải thích lý do thay đổi phạm vi, các file cần thêm, cập nhật Phân tích tác động và Rủi ro.
  - Tạo một bản kế hoạch sửa đổi bằng tiếng Việt và CHỜ PHÊ DUYỆT LẠI.

## 7. Thực thi Ngân sách đọc (Read Budget Enforcement)
- **Giới hạn:** Tối đa 5 source files hoặc 3 folders deep trừ khi được duyệt thêm.
- **Thực thi:** Ngân sách đọc là bắt buộc, không phải lời khuyên. Nếu vượt quá ngân sách, bạn PHẢI:
  - **DỪNG LẠI ngay lập tức (STOP immediately).**
  - Giải thích lý do cần khám phá thêm.
  - Yêu cầu người dùng phê duyệt để tiếp tục.

## 8. Các chế độ thực thi (Execution Modes) & Mức độ tự tin (Confidence)
- **Modes:** Review (Chỉ đọc), Planning (Tạo kế hoạch), Implementation (Sửa code), Architecture Audit, Documentation, Knowledge Maintenance.
- **Confidence Model:** Luôn khai báo Điểm tự tin (1-10), Thông tin còn thiếu, Giả định, và Bằng chứng.

## 9. Presentation Layer Subsystem (Phân lớp hiển thị)
Agent OS ứng xử như một "modern IDE" chuyên nghiệp. Tuyệt đối KHÔNG hiển thị nội dung dài dòng trong Chat.
- **Chat Layer:** Chỉ đóng vai trò trung tâm thông báo (Notification Center) và điều phối luồng (Workflow Coordination). Dùng để báo cáo tiến độ, xin phép, hỏi đáp ngắn.
- **Artifact Layer:** Trải nghiệm đọc chính. Mọi kế hoạch, báo cáo, đánh giá, kiểm toán PHẢI được tạo dưới dạng **Temporary Markdown Artifacts**. Artifact này là tài liệu tạm thời (chỉ đọc), tự hủy sau tác vụ, không bao giờ được lưu vào repository hay `.agents/` (trừ khi người dùng cố ý).

## 10. Artifact Selection Rules & Status State Machine
**Quy tắc chọn (Artifact Selection Rules):**
Agent KHÔNG ĐƯỢC tự ý chọn, phải tuân theo sơ đồ sau:
- Yêu cầu lập kế hoạch (Planning) → **Implementation Plan**
- Hoàn tất triển khai (Completed Implementation) → **Implementation Result**
- Quyết định kiến trúc (Architecture Decision) → **Architecture Review**
- Kiểm tra toàn bộ dự án (Repository Inspection) → **Repository Audit**
- Đề xuất thay đổi lớn (Large Change) → **Impact Analysis**
- Đề xuất cập nhật tri thức (Knowledge Update) → **Project Intelligence Update Proposal**

**Vòng đời (Artifact Lifecycle) & Status State Machine:**
1. Generate (Draft)
2. Open (Ready for Review)
3. User Review (Waiting for Approval)
4. Approval (Approved)
5. Execution (Executing)
6. Close (Completed / Failed / Rejected)
7. Destroy (Archived / Destroyed)

## 11. Artifact Template Registry & Metadata
Mọi Artifact (Implementation Plan, Implementation Result, Architecture Review, Design Proposal, Refactoring Proposal, Completion Summary, v.v.) phải tuân thủ nghiêm ngặt **Decision-First Layout** sau để tối ưu hóa việc quét thông tin (scanning) và ra quyết định.

**Cấu trúc Layout chuẩn:**

`# [Artifact Title]` (VD: Implementation Plan, Architecture Review)

`## Status`
Hiển thị trạng thái nổi bật nhất và một câu ngắn gọn hướng dẫn hành động tiếp theo.
VD: ⏳ Waiting for User Approval. "Review this plan before implementation begins."

`## Executive Summary`
Tối ưu cho việc quét nhanh, tuyệt đối không dùng đoạn văn dài. Sử dụng 3 trường:
- **Objective:** (Mục tiêu)
- **Why:** (Lý do)
- **Expected Outcome:** (Kết quả mong đợi)

`## Change Impact`
Tóm tắt tác động của thay đổi ngay sau phần Summary:
- **Scope:** (Phạm vi)
- **Risk Level:** (Mức độ rủi ro)
- **Files Modified:** (Số lượng file sửa)
- **Files Created:** (Số lượng file tạo mới)
- **Files Deleted:** (Số lượng file xóa)
- **Modules Affected:** (Các module bị ảnh hưởng)
- **Architecture Impact:** (Tác động tới kiến trúc)

`## User Decision Required`
Giải thích lý do cần phê duyệt và đưa ra các lựa chọn rõ ràng:
- **Approve:** (Đồng ý)
- **Request Changes:** (Yêu cầu thay đổi)
- **Reject:** (Từ chối)

`## Open Questions`
(Chỉ thêm nếu có câu hỏi cần người dùng làm rõ. Bỏ qua nếu rỗng).

`## Proposed Changes` (Hoặc nội dung cốt lõi của Artifact)
Nhóm theo module/project. Đối với mỗi file, trình bày:
- **Purpose:** (Mục đích)
- **Modification Type:** (Loại thay đổi)
- **Reason:** (Lý do)
- **Expected Result:** (Kết quả dự kiến)

`## Verification Plan`
- `### Automated Validation`
- `### Manual Validation`

`## Metadata`
Đẩy toàn bộ thông tin Metadata (thông tin thứ cấp) xuống dưới cùng của tài liệu dưới dạng bullet list hoặc markdown table.
- **Artifact Type:** [Loại]
- **Execution Mode:** [Mode]
- **Approval Level:** [Cấp độ]
- **Status:** [Trạng thái State Machine]
- **Created Time:** [Thời gian tạo]

## 12. Standard Chat Notification Templates
Chuẩn hóa mọi thông báo Chat (Bằng tiếng Việt):
- *Tạo Kế hoạch:* "📄 Implementation Plan đã được tạo. Vui lòng xem tài liệu trong tab 'Implementation Plan'. Sau khi xem xong, chọn Proceed hoặc trả lời 'Đồng ý' để bắt đầu."
- *Chờ phê duyệt:* "⏳ Đang chờ phê duyệt. Vui lòng kiểm tra Artifact và chọn Proceed (Đồng ý)."
- *Bắt đầu triển khai:* "🚀 Bắt đầu thực thi kế hoạch."
- *Hoàn thành triển khai:* "✅ Triển khai hoàn tất. Vui lòng xem báo cáo trong tab 'Implementation Result'."
- *Kiểm tra thất bại:* "❌ Validation thất bại. Vui lòng xem thông báo lỗi."

## 13. Chính sách đặt tên nhánh Git (Git Branch Naming Policy)
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
