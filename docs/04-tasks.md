# 04 - Quản Lý Công Việc (Tasks & Tracking)

Dự án này được thiết kế và thực hiện bởi 1 cá nhân (Solo Developer) đóng vai trò là Machine Learning Engineer. Dưới đây là danh sách phân rã công việc (Task breakdown) và Acceptance Criteria.

## Giai Đoạn 1: Thu Thập & Khám Phá Dữ Liệu (EDA)
**Task 1.1: Trích xuất và định dạng dữ liệu (Data Extraction)**
- **Mô tả:** Lấy dữ liệu tỷ giá USD/VND (Frankfurter) và chuyển về dạng cấu trúc bảng (DataFrame).
- **Acceptance Criteria:**
  - Dữ liệu ở định dạng CSV (`exchange_rate.csv`).
  - Không có giá trị Null.
  - Định dạng thời gian chuẩn ISO.

**Task 1.2: Tiền xử lý dạng Sliding Window**
- **Mô tả:** Chuyển đổi dữ liệu Time Series sang cấu trúc features (7 ngày) -> label (1 ngày).
- **Acceptance Criteria:**
  - Data shape khớp quy tắc: 7 cột input, 1 cột target.
  - Target variable được chuyển đổi thành biến Binary (1: UP, 0: DOWN/FLAT).

## Giai Đoạn 2: Xây Dựng Thuật Toán (Modeling)
**Task 2.1: Triển khai Custom Logistic Regression**
- **Mô tả:** Viết script cho các hàm Sigmoid, Log Loss, và thuật toán Gradient Descent.
- **Acceptance Criteria:**
  - Không dùng `sklearn.linear_model`.
  - Loss function phải có xu hướng giảm dần qua từng iteration.

**Task 2.2: Thiết lập Baseline Models**
- **Mô tả:** Implement Random Forest và SVM từ `sklearn` để so sánh với thuật toán Custom.
- **Acceptance Criteria:**
  - Chạy được và lưu lại kết quả F1, Precision, Recall vào file report.

## Giai Đoạn 3: Tối Ưu & Đánh Giá (Optimization)
**Task 3.1: Phân Tích Mất Cân Bằng (Imbalance Tuning)**
- **Mô tả:** Điều chỉnh Decision Threshold để xử lý hiện tượng dự đoán lệch.
- **Acceptance Criteria:**
  - Lập biểu đồ Histogram phân bố xác suất đầu ra.
  - Chọn được mức threshold 0.35.
  - Cải thiện Recall của lớp `UP` (ít nhất > mức Baseline).

**Task 3.2: Chuẩn Hóa Tài Liệu (Documentation)**
- **Mô tả:** Đóng gói toàn bộ kiến thức vào thư mục `docs/`.
- **Acceptance Criteria:**
  - Cấu trúc thư mục theo chuẩn (00-overview đến 05-security).
  - Có file README dẫn dắt.
