# 📦 Hệ Thống Quản Lý Nhập – Xuất – Tồn Kho

> **Đồ án môn học** | Spring Boot 3 + SQL Server + Thymeleaf

---

## 📋 Mục Lục

## [Mô tả dự án]
- [Công nghệ sử dụng]
- [Cấu trúc dự án]
- [Yêu cầu hệ thống]
- [Chuẩn bị Database]
- [Hướng dẫn chạy trên IntelliJ IDEA]
- [Hướng dẫn chạy trên STS4]
- [Cấu hình application.properties]
- [Chạy bằng Maven (Terminal)]
- [Chức năng hệ thống]
- [Giao diện]
- [Database Schema]
- [Xử lý lỗi thường gặp]

---

## 🎯 Mô Tả Dự Án

Hệ thống quản lý nhập – xuất – tồn kho là ứng dụng web giúp doanh nghiệp theo dõi và quản lý hàng hóa trong kho một cách hiệu quả. Hệ thống cung cấp các chức năng:

- ✅ **Quản lý sản phẩm**: Thêm, sửa, xóa, tìm kiếm sản phẩm
- ✅ **Quản lý nhà cung cấp**: CRUD nhà cung cấp
- ✅ **Phiếu nhập kho**: Tạo và theo dõi đơn nhập hàng
- ✅ **Phiếu xuất kho**: Tạo và theo dõi đơn xuất hàng
- ✅ **Theo dõi tồn kho**: Xem số lượng tồn kho theo thời gian thực
- ✅ **Báo cáo thống kê**: Biểu đồ nhập/xuất, cảnh báo hàng sắp hết
- ✅ **Dashboard**: Tổng quan hệ thống

---

## 🛠 Công Nghệ Sử Dụng

| Công nghệ | Phiên bản | Mục đích |
|-----------|-----------|----------|
| Java | 17 | Ngôn ngữ lập trình |
| Spring Boot | 3.2.x | Framework backend |
| Spring Data JPA | 3.2.x | ORM / Database access |
| SQL Server | 2019+ | Cơ sở dữ liệu |
| Thymeleaf | 3.1.x | Template Engine |
| Bootstrap | 5.3 | CSS Framework |
| Chart.js | 4.x | Biểu đồ thống kê |
| Maven | 3.8+ | Build tool |

---

## 📁 Cấu Trúc Dự Án

```
inventory-system/
├── src/
│   ├── main/
│   │   ├── java/com/inventory/
│   │   │   ├── InventoryApplication.java       # Main class
│   │   │   ├── config/
│   │   │   │   └── DataInitializer.java        # Dữ liệu mẫu tự động
│   │   │   ├── controller/
│   │   │   │   ├── DashboardController.java
│   │   │   │   ├── ProductController.java
│   │   │   │   ├── SupplierController.java
│   │   │   │   ├── ImportController.java
│   │   │   │   ├── ExportController.java
│   │   │   │   └── ReportController.java
│   │   │   ├── service/
│   │   │   │   ├── ProductService.java
│   │   │   │   ├── SupplierService.java
│   │   │   │   ├── ImportService.java
│   │   │   │   └── ExportService.java
│   │   │   ├── repository/
│   │   │   │   ├── ProductRepository.java
│   │   │   │   ├── SupplierRepository.java
│   │   │   │   ├── CategoryRepository.java
│   │   │   │   ├── ImportOrderRepository.java
│   │   │   │   └── ExportOrderRepository.java
│   │   │   └── entity/
│   │   │       ├── Product.java
│   │   │       ├── Category.java
│   │   │       ├── Supplier.java
│   │   │       ├── ImportOrder.java
│   │   │       ├── ImportDetail.java
│   │   │       ├── ExportOrder.java
│   │   │       └── ExportDetail.java
│   │   └── resources/
│   │       ├── application.properties          # Cấu hình ứng dụng
│   │       ├── static/
│   │       │   └── css/style.css               # CSS tùy chỉnh
│   │       └── templates/
│   │           ├── layout/base.html            # Layout chung
│   │           ├── dashboard.html
│   │           ├── product/  (list.html, form.html)
│   │           ├── supplier/ (list.html, form.html)
│   │           ├── import/   (list.html, form.html, detail.html)
│   │           ├── export/   (list.html, form.html, detail.html)
│   │           └── report/index.html
├── pom.xml
└── README.md
```

---

## 💻 Yêu Cầu Hệ Thống

| Phần mềm | Phiên bản tối thiểu | Tải về |
|---|---|---|
| JDK | 17+ | https://adoptium.net |
| SQL Server | 2019+ | https://www.microsoft.com/sql-server |
| SQL Server Management Studio | 19+ | https://aka.ms/ssmsfullsetup |
| Maven | 3.8+ | https://maven.apache.org (hoặc dùng bundled trong IDE) |
| **IntelliJ IDEA** | 2023.1+ | https://www.jetbrains.com/idea/download |
| *(hoặc)* **STS4** | 4.20+ | https://spring.io/tools |

> ⚠️ **Lưu ý:** IntelliJ IDEA Community **không hỗ trợ** Spring Boot wizard. Dùng bản **Ultimate** hoặc tạo project từ https://start.spring.io rồi import vào.

---

## 🗄️ Chuẩn Bị Database
### Mở SQLSERVER và chạy file db.sql trong project

## 🚀 Hướng Dẫn Chạy Trên IntelliJ IDEA

### Cách 1: Tạo Project Mới Từ Spring Initializr (Khuyến nghị)

#### Bước 1 — Tạo project từ https://start.spring.io

Mở trình duyệt, truy cập **https://start.spring.io** và điền thông tin:

| Trường | Giá trị |
|--------|---------|
| Project | Maven |
| Language | Java |
| Spring Boot | 3.2.x |
| Group | `com.inventory` |
| Artifact | `inventory-system` |
| Name | `inventory-system` |
| Packaging | Jar |
| Java | 17 |

Tìm và thêm các **Dependencies**:
- ✅ Spring Web
- ✅ Spring Data JPA
- ✅ Thymeleaf
- ✅ MS SQL Server Driver
- ✅ Spring Boot DevTools
- ✅ Lombok
- ✅ Validation

Nhấn **GENERATE** → tải về file `inventory-system.zip` → giải nén.

#### Bước 2 — Mở project trong IntelliJ IDEA

1. Khởi động **IntelliJ IDEA**
2. Chọn **Open** (hoặc **File → Open**)
3. Duyệt đến thư mục vừa giải nén, chọn thư mục `inventory-system`
4. Nhấn **OK / Trust Project**
5. IntelliJ tự nhận diện là Maven project và tải dependencies → chờ thanh tiến trình ở góc phải dưới hoàn tất

#### Bước 3 — Cài đặt Lombok Plugin

1. Vào **File → Settings** (`Ctrl + Alt + S`)
2. Chọn **Plugins** → tìm kiếm **Lombok**
3. Nhấn **Install** → **Restart IDE**
4. Vào **Settings → Build, Execution, Deployment → Compiler → Annotation Processors**
5. Tick chọn **Enable annotation processing** → **OK**

#### Bước 4 — Cấu hình JDK

1. Vào **File → Project Structure** (`Ctrl + Alt + Shift + S`)
2. Chọn **Project** → **SDK**: chọn **JDK 17** (nếu chưa có, nhấn **Add SDK → Download JDK**)
3. **Language level**: chọn **17** → **Apply → OK**

#### Bước 5 — Sao chép source code vào project

Sao chép toàn bộ file `.java`, `.html`, `.css`, `application.properties` từ project mẫu vào đúng vị trí trong cấu trúc thư mục.

#### Bước 6 — Cấu hình database

Mở file `src/main/resources/application.properties`, cập nhật thông tin SQL Server:

```properties
spring.datasource.url=jdbc:sqlserver://localhost:1433;databaseName=inventory_db;encrypt=false;trustServerCertificate=true
spring.datasource.username=sa
spring.datasource.password=YOUR_PASSWORD_HERE
```

> Thay `YOUR_PASSWORD_HERE` bằng mật khẩu SQL Server của bạn.

#### Bước 7 — Chạy ứng dụng

**Cách A — Dùng nút Run:**
1. Mở file `InventoryApplication.java`
2. Nhấn nút ▶️ **Run** màu xanh bên cạnh dòng `public static void main`
3. Hoặc nhấn `Shift + F10`

**Cách B — Dùng Run Configuration:**
1. Vào **Run → Edit Configurations**
2. Nhấn **+** → chọn **Spring Boot**
3. Điền:
    - **Name**: `InventoryApp`
    - **Main class**: `com.inventory.InventoryApplication`
4. Nhấn **Apply → OK → Run**

**Cách C — Dùng Maven Tool Window:**
1. Mở **View → Tool Windows → Maven**
2. Expand `inventory-system → Plugins → spring-boot`
3. Double-click **spring-boot:run**

#### Bước 8 — Kiểm tra ứng dụng

Sau khi console hiển thị:
```
Started InventoryApplication in X.XXX seconds
```
Mở trình duyệt và truy cập: **http://localhost:8080**

---

### Cách 2: Import Project ZIP Có Sẵn

Nếu đã có file `inventory-system.zip`:

1. Giải nén file ZIP
2. Mở IntelliJ IDEA → **File → Open**
3. Chọn thư mục `inventory-system` (thư mục chứa `pom.xml`)
4. IntelliJ tự động nhận diện Maven project
5. Chờ **import dependencies** hoàn tất (xem thanh tiến trình phía dưới)
6. Cập nhật `application.properties` với thông tin SQL Server
7. Chạy `InventoryApplication.java`

---

## 🔧 Hướng Dẫn Chạy Trên STS4

### Bước 1 — Cài đặt STS4

Tải STS4 tại: https://spring.io/tools → Giải nén → Chạy `SpringToolSuite4.exe`

### Bước 2 — Tạo Spring Boot Project Mới

1. Mở STS4 → **File → New → Spring Starter Project**
2. Điền thông tin:
    - **Name**: `inventory-system`
    - **Type**: Maven
    - **Java Version**: 17
    - **Packaging**: Jar
    - **Group**: `com.inventory`
    - **Artifact**: `inventory-system`
    - **Package**: `com.inventory`
3. Nhấn **Next**

### Bước 3 — Chọn Dependencies

Tìm và chọn:
- ✅ Spring Web
- ✅ Spring Data JPA
- ✅ Thymeleaf
- ✅ MS SQL Server Driver
- ✅ Spring Boot DevTools
- ✅ Lombok
- ✅ Validation

Nhấn **Finish** → STS4 tự động tải dependencies.

### Bước 4 — Sao chép source code

Sao chép toàn bộ file từ project mẫu vào đúng vị trí.

### Bước 5 — Cấu hình database

Cập nhật `application.properties` (xem mục bên dưới).

### Bước 6 — Chạy ứng dụng

**Chuột phải vào project** → **Run As → Spring Boot App**

---

## ⚙️ Cấu Hình application.properties

```properties
# ===================================
# SERVER
# ===================================
server.port=8080

# ===================================
# SQL SERVER
# ===================================
spring.datasource.url=jdbc:sqlserver://localhost:1433;databaseName=inventory_db;encrypt=false;trustServerCertificate=true
spring.datasource.username=sa
spring.datasource.password=YourPassword123
spring.datasource.driver-class-name=com.microsoft.sqlserver.jdbc.SQLServerDriver

# Nếu dùng SQL Server Express thì đổi URL thành:
# jdbc:sqlserver://localhost\SQLEXPRESS:1433;databaseName=inventory_db;encrypt=false;trustServerCertificate=true

# ===================================
# JPA / HIBERNATE
# ===================================
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.SQLServerDialect

# ===================================
# THYMELEAF
# ===================================
spring.thymeleaf.cache=false
spring.thymeleaf.encoding=UTF-8
```

---

## ▶️ Chạy Bằng Maven (Terminal)

```bash
# Di chuyển vào thư mục project
cd inventory-system

# Tải dependencies và build
mvn clean install

# Chạy ứng dụng
mvn spring-boot:run
```

Truy cập: **http://localhost:8080**

---

## 🔧 Chức Năng Hệ Thống

### 1. Dashboard
- Tổng số sản phẩm, nhà cung cấp
- Số phiếu nhập/xuất trong tháng
- Cảnh báo sản phẩm sắp hết hàng
- Biểu đồ nhập xuất theo tháng (Chart.js)
- Thao tác nhanh (shortcut buttons)

### 2. Quản lý Sản phẩm
- Danh sách có phân trang và tìm kiếm
- Thêm / Sửa / Xóa mềm (soft delete)
- Gắn danh mục và nhà cung cấp
- Hiển thị trạng thái tồn kho (đủ hàng / sắp hết)

### 3. Quản lý Nhà Cung Cấp
- CRUD đầy đủ
- Tìm kiếm theo mã và tên
- Quản lý trạng thái hoạt động

### 4. Phiếu Nhập Kho
- Tạo phiếu nhập với nhiều dòng sản phẩm (thêm/xóa động bằng JS)
- Tự động gợi ý giá nhập từ dữ liệu sản phẩm
- Xác nhận nhập kho → tự động cộng tồn kho
- Hủy phiếu / xem chi tiết / in phiếu

### 5. Phiếu Xuất Kho
- Tạo phiếu xuất với kiểm tra tồn kho thực tế
- Hiển thị số lượng tồn hiện tại khi chọn sản phẩm
- Xác nhận xuất kho → tự động trừ tồn kho
- Hủy phiếu / xem chi tiết / in phiếu

### 6. Báo Cáo Thống Kê
- Biểu đồ cột: số phiếu nhập/xuất theo 12 tháng
- Biểu đồ tròn: phân bổ tình trạng tồn kho
- Bảng chi tiết tồn kho toàn bộ sản phẩm
- Hỗ trợ in báo cáo

---

## 🎨 Giao Diện

- **Màu chủ đạo**: Xanh navy `#1a237e` + Trắng
- **Sidebar**: Cố định bên trái, highlight trang hiện tại
- **Layout**: Responsive Bootstrap 5
- **Icons**: Bootstrap Icons
- **Charts**: Chart.js 4.x
- **Thông báo**: Flash message tự động ẩn sau 4 giây
- **In phiếu**: Hỗ trợ `window.print()` ẩn sidebar

---

## 🗄️ Database Schema

```
categories      : id, name, description
suppliers       : id, code, name, phone, email, address, status
products        : id, code, name, category_id(FK), supplier_id(FK),
                  unit, cost_price, sell_price, quantity, min_quantity,
                  description, status
import_orders   : id, code, import_date, supplier_id(FK),
                  total_amount, status, note
import_details  : id, import_order_id(FK), product_id(FK),
                  quantity, unit_price, total_price (computed)
export_orders   : id, code, export_date, customer_name, customer_phone,
                  total_amount, status, note
export_details  : id, export_order_id(FK), product_id(FK),
                  quantity, unit_price, total_price (computed)
```

---

## 🐛 Xử Lý Lỗi Thường Gặp

### ❌ Lỗi kết nối SQL Server
```
com.microsoft.sqlserver.jdbc.SQLServerException: Login failed
```
**Giải pháp:**
- Kiểm tra SQL Server đang chạy (Services → SQL Server)
- Kiểm tra `username` và `password` trong `application.properties`
- Bật **SQL Server Authentication** trong SSMS: chuột phải Server → Properties → Security → chọn *SQL Server and Windows Authentication mode*
- Đảm bảo TCP/IP được bật trong **SQL Server Configuration Manager**

### ❌ Lỗi port 1433 không kết nối được
```
TCP/IP connection to host failed
```
**Giải pháp:**
- Mở **SQL Server Configuration Manager**
- SQL Server Network Configuration → Protocols for MSSQLSERVER → TCP/IP → Enable
- Restart SQL Server service

### ❌ Lỗi Lombok không hoạt động (IntelliJ)
```
Cannot find symbol: method builder()
```
**Giải pháp:**
- Cài Lombok plugin: File → Settings → Plugins → tìm "Lombok" → Install
- Bật annotation processing: Settings → Build → Compiler → Annotation Processors → Enable

### ❌ Lỗi Java version
```
Source option 17 is not supported
```
**Giải pháp (IntelliJ):**
- File → Project Structure → Project SDK → chọn JDK 17
- File → Settings → Build → Compiler → Project bytecode version → 17

### ❌ Port 8080 bị chiếm
```
Web server failed to start. Port 8080 was already in use.
```
**Giải pháp:** Đổi port trong `application.properties`:
```properties
server.port=8081
```

---

## 👨‍💻 Thông Tin Đồ Án

**Tên đề tài**: Hệ thống Quản lý Nhập – Xuất – Tồn Kho  
**Công nghệ**: Spring Boot 3 · Spring Data JPA · Thymeleaf · SQL Server · Bootstrap 5  
**IDE hỗ trợ**: IntelliJ IDEA (Ultimate / Community) · Spring Tool Suite 4 (STS4)  
**Truy cập**: http://localhost:8080 sau khi khởi động