# 1. Chức năng Đăng nhập – Authentication

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-AUTH-001** | Người dùng đăng nhập | Đăng nhập với username và password hợp lệ | Tài khoản đã đăng ký và Active | 1. Mở Login<br>2. Nhập username<br>3. Nhập password<br>4. Nhấn Login | Username: `user01`<br>Password: `Password@123` | Đăng nhập thành công; tạo token/session và chuyển vào hệ thống | High |
| **TC-AUTH-002** | Người dùng đăng nhập | Đăng nhập bằng Customer hợp lệ | Customer đã đăng ký | 1. Nhập thông tin<br>2. Nhấn Login | Username: `customer01`<br>Password: `Customer@123` | Đăng nhập thành công với role Customer | High |
| **TC-AUTH-003** | Người dùng đăng nhập | Đăng nhập bằng Driver hợp lệ | Driver tồn tại và Active | 1. Nhập username<br>2. Nhập password<br>3. Login | Username: `driver01`<br>Password: `Driver@123` | Đăng nhập thành công với role Driver | High |
| **TC-AUTH-004** | Người dùng đăng nhập | Đăng nhập bằng Admin hợp lệ | Admin tồn tại và Active | 1. Nhập thông tin<br>2. Login | Username: `admin01`<br>Password: `Admin@123` | Đăng nhập thành công với quyền Administrator | High |
| **TC-AUTH-005** | Người dùng đăng nhập | Username không tồn tại | Hệ thống hoạt động | 1. Mở Login<br>2. Nhập username<br>3. Nhập password<br>4. Login | `unknown01` / `Password@123` | Đăng nhập thất bại; không tạo token | High |
| **TC-AUTH-006** | Người dùng đăng nhập | Password không đúng | Username tồn tại và Active | 1. Nhập username đúng<br>2. Nhập password sai<br>3. Login | `user01` / `Wrong@123` | Đăng nhập thất bại | High |
| **TC-AUTH-007** | Người dùng đăng nhập | Tài khoản bị khóa | Account `user01` Locked | 1. Nhập username<br>2. Nhập password đúng<br>3. Login | `user01` / `Password@123` | Không cho đăng nhập; thông báo tài khoản bị khóa | High |
| **TC-AUTH-008** | Người dùng đăng nhập | Tài khoản Inactive | Account Inactive | 1. Nhập thông tin<br>2. Login | `user02` / `Password@123` | Không tạo session/token | High |
| **TC-AUTH-009** | Người dùng đăng nhập | Username đạt độ dài tối thiểu | Rule username đã định nghĩa | 1. Nhập username ở giới hạn min<br>2. Nhập password<br>3. Login | Username: `u01` | Hệ thống xử lý đúng theo giới hạn username | Medium |
| **TC-AUTH-010** | Người dùng đăng nhập | Username đạt độ dài tối đa | Rule username đã định nghĩa | 1. Nhập username max length<br>2. Login | Username: chuỗi đúng max length | Hệ thống chấp nhận nếu không vượt giới hạn | Medium |
| **TC-AUTH-011** | Người dùng đăng nhập | Password đạt độ dài tối thiểu | Password min = 8 | 1. Nhập password 8 ký tự<br>2. Login | `Abc@1234` | Hệ thống xử lý password đúng giới hạn | Medium |
| **TC-AUTH-012** | Người dùng đăng nhập | Password đạt độ dài tối đa | Password có giới hạn max | 1. Nhập password max length<br>2. Login | Password = chuỗi max length | Hệ thống xử lý đúng giới hạn | Medium |
| **TC-AUTH-013** | Người dùng đăng nhập | Username để trống | Đang ở Login | 1. Không nhập username<br>2. Nhập password<br>3. Login | Username: `""` | Không cho đăng nhập; báo username bắt buộc | High |
| **TC-AUTH-014** | Người dùng đăng nhập | Password để trống | Đang ở Login | 1. Nhập username<br>2. Không nhập password<br>3. Login | Password: `""` | Không cho đăng nhập; báo password bắt buộc | High |
| **TC-AUTH-015** | Người dùng đăng nhập | Username và password đều trống | Đang ở Login | 1. Không nhập dữ liệu<br>2. Login | Username: `""`<br>Password: `""` | Hiển thị lỗi validation cho cả hai trường | High |
| **TC-AUTH-016** | Người dùng đăng nhập | Gửi request thiếu field username | API hoạt động | 1. Gửi request login<br>2. Không truyền username | `{password: "Password@123"}` | API trả lỗi validation; không xác thực | High |
| **TC-AUTH-017** | Người dùng đăng nhập | Username chứa ký tự đặc biệt không hợp lệ | API hoạt động | 1. Nhập username sai format<br>2. Login | `user@@@` | Từ chối username sai định dạng | Medium |
| **TC-AUTH-018** | Người dùng đăng nhập | Username chứa khoảng trắng không hợp lệ | Rule username không cho khoảng trắng | 1. Nhập username<br>2. Login | `user 01` | Từ chối dữ liệu không hợp lệ | Medium |
| **TC-AUTH-019** | Người dùng đăng nhập | Password sai kiểu dữ liệu | API hoạt động | 1. Gửi request<br>2. Truyền password dạng số/object | `password: 123456` | API từ chối nếu password yêu cầu String | Medium |
| **TC-AUTH-020** | Người dùng đăng nhập | Username truyền dạng số | API hoạt động | 1. Gửi request<br>2. Username không phải String | `username: 12345` | API trả lỗi sai kiểu dữ liệu | Medium |

<br>

# 2. Chức năng Đăng ký Customer – Registration

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-REG-001** | Đăng ký Customer | Đăng ký đầy đủ thông tin hợp lệ | Email/Phone chưa tồn tại | 1. Mở Register<br>2. Nhập thông tin<br>3. Submit | Name=`Nguyen Van A`<br>Email=`a@gmail.com`<br>Phone=`0912345678`<br>Password=`Abc@1234` | Tạo Customer thành công | High |
| **TC-REG-002** | Đăng ký Customer | Đăng ký với email hợp lệ khác | Email chưa tồn tại | 1. Nhập form<br>2. Submit | Email=`b@gmail.com`<br>Phone=`0912345679` | Tạo tài khoản thành công | High |
| **TC-REG-003** | Đăng ký Customer | Đăng ký với số điện thoại hợp lệ | Phone chưa tồn tại | 1. Nhập form<br>2. Submit | Phone=`0987654321` | Tài khoản được tạo | High |
| **TC-REG-004** | Đăng ký Customer | Đăng ký password hợp lệ | Password đáp ứng rule | 1. Nhập form<br>2. Submit | Password=`Customer@123` | Tài khoản được tạo, password được hash | High |
| **TC-REG-005** | Đăng ký Customer | Email đã tồn tại | Email đã có | 1. Nhập form<br>2. Submit | Email=`existing@gmail.com` | Từ chối đăng ký; email đã tồn tại | High |
| **TC-REG-006** | Đăng ký Customer | Phone đã tồn tại | Phone đã có | 1. Nhập form<br>2. Submit | Phone=`0912345678` | Từ chối đăng ký | High |
| **TC-REG-007** | Đăng ký Customer | Password không đáp ứng rule | API hoạt động | 1. Nhập password yếu<br>2. Submit | Password=`123456` | Từ chối password không hợp lệ | High |
| **TC-REG-008** | Đăng ký Customer | Email thuộc tài khoản đã khóa | Account tồn tại | 1. Submit form | Email=`locked@gmail.com` | Không tạo tài khoản trùng | Medium |
| **TC-REG-009** | Đăng ký Customer | Name đạt min length | Rule Name có min | 1. Nhập Name min length<br>2. Submit | Name=`An` | Chấp nhận nếu đạt min | Medium |
| **TC-REG-010** | Đăng ký Customer | Name đạt max length | Rule Name có max | 1. Nhập Name max length<br>2. Submit | Chuỗi Name đúng max | Chấp nhận nếu không vượt max | Medium |
| **TC-REG-011** | Đăng ký Customer | Password đúng min length | Password min = 8 | 1. Nhập password 8 ký tự<br>2. Submit | Password=`Abc@1234` | Chấp nhận | Medium |
| **TC-REG-012** | Đăng ký Customer | Phone đạt giới hạn 10 số | Phone yêu cầu 10 số | 1. Nhập phone 10 số<br>2. Submit | Phone=`0912345678` | Chấp nhận | Medium |
| **TC-REG-013** | Đăng ký Customer | Name để trống | Form Register | 1. Bỏ trống Name<br>2. Submit | Name=`""` | Báo Name bắt buộc | High |
| **TC-REG-014** | Đăng ký Customer | Email để trống | Form Register | 1. Bỏ trống Email<br>2. Submit | Email=`""` | Báo Email bắt buộc | High |
| **TC-REG-015** | Đăng ký Customer | Phone để trống | Form Register | 1. Bỏ trống Phone<br>2. Submit | Phone=`""` | Báo Phone bắt buộc | High |
| **TC-REG-016** | Đăng ký Customer | Password để trống | Form Register | 1. Bỏ trống Password<br>2. Submit | Password=`""` | Báo Password bắt buộc | High |
| **TC-REG-017** | Đăng ký Customer | Email sai format | Form Register | 1. Nhập Email sai<br>2. Submit | Email=`abcgmail.com` | Báo Email không hợp lệ | Medium |
| **TC-REG-018** | Đăng ký Customer | Phone chứa chữ | Form Register | 1. Nhập Phone<br>2. Submit | Phone=`09123abc78` | Báo Phone không hợp lệ | Medium |
| **TC-REG-019** | Đăng ký Customer | Name chứa ký tự không hợp lệ | Form Register | 1. Nhập Name<br>2. Submit | Name=`Nguyen@123` | Từ chối Name nếu không cho phép ký tự | Medium |
| **TC-REG-020** | Đăng ký Customer | Password truyền sai kiểu | API hoạt động | 1. Gửi password không phải String | `password: 123456` | API trả lỗi validation | Medium |

<br>

# 3. Chức năng Tạo yêu cầu đặt xe – Booking

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **TC-BOOK-001** | Đặt xe | Tạo booking hợp lệ | Customer đã đăng nhập | 1. Gửi request<br>2. Nhập Pickup<br>3. Nhập Destination<br>4. Submit | Pickup=IUH<br>Destination=Tan Son Nhat<br>Vehicle=4-seat | Tạo Ride thành công; trạng thái Pending | High |
| **TC-BOOK-002** | Đặt xe | Booking với địa chỉ hợp lệ | Customer Active | Nhập đầy đủ thông tin | Pickup=District 1<br>Destination=District 3 | Booking được tạo | High |
| **TC-BOOK-003** | Đặt xe | Booking với loại xe hợp lệ | Customer Active | Chọn loại xe → Submit | Vehicle=4-seat | Hệ thống chấp nhận | High |
| **TC-BOOK-004** | Đặt xe | Booking nhiều thông tin hợp lệ | Customer Active | Nhập toàn bộ field | Pickup, Destination, Vehicle hợp lệ | Tạo booking thành công | High |
| **TC-BOOK-005** | Đặt xe | Pickup = Destination | Customer đăng nhập | Nhập cùng địa điểm | IUH → IUH | Từ chối nếu vi phạm nghiệp vụ | High |
| **TC-BOOK-006** | Đặt xe | Vehicle type không tồn tại | Customer đăng nhập | Gửi request | Vehicle=10-seat | Từ chối Vehicle Type | High |
| **TC-BOOK-007** | Đặt xe | Customer không tồn tại | Token không hợp lệ | Gửi request | CustomerID=C999 | Từ chối request | High |
| **TC-BOOK-008** | Đặt xe | Token hết hạn | Token expired | Gửi request | Token=expired | Trả lỗi authentication | High |
| **TC-BOOK-009** | Đặt xe | Pickup đạt max length | Customer đăng nhập | Nhập Pickup max | Chuỗi đúng max length | Chấp nhận | Medium |
| **TC-BOOK-010** | Đặt xe | Destination đạt max length | Customer đăng nhập | Nhập Destination max | Chuỗi đúng max | Chấp nhận | Medium |
| **TC-BOOK-011** | Đặt xe | Pickup ngay dưới giới hạn | Customer đăng nhập | Nhập Pickup min | Chuỗi min length | Chấp nhận | Medium |
| **TC-BOOK-012** | Đặt xe | Khoảng cách/giá trị biên | Customer đăng nhập | Nhập giá trị min | Distance=0 | Xử lý đúng theo Business Rule | Medium |
| **TC-BOOK-013** | Đặt xe | Pickup rỗng | Customer đăng nhập | Bỏ Pickup → Submit | Pickup="" | Báo Pickup bắt buộc | High |
| **TC-BOOK-014** | Đặt xe | Destination rỗng | Customer đăng nhập | Bỏ Destination | Destination="" | Báo Destination bắt buộc | High |
| **TC-BOOK-015** | Đặt xe | Vehicle Type rỗng | Customer đăng nhập | Không chọn Vehicle | Vehicle="" | Báo Vehicle Type bắt buộc | High |
| **TC-BOOK-016** | Đặt xe | Body request rỗng | Customer đăng nhập | Gửi {} | {} | API trả lỗi validation | High |
| **TC-BOOK-017** | Đặt xe | Pickup sai kiểu | Customer đăng nhập | Gửi Pickup số | pickup=12345 | API từ chối sai kiểu dữ liệu | Medium |
| **TC-BOOK-018** | Đặt xe | Vehicle Type sai format | Customer đăng nhập | Nhập ký tự lạ | vehicleType=@@@ | API từ chối | Medium |
| **TC-BOOK-019** | Đặt xe | CustomerID sai format | Customer đăng nhập | Gửi ID sai | C### | API báo CustomerID không hợp lệ | Medium |
| **TC-BOOK-020** | Đặt xe | Destination chứa dữ liệu không hợp lệ | Customer đăng nhập | Nhập dữ liệu đặc biệt | `<script>alert(1)</script>` | Dữ liệu bị từ chối/sanitize; không thực thi script | High |

<br>

# 4. Chức năng Tìm tài xế khả dụng

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-DRV-001** | Tìm tài xế | Có Driver Available | Operation Staff đăng nhập | Gọi API tìm Driver | `Status=Available` | Trả danh sách Driver Available | High |
| **TC-DRV-002** | Tìm tài xế | Có nhiều Driver Available | Operation Staff đăng nhập | Gọi API | `D1, D2, D3 = Available` | Trả đúng các Driver Available | High |
| **TC-DRV-003** | Tìm tài xế | Driver có Vehicle hợp lệ | Driver Active | Gọi API | `Driver=D001` | Driver được trả về | High |
| **TC-DRV-004** | Tìm tài xế | Driver đủ điều kiện nhận chuyến | Driver Available | Gọi API | `D001=Available` | Driver xuất hiện | High |
| **TC-DRV-005** | Tìm tài xế | Driver Busy | Driver Busy | Gọi API | `D001=Busy` | Không trả Driver Busy | High |
| **TC-DRV-006** | Tìm tài xế | Driver Offline | Driver Offline | Gọi API | `D002=Offline` | Không trả Driver Offline | High |
| **TC-DRV-007** | Tìm tài xế | Driver không tồn tại | API hoạt động | Tìm ID | `D999` | Không tìm thấy Driver | Medium |
| **TC-DRV-008** | Tìm tài xế | Driver đã được phân công | Driver Busy/Assigned | Gọi API | `D003=Busy` | Không đưa vào Available | High |
| **TC-DRV-009** | Tìm tài xế | Chỉ có 1 Driver | API hoạt động | Gọi API | `Available count=1` | Trả đúng 1 Driver | Medium |
| **TC-DRV-010** | Tìm tài xế | Số lượng Driver ở max page size | API có pagination | Gọi API | `Limit=20` | Trả tối đa 20 record | Medium |
| **TC-DRV-011** | Tìm tài xế | Page đầu tiên | API pagination | Gọi API | `Page=1` | Trả dữ liệu trang 1 | Medium |
| **TC-DRV-012** | Tìm tài xế | Limit nhỏ nhất | API pagination | Gọi API | `Limit=1` | Trả tối đa 1 Driver | Medium |
| **TC-DRV-013** | Tìm tài xế | Không có Driver Available | Hệ thống không có Driver Available | Gọi API | `Available=0` | Trả danh sách rỗng | Medium |
| **TC-DRV-014** | Tìm tài xế | Status rỗng | API hoạt động | Gửi status rỗng | `status=""` | Validation error hoặc dùng mặc định theo API | Medium |
| **TC-DRV-015** | Tìm tài xế | Request không có filter | API hoạt động | Gọi API không parameter | `{}` | API xử lý theo default | Medium |
| **TC-DRV-016** | Tìm tài xế | Query rỗng | API hoạt động | Gửi query rỗng | `?status=` | Xử lý đúng theo API | Low |
| **TC-DRV-017** | Tìm tài xế | Status sai format | API hoạt động | Gửi status | `status=123` | API từ chối status | Medium |
| **TC-DRV-018** | Tìm tài xế | Page là chữ | Pagination | Gửi request | `page=abc` | Báo page không hợp lệ | Medium |
| **TC-DRV-019** | Tìm tài xế | Limit là chữ | Pagination | Gửi request | `limit=abc` | Báo limit không hợp lệ | Medium |
| **TC-DRV-020** | Tìm tài xế | Status không thuộc enum | API hoạt động | Gửi status | `status=Unknown` | API từ chối giá trị status | Medium |

<br>

# 5. Chức năng Phân công tài xế

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-ASG-001** | Phân công tài xế | Phân công Driver Available cho Ride | Ride tồn tại, Driver Available | Gửi assignment | `Ride=R001, Driver=D001` | Assignment thành công; Ride → Driver Assigned | High |
| **TC-ASG-002** | Phân công tài xế | Phân công Driver phù hợp Vehicle | Driver và Vehicle phù hợp | Chọn Driver → Submit | `4-seat Ride + 4-seat Driver` | Phân công thành công | High |
| **TC-ASG-003** | Phân công tài xế | Phân công Ride Pending | Ride Pending | Chọn Driver → Submit | `R001=Pending` | Assignment thành công | High |
| **TC-ASG-004** | Phân công tài xế | Assignment hợp lệ | Cả hai ID tồn tại | Gửi request | `R001 / D001` | Tạo Assignment | High |
| **TC-ASG-005** | Phân công tài xế | Driver Busy | Driver Busy | Chọn Driver → Submit | `D001=Busy` | Không cho phân công | High |
| **TC-ASG-006** | Phân công tài xế | Ride đã Completed | Ride Completed | Gửi assignment | `R001=Completed` | Từ chối assignment | High |
| **TC-ASG-007** | Phân công tài xế | Ride đã có Driver | Ride Assigned | Gửi assignment mới | `R001 đã assigned` | Không tạo assignment thứ hai | High |
| **TC-ASG-008** | Phân công tài xế | Driver không tồn tại | API hoạt động | Gửi request | `D999` | Từ chối | High |
| **TC-ASG-009** | Phân công tài xế | Chỉ còn 1 Driver Available | 1 Driver Available | Assignment | `D001` | Assignment thành công | Medium |
| **TC-ASG-010** | Phân công tài xế | ID ở độ dài biên | ID có giới hạn | Gửi ID max | `ID=max length` | Chấp nhận nếu hợp lệ | Medium |
| **TC-ASG-011** | Phân công tài xế | AssignmentID đạt giới hạn | Rule ID | Gửi ID min/max | `ID đúng giới hạn` | Xử lý đúng | Medium |
| **TC-ASG-012** | Phân công tài xế | Request ở giới hạn số field | API schema cố định | Gửi request | `Đủ field bắt buộc` | Chấp nhận | Medium |
| **TC-ASG-013** | Phân công tài xế | DriverID rỗng | Ride tồn tại | Bỏ DriverID → Submit | `DriverID=""` | Báo DriverID bắt buộc | High |
| **TC-ASG-014** | Phân công tài xế | RideID rỗng | Driver tồn tại | Bỏ RideID | `RideID=""` | Báo RideID bắt buộc | High |
| **TC-ASG-015** | Phân công tài xế | Cả hai ID rỗng | API hoạt động | Submit | `{}` | Validation error | High |
| **TC-ASG-016** | Phân công tài xế | Body request rỗng | API hoạt động | Gửi body rỗng | `{}` | Không tạo assignment | High |
| **TC-ASG-017** | Phân công tài xế | DriverID sai format | API hoạt động | Gửi ID | `D###` | Báo ID không hợp lệ | Medium |
| **TC-ASG-018** | Phân công tài xế | RideID sai format | API hoạt động | Gửi ID | `R@@@` | Báo ID không hợp lệ | Medium |
| **TC-ASG-019** | Phân công tài xế | DriverID sai kiểu | API hoạt động | Gửi số | `12345` | API báo sai kiểu | Medium |
| **TC-ASG-020** | Phân công tài xế | Status giả mạo | API hoạt động | Client gửi status không hợp lệ | `status=Completed` | Server không cho client tự thay đổi trạng thái trái rule | High |

<br>

# 6. Tài xế chấp nhận chuyến — ACCEPT

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-ACCEPT-001** | Tài xế chấp nhận chuyến | Tài xế chấp nhận chuyến được phân công | Driver đã đăng nhập, Assignment tồn tại và đang chờ chấp nhận | Gửi yêu cầu Accept Assignment | `Assignment=ASG001, Driver=D001` | Chấp nhận thành công; Ride → Driver Accepted | High |
| **TC-ACCEPT-002** | Tài xế chấp nhận chuyến | Tài xế chấp nhận chuyến của mình | Driver đúng với Assignment | Đăng nhập → Chọn chuyến → Chấp nhận | `ASG=ASG002, Driver=D002` | Assignment được cập nhật thành công | High |
| **TC-ACCEPT-003** | Tài xế chấp nhận chuyến | Chấp nhận Ride đang Driver Assigned | Ride đã được phân công | Gửi request Accept | `Ride=R003, Status=Driver Assigned` | Ride → Driver Accepted | High |
| **TC-ACCEPT-004** | Tài xế chấp nhận chuyến | Chấp nhận Assignment hợp lệ | Assignment tồn tại, chưa được chấp nhận | Gửi request Accept | `ASG=ASG004` | Ghi nhận thời điểm và trạng thái chấp nhận | High |
| **TC-ACCEPT-005** | Tài xế chấp nhận chuyến | Driver không thuộc Assignment | Driver khác với Driver được phân công | Gửi request Accept | `ASG=ASG005, Driver=D002` | Từ chối; không thay đổi trạng thái Ride | High |
| **TC-ACCEPT-006** | Tài xế chấp nhận chuyến | Chấp nhận chuyến đã hoàn thành | Ride đã Completed | Gửi request Accept | `Ride=R006` | Từ chối thao tác | High |
| **TC-ACCEPT-007** | Tài xế chấp nhận chuyến | Chấp nhận Assignment đã được chấp nhận | Assignment đã Accepted | Gửi lại request Accept | `ASG=ASG007` | Từ chối; không tạo dữ liệu trùng | High |
| **TC-ACCEPT-008** | Tài xế chấp nhận chuyến | Assignment không tồn tại | Không có Assignment tương ứng | Gửi request Accept | `ASG=ASG999` | Trả lỗi không tìm thấy Assignment | High |
| **TC-ACCEPT-009** | Tài xế chấp nhận chuyến | Assignment ID ở giới hạn tối thiểu | ID đạt độ dài tối thiểu theo API | Nhập ID → Submit | `ID min` | Xử lý thành công nếu ID hợp lệ | Medium |
| **TC-ACCEPT-010** | Tài xế chấp nhận chuyến | Assignment ID ở giới hạn tối đa | ID đạt độ dài tối đa theo API | Nhập ID → Submit | `ID max` | Xử lý đúng theo giới hạn | Medium |
| **TC-ACCEPT-011** | Tài xế chấp nhận chuyến | Chấp nhận tại thời điểm còn hiệu lực cuối | Assignment vẫn còn hiệu lực | Gửi Accept | `ASG=ASG011` | Accept thành công nếu còn trong thời gian hợp lệ | Medium |
| **TC-ACCEPT-012** | Tài xế chấp nhận chuyến | Chấp nhận đúng trạng thái chuyển tiếp | Ride=Driver Assigned | Gửi Accept → Kiểm tra trạng thái | `Status=Driver Assigned` | Ride chuyển đúng sang Driver Accepted | High |
| **TC-ACCEPT-013** | Tài xế chấp nhận chuyến | Không nhập Assignment ID | Driver đã đăng nhập | Gửi request thiếu ID | `Assignment=""` | Báo thiếu Assignment ID | High |
| **TC-ACCEPT-014** | Tài xế chấp nhận chuyến | Body rỗng | Driver đã đăng nhập | Gửi request body rỗng | `{}` | Request bị từ chối nếu body bắt buộc | Medium |
| **TC-ACCEPT-015** | Tài xế chấp nhận chuyến | Assignment ID là chuỗi rỗng | Driver hợp lệ | Gửi request | `Assignment=""` | Không thực hiện Accept | High |
| **TC-ACCEPT-016** | Tài xế chấp nhận chuyến | Không gửi Token | API yêu cầu đăng nhập | Gửi request không Authorization | `Authorization=""` | Trả 401 Unauthorized | High |
| **TC-ACCEPT-017** | Tài xế chấp nhận chuyến | Assignment ID chứa ký tự đặc biệt | API yêu cầu ID hợp lệ | Nhập ID → Submit | `ASG@#$` | Validation thất bại | High |
| **TC-ACCEPT-018** | Tài xế chấp nhận chuyến | Assignment ID sai kiểu dữ liệu | API yêu cầu ID dạng chuỗi | Gửi request | `123456` | Validation thất bại hoặc không tìm thấy | Medium |
| **TC-ACCEPT-019** | Tài xế chấp nhận chuyến | Assignment ID chứa khoảng trắng | Driver đã đăng nhập | Nhập ID có khoảng trắng → Submit | `" ASG001 "` | Từ chối hoặc xử lý theo quy tắc chuẩn hóa | Medium |
| **TC-ACCEPT-020** | Tài xế chấp nhận chuyến | Sử dụng HTTP Method sai | Endpoint yêu cầu POST | Gửi GET thay vì POST | `GET /assignments/ASG001/accept` | Trả lỗi Method Not Allowed | Medium |

<br>

# 7. Cập nhật trạng thái chuyến — RIDE

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-RIDE-001** | Cập nhật trạng thái chuyến | Cập nhật Driver Accepted → Arriving | Ride đang Driver Accepted | Gửi request cập nhật trạng thái | `R=R001, Status=Arriving` | Cập nhật thành công | High |
| **TC-RIDE-002** | Cập nhật trạng thái chuyến | Cập nhật Arriving → Picked Up | Ride đang Arriving | Gửi request | `R=R002, Status=Picked Up` | Ride → Picked Up | High |
| **TC-RIDE-003** | Cập nhật trạng thái chuyến | Cập nhật Picked Up → In Progress | Ride đang Picked Up | Gửi request | `R=R003, Status=In Progress` | Ride → In Progress | High |
| **TC-RIDE-004** | Cập nhật trạng thái chuyến | Cập nhật theo đúng luồng | Ride đang ở trạng thái hợp lệ | Thực hiện từng bước trạng thái | `Accepted → Arriving → Picked Up → In Progress` | Các trạng thái được cập nhật đúng thứ tự | High |
| **TC-RIDE-005** | Cập nhật trạng thái chuyến | Chuyển trạng thái ngược | Ride đang In Progress | Gửi trạng thái Arriving | `R=R005` | Từ chối cập nhật | High |
| **TC-RIDE-006** | Cập nhật trạng thái chuyến | Cập nhật Ride đã Completed | Ride đã Completed | Gửi request | `R=R006, Status=In Progress` | Không cho phép thay đổi | High |
| **TC-RIDE-007** | Cập nhật trạng thái chuyến | Bỏ qua trạng thái trung gian | Ride=Driver Accepted | Gửi trực tiếp In Progress | `R=R007` | Từ chối do sai luồng trạng thái | High |
| **TC-RIDE-008** | Cập nhật trạng thái chuyến | Ride không tồn tại | Không có Ride | Gửi request | `R=R999` | Trả lỗi không tìm thấy Ride | High |
| **TC-RIDE-009** | Cập nhật trạng thái chuyến | Chuyển trạng thái đầu tiên | Ride=Driver Assigned | Gửi request | `Status=Arriving` | Cập nhật thành công | High |
| **TC-RIDE-010** | Cập nhật trạng thái chuyến | Chuyển trạng thái cuối trước Complete | Ride=Picked Up | Gửi request | `Status=In Progress` | Cập nhật thành công | High |
| **TC-RIDE-011** | Cập nhật trạng thái chuyến | Chuyển sang Completed tại biên | Ride=In Progress | Gửi request Completed | `Status=Completed` | Xử lý theo rule; nếu Complete dùng API riêng thì từ chối | High |
| **TC-RIDE-012** | Cập nhật trạng thái chuyến | Ride ID ở giới hạn hợp lệ | ID đúng min/max | Gửi request | `ID min/max` | Xử lý đúng theo API | Medium |
| **TC-RIDE-013** | Cập nhật trạng thái chuyến | Không nhập Ride ID | Driver đã đăng nhập | Gửi request thiếu ID | `ID=""` | Báo thiếu Ride ID | High |
| **TC-RIDE-014** | Cập nhật trạng thái chuyến | Không nhập Status | Ride tồn tại | Gửi body rỗng | `{}` | Báo thiếu Status | High |
| **TC-RIDE-015** | Cập nhật trạng thái chuyến | Status là chuỗi rỗng | Ride tồn tại | Gửi request | `Status=""` | Validation thất bại | High |
| **TC-RIDE-016** | Cập nhật trạng thái chuyến | Body rỗng | Ride tồn tại | Gửi `{}` | Empty body | Không cập nhật Ride | High |
| **TC-RIDE-017** | Cập nhật trạng thái chuyến | Status không tồn tại | Ride tồn tại | Gửi request | `Status=ABC` | Từ chối giá trị Status | High |
| **TC-RIDE-018** | Cập nhật trạng thái chuyến | Status sai kiểu dữ liệu | Ride tồn tại | Gửi request | `Status=123` | Validation thất bại | High |
| **TC-RIDE-019** | Cập nhật trạng thái chuyến | Ride ID chứa ký tự đặc biệt | API yêu cầu ID chuẩn | Gửi request | `RIDE@#` | Từ chối request | Medium |
| **TC-RIDE-020** | Cập nhật trạng thái chuyến | Status sai định dạng chữ | API quy định enum | Gửi request | `in progress` | Validation thất bại | Medium |

<br>

# 8. Hoàn thành chuyến — COMPLETE

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-COMPLETE-001** | Hoàn thành chuyến | Hoàn thành Ride đang In Progress | Ride=In Progress | Gửi request Complete | `R=R001` | Ride → Completed | High |
| **TC-COMPLETE-002** | Hoàn thành chuyến | Driver hoàn thành chuyến của mình | Driver được phân công | Driver đăng nhập → Complete | `D=D002, R=R002` | Hoàn thành thành công | High |
| **TC-COMPLETE-003** | Hoàn thành chuyến | Hoàn thành sau khi đón khách | Ride đã Picked Up và In Progress | Gửi Complete | `R=R003` | Ride → Completed | High |
| **TC-COMPLETE-004** | Hoàn thành chuyến | Lưu thời gian hoàn thành | Ride đang In Progress | Complete → Kiểm tra dữ liệu | `R=R004` | Lưu thời gian hoàn thành | Medium |
| **TC-COMPLETE-005** | Hoàn thành chuyến | Hoàn thành Ride chưa bắt đầu | Ride=Driver Accepted | Gửi Complete | `R=R005` | Từ chối thao tác | High |
| **TC-COMPLETE-006** | Hoàn thành chuyến | Hoàn thành Ride đã Completed | Ride đã Completed | Gửi lại Complete | `R=R006` | Không tạo lần hoàn thành thứ hai | High |
| **TC-COMPLETE-007** | Hoàn thành chuyến | Driver không thuộc Ride | Driver khác người được phân công | Gửi Complete | `D=D999, R=R007` | Từ chối quyền | High |
| **TC-COMPLETE-008** | Hoàn thành chuyến | Ride không tồn tại | Không có Ride | Gửi Complete | `R=R999` | Trả lỗi không tìm thấy | High |
| **TC-COMPLETE-009** | Hoàn thành chuyến | Complete ngay khi Ride In Progress | Ride vừa chuyển In Progress | Gửi Complete | `R=R009` | Hoàn thành thành công | High |
| **TC-COMPLETE-010** | Hoàn thành chuyến | Thời gian chuyến ở mức tối thiểu | Ride có thời gian hợp lệ | Complete | `Duration=min` | Xử lý đúng theo Business Rule | Medium |
| **TC-COMPLETE-011** | Hoàn thành chuyến | Fare ở giá trị nhỏ nhất | Ride có fare hợp lệ | Complete → Kiểm tra fare | `Fare=min` | Ride hoàn thành, fare không bị thay đổi | Medium |
| **TC-COMPLETE-012** | Hoàn thành chuyến | Ride ID ở giới hạn | ID min/max | Gửi Complete | `ID min/max` | Xử lý đúng theo API | Medium |
| **TC-COMPLETE-013** | Hoàn thành chuyến | Không nhập Ride ID | Driver đã đăng nhập | Gửi request thiếu ID | `ID=""` | Báo thiếu Ride ID | High |
| **TC-COMPLETE-014** | Hoàn thành chuyến | Body rỗng | API không cần dữ liệu bổ sung | Gửi `{}` | Empty body | Xử lý theo API; không phát sinh dữ liệu sai | Medium |
| **TC-COMPLETE-015** | Hoàn thành chuyến | Ride ID rỗng | Driver hợp lệ | Gửi request | `ID=""` | Từ chối request | High |
| **TC-COMPLETE-016** | Hoàn thành chuyến | Không có Authorization | API yêu cầu đăng nhập | Gửi request không token | `Authorization=""` | 401 Unauthorized | High |
| **TC-COMPLETE-017** | Hoàn thành chuyến | Ride ID chứa ký tự đặc biệt | API yêu cầu ID chuẩn | Gửi request | `RIDE@123` | Validation thất bại | High |
| **TC-COMPLETE-018** | Hoàn thành chuyến | Ride ID sai kiểu dữ liệu | API yêu cầu string | Gửi request | `{"id":"R001"}` | Validation thất bại | Medium |
| **TC-COMPLETE-019** | Hoàn thành chuyến | Ride ID có khoảng trắng | ID không chuẩn | Gửi request | `" R001 "` | Không xử lý sai ID | Medium |
| **TC-COMPLETE-020** | Hoàn thành chuyến | Dùng HTTP Method sai | Endpoint yêu cầu POST | Gửi GET | `GET /rides/R001/complete` | Trả lỗi Method Not Allowed | Medium |

<br>

# 9. Tính cước — FARE

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-FARE-001** | Tính cước | Tính cước Ride hợp lệ | Ride đã Completed | Nhập dữ liệu → Tính cước | `Distance=10km` | Tính đúng tổng tiền theo công thức | High |
| **TC-FARE-002** | Tính cước | Tính cước với khoảng cách khác | Ride Completed | Nhập Distance → Submit | `Distance=20km` | Tổng tiền được tính chính xác | High |
| **TC-FARE-003** | Tính cước | Tính cước có phụ phí | Ride Completed | Nhập fare + surcharge | `Base=100000, Surcharge=20000` | Total=120000 | High |
| **TC-FARE-004** | Tính cước | Lưu cước vào Ride | Ride Completed | Tính cước → Kiểm tra DB | `R=R004` | Fare được lưu đúng | High |
| **TC-FARE-005** | Tính cước | Tính cước Ride chưa Completed | Ride=In Progress | Gửi request | `R=R005` | Từ chối theo nghiệp vụ | High |
| **TC-FARE-006** | Tính cước | Khoảng cách âm | Ride Completed | Gửi Distance | `Distance=-5` | Validation thất bại | High |
| **TC-FARE-007** | Tính cước | Fare âm | Ride Completed | Gửi Fare âm | `Fare=-10000` | Không chấp nhận giá trị âm | High |
| **TC-FARE-008** | Tính cước | Ride không tồn tại | Không có Ride | Gửi request | `R=R999` | Trả lỗi không tìm thấy | High |
| **TC-FARE-009** | Tính cước | Distance bằng 0 | API cho phép giá trị 0 | Gửi request | `Distance=0` | Xử lý theo Business Rule | Medium |
| **TC-FARE-010** | Tính cước | Distance nhỏ nhất hợp lệ | Ride Completed | Nhập Distance min | `Distance=min` | Tính cước đúng | Medium |
| **TC-FARE-011** | Tính cước | Distance lớn nhất hợp lệ | Có giới hạn Distance | Nhập Distance max | `Distance=max` | Xử lý đúng giới hạn | Medium |
| **TC-FARE-012** | Tính cước | Fare ở giá trị tối đa | Có giới hạn Fare | Nhập Fare max | `Fare=max` | Không overflow; xử lý đúng | Medium |
| **TC-FARE-013** | Tính cước | Không nhập Ride ID | API yêu cầu ID | Gửi request | `ID=""` | Báo thiếu Ride ID | High |
| **TC-FARE-014** | Tính cước | Không nhập Distance | Ride Completed | Gửi body thiếu Distance | `{}` | Báo thiếu Distance | High |
| **TC-FARE-015** | Tính cước | Distance rỗng | Ride Completed | Gửi request | `Distance=""` | Validation thất bại | High |
| **TC-FARE-016** | Tính cước | Body rỗng | Ride Completed | Gửi `{}` | Empty body | Không tính cước | High |
| **TC-FARE-017** | Tính cước | Distance là chữ | Ride Completed | Gửi request | `"10km"` | Validation thất bại | High |
| **TC-FARE-018** | Tính cước | Fare là chuỗi | Ride Completed | Gửi request | `"150000"` | Từ chối nếu yêu cầu number | High |
| **TC-FARE-019** | Tính cước | Distance chứa ký tự đặc biệt | Ride Completed | Gửi request | `10@km` | Validation thất bại | Medium |
| **TC-FARE-020** | Tính cước | Ride ID sai định dạng | Ride tồn tại | Gửi request | `RIDE@#` | Validation thất bại | High |

<br>

# 10. Thanh toán — PAY

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-PAY-001** | Thanh toán | Thanh toán bằng tiền mặt | Ride đã có Fare | Chọn Cash → Submit | `R=R001, Method=Cash, Amount=150000` | Thanh toán thành công; Payment → Paid | High |
| **TC-PAY-002** | Thanh toán | Thanh toán e-payment mô phỏng | Ride có Fare | Chọn E-payment → Submit | `Method=E_PAYMENT` | Thanh toán mô phỏng thành công | High |
| **TC-PAY-003** | Thanh toán | Thanh toán đúng số tiền | Fare=200000 | Nhập Amount → Submit | `Amount=200000` | Payment thành công | High |
| **TC-PAY-004** | Thanh toán | Lưu Payment vào hệ thống | Payment hợp lệ | Thanh toán → Kiểm tra DB | `R=R004` | Payment được lưu và liên kết đúng Ride | High |
| **TC-PAY-005** | Thanh toán | Thanh toán thiếu tiền | Fare=150000 | Nhập Amount thấp hơn | `Amount=100000` | Thanh toán bị từ chối | High |
| **TC-PAY-006** | Thanh toán | Thanh toán Ride chưa có Fare | Ride chưa tính cước | Gửi Payment | `R=R006` | Không cho thanh toán | High |
| **TC-PAY-007** | Thanh toán | Thanh toán Ride đã Paid | Payment đã thành công | Gửi Payment lần 2 | `R=R007` | Không tạo Payment trùng | High |
| **TC-PAY-008** | Thanh toán | Ride không tồn tại | Không có Ride | Gửi Payment | `R=R999` | Trả lỗi không tìm thấy | High |
| **TC-PAY-009** | Thanh toán | Amount bằng đúng Fare | Fare=150000 | Gửi Amount | `Amount=150000` | Thanh toán thành công | High |
| **TC-PAY-010** | Thanh toán | Amount thấp hơn Fare 1 đơn vị | Fare=150000 | Gửi Amount | `Amount=149999` | Từ chối thanh toán | High |
| **TC-PAY-011** | Thanh toán | Amount cao hơn Fare 1 đơn vị | Fare=150000 | Gửi Amount | `Amount=150001` | Xử lý theo quy tắc tiền thừa | Medium |
| **TC-PAY-012** | Thanh toán | Amount bằng 0 | Ride có Fare | Gửi Amount=0 | `Amount=0` | Từ chối nếu Amount phải >0 | High |
| **TC-PAY-013** | Thanh toán | Không nhập Ride ID | API yêu cầu Ride ID | Gửi request | `RideID=""` | Validation thất bại | High |
| **TC-PAY-014** | Thanh toán | Không nhập Payment Method | Ride có Fare | Gửi request | `Method=""` | Báo thiếu phương thức thanh toán | High |
| **TC-PAY-015** | Thanh toán | Không nhập Amount | Ride có Fare | Gửi request | `Amount=""` | Validation thất bại | High |
| **TC-PAY-016** | Thanh toán | Body rỗng | API nhận JSON | Gửi `{}` | Empty body | Không tạo Payment | High |
| **TC-PAY-017** | Thanh toán | Amount là chữ | Ride có Fare | Gửi request | `"150000 VND"` | Validation thất bại | High |
| **TC-PAY-018** | Thanh toán | Payment Method không hợp lệ | Ride có Fare | Gửi request | `Bitcoin` | Từ chối phương thức không hỗ trợ | High |
| **TC-PAY-019** | Thanh toán | Amount âm | Ride có Fare | Gửi request | `Amount=-150000` | Từ chối | High |
| **TC-PAY-020** | Thanh toán | Ride ID sai định dạng | Ride tồn tại | Gửi request | `RIDE@123` | Validation thất bại | High |

<br>

# 11. Xem lịch sử chuyến — HISTORY

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-HISTORY-001** | Xem lịch sử chuyến | Customer xem lịch sử của mình | Customer đã đăng nhập | Gọi API History | `Customer=C001` | Trả danh sách Ride của Customer | High |
| **TC-HISTORY-002** | Xem lịch sử chuyến | Customer có nhiều chuyến | Customer có nhiều Ride | Gọi API → Kiểm tra danh sách | `C001, 5 Ride` | Trả đúng các Ride thuộc Customer | High |
| **TC-HISTORY-003** | Xem lịch sử chuyến | Xem chuyến đã Completed | Có Ride Completed | Gọi API | `C003` | Hiển thị Ride Completed | High |
| **TC-HISTORY-004** | Xem lịch sử chuyến | Xem lịch sử có phân trang | Customer có nhiều Ride | Gửi page + limit | `page=1, limit=10` | Trả đúng dữ liệu phân trang | Medium |
| **TC-HISTORY-005** | Xem lịch sử chuyến | Xem lịch sử của Customer khác | Customer đã đăng nhập | Truyền ID Customer khác | `C002` | Không trả dữ liệu trái quyền | High |
| **TC-HISTORY-006** | Xem lịch sử chuyến | Token không hợp lệ | API yêu cầu authentication | Gửi token giả | `Bearer=abc123` | 401 Unauthorized | High |
| **TC-HISTORY-007** | Xem lịch sử chuyến | User không có quyền | Role không được phép | Gọi API | `Role=InvalidRole` | Từ chối truy cập | High |
| **TC-HISTORY-008** | Xem lịch sử chuyến | Page vượt dữ liệu | Có ít trang dữ liệu | Gửi page lớn | `page=999` | Trả danh sách rỗng hoặc pagination hợp lệ | Medium |
| **TC-HISTORY-009** | Xem lịch sử chuyến | Page nhỏ nhất | API sử dụng page bắt đầu từ 1 | Gửi request | `page=1` | Trả trang đầu tiên | High |
| **TC-HISTORY-010** | Xem lịch sử chuyến | Limit nhỏ nhất | API cho phép limit=1 | Gửi request | `limit=1` | Trả tối đa 1 Ride | Medium |
| **TC-HISTORY-011** | Xem lịch sử chuyến | Limit lớn nhất | API có max limit | Gửi request | `limit=max` | Không vượt quá giới hạn | Medium |
| **TC-HISTORY-012** | Xem lịch sử chuyến | Page cuối cùng | Có nhiều trang | Gửi page cuối | `page=last` | Trả dữ liệu trang cuối | Medium |
| **TC-HISTORY-013** | Xem lịch sử chuyến | Customer chưa có lịch sử | Customer chưa đặt xe | Gọi API | `C013` | Trả danh sách rỗng | Medium |
| **TC-HISTORY-014** | Xem lịch sử chuyến | Không truyền filter | Customer đã đăng nhập | Gọi API không query | Không có filter | Trả toàn bộ lịch sử được phép | High |
| **TC-HISTORY-015** | Xem lịch sử chuyến | Page để rỗng | API hỗ trợ pagination | Gửi page= | `page=""` | Dùng giá trị mặc định hoặc báo lỗi theo API | Medium |
| **TC-HISTORY-016** | Xem lịch sử chuyến | Limit để rỗng | API hỗ trợ pagination | Gửi limit= | `limit=""` | Dùng mặc định hoặc báo lỗi | Medium |
| **TC-HISTORY-017** | Xem lịch sử chuyến | Page là chữ | API yêu cầu integer | Gửi request | `page=abc` | Validation thất bại | Medium |
| **TC-HISTORY-018** | Xem lịch sử chuyến | Limit là chữ | API yêu cầu integer | Gửi request | `limit=abc` | Validation thất bại | Medium |
| **TC-HISTORY-019** | Xem lịch sử chuyến | Page âm | Page phải >0 | Gửi request | `page=-1` | Từ chối giá trị không hợp lệ | High |
| **TC-HISTORY-020** | Xem lịch sử chuyến | Limit là số thập phân | Limit yêu cầu integer | Gửi request | `limit=1.5` | Validation thất bại | Medium |

<br>

# 12. Đánh giá chuyến xe — RATING

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-RATING-001** | Đánh giá chuyến xe | Customer đánh giá 5 sao | Ride đã Completed | Chọn 5 sao → Submit | `R=R001, Rating=5` | Đánh giá thành công | High |
| **TC-RATING-002** | Đánh giá chuyến xe | Customer đánh giá 1 sao | Ride đã Completed | Chọn 1 sao → Submit | `R=R002, Rating=1` | Đánh giá được ghi nhận | High |
| **TC-RATING-003** | Đánh giá chuyến xe | Đánh giá kèm nhận xét | Ride Completed | Nhập sao + comment → Submit | `Rating=5, Comment=Tài xế phục vụ tốt` | Lưu Rating và Comment | Medium |
| **TC-RATING-004** | Đánh giá chuyến xe | Customer đánh giá chuyến của mình | Customer sở hữu Ride | Login → Chọn Ride → Rating | `C=C001, R=R004` | Rating được lưu đúng Customer | High |
| **TC-RATING-005** | Đánh giá chuyến xe | Đánh giá Ride chưa Completed | Ride đang In Progress | Gửi Rating | `R=R005, Rating=5` | Từ chối đánh giá | High |
| **TC-RATING-006** | Đánh giá chuyến xe | Đánh giá Ride của Customer khác | Ride không thuộc Customer | Gửi Rating | `C=C002, R=R006` | Từ chối quyền | High |
| **TC-RATING-007** | Đánh giá chuyến xe | Đánh giá chuyến đã được đánh giá | Ride đã có Rating | Gửi Rating lần 2 | `R=R007` | Không tạo Rating trùng hoặc xử lý theo Business Rule | High |
| **TC-RATING-008** | Đánh giá chuyến xe | Ride không tồn tại | Không có Ride | Gửi Rating | `R=R999` | Trả lỗi không tìm thấy Ride | High |
| **TC-RATING-009** | Đánh giá chuyến xe | Rating nhỏ nhất | Ride Completed | Chọn 1 → Submit | `Rating=1` | Chấp nhận nếu thang điểm 1–5 | High |
| **TC-RATING-010** | Đánh giá chuyến xe | Rating lớn nhất | Ride Completed | Chọn 5 → Submit | `Rating=5` | Chấp nhận | High |
| **TC-RATING-011** | Đánh giá chuyến xe | Comment ở độ dài tối thiểu | API có quy định min length | Nhập comment min → Submit | `Comment=min` | Chấp nhận nếu hợp lệ | Medium |
| **TC-RATING-012** | Đánh giá chuyến xe | Comment ở độ dài tối đa | API có quy định max length | Nhập comment max → Submit | `Comment=max` | Chấp nhận nếu hợp lệ | Medium |
| **TC-RATING-013** | Đánh giá chuyến xe | Không nhập Rating | Ride Completed | Gửi request thiếu Rating | `{}` | Báo thiếu Rating | High |
| **TC-RATING-014** | Đánh giá chuyến xe | Rating rỗng | Ride Completed | Gửi request | `Rating=""` | Validation thất bại | High |
| **TC-RATING-015** | Đánh giá chuyến xe | Comment để rỗng | Ride Completed | Nhập Rating → Để Comment rỗng → Submit | `Rating=5, Comment=""` | Cho phép nếu Comment không bắt buộc | Medium |
| **TC-RATING-016** | Đánh giá chuyến xe | Body rỗng | Ride Completed | Gửi `{}` | Empty body | Không tạo Rating | High |
| **TC-RATING-017** | Đánh giá chuyến xe | Rating là chữ | Ride Completed | Gửi request | `Rating=five` | Validation thất bại | High |
| **TC-RATING-018** | Đánh giá chuyến xe | Rating vượt mức cho phép | Ride Completed | Gửi Rating | `Rating=6` | Từ chối vì ngoài khoảng 1–5 | High |
| **TC-RATING-019** | Đánh giá chuyến xe | Rating là số thập phân | API yêu cầu integer | Gửi request | `Rating=4.5` | Validation thất bại | Medium |
| **TC-RATING-020** | Đánh giá chuyến xe | Comment chứa script | Ride Completed | Nhập comment → Submit | `<script>alert(1)</script>` | Hệ thống từ chối hoặc sanitize; không thực thi script | High |
