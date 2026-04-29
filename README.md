# F.E.N.S | VinUni Datathon 2026 - Round 1

Repository này lưu toàn bộ file làm bài cho vòng 1 của VinUni Datathon 2026, bao gồm phần phân tích dữ liệu, giải câu hỏi trắc nghiệm và baseline cho bài toán dự báo doanh thu.

## 1. Nội dung repo

- `EDA.ipynb`: Notebook phân tích khám phá dữ liệu, trực quan hóa và rút ra insight.
- `trac_nghiem.ipynb`: Notebook xử lý và trả lời các câu hỏi trắc nghiệm.
- `Đề thi Vòng 1.pdf`: Đề thi gốc của vòng 1.
- `datathon-2026-round-1/`: Thư mục dữ liệu BTC cung cấp.
- `datathon-2026-round-1/baseline.ipynb`: Baseline forecasting cho bài toán dự báo `Revenue` và `COGS`.

## 2. Cấu trúc thư mục

```text
datathon_2026/
├── README.md
├── EDA.ipynb
├── trac_nghiem.ipynb
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

### 5.3. Chạy baseline forecasting

Mở `datathon-2026-round-1/baseline.ipynb`.

Baseline này thực hiện:

1. Đọc lịch sử `sales.csv`
2. Tạo seasonal profile theo ngày trong năm
3. Ước lượng trend tăng trưởng theo năm
4. Dự báo `Revenue` và `COGS` cho giai đoạn test
5. Xuất file submission

Lưu ý: trong notebook baseline, biến `DATA_DIR` đang để là `dataset/`. Nếu chạy theo cấu trúc repo hiện tại, cần đổi lại cho phù hợp với vị trí của `sales.csv`.

## 6. Đầu ra kỳ vọng

- Từ `EDA.ipynb`: các bảng tóm tắt, biểu đồ và insight phục vụ báo cáo.
- Từ `trac_nghiem.ipynb`: đáp án và cách tính cho các câu hỏi trắc nghiệm.
- Từ `baseline.ipynb`: file dự báo theo định dạng submission của bài toán forecast.


