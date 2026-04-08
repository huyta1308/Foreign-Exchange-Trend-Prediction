# 03 - Kiến Trúc Mô Hình (Architecture)

Tài liệu này đi sâu vào thiết kế toán học và cách thức hoạt động của mô hình Học máy được xây dựng cho dự án.

## 1. Tổng Quan
Thay vì sử dụng các thư viện sẵn có như scikit-learn, dự án triển khai thuật toán **Logistic Regression** hoàn toàn từ đầu (from scratch) để hiểu sâu về quá trình học của máy (Learning process).

## 2. Cơ Sở Toán Học (Mathematical Foundations)

### 2.1 Hàm Kích Hoạt (Sigmoid Function)
Hàm Sigmoid được sử dụng để ánh xạ đầu ra của mô hình tuyến tính thành dạng xác suất (từ 0 đến 1):
$$ \sigma(x) = \frac{1}{1 + e^{-x}} $$

### 2.2 Hàm Mất Mát (Cost Function - Log Loss)
Để đo lường sai số giữa dự báo và thực tế, mô hình sử dụng hàm Log Loss:
$$ J = -\frac{1}{m} \sum_{i=1}^{m} [y^{(i)} \log(\hat{y}^{(i)}) + (1 - y^{(i)}) \log(1 - \hat{y}^{(i)})] $$

### 2.3 Quá Trình Tối Ưu (Gradient Descent)
Mô hình cập nhật trọng số dựa trên đạo hàm của Loss:
$$ \theta = \theta - \alpha \cdot \nabla J $$
- **Learning rate ($\alpha$):** `0.03`
- **Iterations (Epochs):** `5000`

## 3. Chiến Lược Điều Chỉnh Decision Threshold

### Vấn Đề
Mặc định, Logistic Regression dùng ngưỡng (threshold) là `0.5`:
- Nếu xác suất $\ge 0.5 \rightarrow$ Dự đoán `UP`
- Nếu xác suất $< 0.5 \rightarrow$ Dự đoán `DOWN`

Do dữ liệu bị **Mất Cân Bằng (Imbalanced Dataset)**, mô hình có xu hướng dự đoán lớp đa số (`DOWN/FLAT`). Xác suất đầu ra thường bị ép về khoảng 0.3 - 0.45. Hầu như không có mẫu nào vượt qua ngưỡng 0.5, dẫn đến việc bỏ sót gần như toàn bộ các trường hợp `UP` thực tế.

### Giải Pháp
Dự án điều chỉnh ngưỡng quyết định xuống **0.35**.
- Nếu xác suất $\ge 0.35 \rightarrow$ Dự đoán `UP`

**Trade-off (Sự Đánh Đổi):**
- Tăng số lượng False Positives (dự đoán sai thành UP).
- Nhưng giảm đáng kể False Negatives (Không bỏ sót các trường hợp UP thực sự).
- Do mục tiêu chính của hệ thống là cảnh báo người dùng khi tỷ giá có dấu hiệu tăng để họ đổi tiền sớm, trade-off này là hoàn toàn hợp lý và mang lại giá trị thực tiễn cao.
