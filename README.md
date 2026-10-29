# DỰ ÁN HỌC MÁY: DỰ ĐOÁN NGUY CƠ KHÁCH HÀNG RỜI BỎ MẠNG VIỄN THÔNG (TELCO CUSTOMER CHURN)

> **Báo cáo Tiểu luận: Xác định bài toán, khảo sát và tiền xử lý dữ liệu**  
> **Trường Đại học Công nghệ Thông tin & Truyền thông - Đại học Thái Nguyên (ICTU)**  
> **Khoa Công nghệ Thông tin - Học phần: Học máy (Machine Learning)**

---

## 👥 THÀNH VIÊN NHÓM THỰC HIỆN (NHÓM 20)

| STT | Họ và tên | Mã sinh viên | Lớp học phần | Vai trò & Nhiệm vụ chính |
|:---:|:---|:---:|:---:|:---|
| 1 | **Hoàng Anh Tuấn** | DTC235200797 | CNTT K22H | Thu thập dữ liệu, xử lý dữ liệu khuyết, kiểm định ngoại lai 1.5 IQR, xây dựng đường ống tiền xử lý `ColumnTransformer` (OneHotEncoder, StandardScaler), chia tập Train/Test phân tầng 80/20, hoàn thiện mã nguồn và xuất bản báo cáo. |
| 2 | **Hoàng Quốc Vượng** | DTC235200857 | CNTT K22H | Phát biểu bài toán học máy, thiết lập hệ chỉ số đánh giá, đo lường Baseline `DummyClassifier`, khảo sát thống kê mô tả EDA, trực quan hóa phân bố dữ liệu và kiểm định $\chi^2$, viết báo cáo Mở đầu, Chương 1 và Chương 2. |

* **Giảng viên hướng dẫn:** ThS. Nguyễn Tuấn Anh

---

## 📌 GIỚI THIỆU BÀI TOÁN & BỘ DỮ LIỆU

- **Bài toán:** Phân loại nhị phân (*Binary Classification*) dự đoán nguy cơ rời mạng của khách hàng viễn thông (`Churn = Yes / No`).
- **Tập dữ liệu:** *Telco Customer Churn* gồm **7.043 bản ghi** với **20 thuộc tính** đầu vào.
- **Mất cân bằng nhãn:** 5.174 mẫu ở lại (73,46%) và 1.869 mẫu rời mạng (26,54%).
- **Xử lý chất lượng dữ liệu:**
  - Điền giá trị 0.0 cho 11 bản ghi có `TotalCharges` mang chuỗi khoảng trắng `' '` (khách hàng có `tenure = 0`).
  - Loại bỏ hoàn toàn cột định danh `customerID` để triệt tiêu nhiễu.
  - Kiểm định ngoại lai theo quy tắc $1.5 \times \text{IQR}$: Xác nhận 0 điểm ngoại lai trên cả 3 biến số định lượng.
- **Đường ống tiền xử lý (`ColumnTransformer`):**
  - Chuẩn hóa 3 biến định lượng bằng `StandardScaler()`.
  - Mã hóa 5 biến nhị phân bằng `OneHotEncoder(drop='if_binary')`.
  - Mã hóa 10 biến danh mục đa nhóm bằng `OneHotEncoder(drop='first')` tránh bẫy biến giả.
  - Giữ nguyên 1 biến nhị phân sẵn có `SeniorCitizen` (`remainder='passthrough'`).
  - Ma trận đặc trưng sau xử lý: **30 chiều** (Train: $5.634 \times 30$, Test: $1.409 \times 30$).

---

## 📁 CẤU TRÚC KHO MÃ NGUỒN

```text
├── Telco-Customer-Churn.csv          # Tệp dữ liệu gốc (7.043 bản ghi)
├── check.ipynb                       # Jupyter Notebook thực nghiệm toàn bộ quy trình (Cell 0 - Cell 6)
├── Bao_cao_hoc_may.pdf               # Báo cáo tiểu luận hoàn chỉnh (35 trang chuẩn ICTU)
├── main.tex                          # Toàn bộ mã nguồn LaTeX biên dịch XeLaTeX
├── requirements.txt                  # Danh mục các thư viện Python cần thiết
├── .gitignore                        # Cấu hình bỏ qua tệp rác và môi trường ảo
└── README.md                         # Hướng dẫn chi tiết dự án
```

---

## 🚀 HƯỚNG DẪN CÀI ĐẶT VÀ CHẠY LẠI THỰC NGHIỆM

### 1. Yêu cầu môi trường
- Python $\ge$ 3.10
- Khuyến khích sử dụng môi trường ảo (`venv` hoặc `conda`).

### 2. Cài đặt các thư viện phụ thuộc
Mở terminal hoặc Command Prompt tại thư mục dự án và chạy lệnh:
```bash
pip install -r requirements.txt
```

### 3. Thực thi kiểm chứng kết quả trên Notebook
Chạy Jupyter Notebook hoặc mở trên VS Code:
```bash
jupyter notebook check.ipynb
```
Chạy tuần tự các Cell từ trên xuống dưới:
- **Cell 0:** Đọc dữ liệu và khám phá tổng quan.
- **Cell 1:** Đo lường mô hình cơ sở tham chiếu (*Baseline DummyClassifier*).
- **Cell 2:** Khảo sát thống kê mô tả và kiểm định tương quan $\chi^2$.
- **Cell 3:** Trực quan hóa Hình 2.1 và Hình 2.2.
- **Cell 4:** Xử lý 11 giá trị trống ở `TotalCharges` và tính toán ngưỡng IQR.
- **Cell 5:** Thiết lập `ColumnTransformer` và chia tập Train/Test phân tầng 80/20.
- **Cell 6:** Tạo sinh trực tiếp 3 biểu đồ học thuật nâng cao (Hình 2.3, 2.4, 3.1).
