# 05 - Bảo Mật (Security & Compliance)

Mặc dù đây là một dự án phân tích dữ liệu mở và chạy trên local (môi trường máy tính cá nhân), các nguyên tắc bảo mật và quản lý an toàn dữ liệu cơ bản vẫn được áp dụng.

## 1. Quản Lý Dữ Liệu
- **Dữ liệu Tỷ giá (Exchange Rate):** Là dữ liệu public, không chứa Thông tin Nhận dạng Cá nhân (PII). Tuy nhiên, các bản snapshot dữ liệu phải được lưu trữ trong thư mục được `.gitignore` (nếu kích thước lớn) hoặc khóa cứng (immutable) để đảm bảo tính tái lập của thuật toán (Reproducibility).
- **Data Leakage (Rò rỉ dữ liệu máy học):** Cực kỳ nghiêm cấm việc rò rỉ dữ liệu tương lai vào dữ liệu huấn luyện. Xem phần [02-standards.md](./02-standards.md) để biết thêm về cách tính Z-Score.

## 2. Quản Lý Mã Nguồn
- **Không Hardcode Credentials:** Nếu trong tương lai dự án tích hợp thêm API bên thứ ba (Ví dụ: Frankfurter API, hoặc Fixer.io) để lấy giá realtime, tuyệt đối KHÔNG lưu trữ API keys trong mã nguồn. Cần sử dụng file `.env` hoặc các trình quản lý Secret (Environment variables).
- **Execution Security:** Việc nạp các models định dạng Pickle (`.pkl`) có rủi ro thực thi mã độc. Do dự án tự triển khai model từ đầu qua class, các trọng số $\theta$ (theta) nên được serialize dạng mảng `.npy` hoặc `.json` thay vì dùng Pickle để đảm bảo an toàn tuyệt đối nếu chia sẻ file trọng số.

## 3. Khuyến Cáo Khi Chạy Script
- Chạy hệ thống trên Virtual Environment (`venv` hoặc `conda env`) để cô lập các dependencies.
- Tránh cấp quyền Admin/Root không cần thiết cho user chạy python script.
