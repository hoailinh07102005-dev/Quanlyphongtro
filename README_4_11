# BÁO CÁO TỔNG QUAN VỀ HỆ THỐNG WEB VÀ CỘNG VIỆC CỤ THỂ 

**Giảng viên hướng dẫn:** Tô Hải Thiên
**Sinh viên thực hiện:** Nguyễn Hoài Linh  
**Nhánh Git (Branch):** `linh`  
**Dự án:** Hệ thống Web Quản lý Phòng trọ  

---

## I. TỔNG QUAN VỀ DỰ ÁN 

### 1. Thực trạng & Thách thức trong quản lý trọ truyền thống
Hiện nay, phần lớn các chủ dãy trọ và chung cư mini vẫn quản lý bằng sổ sách chép tay hoặc file Excel rời rạc. Phương pháp này tồn tại 3 hạn chế lớn:
* **Tốn thời gian & Dễ sai sót:** Hàng tháng chủ trọ phải đến tận phòng chép chỉ số điện nước, sau đó tự tính toán từng hóa đơn thủ công, rất dễ nhầm lẫn khi nhân đơn giá hoặc cộng trừ công nợ.
* **Thiếu sự minh bạch:** Khách thuê thường không theo dõi được chi tiết lượng điện/nước mình đã sử dụng theo tháng, dễ dẫn đến thắc mắc và tranh cãi khi đóng tiền.
* **Khó kiểm soát công nợ:** Khi khách thuê thanh toán làm nhiều đợt (trả trước một phần, nợ lại một phần), chủ trọ rất khó theo dõi chính xác số tiền còn thiếu của từng phòng, dẫn đến trôi nợ hoặc thất thoát.

### 2. Giải pháp của hệ thống
Hệ thống **Web Quản lý Phòng trọ** được thiết kế nhằm tự động hóa quy trình quản lý, tạo ra một nền tảng tập trung cho cả Chủ trọ và Người thuê:
* **Tự động hóa tính toán:** Chủ trọ chỉ cần **nhập tay chỉ số điện/nước mới**, hệ thống sẽ tự động đối soát với chỉ số cũ, tính lượng tiêu thụ, nhân đơn giá và tự động sinh hóa đơn tổng trong vài giây.
* **Minh bạch thông tin:** Người thuê trọ có tài khoản riêng để chủ động tra cứu hóa đơn, xem chi tiết lượng điện/nước tiêu thụ và lịch sử đóng tiền của mình.
* **Quản lý công nợ rõ ràng:** Hỗ trợ thanh toán linh hoạt nhiều đợt (tiền mặt / chuyển khoản), tự động gạch nợ và theo dõi chính xác số tiền đã trả - còn nợ của từng phòng.

---

## II. BÁO CÁO PHÂN CÔNG CÔNG VIỆC CÁ NHÂN

**Sinh viên phụ trách:** Nguyễn Hoài Linh  
**Phân hệ đảm nhận:** Module **Điện nước, Hóa đơn & Thanh toán**

Trong dự án này, em trực tiếp đảm nhận phân hệ quản lý tài chính và hóa đơn hàng tháng. Cụ thể bao gồm các hạng mục sau:

### 1. Màn hình Quản lý Chỉ số Điện & Nước (`/utilities`)
* **Giao diện & Chức năng:** Thiết kế màn hình cho phép chủ trọ **nhập tay** chỉ số điện và nước mới của từng phòng theo Tháng/Năm.
* **Nghiệp vụ xử lý:**
  * Tự động hiển thị chỉ số điện/nước cũ của tháng liền trước.
  * Tự động tính lượng tiêu thụ ngay khi nhập chỉ số mới:  
    $$\text{Lượng dùng (kWh/m}^3\text{)} = \text{Số mới (nhập tay)} - \text{Số cũ}$$
  * Hiển thị trạng thái kiểm tra (`Chưa nhập`, `Đã nhập`) giúp chủ trọ không bỏ sót phòng nào.
  * Cung cấp công cụ chỉnh sửa chỉ số trong trường hợp nhập nhầm.

### 2. Màn hình Hóa đơn & Quản lý Thanh toán (`/invoices`)
* **Tự động sinh hóa đơn:** Tổng hợp tiền phòng, tiền điện/nước (từ số tiêu thụ nhân đơn giá) và các dịch vụ bổ sung (Wifi, vệ sinh...) để ra Tổng tiền hóa đơn.
* **Xử lý đóng tiền nhiều đợt & Công nợ:**
  * Hỗ trợ ghi nhận trường hợp người thuê thanh toán trước một phần tiền.
  * Tự động tính toán và hiển thị rõ ràng: `Số tiền đã trả` và `Số tiền còn nợ`.
  * Tự động cập nhật trạng thái hóa đơn (`Chưa thanh toán` $\rightarrow$ `Thanh toán một phần` $\rightarrow$ `Đã thanh toán`).
* **Lịch sử giao dịch:** Form ghi nhận thu tiền (tiền mặt/chuyển khoản) và bảng lưu trữ chi tiết mốc thời gian từng đợt nộp tiền.

### 3. Thiết kế Cơ sở dữ liệu & Viết API (MySQL & Node.js)
* **Cơ sở dữ liệu (MySQL):**
  1. Bảng `utility_readings`: Lưu chỉ số điện/nước cũ và mới nhập tay theo từng tháng, có ràng buộc chống nhập trùng 2 lần trong 1 tháng cho cùng 1 phòng.
  2. Bảng `invoices`: Lưu mã hóa đơn, chi tiết các khoản phí, tổng tiền phải trả, số tiền đã trả dồn tích và hạn thanh toán.
  3. Bảng `payments`: Lưu vết chi tiết từng giao dịch đóng tiền của khách thuê.
* **Hệ thống RESTful API:**
  * `POST /api/v1/utilities`: Nhận và lưu chỉ số điện/nước nhập tay từ giao diện.
  * `POST /api/v1/invoices/generate`: Tự động tính toán chi phí và sinh hóa đơn hàng tháng.
  * `POST /api/v1/invoices/{id}/payments`: Ghi nhận giao dịch đóng tiền, tự động cập nhật số tiền đã trả và công nợ.

---

## III. CÔNG CỤ SỬ DỤNG & QUY TRÌNH PHÁT TRIỂN

* **Công nghệ sử dụng:** ReactJS, Node.js (Express), MySQL, Tailwind CSS / Bootstrap.
* **Kiểm thử & Quản lý code:**
  * Sử dụng **Postman** để kiểm thử dữ liệu và các đầu API.
  * Quản lý mã nguồn bằng Git/GitHub, toàn bộ công việc cá nhân được đẩy lên nhánh (branch) `linh`.




