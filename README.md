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
 
 <br> 1.5 Các câu lệnh trong INFORMATION_SCHEMA<a name="kn"></a></br>
