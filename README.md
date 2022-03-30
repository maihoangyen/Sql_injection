 # <div align="center"><p> Sql_injection </p></div>
 ## Họ và tên: Mai Thị Hoàng Yến
 ## Ngày báo cáo: Ngày 31/3/2022
 ### MỤC LỤC
 1. [Cài đặt xampp, mysql. Tìm hiểu về database: information_schema](#gioithieu)

       1.1 [Cài đặt xampp](#xap)
      
       1.2 [Cài đặt mysql](#my)
 
       1.3 [Khái niệm INFORMATION_SCHEMA](#kni)
      
       1.4 [Các table trong INFORMATION_SCHEMA](#tab)
      
       1.5 [Các câu lệnh trong INFORMATION_SCHEMA](#cc)
      
 2. [Thực hành lab](#tha)
 3. [Tìm hiểu sqli là gì, Xảy ra khi nào, Tác hại, Khắc phục, Dẫn chứng](#ths)
 
       3.1 [Khái niệm sqli](#kns)
      
       3.2 [Xảy ra khi nào](#xa)
      
       3.3 [Tác hại](#th)
       
       3.4 [Khắc phục](#kp)
      
       3.5 [Dẫn chứng](#dc)
          
 4. [Cách nhúng sql vào php](#ca)
 
### Nội dung báo cáo 
#### 1. Cài đặt xampp, mysql. Tìm hiểu về database: information_schema <a name="gioithieu"></a>
 <br> 1.1 Cài đặt xampp <a name="xap"></a></br>
   
 <br> 1.2 Cài đặt mysql<a name="my"></a></br>
 
 <br> 1.3 Khái niệm INFORMATION_SCHEMA<a name="kni"></a></br>
 
  - INFORMATION_SCHEMA là 1 database nằm bên trong 1 máy chủ MySQL, lưu thông tin về tất cả các database khác mà máy chủ MySQL đang lưu giữ. INFORMATION_SCHEMA chứa các table read-only. Chúng thực chất là các view, chứ không phải các table thực sự, do đó không có file nào liên kết với chúng, và chúng ta không thể đặt trigger lên các table này. Ngoài ra thì không có thư mục của database này trong máy chủ MySQL. Vì các table trong database này là read-only, nên chúng ta chỉ có thể sử dụng lệnh SELECT trên chúng, các lệnh INSERT, UPDATE và DELETE sẽ không chạy được trên database này.
      
 <br> 1.4 Các table trong INFORMATION_SCHEMA<a name="tab"></a></br>
 
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
 <br> 1.5 Các câu lệnh trong INFORMATION_SCHEMA<a name="cc"></a></br>
 
  - Để Hiển thị TABLESvà COLUMNS trong cơ sở dữ liệu hoặc tìm TABLES và COLUMNS.Truy vấn đầu tiên này sẽ trả về tất cả các bảng trong cơ sở dữ liệu mà chúng ta đang truy vấn.

    `SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES`
 
  - Truy vấn thứ hai sẽ trả về danh sách tất cả các cột và bảng trong cơ sở dữ liệu mà chúng ta đang truy vấn.
  
    `SELECT TABLE_NAME, COLUMN_NAME FROM INFORMATION_SCHEMA.COLUMNS` 
    
  - Hoặc, chúng ta cũng có thể chỉ truy vấn COLUMNS từ một bảng cụ thể và trả về tên cột từ bảng cụ thể 'Album' trong cơ sở dữ liệu.
  
    `SELECT COLUMN_NAME FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = 'Album'`
    
  - Tiếp theo, chúng ta có thể tìm xem có hay không TABLE nguồn dữ liệu khớp với một số loại tham số tìm kiếm.
  
    ` IF EXISTS( SELECT * FROM INFORMATION_SCHEMA.COLUMNS WHERE COLUMN_NAME = 'Title')
    SELECT 'found' AS search_result ELSE SELECT 'not found' AS search_result;`
    
  - Sử dụng INFORMATION_SCHEMA chế độ xem trong nguồn dữ liệu của chúng ta có thể là một cách đáng tin cậy để xác định những gì có trong nguồn dữ liệu trong khi chúng ta xây dựng các truy vấn của mình.
  
#### 2. Thực hành lab <a name="tha"></a>
#### 3. Tìm hiểu sqli là gì, Xảy ra khi nào, Tác hại, Khắc phục, Dẫn chứng. <a name="ths"></a>
 <br> 3.1 Khái niệm sqli <a name="kns"></a></br>
  - SQL injection là kĩ thuật cho phép các kẻ tấn công chèn và thực thi các lệnh SQL bất hợp pháp (mà người phát triển không lường trước được) bên trong hệ thống, bằng cách lợi dụng các lỗ hổng bảo mật từ dữ liệu nhập vào của các ứng dụng. Qua đó làm lộ thông tin trong cơ sở dữ liệu, tạo ra sự sai lệch hoặc gây ra hư hỏng dữ liệu của hệ thống.
Một cách nôm na, ta khả năng hiểu tấn công SQL injection là việc truyền vào các mã SQL thông qua các ô nhập liệu, để làm thay đổi ngay mục đích câu truy vấn ban đầu. Với định nghĩa trên, ta khả năng tạm chia SQL injection thành một vài loại chính sau đây dựa vào cách tấn công dữ liệu truyền vào:
    - Tấn công: không mã hóa kí tự nhập
    - Tấn công: không kiểm tra kiểu dữ liệu nhập

 <br> 3.2 Xảy ra khi nào <a name="xa"></a></br>
   - lỗi Sql injection thường xảy ra do hệ thống đã thiếu kiểm tra dữ liệu truyền vào. Điều này sẽ thay đổi ngay mục đích ban đầu của câu truy vấn và vì thế gây ra ra những tác động không mong muốn. 
   
 <br> 3.3 Tác hại <a name="th"></a></br>
  - Thông tin đăng nhập bị đánh cắp: Sử dụng SQL Injection để tìm kiếm thông tin đăng nhập người dùng. Sau đó, những kẻ tấn công có thể mạo danh người dùng, sử dụng và thay đổi các quyền hạn của người dùng sẵn có.
  - Truy cập cơ sở dữ liệu: Sử dụng SQL Injection để truy cập vào nguồn thông tin được lưu trữ trong máy chủ cơ sở dữ liệu. Điều này có thể gây ra những vấn đề nghiêm trọng cho các dữ liệu của toàn bộ hệ thống vận hành.
  - Xóa dữ liệu: Sử dụng SQL Injection để xóa các bản ghi của cơ sở dữ liệu, bao gồm cả drop tables, gây ra những sự thay đổi hoặc phá vỡ các cấu trúc của cơ sở dữ liệu.
  - Thay đổi dữ liệu: Sử dụng SQL Injection để chủ động thay đổi hoặc thêm dữ liệu mới vào cơ sở dữ liệu hiện tại, ảnh hưởng đến kết quả chiết xuất dữ liệu cuối cùng xảy ra những sai lệch.
  
 <br> 3.4 Khắc phục <a name="kp"></a></br>
 
  - Dọn dẹp: Bạn có thể sử dụng trình xác thực hoặc phần mềm làm sạch đầu vào, ứng dụng web chỉ chấp nhận một số đầu vào nhất định và từ chối những đầu vào không chấp nhận. Đây là phương pháp phổ biến, được người dùng sử dụng thường xuyên.

  - Lọc và xác thực: Để lọc SQL Injection và ngăn chặn các mối đe dọa tiềm ẩn, bạn có thể cài đặt tường lửa (WAF). WAF sẽ lọc các đầu vào trong danh sách và sử dụng các phương pháp xác thực riêng biệt để ngăn các truy vấn SQL Injection. Danh sách sẽ được kiểm tra và cập nhật thường xuyên để thích ứng với mọi hoàn cảnh của doanh nghiệp.

  - Giới hạn phạm vi của SQL Injection: Việc ngăn chặn hoàn toàn SQL Injection là rất khó thực hiện, tính khả thi không cao. Các chuyên gia trong lĩnh vực bảo mật sẽ phải thường xuyên kiểm tra để tối ưu hóa hiệu suất của phần mềm. WAF có thể xác minh chéo đầu vào với dữ liệu Giao thức Internet (IP) trước khi chặn yêu cầu.

  - Tránh các URL không an toàn: Nếu một trang web không sử dụng Giao thức truyền siêu văn bản an toàn (HTTPS) hoặc sử dụng Lớp cổng bảo mật an toàn (SSL) và Bảo mật lớp truyền tải (TLS) để mã hóa. Những kẻ tấn công có thể sử dụng các URL chứa các cookie SQL Injection để giành quyền truy cập vào cơ sở dữ liệu của bạn. 

  -  Điểm để tấn công chính là tham số truyền vào câu truy vấn. Do vậy, cần phải đảm bảo thực hiện việc kiểm tra dữ liệu truyền vào từ người dùng, để tránh người dùng nhập vào những nội dung khả năng gây ra ra sai lệch khi thực hiện truy vấn. Để kiểm tra dữ liệu từ người dùng, ta cần lọc bớt những nội dung nguy hiểm. Giải pháp cho việc lọc dữ liệu này là dùng chuỗi được escape (mã hóa). Lưu ý: mình sẽ dùng từ “escape” để chỉ việc mã hóa cho sát nghĩa.

  - Khi thực hiện escape một chuỗi, tức là mã hoá các kí tự đặc biệt của chuỗi (ví dụ như kí tự ‘, &, |, …) để nó không còn được hiểu là 1 kí tự đặc biệt nữa. Mỗi ngôn ngữ lập trình đều cung cấp các hàm để thực hiện escape chuỗi, trong `PHP` ta sẽ dùng hàm `mysqli_real_escape_string()` hoặc cũng khả năng dùng `addslashes()` để thực hiện điều này.

  - Các tổ chức có thể tập trung vào những bước sau đây để bảo vệ mình khỏi những cuộc tấn công SQL Injection:

   - Không bao giờ được tin tưởng những input người dùng nhập vào: Dữ liệu luôn phải được xác thực trước khi sử dụng trong các câu lệnh SQL.
   - Các thủ tục được lưu trữ: Những thủ tục này có thể trừu tượng hóa các lệnh SQL và xem xét toàn bộ input như các tham số. Nhờ đó, nó không thể gây ảnh hưởng đến cú pháp lệnh SQL.
   - Các lệnh được chuẩn bị sẵn: Điều này bao gồm việc tạo truy vấn SQL như hành động đầu tiên và sau đó xử lý toàn bộ dữ liệu được gửi như những tham số.
   - Những cụm từ thông dụng: Những cụm từ này được sử dụng để phát hiện mã độc và loại bỏ nó trước khi câu lệnh SQL được thực hiện.
   - Thông báo lỗi đúng: Thông báo lỗi phải tuyệt đối tránh tiết lộ những thông tin/chi tiết nhạy cảm và vị trí xảy ra lỗi trên thông báo lỗi.
   - Giới hạn quyền truy cập của người dùng đối với cơ sở dữ liệu: Chỉ những tài khoản có quyền truy cập theo yêu cầu mới được kết nối với cơ sở dữ liệu. Điều này có thể giúp giảm thiểu những lệnh SQL được thực thi tự động trên server.
   - Hãy loại bỏ các kí tự meta như ‘”/\; và các kí tự extend như NULL, CR, LF, … trong các string nhận được từ:
   
     >input do người dùng đệ trình
     
     >các tham số từ URL
     
     >các giá trị từ cookie
     
   - Đối với các giá trị numeric, hãy chuyển nó sang integer trước khi query SQL, hoặc dùng ISNUMERIC để chắc chắn nó là một số integer.
   - Thay đổi “Startup and run SQL Server” dùng mức low privilege user trong tab SQL Server Security.
   - Xóa các stored procedure trong database master mà không dùng như:
   
     >xp_cmdshell
     
     >xp_startmail
     
     >xp_sendmail
     
     >sp_makewebtask
     
<br> 3.5 Dẫn chứng <a name="dc"></a></br>

#### 4. Cách nhúng sql vào php <a name="ca"></a>

 - Một cách khả thi để lấy mật khẩu là phá vỡ các trang kết quả tìm kiếm của bạn. Điều duy nhất mà kẻ tấn công cần làm là xem liệu có bất kỳ biến đã gửi nào được sử dụng trong các câu lệnh SQL không được xử lý đúng cách hay không. Các bộ lọc này có thể được đặt thường ở dạng trước để tùy chỉnh WHERE, ORDER BY, LIMIT và OFFSET các mệnh đề trong SELECT câu lệnh. Nếu cơ sở dữ liệu của bạn hỗ trợ UNION cấu trúc, kẻ tấn công có thể cố gắng nối toàn bộ truy vấn vào truy vấn ban đầu để liệt kê mật khẩu từ một bảng tùy ý. Việc sử dụng các trường mật khẩu được mã hóa rất được khuyến khích.
     >Ví dụ: Liệt kê các bài viết ... và một số mật khẩu 
 
     ``<?php`
     
         $query  = "SELECT id, name, inserted, size FROM products
         
           WHERE size = '$size'";
           
         $result = odbc_exec($conn, $query);
         
      `?>``
 - SQL UPDATE cũng dễ bị tấn công. Những truy vấn này cũng bị đe dọa bằng cách cắt và thêm một truy vấn hoàn toàn mới vào nó. Nhưng kẻ tấn công có thể lúng túng với SET điều khoản. Trong trường hợp này, một số thông tin lược đồ phải được sở hữu để thao tác truy vấn thành công. Điều này có thể đạt được bằng cách kiểm tra các tên biến biểu mẫu, hoặc chỉ đơn giản là ép buộc thô bạo. Không có quá nhiều quy ước đặt tên cho các trường lưu trữ mật khẩu hoặc tên người dùng.
    >Ví dụ: Từ đặt lại mật khẩu ... đến nhận được nhiều đặc quyền hơn 
    
    `<?php
    
        $query = "UPDATE usertable SET pwd='$pwd' WHERE uid='$uid';";
        
    `?>
 - Nhưng nếu một người dùng độc hại gửi giá trị ' or uid like'%admin% cho $ uid để thay đổi mật khẩu của quản trị viên hoặc chỉ cần đặt $ pwd để hehehe', trusted=100, admin='yes có được nhiều đặc quyền hơn, thì truy vấn sẽ bị xoắn:
    >Ví dụ:  
      
    `<?php`
    
       // $uid: ' or uid like '%admin%
       
          $query = "UPDATE usertable SET pwd='...' WHERE uid='' or uid like '%admin%';";
          
      // $pwd: hehehe', trusted=100, admin='yes
      
         $query = "UPDATE usertable SET pwd='hehehe', trusted=100, admin='yes' WHERE...;";     
    `?>`
