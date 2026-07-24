# 📊 Phân tích Thị trường Dược phẩm IQVIA (2019–2022)

## 📌 Giới thiệu dự án

Đây là dự án phân tích dữ liệu thị trường dược phẩm từ **IQVIA** trong giai đoạn **2019–2022** bằng **Power BI**.

Mục tiêu của dự án:

- Làm sạch và chuẩn hóa dữ liệu.
- Chuyển đổi dữ liệu sang mô hình phù hợp cho Power BI.
- Thiết kế Dashboard trực quan hỗ trợ phân tích.
- Phân tích xu hướng thị trường theo thời gian và kênh bán hàng.
- Tìm ra các insight hỗ trợ hoạt động Marketing và Kinh doanh.

---

# 📂 Cấu trúc dự án

```
.
│
├── IQVIA data 2019-2022.xlsx          # Dữ liệu gốc
├── IQVA Analysis.pbix                 # Dashboard Power BI
├── EDA_IQVIA data 2019-2022.xlsx      # Phân tích dữ liệu sơ bộ (EDA)
└── README.md
```

---

# 📁 Mô tả dữ liệu

Bộ dữ liệu chứa thông tin doanh số thị trường dược phẩm từ IQVIA trong giai đoạn 2019–2022.

Mỗi dòng dữ liệu đại diện cho **một sản phẩm (SKU)** cùng doanh số bán theo từng kênh và từng năm.

## Ý nghĩa các trường dữ liệu

| Trường | Ý nghĩa |
|---------|----------|
| **ATC4** | Nhóm điều trị (Therapeutic Class) |
| **Pack Molecule String** | Thành phần hoạt chất |
| **Product** | Tên sản phẩm |
| **Pack Strength** | Hàm lượng |
| **Pack Form** | Dạng bào chế (Gel, Paste, Capsule...) |
| **Hospital 2019–2022** | Doanh số kênh ETC (Hospital) |
| **Retail 2019–2022** | Doanh số kênh OTC (Retail) |
| **Total Market 2019–2022** | Tổng doanh số thị trường |

---

# 🏥 Ý nghĩa các kênh bán hàng

## Hospital (ETC)

Là doanh số bán qua:

- Bệnh viện
- Trung tâm y tế
- Phòng khám

Đây chủ yếu là các thuốc kê đơn hoặc thuốc sử dụng trong bệnh viện.

---

## Retail (OTC)

Là doanh số bán qua:

- Nhà thuốc
- Quầy thuốc
- Chuỗi bán lẻ dược phẩm

Đây là kênh tiêu thụ của các thuốc không kê đơn và các sản phẩm chăm sóc sức khỏe.

---

## Total Market

Là doanh số thị trường được cung cấp trong bộ dữ liệu IQVIA.

> **Lưu ý**

Trong quá trình phân tích phát hiện:

```
Hospital + Retail ≠ Total Market
```

đối với nhiều dòng dữ liệu.

Do đó **không thể mặc định Total Market bằng tổng Hospital và Retail**.

Nguyên nhân có thể đến từ:

- Phương pháp thống kê khác nhau
- Dữ liệu được tổng hợp từ nhiều nguồn
- Thiếu dữ liệu ở một số kênh
- Khác biệt trong quy trình tổng hợp dữ liệu của IQVIA

---

# 🔄 Tiền xử lý dữ liệu

Dữ liệu ban đầu được lưu ở dạng **Wide Table**.

Ví dụ:

| Product | Hospital 2019 | Hospital 2020 | Retail 2019 | Retail 2020 |
|----------|---------------|---------------|--------------|--------------|

Để thuận tiện cho việc phân tích trong Power BI, các cột doanh số được **Unpivot** thành:

| Product | Channel | Year | Sales |
|----------|----------|------|--------|
| Product A | Hospital | 2019 | xxx |
| Product A | Retail | 2020 | xxx |

Việc chuyển đổi này giúp:

- Dễ dàng xây dựng Dashboard
- Tính toán DAX đơn giản hơn
- Phân tích theo thời gian
- So sánh giữa các kênh bán hàng

---

# 📊 Dashboard

Dashboard được xây dựng trên Power BI với các thành phần chính:

- KPI tổng doanh số Hospital
- KPI tổng doanh số Retail
- Cơ cấu doanh số theo kênh
- Xu hướng doanh số theo năm
- Top 5 nhóm điều trị (ATC4)
- Top 5 sản phẩm theo doanh số
- Dashboard tương tác với bộ lọc

---

# Các nội dung phân tích

Sau khi xử lý dữ liệu việc phân tích được tập trung vào 5 trường chính:
 - Sales
 - Chanel (Retail, Hospital)
 - Year
 - ACT4
 - Product

Ngoài ra dùng Dax để tạo các measure tính toán cho các chỉ số như YoY Growth, CAGR,...

---

# 📈 Các Insight chính

## 1. Retail là kênh bán hàng chủ lực

Doanh số Retail chiếm khoảng **60%** tổng doanh số, trong khi Hospital chiếm khoảng **40%**.

Điều này cho thấy doanh thu của thị trường chủ yếu đến từ hệ thống nhà thuốc và chuỗi bán lẻ.

---

## 2. Retail tăng trưởng liên tục

Doanh số Retail tăng đều qua các năm:

| Năm | Retail |
|-----|---------|
|2019|79T|
|2020|83T|
|2021|95T|
|2022|120T|

Retail là động lực tăng trưởng chính của thị trường trong giai đoạn 2019–2022.

---

## 3. Hospital biến động theo từng năm

Doanh số Hospital có xu hướng giảm trong giai đoạn 2019–2021 trước khi phục hồi vào năm 2022.

| Năm | Hospital |
|-----|-----------|
|2019|66T|
|2020|64T|
|2021|51T|
|2022|68T|

Có thể liên quan đến:

- Ảnh hưởng của COVID-19
- Thay đổi trong hoạt động khám sức khoẻ của bệnh nhân
- Sự phục hồi của hệ thống bệnh viện

---

## 4. Retail chiếm ưu thế ở nhiều nhóm điều trị

Ở hầu hết trong các nhóm ATC4 và Product, doanh số Retail đều cao hơn Hospital.

Điều này phản ánh vai trò quan trọng của hệ thống nhà thuốc trong việc phân phối thuốc.

---
## 5. Chi tiết về ATC4 và Product

Retail có cơ cấu doanh thu tập trung chủ yếu vào các nhóm điều trị phổ biến như kháng sinh đường uống (Cephalosporins, Penicillins), thuốc giảm đau, thuốc tiêu hóa và các nhóm điều trị bệnh mạn tính. Điều này phản ánh nhu cầu chăm sóc sức khỏe hàng ngày và điều trị ngoại trú vẫn là động lực chính của thị trường bán lẻ.

Về sản phẩm, các vaccine đều nằm trong nhóm dẫn đầu doanh thu, cho thấy thị trường Retail được dẫn dắt bởi cả thuốc kê đơn, vaccine và các sản phẩm chăm sóc sức khỏe. Tuy nhiên, doanh thu được phân bổ trên nhiều sản phẩm, không có một thương hiệu nào chiếm tỷ trọng quá lớn, phản ánh mức độ cạnh tranh cao của thị trường. 

-> Có thể mở rộng doanh thu bằng cách tập trung vào các nhóm điều trị như là Kháng sinh, Đau - viêm, Dạ dày, Gan, Ho, Dị ứng, Da liễu hoặc nhóm sản phẩm như là thuốc kê đơn, vaccine và các sản phẩm chăm sóc sức khỏe.

---

# 🔍 Phát hiện về chất lượng dữ liệu

Trong quá trình phân tích phát hiện một số vấn đề của dữ liệu hiện đang bị trống và lỗi tính toán:

## 1. Giá trị "(Blank)"

Dashboard xuất hiện các giá trị:

- (Blank) Product
- (Blank) ATC4

Các bản ghi này vẫn có doanh số khá lớn.

Sau khi kiểm tra và làm sạch người làm dữ liệu quyết định giữ dữ liệu trống để có kết quả tốt nhất và tính trung thực nhất

---

## 2. Total Market không bằng Hospital + Retail

Qua kiểm tra dữ liệu phát hiện:

```
Hospital + Retail ≠ Total Market
```

Do đó:

- Không sử dụng Total Market để cộng trực tiếp với Hospital và Retail.
- Cần xác minh lại định nghĩa dữ liệu trước khi tính toán.

---

## Cải thiện Dashboard

- Thêm bộ lọc theo dạng bào chế

- Chuẩn hóa định dạng KPI.

- Loại bỏ các giá trị "(Blank)" sau khi làm sạch dữ liệu.

---

# 🛠 Công cụ sử dụng

- Microsoft Power BI
- Power Query
- Microsoft Excel
- DAX

---

# 📚 Kiến thức và kỹ năng áp dụng

- Data Cleaning
- Data Transformation
- Exploratory Data Analysis (EDA)
- Power Query
- Data Modeling
- Star Schema
- DAX
- Dashboard Design
- Business Intelligence
- Marketing Analytics
- Pharmaceutical Market Analysis

