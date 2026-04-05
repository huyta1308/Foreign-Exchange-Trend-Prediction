# Hướng Dẫn Đọc Tài Liệu (Reading Guide)

Tài liệu của dự án được phân chia theo cấu trúc đánh số để tạo luồng đọc logic. Tùy thuộc vào mục đích của bạn, hãy làm theo các gợi ý dưới đây.

## Dành cho Giảng Viên / Người Đánh Giá
Nếu bạn muốn xem xét kết quả và chất lượng của dự án (ví dụ: đồ án môn học), hãy tập trung vào:
1. **[00-overview.md](./docs/00-overview.md)**: Để hiểu rõ ý tưởng và cách đặt vấn đề.
2. **[03-architecture.md](./docs/03-architecture.md)**: Đánh giá phần tự triển khai mô hình (Custom Logistic Regression) thay vì dùng thư viện có sẵn và tư duy điều chỉnh Decision Threshold.
3. **[02-standards.md](./docs/02-standards.md)**: Xem cách dự án này kiểm soát data leakage (Z-score trên tập train) và các metrics (Log Loss).

## Dành cho Nhà Phát Triển / Machine Learning Engineer
Nếu bạn muốn tiếp tục phát triển hoặc tái hiện lại kết quả:
1. Đọc **[01-workflow.md](./docs/01-workflow.md)** để nắm rõ cấu trúc Sliding Window.
2. Đọc **[04-tasks.md](./docs/04-tasks.md)** để xem lịch sử và các tiêu chuẩn nghiệm thu (Acceptance Criteria) của các tính năng.
3. Tham khảo **[03-architecture.md](./docs/03-architecture.md)** để hiểu cấu trúc code thuật toán.

## Dành cho Người Sử Dụng (End-users)
Dự án hiện tại là dạng mã nguồn (CLI script). Để hiểu cách nó hoạt động ở mức cơ bản, vui lòng đọc phần **Bối cảnh và Tầm nhìn** ở [README.md](./README.md) và chạy tệp `final_project.py`.
