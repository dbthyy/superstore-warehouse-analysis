# Phân Tích Hiệu Suất Bán Hàng & Lợi Nhuận
Môn học IS217 - Kho dữ liệu và OLAP

## Tổng quan
Dự án này xây dựng hệ thống hỗ trợ ra quyết định (DSS) cho chuỗi cung ứng bán lẻ dựa trên bộ dữ liệu Superstore Sales. Hệ thống thực hiện chuyển đổi dữ liệu thô thành kho dữ liệu chuẩn hóa, xây dựng các khối phân tích đa chiều để phục vụ báo cáo quản trị chuyên sâu.

<img width="828" height="427" alt="image" src="https://github.com/user-attachments/assets/690174fb-ef52-480c-a983-25d806554cba" />

## Kiến trúc Hệ thống
Dự án được triển khai qua 4 giai đoạn kỹ thuật chính:
- Tiền xử lý dữ liệu: Sử dụng Python/Pandas để làm sạch, chuẩn hóa tên biến và tạo các đặc trưng mới như IsHoliday.
- Data Warehouse & SSIS: Thiết kế lược đồ và thực hiện quy trình ETL.
- SSAS (Online Analytical Processing): Xây dựng các khối Cube đa chiều và định nghĩa các Measures/Hierarchies.
- Data Visualization: Trực quan hóa dữ liệu qua Power BI và Excel.

## Thiết kế Kho dữ liệu (Data Warehouse)
Hệ thống sử dụng mô hình Lược đồ Bông tuyết (Snowflake Schema) để tối ưu hóa việc lưu trữ và phân tích.
<img width="828" height="348" alt="image" src="https://github.com/user-attachments/assets/1c2f0714-a721-47cc-948e-5a0cedd7ebf4" />

Các thành phần chính:
- Bảng Sự kiện (Fact Table): FACT chứa các chỉ số đo lường như Sales, Quantity, Discount, Profit, DaysToShip, và HolidayScore.
- Các bảng Chiều (Dimension Tables): 
- DimTime: Phân cấp theo Năm > Tháng > Ngày.
- DimLocation: Chứa thông tin địa lý (Khu vực, Bang, Thành phố, Mã bưu chính).
- DimShipMode: Thông tin loại giao hàng.
- DimProduct: Thông tin sản phẩm.
- DimCategory: Thông tin danh mục sản phẩm.
- DimCustomer: Thông tin khách hàng.
- DimSegment: Thông tin phân khúc khách hàng.

## Tích hợp dữ liệu (SSIS)
Quy trình ETL được thực hiện bằng SQL Server Integration Services (SSIS) để chuyển đổi dữ liệu từ file phẳng (.csv) vào SQL Server.

<img width="828" height="400" alt="image" src="https://github.com/user-attachments/assets/f3fa95ca-46b0-4c50-8f50-d89eeec99335" />

## Phân tích đa chiều (SSAS)
Sử dụng SQL Server Analysis Services (SSAS) để xây dựng Cube, cho phép truy vấn dữ liệu nhanh chóng bằng ngôn ngữ MDX.
- Measures: Tính toán các độ đo quan trọng như Sales, Profit, Quantity và các thành viên tính toán (Calculated Members) như Discount Amount, Avg Profit.
- Hierarchies: Thiết lập phân cấp cho OrderDate (Year > Month > Day) và Location (Region > State > City > PostalCode) để hỗ trợ tính năng Drill-down.
- Querying: Triển khai 14 câu truy vấn nghiệp vụ phức tạp về doanh thu theo năm, top thành phố, lợi nhuận âm và hiệu quả vận chuyển.
- 
<img width="828" height="460" alt="image" src="https://github.com/user-attachments/assets/2246cc17-f817-43d3-92a9-e0e9e72ac090" />

Ví dụ 1 câu truy vấn sử dụng MDX:

<img width="828" height="624" alt="image" src="https://github.com/user-attachments/assets/97df9d41-0d6a-4d41-9d3d-31c5d5fb10d4" />


## Báo cáo & Trực quan hóa 
### Công cụ Power BI: 

- Báo biểu 1: Phân tích Doanh số theo Thời gian
<img width="828" height="460" alt="image" src="https://github.com/user-attachments/assets/66cf8fd5-6cce-4a01-af99-b80db5822924" />

- Báo biểu 2: Phân Tích Theo Danh Mục Sản Phẩm

<img width="828" height="460" alt="image" src="https://github.com/user-attachments/assets/d90f755f-013b-4a0b-9a67-55f205932a10" />

- Báo biểu 3: Phân tích Doanh thu theo Khu vực Địa lý

<img width="828" height="460" alt="image" src="https://github.com/user-attachments/assets/e2c83681-c142-492b-86ef-75f7eb96a9c1" />

### Công cụ Excel:
- Báo biểu 4: Phân tích theo Danh mục và Sản phẩm Lợi nhuận Âm
<img width="828" height="460" alt="image" src="https://github.com/user-attachments/assets/4dc78942-9b32-48c4-8898-d68b279c98d4" />

- Báo biểu 5: Thời gian giao hàng trung bình (DaysToShip) của các đơn hàng có sự khác biệt như thế nào giữa các Phân khúc Khách hàng và theo từng Năm đặt hàng?

<img width="828" height="460" alt="image" src="https://github.com/user-attachments/assets/8586bf6f-f024-4cdd-b70f-6da048e08a29" />


## Công cụ sử dụng
- Database: Microsoft SQL Server.
- ETL Tool: SQL Server Integration Services (SSIS).
- OLAP Tool: SQL Server Analysis Services (SSAS).
- Visualization: Power BI Desktop & Excel Pivot Table.
- Programming: Python (cho tiền xử lý dữ liệu).

## Tác giả

| MSSV | Họ và tên | Nội dung đóng góp |
|------|----------|-------------------|
| 23521021 | Hồ Như Hồng Ngọc | Thiết kế kiến trúc Kho dữ liệu (Snowflake Schema), cấu hình các chiều (Dimensions) và bảng sự kiện (Fact table). Kết hợp Machine Learning và Data Mining để tìm insights. |
| 23521563 | Đinh Bảo Thy | Triển khai ETL bằng SSIS, xây dựng Cube trong SSAS, thiết lập Measures & Hierarchies. Thiết kế Dashboard Power BI, Excel và truy vấnMDX. |
