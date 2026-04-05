# USD/VND Short-term Trend Prediction

## Bối cảnh và Tầm nhìn
Dự án nhằm mục đích xây dựng một mô hình Machine Learning đơn giản để xác định xu hướng ngắn hạn của tỷ giá USD/VND. Dự án giúp giải quyết vấn đề ra quyết định dựa trên cảm tính của người dùng (cá nhân, doanh nghiệp, du học sinh) trong việc chọn thời điểm giao dịch ngoại tệ.

Dự án này sử dụng mô hình Logistic Regression được xây dựng thủ công (Custom Logistic Regression) từ con số 0, kết hợp điều chỉnh Decision Threshold chuyên sâu để xử lý bài toán dữ liệu mất cân bằng (Imbalanced Data).

---

## Mục lục Tài liệu (Documentation)

Bộ tài liệu này được cấu trúc hóa để đảm bảo tính minh bạch, dễ bảo trì và dễ hiểu.

| STT | Tài liệu | Mô tả Nội dung |
|:---:|:---|:---|
| - | [guides.md](./guides.md) | Hướng dẫn đọc và sử dụng bộ docs (Role-based Guide). |
| 0 | [00-overview.md](./docs/00-overview.md) | Tổng quan dự án, mục tiêu, và kiến trúc hệ thống cấp cao. |
| 1 | [01-workflow.md](./docs/01-workflow.md) | Quy trình xử lý dữ liệu (ETL), kỹ thuật Sliding Window và Pipeline huấn luyện. |
| 2 | [02-standards.md](./docs/02-standards.md) | Các tiêu chuẩn đánh giá mô hình, quy chuẩn code và xử lý log. |
| 3 | [03-architecture.md](./docs/03-architecture.md) | Kiến trúc mô hình, nền tảng toán học của Custom Logistic Regression và chiến lược Threshold. |
| 4 | [04-tasks.md](./docs/04-tasks.md) | Danh sách công việc (Task breakdown) và Acceptance Criteria cho từng giai đoạn. |
| 5 | [05-security.md](./docs/05-security.md) | Các nguyên tắc bảo mật cơ bản và quản lý dữ liệu. |

---

## Cấu trúc Thư mục

```text
Project ML1/
├── README.md                      # Index tài liệu
├── guides.md                      # Hướng dẫn điều hướng docs
├── docs/                          # Thư mục chứa tài liệu chi tiết
│   ├── 00-overview.md
│   ├── 01-workflow.md
│   ├── 02-standards.md
│   ├── 03-architecture.md
│   ├── 04-tasks.md
│   └── 05-security.md
├── exchange_rate.csv              # Dữ liệu raw
└── final_project.py               # Mã nguồn chính
```

---

## Cài đặt và Chạy thử
*(Phần này dành cho việc mô tả cách chạy dự án)*
1. Cài đặt các thư viện cần thiết: `pip install pandas numpy scikit-learn`
2. Chạy pipeline: `python final_project.py`
