# Hệ Thống Quản Lý & Tra Cứu Lịch Điểm Đến

Ứng dụng web Single Page Application (SPA) điều hành tour học sinh và dã ngoại trải nghiệm, kết nối và đồng bộ trực tuyến hai chiều với cơ sở dữ liệu Google Sheets và tích hợp Google Gemini AI.

---

## 🌟 Tính Năng Chính

1. **Đồng bộ đám mây 100% qua Google Sheets (Không lưu trữ dữ liệu nghiệp vụ trên máy tính cá nhân)**:
   - Dữ liệu điểm đến, lịch đặt, danh sách đoàn và nhật ký kiểm toán thay đổi lịch được lưu trữ trực tiếp trên Google Spreadsheet.
   - Cache buster thời gian thực (`?t=timestamp`) đảm bảo dữ liệu luôn mới nhất khi truy cập.
2. **Giao diện chuẩn tỉ lệ màn hình cố định (100vh / 100dvh)**:
   - **Top Header (22vh)**: Tên hệ thống, tài khoản điều hành đang online, danh sách nút thao tác nhanh (Đăng xuất, Lịch sử, Chỉnh lịch, Lịch đã chốt, Quản trị), dropdown chọn điểm đến kèm huy hiệu sức chứa tối đa và 4 chú giải màu sắc trạng thái.
   - **Middle Calendar (54vh)**: Thanh điều hướng tháng (hỗ trợ tối đa 24 tháng), lưới 42 ô lịch hiển thị song song ngày Dương lịch và ngày Âm lịch Việt Nam (thuật toán thiên văn Hồ Ngọc Đức), huy hiệu số lượng khách/trạng thái và hỗ trợ vuốt màn hình (Swipe left/right) trên điện thoại.
   - **Bottom Footer (24vh)**: Ảnh toàn cảnh điểm đến với lớp gradient overlay và địa chỉ địa lý chi tiết.
3. **Phân loại màu sắc trực quan**:
   - 🟢 **Còn trống (TRONG)**: Màu trắng viền xanh lá, chưa có đoàn đặt.
   - 🟡 **Ít khách (NHO)**: Màu vàng hổ phách, đoàn ngoài < 500 học sinh.
   - 🔴 **Đông khách / Kín lịch (DONG)**: Màu đỏ hồng, đã nhận ≥ 500 học sinh hoặc điểm đến dừng nhận đoàn.
   - 🔵 **Lịch Công ty mình (VAT)**: Nền xanh da trời, viền xanh nổi bật khi do Viện Khoa học An Toàn trực tiếp chốt lịch.
4. **Đặt lịch đa đoàn & Tích lũy không mất đoàn cũ**:
   - Hỗ trợ lưu trữ mảng JSON `danh_sach_doan_json` cho mỗi ngày, cho phép nhiều trường cùng đăng ký trên một ngày mà không bị đè dữ liệu.
   - Cảnh báo thông minh: chặn đặt lịch khi ô màu đỏ; hiển thị cảnh báo số lượng học sinh hiện có khi ô màu vàng; mở form trực tiếp khi ô màu xanh.
5. **Cập nhật thủ công trạng thái lịch (Full Screen)**:
   - Cơ chế 1-chạm xoay vòng: `Còn trống ➔ Ít khách ➔ Kín lịch ➔ Còn trống`.
   - Nút **Toàn bộ (🔴)** chuyển toàn bộ tháng sang kín lịch chỉ với 1 click.
   - Cảnh báo an toàn khi can thiệp vào ngày công ty mình đã chốt.
   - Chuyển về "Còn trống" sẽ xóa sạch dữ liệu đoàn cũ trên Google Sheet.
   - Tự động ghi nhật ký kiểm toán vào trang tính `LICH_SU_SUA`.
6. **Nhật ký kiểm toán Online (Audit Log)**:
   - Tải trực tiếp từ trang tính `LICH_SU_SUA`.
   - Tìm kiếm realtime theo tên điểm, ngày, người sửa, trường cũ.
   - Nút xóa sạch lịch sử trên Google Sheet.
7. **Tra cứu điểm đến khả dụng theo ngày (🔍)**:
   - Nhập ngày linh hoạt: gõ số ngày (`15`), ngày tháng (`20/11`), hoặc ngày tháng năm (`20/11/2026`).
   - Quét toàn bộ điểm đến, chỉ hiển thị điểm còn trống hoặc còn nhận khách (<500 hs). Nhấp vào điểm đến sẽ tự động điều hướng lịch chính đến điểm đó.
8. **Danh sách lịch công ty đã chốt (📋)**:
   - Lọc riêng các trường do Viện KH An Toàn đặt.
   - Nút gọi điện nhanh (`tel:...`), bộ lọc tìm kiếm và bật/tắt ẩn lịch ngày cũ.
9. **Quản trị hệ thống & Nhập file Excel / AI**:
   - Thêm, sửa, xóa điểm đến (form 2/3 tên, 1/3 sức chứa).
   - Đọc file Excel `.xlsx`, `.xls` bằng SheetJS, xử lý các sheet năm 2026/2027, lọc bỏ tên công ty lữ hành và tự động đồng bộ theo lô lên Google Sheet.
   - Tích hợp Google Gemini AI qua Apps Script (`GEMINI_API_KEY`).

---

## 🗄️ Cấu Trúc Cơ Sở Dữ Liệu Google Sheet

- **Link Google Sheet**: [Xem Google Spreadsheet](https://docs.google.com/spreadsheets/d/1RXnMFMT43iU9qUYCa3Yjp4sUwA47Hao19K28cXleQiI/edit)
- **ID Bảng tính**: `1RXnMFMT43iU9qUYCa3Yjp4sUwA47Hao19K28cXleQiI`

### 1. Trang tính `DIEM_DEN`
| Cột | Tên trường | Mô tả |
| :--- | :--- | :--- |
| **A** | `id` | Mã định danh duy nhất (VD: `DD_1793789870676`) |
| **B** | `ten` | Tên khu du lịch, điểm đến |
| **C** | `dia_chi` | Địa chỉ địa lý chi tiết |
| **D** | `anh_url` | Đường dẫn ảnh minh họa cảnh quan |
| **E** | `suc_chua` | Sức chứa tối đa trong ngày (số học sinh) |

### 2. Trang tính `LICH_DAT`
| Cột | Tên trường | Mô tả |
| :--- | :--- | :--- |
| **A** | `ID` | Mã phiên đặt lịch (VD: `BK_1793868033376_aouh`) |
| **B** | `destination_ID` | Mã điểm đến liên kết (`DD_...`) |
| **C** | `Năm tháng ngày` | Chuẩn `YYYY-MM-DD` |
| **D** | `Tên trường / Tên đoàn` | Tên trường, phân hiệu hoặc các đơn vị đối tác |
| **E** | `Số lượng` | Tổng số học sinh tiếp đón trong ngày |
| **F** | `Phân loại` | `TRONG` (Còn trống), `NHO` (Ít khách), `DONG` (Kín lịch) |
| **G** | `Địa chỉ xã/phường` | Địa chỉ xã của trường |
| **H** | `Người đặt / Sale phụ trách`| Tên người điều hành / booker |
| **I** | `SĐT liên hệ` | Số điện thoại liên hệ |
| **J** | `Đối tác` | "Viện KH An Toàn" nếu là lịch nội bộ |
| **K** | `is_internal` | `TRUE` nếu là công ty mình, `FALSE` nếu là khách ngoài |
| **L** | `danh_sach_doan_json` | Chuỗi JSON mảng các đoàn cùng đi trong ngày |

### 3. Trang tính `LICH_SU_SUA`
| Cột | Tên trường | Mô tả |
| :--- | :--- | :--- |
| **A** | `Mã Log` | Mã định danh phiên sửa |
| **B** | `Tên điểm đến` | Tên khu du lịch |
| **C** | `Ngày tour` | Chuẩn `YYYY-MM-DD` |
| **D** | `Trạng thái mới` | `TRONG`, `NHO`, hoặc `DONG` |
| **E** | `Tài khoản thực hiện sửa` | Họ và tên người sửa |
| **F** | `Số điện thoại người sửa` | SĐT người sửa |
| **G** | `Thời gian sửa` | Thời gian thực hiện (DD/MM/YYYY HH:mm:ss) |
| **H** | `Lịch công ty mình bị sửa?` | `TRUE` / `FALSE` |
| **I** | `Thông tin trường cũ` | Tên trường + phân hiệu trước khi bị thay thế |
| **J** | `Người chốt trước đó` | Người chốt lịch trước đó |
| **K** | `Số điện thoại người chốt trước đó`| SĐT người chốt trước đó |
| **L** | `Ngày xác nhận chốt trước đó` | Ngày xác nhận chốt trước đó |

---

## 🚀 Hướng Dẫn Cài Đặt & Triển Khai

### 1. Cập nhật mã nguồn lên Google Apps Script
1. Mở dự án Apps Script liên kết với bảng tính Google Sheets:
   - Vào Google Sheet ➔ Menu **Tiện ích mở rộng (Extensions)** ➔ **Apps Script**.
2. Sao chép toàn bộ mã nguồn trong tệp [`Code.gs`](./Code.gs) hoặc [`app script.txt`](./app%20script.txt) và dán đè vào trình soạn thảo tệp `Mã.gs` (hoặc `Code.gs`) trên Apps Script.
3. Kiểm tra khóa API Gemini:
   - Vào biểu tượng bánh răng **Cài đặt dự án (Project Settings)** ở thanh bên trái Apps Script.
   - Mục **Thuộc tính tập lệnh (Script Properties)**: Đảm bảo đã có thuộc tính `GEMINI_API_KEY` với giá trị API key của bạn.
4. Triển khai Web App (Deploy):
   - Nhấp vào nút **Triển khai (Deploy)** ➔ **Quản lý bản triển khai (Manage deployments)**.
   - Chọn bản triển khai hiện tại, nhấp biểu tượng cây bút **Chỉnh sửa (Edit)**.
   - Mục **Phiên bản (Version)**: Chọn **Phiên bản mới (New version)**.
   - Quyền truy cập: **Bất kỳ ai (Anyone)**.
   - Nhấp **Triển khai (Deploy)**.
   - Đảm bảo URL Web App trùng với URL cấu hình trong `index.html`:
     ```javascript
     const APPS_SCRIPT_URL = "https://script.google.com/macros/s/AKfycbwHzF5cCopy1EQH9UkAQcG3sfX_usbG3z9CxuFtspRwf_b1lHzGf_UbamE3suyqy0jT/exec";
     ```

### 2. Đẩy mã nguồn lên Github và chạy GitHub Pages
1. Khởi tạo Git và Commit:
   ```bash
   git init
   git add .
   git commit -m "Khoi tao he thong quan ly va tra cuu lich diem den"
   ```
2. Tạo một Repository mới trên [GitHub.com](https://github.com/new) (ví dụ đặt tên là `lich-diem-den`).
3. Đẩy code lên GitHub:
   ```bash
   git remote add origin https://github.com/<tai-khoan-github-cua-ban>/lich-diem-den.git
   git branch -M main
   git push -u origin main
   ```
4. Bật GitHub Pages để chạy web trực tiếp miễn phí:
   - Vào Repository trên GitHub ➔ Chọn tab **Settings**.
   - Ở thanh bên trái, chọn mục **Pages**.
   - Tại phần **Build and deployment** ➔ **Branch**: Chọn nhánh `main` và thư mục `/ (root)`.
   - Nhấp **Save**.
   - Sau 1-2 phút, bạn sẽ nhận được đường dẫn trang web trực tiếp: `https://<tai-khoan-github-cua-ban>.github.io/lich-diem-den/`.
