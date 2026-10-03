# BÁO CÁO TỔNG QUAN VỀ HỆ THỐNG WEB VÀ CÔNG VIỆC CỤ THỂ  

**Giảng viên hướng dẫn:** Tô Hải Thiên  
**Sinh viên thực hiện:** Nguyễn Hoài Linh  
**Nhánh Git (Branch):** `linh`  
**Dự án:** Hệ thống Web Quản lý Phòng trọ  

---

## I. TỔNG QUAN VỀ DỰ ÁN  

### 1. Thực trạng & Thách thức trong quản lý trọ truyền thống
Hiện nay, phần lớn các chủ dãy trọ và chung cư mini vẫn quản lý bằng sổ sách chép tay hoặc file Excel rời rạc. Phương pháp này tồn tại 3 hạn chế lớn:
* **Tốn thời gian & Dễ sai sót:** Hàng tháng chủ trọ phải đến tận phòng chép chỉ số điện/nước, sau đó tự tính toán từng hóa đơn thủ công, rất dễ nhầm lẫn khi nhân đơn giá hoặc cộng trừ công nợ.
* **Thiếu sự minh bạch:** Khách thuê thường không theo dõi được chi tiết lượng điện/nước mình đã sử dụng theo tháng, dễ dẫn đến thắc mắc và tranh cãi khi đóng tiền.
* **Khó kiểm soát công nợ:** Khi khách thuê thanh toán làm nhiều đợt (trả trước một phần, nợ lại một phần), chủ trọ rất khó theo dõi chính xác số tiền còn thiếu của từng phòng, dẫn đến trôi nợ hoặc thất thoát.

### 2. Giải pháp của hệ thống
Hệ thống **Web Quản lý Phòng trọ** được thiết kế nhằm tự động hóa quy trình quản lý, tạo ra một nền tảng tập trung cho cả Chủ trọ và Người thuê:
* **Tự động hóa tính toán:** Chủ trọ chỉ cần **nhập tay chỉ số điện/nước mới**, hệ thống sẽ tự động đối soát với chỉ số cũ, tính lượng tiêu thụ, nhân đơn giá và tự động sinh hóa đơn tổng trong vài giây.
* **Minh bạch thông tin:** Người thuê trọ có tài khoản riêng để chủ động tra cứu hóa đơn, xem chi tiết lượng điện/nước tiêu thụ và lịch sử đóng tiền của mình.
* **Quản lý công nợ rõ ràng:** Hỗ trợ thanh toán linh hoạt nhiều đợt (tiền mặt / chuyển khoản), tự động gạch nợ và theo dõi chính xác số tiền đã trả - còn nợ của từng phòng.

---

## II. BÁO CÁO PHÂN CÔNG CÔNG VIỆC CÁ NHÂN & TIẾN ĐỘ THỰC HIỆN

**Sinh viên phụ trách:** Nguyễn Hoài Linh  
**Phân hệ đảm nhận:** Module **Điện nước, Hóa đơn & Thanh toán**  

### 1. Vai trò & Phân công Trách nhiệm trong Nhóm
* **Vai trò:** UI Frontend Developer & Backend Designer cho Phân hệ Điện - Nước & Hóa đơn.
* **Trách nhiệm đảm nhận:**
  * Thiết kế Giao diện người dùng (UI/UX) cho màn hình Quản lý Chỉ số Điện & Nước (`/utilities`) và Quản lý Hóa đơn & Thanh toán (`/invoices`).
  * Xây dựng cấu trúc Cơ sở dữ liệu (Database Schema) cho 3 bảng: `utility_readings`, `invoices`, `payments`.
  * Đặc tả chi tiết logic nghiệp vụ và kịch bản xử lý API cho phân hệ tài chính.

### 2. Chi tiết Nghiệp vụ & Giao diện Phụ trách

#### A. Màn hình Quản lý Chỉ số Điện & Nước (`/utilities`)
* **Giao diện & Chức năng:** Thiết kế màn hình cho phép chủ trọ **nhập tay** chỉ số điện và nước mới của từng phòng theo Tháng/Năm.
* **Nghiệp vụ xử lý:**
  * Tự động hiển thị chỉ số điện/nước cũ của tháng liền trước.
  * Tự động tính lượng tiêu thụ ngay khi nhập chỉ số mới:  
    $$\text{Lượng dùng (kWh/m}^3\text{)} = \text{Số mới (nhập tay)} - \text{Số cũ}$$
  * Hiển thị trạng thái kiểm tra (`Chưa nhập`, `Đã nhập`) giúp chủ trọ không bỏ sót phòng nào.
  * Cung cấp công cụ chỉnh sửa chỉ số trong trường hợp nhập nhầm.

#### B. Màn hình Hóa đơn & Quản lý Thanh toán (`/invoices`)
* **Tự động sinh hóa đơn:** Tổng hợp tiền phòng, tiền điện/nước (từ số tiêu thụ nhân đơn giá) và các dịch vụ bổ sung (Wifi, vệ sinh...) để ra Tổng tiền hóa đơn.
* **Xử lý đóng tiền nhiều đợt & Công nợ:**
  * Hỗ trợ ghi nhận trường hợp người thuê thanh toán trước một phần tiền.
  * Tự động tính toán và hiển thị rõ ràng: `Số tiền đã trả` và `Số tiền còn nợ`.
  * Tự động cập nhật trạng thái hóa đơn (`Chưa thanh toán` $\rightarrow$ `Thanh toán một phần` $\rightarrow$ `Đã thanh toán`).
* **Lịch sử giao dịch:** Form ghi nhận thu tiền (tiền mặt/chuyển khoản) và bảng lưu trữ chi tiết mốc thời gian từng đợt nộp tiền.

---

### 3. Thiết kế CSDL & Định hướng Nghiệp vụ Backend (Sẵn sàng lập trình API)
* **Cấu trúc Cơ sở dữ liệu (MySQL):**
  1. Bảng `utility_readings`: Lưu chỉ số điện/nước cũ và mới nhập tay theo từng tháng `(id, room_id, month, year, old_electric, new_electric, old_water, new_water)`.
  2. Bảng `invoices`: Lưu chi tiết tổng tiền, số tiền đã trả và công nợ `(id, contract_id, month, year, room_fee, utility_fee, service_fee, total_amount, paid_amount, status)`.
  3. Bảng `payments`: Lưu vết chi tiết từng đợt đóng tiền `(id, invoice_id, payment_date, amount, payment_method, note)`.
* **Định hướng Logic API sẽ triển khai:**
  * `POST /api/v1/utilities`: Nhận chỉ số điện/nước nhập tay từ giao diện, kiểm tra điều kiện hợp lệ trước khi lưu.
  * `POST /api/v1/invoices/generate`: Tự động lấy chỉ số điện/nước tiêu thụ nhân đơn giá dịch vụ để tính tổng tiền hóa đơn.
  * `POST /api/v1/invoices/{id}/payments`: Ghi nhận giao dịch thanh toán, tự động trừ lùi công nợ `(Còn nợ = Tổng tiền - Đã trả)` và cập nhật trạng thái hóa đơn.

---

## III. DỰ KIẾN XỬ LÝ CÁC TRƯỜNG HỢP NGOẠI LỆ (EDGE CASES)

Trong bước phát triển logic backend tiếp theo, em thiết lập các quy tắc ràng buộc chặt chẽ sau:
1. **Ràng buộc chỉ số hợp lệ:** Khóa không cho phép lưu nếu $\text{Số mới} < \text{Số cũ}$.
2. **Chống trùng lặp dữ liệu:** Ràng buộc Unique cho bộ `(room_id, month, year)` để tránh việc nhập trùng chỉ số 2 lần trong 1 tháng.
3. **Quản lý khóa hóa đơn:** Khi hóa đơn đã chuyển trạng thái `Đã thanh toán`, hệ thống sẽ chặn không cho chỉnh sửa chỉ số điện/nước của kỳ đó.

---

## IV. HÌNH ẢNH MINH HỌA GIAO DIỆN ĐÃ THIẾT KẾ

### 1. Giao diện Màn hình Điện nước (`/utilities`)
<img width="1457" height="722" alt="image" src="https://github.com/user-attachments/assets/327314b5-e4f4-49b2-a609-2b0e79434eed" />


### 2. Giao diện Màn hình Hóa đơn & Thu tiền (`/invoices`)
<img width="1472" height="728" alt="image" src="https://github.com/user-attachments/assets/ee7ba52e-0acd-471d-85e0-15371c76be5b" />


## V. CÔNG CỤ SỬ DỤNG & QUY TRÌNH QUẢN LÝ CODE

* **Công nghệ UI:** ReactJS, HTML/CSS, Tailwind CSS / Bootstrap.
* **Quản lý mã nguồn (Git Flow):**
  * Tất cả các file giao diện và cấu hình được làm việc trên nhánh cá nhân `linh`.
  * **Lệnh Git thực hiện:**
    ```bash
    git checkout linh
    git add .
    git commit -m "Tạo giao diện hóa đơn và điện nước"
    git push origin linh
    ```
