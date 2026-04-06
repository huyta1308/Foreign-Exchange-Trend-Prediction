# 00 - Tổng Quan Dự Án (Project Overview)

## 1. Vấn đề Giải Quyết
Tỷ giá hối đoái (Exchange rates) thay đổi liên tục theo thời gian. Trong bối cảnh toàn cầu hóa, tỷ giá USD/VND tác động mạnh mẽ đến các giao dịch quốc tế, du học, du lịch và xuất nhập khẩu.

Tuy nhiên, người dùng hiện nay thường chỉ quan sát tỷ giá tại một thời điểm nhất định mà không có công cụ dự báo:
- Xu hướng ngắn hạn tiếp theo là tăng hay giảm.
- Thời điểm tối ưu để thực hiện giao dịch (mua/bán ngoại tệ).

Hệ quả là các quyết định thường dựa trên cảm tính, dẫn đến tỷ giá hối đoái giao dịch không có lợi.

## 2. Mục Tiêu Dự Án
Xây dựng một mô hình Machine Learning đơn giản để dự đoán xu hướng ngắn hạn của tỷ giá USD/VND.
- **Input:** Chuỗi tỷ giá của 7 ngày gần nhất.
- **Output:** Xu hướng của ngày tiếp theo (`UP` hoặc `DOWN/FLAT`).

Dự án chuyển đổi bài toán *Dự báo chuỗi thời gian (Time Series Forecasting)* thành bài toán *Phân loại nhị phân (Binary Classification)*.

## 3. Đối Tượng Người Dùng
- **Cá nhân, du học sinh, khách du lịch:** Cần chọn thời điểm đổi tiền có lợi nhất.
- **Chủ doanh nghiệp xuất nhập khẩu:** Tối ưu hóa lợi nhuận hoặc giảm thiểu rủi ro tỷ giá trong các thanh toán ngắn hạn.

## 4. Công Nghệ và Nền Tảng (Tech Stack)
- **Ngôn ngữ:** Python
- **Mô hình học máy:**
  - *Core:* Custom Logistic Regression (viết từ đầu bằng Numpy, không dùng thư viện).
  - *Baseline & Comparison:* Random Forest, Support Vector Machine (SVM).
- **Tiền xử lý dữ liệu:** Pandas, Z-score Normalization.

## 5. Yêu Cầu Đặc Biệt (Key Requirements)
1. **Phải có phần ML thực tế:** Không gọi API dự báo có sẵn từ các bên thứ ba.
2. **Triển khai thuật toán từ đầu:** Yêu cầu cài đặt Custom Logistic Regression (tự viết hàm Sigmoid, Log Loss, Gradient Descent) thay vì chỉ gọi `sklearn`.
3. **Xử lý Imbalanced Data hiệu quả:** Vì số lượng mẫu `DOWN/FLAT` lớn hơn `UP`, mô hình cần có chiến lược điều chỉnh Decision Threshold (hạ từ `0.5` xuống `0.35`) để tăng độ nhạy cảm với các xu hướng tăng.
