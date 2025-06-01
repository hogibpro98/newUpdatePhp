# Database Memory Bank - KANTAKI-WIZ

## Mục đích
Thư mục này chứa tất cả tài liệu liên quan đến database của hệ thống KANTAKI-WIZ, bao gồm cấu trúc bảng, comment tiếng Nhật, và hướng dẫn phát triển.

## Cấu trúc Files

### 📋 [databaseContext.md](databaseContext.md)
**File tổng quan** - Tài liệu toàn diện về database
- **Tổng quan**: Thông tin kết nối, thống kê database (MySQL 8.0, kantaki_dev)
- **Phân loại bảng**: 82 bảng được phân loại theo 5 nhóm chính
- **Comment tiếng Nhật**: Tích hợp comment gốc với mô tả tiếng Việt
- **Kiến trúc**: Mối quan hệ giữa các entity
- **Hướng dẫn**: Development guidelines, backup, monitoring, troubleshooting

### 🔧 [databaseCommands.md](databaseCommands.md)
**Lệnh Database** - Tập hợp lệnh thao tác database qua Docker
- **Template Commands**: Base commands sử dụng Docker MySQL container
- **Search & Analysis**: Tìm kiếm table/column theo comment và tên
- **Structure Analysis**: Kiểm tra cấu trúc bảng, indexes, foreign keys
- **Statistics**: Thống kê database, dung lượng, performance
- **Utilities**: Backup, maintenance, troubleshooting commands
- **Examples**: Lệnh mẫu cho các use case thường gặp

### 🔧 [system-tables.md](system-tables.md)
**Bảng Hệ thống** - Framework và hạ tầng (7 bảng)
- Cache system, job queues, migrations
- Performance monitoring và troubleshooting
- Integration patterns với PHP frameworks

### 💾 [master-tables.md](master-tables.md)
**Bảng Master Data** - Dữ liệu tham chiếu (36 bảng)
- Entity cốt lõi: user, staff, office, place
- Y tế chuyên biệt: disease, insurance, services
- User extensions: 17 bảng mở rộng thông tin người dùng
- Compliance và data quality guidelines

### 📊 [operational-tables.md](operational-tables.md)
**Bảng Vận hành** - Dữ liệu hoạt động hàng ngày (18 bảng)
- Planning vs Records (予定 vs 実績)
- Weekly scheduling patterns
- Pricing & billing architecture
- Japanese healthcare compliance

### 📄 [document-tables.md](document-tables.md)
**Bảng Tài liệu** - Healthcare documentation (19 bảng)
- Kantaki multi-functional nursing records
- Visiting nurse documentation
- Legal compliance & audit requirements
- Document workflow patterns

### 📝 [log-tables.md](log-tables.md)
**Bảng Log** - Audit trail & system monitoring (2 bảng)
- Complete audit trail cho compliance
- Error tracking & troubleshooting
- Security monitoring & alerts
- Performance optimization strategies

### 🔧 [databaseCommands.md](databaseCommands.md)
**Lệnh Database** - Tập hợp lệnh thao tác database qua Docker
- **Template Commands**: Base commands sử dụng Docker MySQL container
- **Search & Analysis**: Tìm kiếm table/column theo comment và tên
- **Structure Analysis**: Kiểm tra cấu trúc bảng, indexes, foreign keys
- **Statistics**: Thống kê database, dung lượng, performance
- **Utilities**: Backup, maintenance, troubleshooting commands
- **Examples**: Lệnh mẫu cho các use case thường gặp với aliases

## Phân loại Database

### 🔧 Bảng Hệ thống (7 bảng)
- Framework và hạ tầng
- Cache, jobs, migrations

### 💾 Bảng Master Data (36 bảng - `mst_`)
- **Entity cốt lõi**: user, staff, office, place
- **Y tế chuyên biệt**: disease, insure, service
- **Người dùng mở rộng**: 17 bảng mst_user_*
- **Hỗ trợ**: area, bank, car, code, news

### 📊 Bảng Vận hành (18 bảng - `dat_`)
- **Kế hoạch (予定)**: Lịch trình và planning
- **Thành tích (実績)**: Kết quả thực tế
- **Lịch trình tuần**: Weekly scheduling
- **Cấu hình**: System configuration

### 📄 Bảng Tài liệu (19 bảng - `doc_`)
- **Kantaki records**: Hồ sơ điều dưỡng đa chức năng
- **Visit records**: Thăm khám điều dưỡng
- **Reports**: Báo cáo và sự kiện

### 📝 Bảng Log (2 bảng)
- System logging và error tracking

## Thuật ngữ quan trọng

### Từ khóa cốt lõi
- **看多機** (Kantaki) = Điều dưỡng đa chức năng
- **利用者** (Riyōsha) = Người sử dụng dịch vụ
- **従業員** (Jūgyōin) = Nhân viên
- **予定** (Yotei) = Lịch trình/kế hoạch
- **実績** (Jisseki) = Thành tích/kết quả thực tế

### Dịch vụ y tế
- **訪問看護** (Hōmon Kango) = Điều dưỡng thăm khám
- **加減算** (Kagensan) = Cộng trừ (điều chỉnh phí)
- **実費** (Jippi) = Chi phí thực tế

## Sử dụng Memory Bank này

### 🔍 Tìm kiếm bảng
1. **Theo nhóm chức năng**: Chọn file phù hợp (system, master, operational, document, log)
2. **Theo tên bảng**: Dùng Ctrl+F trong file tương ứng
3. **Theo comment tiếng Nhật**: Search comment trong từng file chuyên biệt
4. **Theo prefix**: mst_, dat_, doc_ để xác định loại dữ liệu

### 🛠️ Development
1. **Naming convention**: Tuân theo pattern `prefix_description`
2. **Database access**: Chỉ sử dụng PDO với prepared statements
3. **Japanese support**: UTF-8 và JST timezone

### 📊 Monitoring
- Query response time < 2 seconds
- Connection pool < 80%
- Backup: Daily full + 4-hour incremental

## Vấn đề đã phát hiện

### ⚠️ Data inconsistency
- `dat_user_record_add` có comment sai
- Một số bảng thiếu comment

### 📦 Backup tables
- `mst_add.20240122` - Backup từ 22/01/2024
- `mst_user.20240123` - Backup từ 23/01/2024

## Cập nhật Memory Bank

### Khi có thay đổi database:
1. **Xác định nhóm bảng**: Xác định bảng thuộc nhóm nào (system/master/operational/document/log)
2. **Cập nhật file chuyên biệt**: Update file tương ứng với thông tin mới
3. **Sync databaseContext.md**: Cập nhật file tổng quan nếu cần
4. **Cross-check consistency**: Đảm bảo thông tin consistent giữa các files
5. **Update README**: Nếu có structural changes

### Versioning:
- Ghi chú ngày cập nhật trong commit message
- Backup các file cũ trước khi thay đổi lớn
- Cross-reference với database migration files

---

> 💡 **Tip**: Luôn sử dụng encoding UTF-8 khi làm việc với database MySQL để đảm bảo comment tiếng Nhật hiển thị đúng.