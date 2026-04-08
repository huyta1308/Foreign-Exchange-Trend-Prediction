# 02 - Tiêu Chuẩn (Standards & Guidelines)

Tài liệu này định nghĩa các tiêu chuẩn về đánh giá mô hình và phong cách mã nguồn để đảm bảo dự án thống nhất và dễ bảo trì.

## 1. Tiêu Chuẩn Đánh Giá Mô Hình (Evaluation Standards)

Do bộ dữ liệu đối mặt với vấn đề **Mất Cân Bằng (Imbalanced Dataset)** (Số mẫu `DOWN/FLAT` lớn hơn đáng kể so với `UP`), chúng tôi áp dụng các tiêu chuẩn đo lường khắt khe hơn thay vì chỉ dùng Accuracy thông thường.

### Metrics Ưu Tiên:
1. **Precision & Recall cho class `UP`**:
   - Đặc biệt ưu tiên **Recall** vì mục tiêu quan trọng nhất là không được bỏ lỡ các xu hướng tăng.
   - Chấp nhận đánh đổi (trade-off) một lượng False Positives nhất định để giảm thiểu False Negatives.
2. **Log Loss (Cross Entropy)**:
   - Dùng để theo dõi quá trình hội tụ trong lúc training. Loss phải giảm đều đặn theo mỗi iteration.
   - Thể hiện sự tự tin của dự đoán chứ không chỉ đánh giá phân loại cứng (hard classification).
3. **Confusion Matrix**:
   - Bắt buộc phải báo cáo Confusion Matrix trong mọi cuộc thử nghiệm để thấy rõ lỗi thiên lệch về lớp đa số (Majority class bias).

## 2. Tiêu Chuẩn Mã Nguồn (Code Standards)

- **Ngôn ngữ:** Python 3.10+
- **Style Guide:** Tuân thủ PEP 8 (sử dụng Black linter).
- **Phụ thuộc bên ngoài (Dependencies):**
  - Khuyến khích giới hạn các thư viện ngoại lai ở module mô hình chính. Custom Logistic Regression **phải** được thực thi hoàn toàn bằng `numpy` hoặc các thao tác tensor cơ bản.
  - Các thư viện ML (như `sklearn`) chỉ được dùng làm Baseline so sánh (Random Forest, SVM).

## 3. Tiêu Chuẩn Chống Data Leakage (Bắt Buộc)

- Không bao giờ truyền toàn bộ dữ liệu vào `StandardScaler` (hoặc tính Z-score) trước khi chia Train/Test.
- Quy trình chuẩn phải là: Khởi tạo Z-score > Fit trên Train > Transform trên Train > Transform trên Test.
- Tham số `shuffle=False` luôn phải được duy trì khi dùng `train_test_split` do tính chất tuần tự của chuỗi thời gian.
