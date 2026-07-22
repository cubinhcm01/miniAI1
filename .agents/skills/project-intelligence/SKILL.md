---
name: project-intelligence
description: The Librarian & Memory. Governs the Information Architecture, Living Memory (snapshots/health/logs), Evolution, and Drift Detection.
---

# Project Intelligence

This skill controls how the Agent OS remembers context and evolves with the repository. 
You MUST interact với thư mục `.agents/context/` và `.agents/intelligence/` theo các quy tắc nghiêm ngặt sau.

## Kiến trúc thông tin (Information Architecture)
- **Context Index (`.agents/context/index.md`):** Điểm bắt đầu tuyệt đối của bạn. Tài liệu này quy định thứ tự đọc và ưu tiên của mọi tài liệu khác.
- **Project Manifest (`.agents/context/manifest.md`):** Nguồn sự thật duy nhất về trạng thái dự án, công nghệ và vòng đời.
- **Module Registry (`.agents/context/modules/index.md`):** Mục lục mở rộng của các ranh giới module.
- **Repository Map (`.agents/context/repo-map.md`):** Sơ đồ cấu trúc nhẹ nhằm tránh quét toàn bộ kho lưu trữ.
- **Goal Registry (`.agents/context/goals.md`):** Các mục tiêu hiện tại của dự án. Hãy đảm bảo kế hoạch của bạn không xung đột với các mục tiêu này.

## Quản lý bộ nhớ sống (Living Memory Management)
Toàn bộ tri thức động (dynamic knowledge) được lưu trữ trong `.agents/intelligence/`.
- **Decision Log & Assumptions:** Đọc trước khi đưa ra bất kỳ giả định kiến trúc nào.
- **Repository Health:** Đánh giá tech debt, tight coupling, và rủi ro kiến trúc trước khi triển khai.
- **Session Snapshots:** Lịch sử các phiên làm việc trước đó. Sử dụng thay vì quét `git log`.

## Quy trình cập nhật Project Intelligence (Project Intelligence Workflow)
Khi dự án thay đổi (ví dụ: tạo folder mới, đổi tên dự án), dữ liệu Project Intelligence phải được tiến hóa theo.
1. **Phát hiện sai lệch (Detect Drift):** Nếu cấu trúc file thực tế khác với Manifest, Repo Map hoặc Context, bạn PHẢI báo cáo "Repository Drift".
2. **CẤM TỰ ĐỘNG CẬP NHẬT (NEVER AUTO-UPDATE):** Bạn TUYỆT ĐỐI KHÔNG được tự động viết lại các file Context hoặc Intelligence.
3. **Tuân thủ luồng Project Intelligence Update:**
   - Implementation -> Validation -> Project Intelligence Update Proposal -> **WAIT FOR USER APPROVAL** -> Update Project Intelligence.
4. **Tạo Session Snapshot:** Sau khi triển khai thành công một kế hoạch, bạn PHẢI đề xuất một Session Snapshot bằng tiếng Việt mô tả Mục tiêu, Các module bị ảnh hưởng, Các file đã sửa đổi, Kết quả, và Bài học kinh nghiệm. Chờ phê duyệt trước khi ghi vào file.
