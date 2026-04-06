# 01 - Quy Trình Workflow (Data & Training Pipeline)

Tài liệu này mô tả cách luồng dữ liệu di chuyển từ tệp raw đến lúc xuất ra dự đoán cuối cùng.

## 1. Data Source & Cấu trúc Dữ Liệu
- **Nguồn dữ liệu:** Dữ liệu tỷ giá USD/VND thực tế (Frankfurter).
- **Phương pháp Sliding Window:** Dữ liệu chuỗi thời gian được tái cấu trúc thành các mẫu dữ liệu (samples). Mỗi mẫu sử dụng khung cửa sổ trượt (sliding window) kích thước 7 ngày.

**Ví dụ một mẫu dữ liệu:**
- *Features (X):* Tỷ giá của `Day_1, Day_2, Day_3, Day_4, Day_5, Day_6, Day_7`
- *Target (y):* Xu hướng của `Day_8`

## 2. Chiến Lược Gán Nhãn (Label Definition)
Biến mục tiêu (Target variable) được xác định như sau:
- `Target = 1 (UP)` nếu tỷ giá ngày tiếp theo (next_day_rate) > tỷ giá ngày 7 (Day_7).
- `Target = 0 (DOWN/FLAT)` cho các trường hợp còn lại.

*Lợi ích:* Giúp mô hình tập trung vào việc dự báo **chiều hướng** (Trend Direction) thay vì phải cố gắng dự báo chính xác giá trị số tuyệt đối.

## 3. Quy Trình Tiền Xử Lý (Data Preprocessing)

### Phân chia tập Train/Test
- **Tỉ lệ:** Train (80%), Test (20%).
- **Shuffle:** `False`. (Cực kỳ quan trọng trong Time Series, không được xáo trộn để giữ tính toàn vẹn của chuỗi thời gian, ngăn ngừa Data Leakage).

### Chuẩn hóa Dữ Liệu (Z-score Normalization)
$$ X_{scaled} = \frac{X - \mu}{\sigma} $$

**Quy tắc chống Leakage:**
- Các tham số $\mu$ (mean) và $\sigma$ (std) **chỉ** được tính toán từ tập `Train`.
- Các tham số này sau đó được áp dụng để transform tập `Test`.
- Dữ liệu chuẩn bị cho mô hình Custom Logistic Regression được thêm thành phần `bias term` (cột chứa toàn giá trị 1).

## 4. Quy Trình Huấn Luyện (Training Pipeline)

1. **Khởi tạo:** Thiết lập vector trọng số $\theta$.
2. **Forward Pass:** Tính $Z = X \cdot \theta$, sau đó tính Sigmoid $\sigma(Z)$.
3. **Loss Calculation:** Tính hàm chi phí Log Loss.
4. **Backward Pass (Gradient Descent):** Tính đạo hàm của Loss theo $\theta$.
5. **Update:** Cập nhật $\theta = \theta - \alpha \cdot \nabla J$.
6. **Lặp lại:** Thực hiện 5000 epochs với Learning rate $\alpha = 0.03$.
