 # <div align="center"><p> Sql_injection </p></div>
 ## Họ và tên: Mai Thị Hoàng Yến
 ## Ngày báo cáo: Ngày 31/3/2022
 ### MỤC LỤC
 1. [Cài đặt xampp, mysql. Tìm hiểu về database: information_schema](#gioithieu)

       1.1 [Cài đặt xampp](#kn)
      
       1.2 [Cài đặt mysql](#dn)
 
       1.3 [Khái niệm](#kn)
      
       1.4 [Các table trong INFORMATION_SCHEMA](#dn)
      
       1.5 [Các câu lệnh trong INFORMATION_SCHEMA](#upl)
      
 2. [Thực hành lab](#dangnhap)
 3. [Tìm hiểu sqli là gì, Xảy ra khi nào, Tác hại, Khắc phục, Dẫn chứng, Code mẫu](#dangki)
 
       3.1 [Khái niệm](#kn)
      
       3.2 [Xảy ra khi nào](#dn)
      
       3.3 [Tác hại](#upl)
       
       3.4 [Khắc phục](#dow)
      
       3.5 [Dẫn chứng và code mẫu](#se)
          
 4. [Cách nhúng sql vào php](#dangxuat)
 
### Nội dung báo cáo 
#### 1. Cài đặt xampp, mysql. Tìm hiểu về database: information_schema <a name="gioithieu"></a>
 <br> 1.1 Cài đặt xampp <a name="kn"></a></br>
   
 <br> 1.2 Cài đặt mysql<a name="kn"></a></br>
 
 <br> 1.3 Khái niệm INFORMATION_SCHEMA<a name="kn"></a></br>
 
  - INFORMATION_SCHEMA là 1 database nằm bên trong 1 máy chủ MySQL, lưu thông tin về tất cả các database khác mà máy chủ MySQL đang lưu giữ. INFORMATION_SCHEMA chứa các table read-only. Chúng thực chất là các view, chứ không phải các table thực sự, do đó không có file nào liên kết với chúng, và chúng ta không thể đặt trigger lên các table này. Ngoài ra thì không có thư mục của database này trong máy chủ MySQL. Vì các table trong database này là read-only, nên chúng ta chỉ có thể sử dụng lệnh SELECT trên chúng, các lệnh INSERT, UPDATE và DELETE sẽ không chạy được trên database này.
      
 <br> 1.4 Các table trong INFORMATION_SCHEMA<a name="kn"></a></br>
 
 <table align="center">
   <tr>
        <td align="center" ><b>Tên table</b></td>
        <td align="center"><b>Nội dung</b></td>
        
   </tr>
   <tr>
        <td ><b>CHECK_CONSTRAINTS</b></td>
        <td ><b>Chi tiết liên quan đến từng ràng buộc CHECK</b></td>      
   </tr>
   <tr>
        <td ><b>COLUMN_DOMAIN_USAGE</b></td>
        <td ><b>Chi tiết liên quan đến các cột có kiểu dữ liệu bí danh</b></td>      
   </tr>
   <tr>
        <td><b>COLUMN_PRIVILEGES</b></td>
        <td><b>Đặc quyền cột do người dùng hiện tại cấp hoặc cấp</b></td>      
   </tr>
   <tr>
        <td><b>COLUMNS</b></td>
        <td><b>cột từ cơ sở dữ liệu hiện tại</b></td>      
   </tr>
   <tr>
        <td><b>CONSTRAINT_COLUMN_USAGE</b></td>
        <td><b>Chi tiết về các ràng buộc liên quan đến cột</b></td>      
   </tr>
  <tr>
        <td><b>CONSTRAINT_TABLE_USAGE</b></td>
        <td><b>Chi tiết về các ràng buộc liên quan đến bảng</b></td>      
   </tr>
 <tr>
        <td><b>DOMAIN_CONSTRAINTS</b></td>
        <td><b>Chi tiết liên quan đến các loại dữ liệu bí danh và các quy tắc liên quan đến chúng (người dùng này có thể truy cập được)</b></td>      
   </tr>
 <tr>
        <td><b>DOMAINS</b></td>
        <td><b>Chi tiết kiểu dữ liệu bí danh (người dùng này có thể truy cập)</b></td>      
   </tr>
 <tr>
        <td><b>KEY_COLUMN_USAGE</b></td>
        <td><b>Chi tiết được trả về nếu cột có liên quan đến khóa hay không</b></td>      
   </tr>
 <tr>
        <td><b>PARAMETERS</b></td>
        <td><b>Chi tiết liên quan đến từng tham số liên quan đến các chức năng và thủ tục do người dùng xác định mà người dùng này có thể truy cập</b></td>      
   </tr>
 <tr>
        <td><b>REFERENTIAL_CONSTRAINTS</b></td>
        <td><b>Chi tiết về khóa ngoại</b></td>      
   </tr>
 <tr>
        <td><b>ROUTINES</b></td>
        <td><b>Các chi tiết liên quan đến các quy trình (hàm & thủ tục) được lưu trữ trong cơ sở dữ liệu</b></td>      
   </tr>
 <tr>
        <td><b>ROUTINE_COLUMNS</b></td>
        <td><b>Một hàng cho mỗi cột được trả về bởi hàm giá trị bảng</b></td>      
   </tr>
 <tr>
        <td><b>SCHEMATA</b></td>
        <td><b>Chi tiết liên quan đến các lược đồ trong cơ sở dữ liệu hiện tại</b></td>      
   </tr>
 <tr>
        <td><b>TABLE_CONSTRAINTS</b></td>
        <td><b>Chi tiết liên quan đến các ràng buộc bảng trong cơ sở dữ liệu hiện tại</b></td>      
   </tr>
  <tr>
        <td><b>TABLE_PRIVILEGES</b></td>
        <td><b>Các đặc quyền được cấp bởi người dùng hiện tại</b></td>      
   </tr>
  <tr>
        <td><b>TABLES</b></td>
        <td><b>Các chi tiết liên quan đến bảng được lưu trữ trong cơ sở dữ liệu</b></td>      
   </tr>
  <tr>
        <td><b>VIEW_COLUMN_USAGE</b></td>
        <td><b>Chi tiết về các cột được sử dụng trong định nghĩa chế độ xem</b></td>      
   </tr>
  <tr>
        <td><b>VIEW_TABLE_USAGE</b></td>
        <td><b>Chi tiết về các bảng được sử dụng trong định nghĩa chế độ xem</b></td>      
   </tr>
  <tr>
        <td><b>VIEW</b></td>
        <td><b>Chi tiết liên quan đến các ràng buộc bảng trong cơ sở dữ liệu hiện tại</b></td>      
   </tr>
  <tr>
        <td><b>TABLE_CONSTRAINTS</b></td>
        <td><b>Chi tiết liên quan đến các chế độ xem được lưu trữ trong cơ sở dữ liệu</b></td>      
   </tr>
 </table>
 <br> 1.5 Các câu lệnh trong INFORMATION_SCHEMA<a name="kn"></a></br>
 
  - Để Hiển thị TABLESvà COLUMNStrong cơ sở dữ liệu hoặc tìm TABLESvà COLUMNS.Truy vấn đầu tiên này sẽ trả về tất cả các bảng trong cơ sở dữ liệu mà chúng ta đang truy vấn.

 `SELECT
  	TABLE_NAME
FROM
  	INFORMATION_SCHEMA.TABLES`
