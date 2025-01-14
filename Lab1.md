## Báo cáo phân tích kiến trúc và ca sử dụng hệ thống "Payroll System"

### 1. Phân tích kiến trúc

 #### 1.1. Đề xuất kiến trúc

 - **Kiến trúc Client-server**
   - **Client:** Ứng dụng desktop cài trên máy của nhân viên, họ có thể nhập thông tin về timecard, đơn hàng, và thay đổi phương thức thanh toán.
   - **Server:** Chứa logic xử lý nghiệp vụ và quản lý cơ sở dữ liệu liên quan đến nhân viên, thời gian làm việc, thanh toán và báo cáo.

 - **Giải thích:**
   
   - Kiến trúc này cho phép phân chia rõ ràng giữa các thành phần xử lý trên client và server. Điều này tối ưu cho việc xử lý nhiều yêu cầu từ 5000 nhân viên trên toàn cầu.
     
 - **Package:**
   
   - Các package chính gồm:
     
    - Gói giao diện: Giao diện nhập liệu trên client.
    - Gói xử lý nghiệp vụ: Xử lý nghiệp vụ chính như tính toán lương, quản lý nhân viên.
    - Gói truy cập dữ liệu: Giao tiếp với cơ sở dữ liệu và hệ thống DB2.
    - Gói tích hợp: Tích hợp với DB2 Project Management Database.

 **Biểu đồ Package:**
 
![Diagram](https://www.planttext.com/api/plantuml/png/d9GnIyD068Rt_8gFJ3eKmT51IbkeOYaAiRWUQSWTffUGD4AHJWuE8kZWu5XB5o5OSCiX3f7-Z_i5_WNlMjeclOIctlgztyFxtht9B_kk1dtazyEUetd8l4Qs1Ve9P_TWOCwUgGtdQE2xZgF3hGRYh4JDv9D0ao0N6aJeAUnTdkulLVAO3Wg2kM8XQEFaZNP8yavJec6X_2BayPWQFcSFYdwevNYvuYo2Ll85RHjBWWSTpYQgeuOWcbZEZ2IYk3MRpaOYPx6dzKAf22a-wLacyhlbn1XHRBZ9I6NdnZNyS01r7aUUX7n0IsOErRXds9NpnRXKWCn6YGnP_QunaiZ481etzbJlDSvUwpWSS7P7VvuuUo6Dsc4HDxTfbSfnqOCVWHx8odJ5WDhw1YDTlnqX1T8ifItkgKCiAWasPuzaXztLc_ndT_q-sUqDnCgVN2_ga20uisbuq9TTlE7nX2fEbbOLJ3h4DiZQiuh9v550soucls62D8UOylFIDL6mgaMxyX_v1m00__y30000)

### 2. Cơ chế phân tích:

 #### 2.1 Cơ chế xác thực 
 
  - Mục đích: Đảm bảo rằng chỉ nhân viên hợp lệ mới có thể truy cập vào hệ thống.
  - Giải thích: Với khoảng 5000 nhân viên, hệ thống cần đảm bảo tính bảo mật. Mỗi nhân viên cần đăng nhập để truy cập các chức năng, đảm bảo rằng không ai khác có thể xem hoặc thay đổi thông tin của người khác.
 
 #### 2.2 Cơ chế phân quyền
 
  - Mục đích: Chỉ cho phép nhân viên chỉnh sửa thông tin của chính mình và Payroll Administrator quản lý toàn bộ thông tin.
  - Giải thích: Nhân viên chỉ có quyền nhập thông tin timecard và phương thức thanh toán của họ. Payroll Administrator có quyền cao hơn, quản lý việc thêm, xóa nhân viên và chạy các báo cáo quản lý.
 
 #### 2.3 Cơ chế tính lương
 
  - Mục đích: Tính toán chính xác lương của nhân viên theo phương thức trả lương của từng loại (hàng giờ, cố định, có hoa hồng).
  - Giải thích: Mỗi nhân viên có phương thức trả lương khác nhau, cần hệ thống tính toán lương theo số giờ làm việc, hoa hồng, và tính thêm lương làm ngoài giờ.
 
 #### 2.4 Cơ chế nhập và quản lý timecard
 
  - Mục đích: Nhân viên có thể nhập giờ làm việc và hệ thống ghi nhận chính xác số giờ để tính lương.
  - Giải thích: Hệ thống cần cho phép nhân viên ghi nhận thông tin về giờ làm việc từng ngày, và tính toán lương dựa trên những dữ liệu này.

 #### 2.5 Cơ chế báo cáo cho nhân viên
 
  - Mục đích: Nhân viên có thể truy vấn các thông tin như số giờ đã làm, lương nhận được, số dư ngày nghỉ phép.
  - Giải thích: Hệ thống cần cung cấp chức năng cho phép nhân viên xem được các thông tin cá nhân quan trọng liên quan đến công việc và lương của họ.
 
 #### 2.6 Cơ chế lựa chọn phương thức thanh toán
 
  - Mục đích: Cho phép nhân viên chọn phương thức thanh toán như séc, chuyển khoản ngân hàng, hoặc nhận trực tiếp tại văn phòng.
  - Giải thích: Phương thức thanh toán là quyền lựa chọn của nhân viên, và hệ thống phải hỗ trợ lưu và áp dụng đúng phương thức mỗi lần trả lương.
 
 #### 2.7 Cơ chế tự động thanh toán (Payment Scheduling)
 
  - Mục đích: Hệ thống tự động tính lương và trả lương cho nhân viên vào mỗi thứ 6 và ngày làm việc cuối cùng của tháng.
  - Giải thích: Để đảm bảo lương luôn được trả đúng hạn mà không cần can thiệp thủ công, hệ thống phải tự động hóa hoàn toàn quá trình thanh toán.
 
 #### 2.8 Cơ chế tích hợp với DB2 Project Management Database
 
  - Mục đích: Đọc dữ liệu từ cơ sở dữ liệu DB2 để tra cứu thông tin về các dự án và mã số dự án nhưng không làm thay đổi dữ liệu.
  - Giải thích: Vì Acme không muốn thay đổi hệ thống DB2 hiện có, nên việc tích hợp cần diễn ra một cách an toàn, chỉ đọc dữ liệu mà không làm thay đổi cấu trúc hoặc nội dung của cơ sở dữ liệu đó.

 ### Kết quả mong đợi:

 - Authentication & Authorization: Bảo mật dữ liệu, mỗi nhân viên chỉ có thể truy cập thông tin của chính họ, Payroll Admin có quyền quản lý cao nhất.
 - Tính toán lương: Xử lý các phương thức thanh toán khác nhau như trả theo giờ, lương cố định, và lương có hoa hồng.
 - Data Validation: Kiểm tra tính hợp lệ của dữ liệu nhập vào (thời gian làm việc, đơn hàng).
 - Payment Scheduling: Lên lịch tự động trả lương vào ngày quy định mà không cần can thiệp thủ công.
 - Legacy System Integration: Đảm bảo hệ thống mới có thể đọc dữ liệu từ DB2 mà không làm thay đổi cấu trúc dữ liệu của hệ thống cũ.

### 3. Phân tích ca sử dụng payment

 #### 3.1 Xác định các lớp phân tích cho ca sử dụng Payment

  Lớp NhânViên (Employee): Đại diện cho mỗi nhân viên trong hệ thống. Lớp này có nhiệm vụ lưu thông tin cơ bản như mã nhân viên, tên, phương thức thanh toán và loại nhân viên (trả lương theo giờ, trả lương cố định, có hoa hồng).

   **Thuộc tính:**
  
    - maNhanVien
    - tenNhanVien
    - phuongThucThanhToan
    - loaiNhanVien
     
  Lớp DịchVụThanhToán (PaymentService): Lớp chính chịu trách nhiệm xử lý việc tính toán và thực hiện thanh toán cho nhân viên. Lớp này sử dụng thông tin từ nhân viên và timecard để tính toán số tiền phải trả.

   **Thuộc tính:**
   
     - ngayThanhToan  
     
   **Phương thức:**
   
     - tinhToanLuong(nhanVien)
     - thucHienThanhToan(nhanVien)

  Lớp KhoDuLieuThanhToán (PaymentRepository): Quản lý việc lưu trữ và truy vấn thông tin thanh toán từ cơ sở dữ liệu.
  
   **Phương thức:**
   
     - luuThongTinThanhToan(thongTinThanhToan)
     - layThongTinThanhToan(maNhanVien)

  Lớp Timecard: Đại diện cho thẻ thời gian mà nhân viên nhập liệu. Thẻ này chứa thông tin về số giờ làm việc và mã dự án tương ứng.
  
   **Thuộc tính:**
   
    - ngay
    - soGioLamViec
    - maDuAn
      
  Lớp KhoDuLieuNhanVien (EmployeeRepository): Lưu trữ và truy xuất thông tin nhân viên từ cơ sở dữ liệu, bao gồm phương thức thanh toán và thông tin cơ bản của nhân viên.
  
   **Phương thức:**
   
    - layThongTinNhanVien(maNhanVien)

 #### 3.2. Biểu đồ Sequence cho ca sử dụng Payment

 ![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3fTVnk55UM6PXrVbAUZQARWytDsTd17sSFVIa8p4l8oG_CCBynIi50pr52eFhofLI7wuQtcfGWb8Ig449CU5LGFG8E-CV9TIdypKKZ-WS5XcAiWK8ps5d8UxbbO23JYy9IzTeIGpJo4FPBr26SX-ZTn4c69DBapzk5rdhATGKlHmrsA5ieUx6t4OZjEX8PcvgSc9HIb0SqomkAy4AatOeoXECWKQTMn3AOf9H8GQKcHOAPW1lPNnSFV6P8MCp8Uxsr5Cq2Z8ACtFIm_9A4s6cf0833I7rBmKK9m20000__y30000)
 
 #### 3.3. Xác định nhiệm vụ của từng lớp phân tích
 
  - Lớp NhânViên: Gửi yêu cầu thanh toán và cung cấp thông tin cá nhân và phương thức thanh toán cho lớp dịch vụ thanh toán.
  
  - Lớp DịchVụThanhToán:
   - Nhận yêu cầu thanh toán từ nhân viên. 
   - Truy xuất thông tin nhân viên và timecard.  
   - Tính toán lương dựa trên số giờ làm việc, lương cố định, và hoa hồng (nếu có).  
   - Lưu thông tin thanh toán vào cơ sở dữ liệu.  
   - Thực hiện thanh toán theo phương thức được chỉ định.
  
  - Lớp KhoDữLiệuNhanVien: Cung cấp thông tin về nhân viên như phương thức thanh toán và loại nhân viên.
  
  - Lớp KhoDữLiệuThanhToán: Lưu thông tin về các khoản thanh toán đã thực hiện.
  
  - Lớp Timecard: Cung cấp thông tin về số giờ làm việc để tính toán lương.

 #### 3.4. Biểu đồ lớp (Class Diagram) mô tả các lớp phân tích

![Diagram](https://www.planttext.com/api/plantuml/png/Z58nJiGm4EppYYsF8X-WG8SK2IIYQuYkNpacjkJOAB6HqEbUm2j0ek4BAIZoadi1Ny2-62SNkw2TdTsTcTsVuNlRQ-oqQKL61FOzxDZu8VTy_99mo01oQ777q29KmZKywexBvenhAjE5PsQKR2fcI6Nhh5Au8WY5F6uzPbv1SHhU2DkVXa_VFxvFMW1aWw_BeGLgUYveFc6bMxsHVlYLfRmeNayKA-ZUWg4_fWK95MyfmQxs4RYryxOSUdN7LOcjRIOMVxA6jC-gCBSfJmzC5QRar0JVao7X_BYqU0XpCmVkXCttI4oB0XB6_CsRVUerSf7BGiBSSgaXgZifYqV9yviGsHfFNJDBdjYnevp-GLtCtL9PkrV-1G00__y30000)

### 4. Phân tích ca sử dụng Maintain Timecard
 
 #### 4.1 Xác định các lớp phân tích cho ca sử dụng Maintain Timecard
 
 ##### Dưới đây là các lớp phân tích chính trong ca sử dụng Maintain Timecard:

  Lớp NhânViên (Employee): Đại diện cho nhân viên nhập thông tin về giờ làm việc và mã dự án. Lớp này lưu trữ thông tin cá nhân và cung cấp quyền truy cập vào các timecard của nhân viên.
  
   Thuộc tính:
   
    - maNhanVien
    - tenNhanVien
    - danhSachTimecard

  Lớp Timecard: Chứa thông tin về số giờ làm việc và mã dự án của nhân viên. Timecard có thể được tạo mới, sửa đổi hoặc xóa bỏ bởi nhân viên.

   Thuộc tính:
   
    - ngay
    - soGioLamViec
    - maDuAn

  Lớp DịchVụTimecard (TimecardService): Chịu trách nhiệm xử lý các hoạt động liên quan đến timecard, bao gồm việc tạo mới, cập nhật hoặc xóa timecard. Lớp này quản lý logic nghiệp vụ khi nhân viên thay đổi thông tin giờ làm việc.

   Phương thức:
   
    - taoTimecard(nhanVien)
    - capNhatTimecard(timecard)
    - xoaTimecard(timecard)
     
  Lớp KhoDuLieuTimecard (TimecardRepository): Lưu trữ và truy vấn dữ liệu timecard từ cơ sở dữ liệu, hỗ trợ các thao tác thêm mới, cập nhật và xóa timecard.

   Phương thức:
   
    - luuTimecard(timecard)
    - layTimecard(maNhanVien)
    - xoaTimecard(timecard)

   #### 4.2. Biểu đồ Sequence cho ca sử dụng Maintain Timecard
   
   ##### Dưới đây là mô tả hành vi của hệ thống thông qua biểu đồ sequence cho việc duy trì timecard:

 ![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3fTVnk55UM6PXrVbAUZQARWytDsTd17sSFVIaCpSrEJ4eXG5AuNAmwjA5P8VxbfUgb3oSDV2V7qWUss1Gbu6a2fHA84gvCAY5sYYTqO-K6AzJ-R3tUsbI8Rc7DjGgf2H_t3NzcG5xEPXrudBaIL53tSjLYXxkBjH8VlXhlqb2eMb806mDK2vtUjnk0_9_pWDASaul20lGo7vy9QyTFqIe3ENbYWa0KCYayiXDIy558e00000__y30000)

   #### 4.3. Xác định nhiệm vụ của từng lớp phân tích
   
    Lớp NhânViên: Gửi yêu cầu tạo mới, cập nhật hoặc xóa timecard đến lớp dịch vụ.
    
    Lớp DịchVụTimecard:
     - Nhận yêu cầu từ nhân viên.
     - Xử lý logic nghiệp vụ liên quan đến việc tạo mới, cập nhật hoặc xóa timecard.
     - Gửi yêu cầu lưu trữ đến kho dữ liệu.
     - Thông báo kết quả lại cho nhân viên.
    
    Lớp KhoDữLiệuTimecard: Quản lý lưu trữ thông tin timecard và xử lý các yêu cầu liên quan đến truy vấn và cập nhật timecard trong cơ sở dữ liệu.
    
   #### 4.4. Biểu đồ lớp (Class Diagram) mô tả các lớp phân tích

   
   ![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bToJc9niO9Vnk55UM6PXrVbALHpAIZeAkGc-cKa0aLIynIi589BYZBpqi7Y9Qbvs2LI4lCoWXEJCq8oSrEJ4ujIWB8-cSKbDZ2-7LSj5zGok1A8LNdfYPL0rIw99QbWVd6-UsQ-Js8kq8vae7XQJdvY2THDBgMEIDR23NHvkBixEIFiuUwbA4OhA9GaviD4DFAWpjO46b2Mdva2Lf2SM03qJWbSKGcKWQAe8ZyHjmAu8xmpye7kME-J-N1tUocQEt9AI_5RaPDO2LU027fDp40anZr8aQchQmSFRdHnp53ZmXAG89LOlSRba9gN0af100000F__0m00)

   **Giải thích:**
   
    Quan hệ giữa các lớp:
    - NhânViên có một danh sách các Timecard và gửi yêu cầu tạo hoặc cập nhật timecard đến DịchVụTimecard.
    - DịchVụTimecard liên kết với KhoDữLiệuTimecard để thực hiện các thao tác lưu trữ hoặc xóa timecard.

    Nhiệm vụ của các lớp:
    - NhânViên thực hiện thao tác liên quan đến timecard.
    - DịchVụTimecard xử lý logic nghiệp vụ như tạo mới, cập nhật hoặc xóa timecard.
    - KhoDữLiệuTimecard thực hiện thao tác truy vấn và lưu trữ timecard trong cơ sở dữ liệu.
    
  ### 5. Hợp nhất kết quả phân tích

   #### 5.1 Tóm tắt các lớp phân tích chính
   
   ##### Các lớp phân tích được xác định qua hai ca sử dụng:

    NhânViên(Employee): Đại diện cho nhân viên với các thông tin cơ bản như mã nhân viên, tên, phương thức thanh toán, danh sách timecard.

    Timecard: Đại diện cho thông tin giờ làm việc của nhân viên, bao gồm ngày làm việc, số giờ làm việc và mã dự án.

    DịchVụThanhToán (PaymentService): Quản lý các hoạt động liên quan đến tính toán và thực hiện thanh toán lương cho nhân viên.

    DịchVụTimecard (TimecardService): Chịu trách nhiệm xử lý các hoạt động liên quan đến timecard như tạo mới, cập nhật hoặc xóa timecard.

    KhoDữLiệuNhânViên (EmployeeRepository): Quản lý lưu trữ và truy xuất thông tin nhân viên.

    KhoDữLiệuTimecard (TimecardRepository): Quản lý lưu trữ và truy vấn thông tin timecard.

    KhoDữLiệuThanhToán (PaymentRepository): Quản lý lưu trữ và truy vấn thông tin về thanh toán.

   #### 5.2 Mối quan hệ giữa các lớp
   
   ###### Qua hai ca sử dụng, chúng ta thấy rằng các lớp có mối quan hệ qua lại với nhau để hoàn thành các nhiệm vụ khác nhau trong hệ thống:
    
    Lớp NhânViên liên kết với Timecard để quản lý thông tin giờ làm việc của nhân viên.
    
    DịchVụTimecard và DịchVụThanhToán sử dụng thông tin từ các lớp KhoDữLiệuTimecard và KhoDữLiệuNhânViên để truy xuất thông tin cần thiết cho các thao tác.
    
    DịchVụThanhToán cũng liên kết với KhoDữLiệuThanhToán để lưu và quản lý thông tin thanh toán.
    
   #### 5.3 Biểu đồ lớp hợp nhất
   
   ##### Biểu đồ lớp dưới đây hợp nhất các lớp từ hai ca sử dụng và thể hiện mối quan hệ giữa chúng:

   ![Diagram](https://www.planttext.com/api/plantuml/png/d5InJiCm4Dtp5HxBa1z0g2fI9928kZJgVd92RIcngyH6L8YPWQy0YOM53yZ0q2_95_0Bd9lKJM8tGxVuxjszz-vE-Qj_5vM2KkaY3sWELKMMRFyfrdp_BSXBG4X82bWom4Wco3LPgPABpI6kCk5FR9cMOfCmJHFCiqJ2291BuFxI5F4he2pXHKQXJ34RyqhT7D_pu3NeT5f8gr9iO8Ve25HsU5VoZiiO2kIW67z4JjNPYVHjZzOsZ9hwdR9rKtzrilSVxGW8KRor4HjZCz59ly8cJvAdBGJjtcFGMdPXFgQ-2Mm2yXZnir3Ouk2K1QdkOm1wbd0UO4KyC8awVcBUr6zwj7H2SjWbp6oHsoNFJeTWkfrAplGSUSkrdfPjA8-08TNe12xqw6pLAEeydhQcnX57erCo5ElaZPpUVCDmRczt77SFOm9XxGIUUp9OxpO2xvcxS6_tYOBUEImoaPh_oJy0003__mC0)
   #### 5.4. Hợp nhất luồng hoạt động
   
   Khi hợp nhất hai ca sử dụng, hệ thống có thể hoạt động theo luồng sau:

   **Maintain Timecard:**

    - Nhân viên nhập hoặc cập nhật thông tin timecard.
    - Thông tin này được gửi đến lớp DịchVụTimecard để xử lý nghiệp vụ.
    - DịchVụTimecard tương tác với KhoDữLiệuTimecard để lưu hoặc cập nhật timecard.
   
   **Payment:**

    - Vào ngày trả lương, hệ thống sẽ tự động kích hoạt chức năng thanh toán.
    
    - DịchVụThanhToán truy xuất thông tin nhân viên và timecard từ KhoDữLiệuNhânViên và KhoDữLiệuTimecard để tính toán số tiền cần trả.
    
    - DịchVụThanhToán thực hiện thanh toán và lưu thông tin vào KhoDữLiệuThanhToán.

   #### 5.5 Tài liệu mô tả
   
   **Qua quá trình phân tích và hợp nhất, hệ thống quản lý payroll của Acme Inc. sẽ bao gồm các chức năng:**

   - Quản lý thông tin nhân viên: Lưu trữ thông tin nhân viên, phương thức thanh toán, và quản lý timecard.
     
   - Duy trì timecard: Cho phép nhân viên tạo, cập nhật hoặc xóa thông tin timecard.
     
   - Thanh toán: Tự động tính toán lương và thực hiện thanh toán dựa trên thông tin nhân viên và timecard.
