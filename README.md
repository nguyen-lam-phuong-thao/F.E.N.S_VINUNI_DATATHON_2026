# F.E.N.S | VinUni Datathon 2026 - Round 1

Repository này lưu toàn bộ file làm bài cho vòng 1 của VinUni Datathon 2026, bao gồm phần phân tích dữ liệu, giải câu hỏi trắc nghiệm và baseline cho bài toán dự báo doanh thu.

## 1. Nội dung repo

- `EDA.ipynb`: Notebook phân tích khám phá dữ liệu, trực quan hóa và rút ra insight.
- `trac_nghiem.ipynb`: Notebook xử lý và trả lời các câu hỏi trắc nghiệm.
- `Đề thi Vòng 1.pdf`: Đề thi gốc của vòng 1.
- `datathon-2026-round-1/`: Thư mục dữ liệu BTC cung cấp.
- `revenue-forcasting.ipynb`:  Forecasting cho bài toán dự báo `Revenue` và `COGS`.

## 2. Cấu trúc thư mục

```text
datathon_2026/
├── README.md
├── EDA.ipynb
├── trac_nghiem.ipynb
├── revenue-forcasting.ipynb
├── Đề thi Vòng 1.1.pdf
└── datathon-2026-round-1/
    ├── baseline.ipynb
    ├── customers.csv
    ├── geography.csv
    ├── inventory.csv
    ├── order_items.csv
    ├── orders.csv
    ├── payments.csv
    ├── products.csv
    ├── promotions.csv
    ├── returns.csv
    ├── reviews.csv
    ├── sales.csv
    ├── sample_submission.csv
    ├── shipments.csv
    └── web_traffic.csv
```

## 3. Mục tiêu bài làm

Repo hiện tại tập trung vào 3 phần chính:

1. Phân tích khám phá dữ liệu để hiểu cấu trúc business, hành vi khách hàng và các bảng liên quan.
2. Xử lý các câu hỏi trắc nghiệm dựa trên dataset của đề.
3. Xây dựng baseline cho bài toán dự báo doanh thu ngày, với mục tiêu dự đoán `Revenue` và `COGS`.

## 4. Môi trường đề xuất

Có thể chạy với Python 3.10+ hoặc môi trường notebook tương đương.

Thư viện đang được sử dụng trong repo:

- `numpy`
- `pandas`
- `matplotlib`
- `seaborn`
- `jupyter`
- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `statsmodels`
- `scikit-learn`
- `lightgbm`
- `xgboost`

Nếu chạy bằng local:

```bash
pip install numpy pandas matplotlib seaborn notebook
```

## 5. Cách chạy lại

### 5.1. Chạy EDA

Mở `EDA.ipynb` và chạy lần lượt từ trên xuống dưới.

Notebook này ưu tiên đọc dữ liệu từ thư mục:

```text
datathon-2026-round-1/
```

Nếu đổi cấu trúc repo hoặc chạy trên máy khác, cần cập nhật biến `DATA_DIR_CANDIDATES` trong notebook.

### 5.2. Chạy notebook trắc nghiệm

Mở `trac_nghiem.ipynb` và chạy từ trên xuống dưới.

Lưu ý: notebook này hiện đang dùng đường dẫn cụ thể trên máy local. Nếu mở trên máy khác, cần sửa `DATA_DIR_CANDIDATES` để trỏ đến thư mục:

```text
datathon-2026-round-1/
```

### 5.3. Chạy Pipeline Dự báo (Advanced Forecasting)

Mở file notebook chính (ví dụ: `revenue-forecasting.ipynb`). 

Giải pháp này áp dụng chiến thuật **Hybrid Model** kết hợp sức mạnh của Hồi quy và Học cây quyết định, bao gồm các bước sau:
1. **Tiền xử lý & Trimming Dữ liệu:** Đọc dữ liệu `sales.csv` và `promotions.csv`. Tự động cắt bỏ các dữ liệu quá khứ bị nhiễu (chỉ giữ lại từ năm 2020 trở đi) để mô hình bám sát hành vi tiêu dùng hiện tại sau đại dịch.
2. **Feature Engineering Chuyên sâu:** Trích xuất các đặc trưng thời gian (cuối tuần, ngày trong tháng) và xây dựng các đặc trưng tâm lý mua sắm (ngày nhận lương, ngày sale đôi, đợt khuyến mãi, Tết Âm lịch, Black Friday...).
3. **Huấn luyện Mô hình (Linear Regression + XGBoost/LightGBM):**
   - **Linear Regression:** Đóng vai trò học Xu hướng (Trend) và đà lạm phát/tăng trưởng dài hạn.
   - **Ensemble (LGBM + XGB):** Sử dụng hàm mất mát L1 (Absolute Error) để học Phần dư (Residuals), giúp mô hình linh hoạt bắt trúng các đỉnh (spikes) doanh thu mùa vụ mà không bị nhiễu bởi Outliers.
4. **Kiểm chứng chặt chẽ (Validation):** Đánh giá hiệu năng bằng Out-of-Time Validation (giữ lại 60 ngày cuối năm 2022) với các chỉ số thực tế MAE, RMSE và R².
5. **Dự báo & Xuất kết quả:** Đưa ra dự báo `Revenue` và `COGS` cho tập Test. Áp dụng Post-processing (Clip giá trị >= 0) để đảm bảo logic kinh doanh, sau đó xuất ra file `submission.csv`.

**💡 Lưu ý về đường dẫn dữ liệu:** Đảm bảo các file `sales.csv`, `promotions.csv` và `sample_submission.csv` được đặt đúng trong thư mục được khai báo (ví dụ: biến `DATA_DIR = 'datathon-2026-round-1/'`). Nếu đang chạy theo cấu trúc thư mục khác, vui lòng cập nhật lại biến này trong block code đầu tiên của notebook.

## 6. Đầu ra kỳ vọng

- Từ `EDA.ipynb`: các bảng tóm tắt, biểu đồ và insight phục vụ báo cáo.
- Từ `trac_nghiem.ipynb`: đáp án và cách tính cho các câu hỏi trắc nghiệm.
- Từ `revenue-forcasting.ipynb`: file dự báo theo định dạng submission của bài toán forecast.


