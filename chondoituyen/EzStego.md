tải zip về và giải nén ra challenge.pdf  
check xem kiểu file bằng : file challenge.pdf  
thấy không có gì bất thường. <img width="994" height="102" alt="image" src="https://github.com/user-attachments/assets/eb6a348e-1399-4ec5-87b6-2d1b80f7e3f3" />  
kiểm tra xem có embedded files không (bằng pdfdetach -list) thấy có 2 files đính kèm  
<img width="979" height="159" alt="image" src="https://github.com/user-attachments/assets/89342170-b736-44e2-a71b-15707cb09b15" />  
extract 2 files bằng pdfdetach -saveall và kiểm tra nội dung  
<img width="992" height="443" alt="image" src="https://github.com/user-attachments/assets/708d9ebd-4d43-4191-bbe3-12cfb5e72ff8" />  
nội dung của secret.txt là "^" , ta nghĩ đến XOR (^ là kí hiệu XOR), nội dung file còn lại chưa khai thác được gì  
phân tích nội dung file pdf, chỉ là những kí tự S T L lặp đi lặp lại  
- S/T/L là cách viết lại của Whitespace language (một ngôn ngữ lập trình mà source code chỉ gồm 3 ký tự: space/tab/linefeed)
- S = Space (0x20)
T = Tab (0x09)
L = LineFeed (0x0A)
ta chuyển nội dung trong challenge.pdf thành whitespace, rồi chạy nó xem được gì  
ta dùng code python để chuyển:
[stl_to_hex.py](https://github.com/user-attachments/files/25169135/stl_to_hex.py)  
file này giúp ta
trích S/T/L từ PDF theo đúng thứ tự  
map S/T/L → whitespace (space/tab/newline) để ra source code whitespace  
chạy chương trình whitespace và ra được output là hex
<img width="1397" height="101" alt="image" src="https://github.com/user-attachments/assets/3ffc6a0b-63c9-4fed-a2c8-50a2636c72c8" />
XOR : dữ liệu gốc = key ^ dữ liệu bị mã hóa
mã hex ta vừa nhận được từ chạy chương trình whitespace là dữ liệu bị mã hóa
vậy key là gì? ta nhớ lại những gì bài cho mà mình chưa xài=)) có thể là manh mối.
embedded file you_cannot_read_this.txt có nội dung : just ######## this line you will have flag.
ta dùng nó làm key để xor với mã hex
độ dài bytes của cả 2 bằng nhau nên chắc rằng là chuẩn ròi...
chạy file python để xor  
[solve.py](https://github.com/user-attachments/files/25169432/solve.py)
oke ra lun flag: <img width="2559" height="102" alt="image" src="https://github.com/user-attachments/assets/c06ecfd6-a197-48b6-a8d6-66d775c92bb3" />
vậy flag là: InfosecPTIT{y0u_c4n_501v3_1t_345i1y_innit?}  






