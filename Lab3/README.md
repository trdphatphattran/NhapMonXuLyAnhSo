# THỰC HÀNH 3: BIẾN ĐỔI HÌNH HỌC  
## Mục tiêu bài học  
- Viết được chương trình chọn đối tượng trong ảnh
- Viết được chương trình tịnh tiến ảnh
- Viết được chương trình thay đổi kích thước ảnh
- Viết được chương trình xoay ảnh
- Viết được chương trình biến đổi cực
## Giới thiệu  
Biến đổi hình học là sắp xếp lại vị trí các điểm ảnh. Có 2 phép biến đổi là tịnh tiến và xoay.  
## Cách hoạt động:  
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

 





















