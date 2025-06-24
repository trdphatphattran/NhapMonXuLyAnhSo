# THỰC HÀNH 3: BIẾN ĐỔI HÌNH HỌC  
## Thông tin:  
Sinh viên: Trần Đại Phát  
MSSV: 2374802010379  
Môn học: Nhập môn Xử lý ảnh số  
GVHD: Đỗ Hữu Quân  
Năm học: 2024 - 2025  
## Mục tiêu bài học  
- Viết được chương trình chọn đối tượng trong ảnh
- Viết được chương trình tịnh tiến ảnh
- Viết được chương trình thay đổi kích thước ảnh
- Viết được chương trình xoay ảnh
- Viết được chương trình biến đổi cực
## Giới thiệu  
Biến đổi hình học là sắp xếp lại vị trí các điểm ảnh. Có 2 phép biến đổi là tịnh tiến và xoay.  
## Phần 1: Viết chương trình biến đổi điểm ảnh    
### 1. Chọn đối tượng trong ảnh:  
Là phép trích ảnh nhỏ trong ảnh lớn ban đầu.  
#### Công thức cắt ảnh: [y1:y2, x1:x2]  
Trong đó:  
- x1: Cột bắt đầu (bên trái).  
- x2: Cột kết thúc (bên phải).  
- y1: Dòng bắt đầu (bên trên).  
- y2: Dòng kết thúc (bên dưới).  
Code chính:  
![image](https://github.com/user-attachments/assets/9a888dee-8529-43ca-8e9a-d6f5c6c4cd73)  
Giải thích:  
- 800:1200: Cắt từ dòng 800 đến 1199 theo chiều cao.
- 570:980: Cắt từ cột 570 đến 979 theo chiều dọc.

### 2. Tịnh tiến đơn  
Là di chuyển toàn bộ ảnh theo một hướng cố định.  
#### Công thức tịnh tiến:  
(x, y) --> (x', y') = (x + dx, y + dy)  
Trong đó:  
- x, y: Tọa độ điểm ban đầu.  
- x', y': Tọa độ điểm sau tịnh tiến.  
- dx: Tịnh tiến theo chiều ngang.  
- dy: Tịnh tiến theo chiều dọc.  
Code chính:  
![image](https://github.com/user-attachments/assets/54953ce4-6d16-446b-bb97-01fc49bc2603)  
Giải thích:  
- Dịch chuyển 100 pixel xuống dưới.
- Dịch chuyển 25 pixel sang phải.

### 3. Thay đổi kích thước ảnh  
Là tăng hoặc giảm không gian ảnh.  
#### Công thức:  
Kích thước mới = Kích thước cũ * Chỉ số zoom.  
Code chính:  
![image](https://github.com/user-attachments/assets/a5ee9104-60df-4cca-9da8-4218910b50bd)  
Giải thích:  
Cho ảnh gốc có giá trị data.shape = [height, width, channels].  
- bdata = nd.zoom(data, 2):  Zoom lên 2 lần ở tắt cả các chiều (kể cả màu).
- data2 = nd.zoom(data, (2, 2, 1)): Chiều cao và rộng nhân 2, màu giữ nguyên.
- data3 = nd.zoom(data, (0.5, 0.9, 1)): Chiều cao * 0.5, Chiều rộng * 0.9, màu giữ nguyên.

### 4. Xoay ảnh  
Là xoay toàn bộ ảnh sang một góc cố định.  
Công thức:  
rotate(image, degree)  
Trong đó:  
- image: ảnh trong bộ nhớ.
- degree: góc xoay.  
Code chính:  
![image](https://github.com/user-attachments/assets/8756ed1e-7cbe-4772-9989-3f40bc202363)  
Giải thích:  
- d1 = nd.rotate(data, 20): ảnh kết quả sẽ mở rộng đủ để chứa toàn bộ ảnh đã xoay.  
- d2 = nd.rotate(data, 20, reshape=False): ảnh kết quả giữ nguyên kích thước cũ, nên cắt mất góc.

### 5. Dilation và Erosion  
- Dùng để loại bỏ những pixel nhiễu.
- Dilation (giãn ảnh): thay thế pixel tọa độ (i, j) bằng giá trị lớn nhất của những pixel lân cận (kề).
- Erosion (co ảnh): thay thế pixel tọa độ (i, j) bằng giá trị nhỏ nhất của những pixel lân cận (kề).
Code chính:
![image](https://github.com/user-attachments/assets/da72e862-aace-41da-a56e-85917a17b0ea)  
Giải thích:  
- d1 = nd.binary_dilation(data): giãn ảnh với 1 lần lặp.  
- d2 = nd.binary_dilation (data, iterations=3): giãn ảnh lặp lại 3 lần.  
- e1 = nd.binary_erosion(data): co ảnh 1 lần.

### 6. Coordinate Mapping  
Cho phép tạo hàm mới do người dùng định nghĩa ngoài các hàm có sẵn như shifting, rotate.  
- Tạo 1 coordinate map chứa các pixel mới.   
- Dùng hàm map_coordinate để ánh xạ vị trí mới cho ảnh đầu vào.  
Code chính:  
![image](https://github.com/user-attachments/assets/c2cdcb8f-cbeb-43dd-a82e-cb163f0ad26a)  
Giải thích:  
- V: Chiều cao.
- H: Chiều rộng.
- M: Tạo 1 lưới tọa độ 2D tương ứng với kích thước ảnh.
- d: Mức độ nhiễu.
- q: Sinh ra một mảng q có cùng kích thước với M, chứa giá trị trong khoảng [-d; d].
- mp: Cộng M với q sẽ sinh ra lưới tọa độ mới.  

### 7. Biến đổi chung (Generic Transformation)  
Dùng khi ta muốn biến đổi các ảnh chung phép toán do người dùng định nghĩa.  
Công thức:  
I1 (y, x) = I2 (fy(y, x), fx(y, x)).  
Trong đó:  
- (y, x): Tọa độ điểm ban đầu.  
- fy(y, x): Hàm ánh xạ ngược theo trục Y.  
- fx(y, x): Hầm ánh xạ ngược theo trục X.  
- I2: giá trị điểm ảnh trong ảnh gốc.  
- I1: ảnh sau biến đổi.  
Code chính:  
![image](https://github.com/user-attachments/assets/3ee8dfa0-3a68-4ee4-948d-90964e357727)  
Giải thích:  
- fy(y, x): a = 10 * np.cos(outcoord[0]/10.0 + outcoord[0]).  
- fx(y, x): b = 10 * np.cos(outcoord[1]/10.0 + outcoord[1]).

## Phần 2: Bài tập  
### Bài 1:  
Trong bài này, viết chương trình chọn quả kiwi từ ảnh colorful-ripe-tropical-fruits.jpg trong thư mục exercise. Tinh tiến quả kiwi sang phải 30 pixels ta làm như sau:  
![image](https://github.com/user-attachments/assets/9e0a1538-66fb-41d7-a6b3-087714383f8e)  
- Tìm tọa độ quả kiwi trong ảnh gốc.
- (0, 30, 0): chiều cao không dịch, dịch sang phải 30 pixels, kênh màu không dịch.
- In ảnh mới ra màn hình.

### Bài 2:  
Trong bài này, viết chương trình chọn quả đu đủ và quả dưa hấu từ ảnh colorful-ripe-tropical-fruits.jpg trong thư mục exercise. Đổi màu hai đối tượng này ta làm như sau:  
![image](https://github.com/user-attachments/assets/755d07cc-ef41-411a-977d-d5659b1fd52a)  
- Tìm tọa độ quả đu đủ và dưa hấu trong ảnh gốc.
- [0.5, 0.5, 1.2], 0, 255: giảm đỏ và xanh lá xuống 50%, tăng xanh dương lên 120%.
- [1.2, 0.5, 1.2], 0, 255: tăng đỏ và xanh dương lên 120%, giảm xanh lá xuống 50%.
- astype(np.uint8): ép kiểu ảnh về dạng 8-bit.
- In 2 ảnh mới ra màn hình.

### Bài 3:  
Trong bài này, viết chương trình chọn ngọn núi và con thuyền từ ảnh quang_ninh.jpg trong thư mục exercise. Xoay 2 đối tượng này 1 góc 45 độ và lưu vào máy ta làm như sau:  
![image](https://github.com/user-attachments/assets/b46975ad-86e2-45e1-bce9-758469356a45)  
- Tìm tọa độ của núi và con tàu trong ảnh gốc.
- d1 = nd.rotate(bmg, 45): trả về ảnh núi đã xoay 45 độ.
- d2 = nd.rotate(bmg2, 45): trả về ảnh tàu đã xoay 45 độ.
- In 2 ảnh mới ra màn hình.

### Bài 4:  
Trong bài này, viết chương trình chọn ngôi chùa từ ảnh pagoda.jpg trong thư mục exercise. Tăng kích thước ngôi chùa lên 5 lần và lưu vào máy ta làm như sau:  
![image](https://github.com/user-attachments/assets/4cf4d51a-b21b-47e6-b883-91e26609f26a)  
- Tìm tọa độ ảnh 1 ngôi chùa bất kỳ trong ảnh gốc.
- bdata = nd.zoom(bmg, (5, 5, 1)): tăng chiều dài và rộng lên 5 lần, kênh màu giữ nguyên.
- In ảnh mới ra màn hình.

### Bài 5:  
Trong bài này, viết chương trình tạo menu khi chọn phím T, X, P, H, C thì hỏi muốn thực hiện trên hình nào từ 3 hình trong thư mục exercise. Người dùng chọn hình nào thì thực hiện phép biến đổi trên hình đó ta làm như sau:  
![image](https://github.com/user-attachments/assets/9b0a20d5-eb6f-4d40-b269-65d686c5d183)  
Đây là phần khai báo ra hình ảnh trong thư mục exercise và triển khai các phép biến đổi cho người dùng chọn lựa.  
![image](https://github.com/user-attachments/assets/0766e3ad-22b6-4eb3-9879-50782986fbfb)  
Lưu ý là hình phải có trong thư mục, nếu không có ảnh sẽ không thể thực hiện biến đổi.  
![image](https://github.com/user-attachments/assets/ec5c86a9-4804-477a-bc79-63992c475525)  
![image](https://github.com/user-attachments/assets/15c97a2d-2b6e-4352-affb-70b3b15187ed)  
Đây là đoạn code xử lý từng phép biến đổi ảnh.  
Ví dụ: Người dùng muốn xoay ảnh thì chọn "X", sau đó tiếp tục nhập góc xoay muốn biến đổi, chương trình sẽ trả về ảnh sau khi xoay lên màn hình.  

## Hướng dẫn  
### 1. Cài đặt môi trường  
Cài python, sau đó cài các thư viện:  
Dùng tổ hợp phím: Windows + R + cmd.  
- pip install imageio.
- pip install matplotlib.
- pip install scipy.

### 2. Chạy notebook  
- Mở Jupyter Notebook trên VSCode.
- Code từng bài và chạy để xem kết quả.
- Nếu xảy ra lỗi như code sai, không có ảnh, chưa tải thư viện -> Không hiển thị kết quả.

### 3. Tùy chỉnh tham số  
Ví dụ:  
- Nhập tọa độ cắt ảnh bất kỳ trong ảnh lớn.
- Nhập tọa độ tịnh tiến ảnh.
- Nhập tỉ lệ thay đổi kích thước ảnh.
- Nhập góc xoay ảnh.

## Tài liệu tham khảo  
- Bài giảng Nhập môn Xử lý ảnh số - Van Lang University.
- Chương 6 - Sách Digital Image Processing – Gonzalez & Woods.










 










 





















