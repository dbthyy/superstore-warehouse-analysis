# Phân Tích Hiệu Suất Bán Hàng & Lợi Nhuận
Môn học IS217 - Kho dữ liệu và OLAP

## Tổng quan
Dự án này tập trung vào việc xây dựng hệ thống hỗ trợ ra quyết định (DSS) cho chuỗi cung ứng bán lẻ dựa trên bộ dữ liệu Superstore Sales. Hệ thống thực hiện chuyển đổi dữ liệu thô thành kho dữ liệu chuẩn hóa, xây dựng các khối phân tích đa chiều để phục vụ báo cáo quản trị chuyên sâu.

## Kiến trúc Hệ thống
Dự án được triển khai qua 4 giai đoạn kỹ thuật chính:
- Tiền xử lý dữ liệu: Sử dụng Python/Pandas để làm sạch, chuẩn hóa tên biến và tạo các đặc trưng mới như IsHoliday.
- Data Warehouse & SSIS: Thiết kế lược đồ và thực hiện quy trình ETL.
- SSAS (Online Analytical Processing): Xây dựng các khối Cube đa chiều và định nghĩa các Measures/Hierarchies.
- Data Visualization: Trực quan hóa dữ liệu qua Power BI và Excel.

## Thiết kế Kho dữ liệu (Data Warehouse)
Hệ thống sử dụng mô hình Lược đồ Bông tuyết (Snowflake Schema) để tối ưu hóa việc lưu trữ và phân tích.

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
- Data Flow Task: Sử dụng các component Sort để loại bỏ trùng lặp và Data Conversion để chuẩn hóa kiểu dữ liệu.
- Derived Columns: Tạo các cột phái sinh cho DimTime (phân tách Ngày, Tháng, Năm).
- Merge Join: Kết hợp các bảng Bridge để hoàn thiện cấu trúc Dimension và Fact.

## Phân tích đa chiều (SSAS)
Sử dụng SQL Server Analysis Services (SSAS) để xây dựng Cube, cho phép truy vấn dữ liệu nhanh chóng bằng ngôn ngữ MDX.
- Measures: Tính toán các độ đo quan trọng như Sales, Profit, Quantity và các thành viên tính toán (Calculated Members) như Discount Amount, Avg Profit.
- Hierarchies: Thiết lập phân cấp cho OrderDate (Year > Month > Day) và Location (Region > State > City > PostalCode) để hỗ trợ tính năng Drill-down.
- Querying: Triển khai 14 câu truy vấn nghiệp vụ phức tạp về doanh thu theo năm, top thành phố, lợi nhuận âm và hiệu quả vận chuyển.

## Báo cáo & Trực quan hóa (Power BI)
Hệ thống báo cáo được xây dựng trên Power BI kết nối trực tiếp với SQL Server/SSAS Cube để cung cấp cái nhìn trực quan về hiệu suất kinh doanh.
- Báo biểu 1 (Thời gian): Phân tích xu hướng doanh thu ổn định qua các năm, đặc biệt tăng mạnh vào quý 4.
- Báo biểu 2 (Sản phẩm): Làm rõ sự đối lập giữa Office Supplies (số lượng bán cao nhất) và Technology (lợi nhuận cao nhất).
- Báo biểu 3 (Địa lý): Xác định New York City và California là hai thị trường trọng điểm mang lại lợi nhuận lớn nhất.

## Công cụ sử dụng
- Database: Microsoft SQL Server.
- ETL Tool: SQL Server Integration Services (SSIS).
- OLAP Tool: SQL Server Analysis Services (SSAS).
- Visualization: Power BI Desktop & Excel Pivot Table.


Programming: Python (cho tiền xử lý dữ liệu)
