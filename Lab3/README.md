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
Công thức cắt ảnh: [y1:y2, x1:x2]  
Trong đó:  
x1: Cột bắt đầu (bên trái).  
x2: Cột kết thúc (bên phải).  
y1: Dòng bắt đầu (bên trên).  
y2: Dòng kết thúc (bên dưới).  
Code chính:  
![image](https://github.com/user-attachments/assets/9a888dee-8529-43ca-8e9a-d6f5c6c4cd73)  
Giải thích:  
- 800:1200: Cắt từ dòng 800 đến 1199 theo chiều cao.
- 570:980: Cắt từ cột 570 đến 979 theo chiều dọc.

### 2. Tịnh tiến đơn  
Là di chuyển toàn bộ ảnh theo một hướng cố định.  
Công thức tịnh tiến:  
(x, y) --> (x', y') = (x + dx, y + dy)  
Trong đó:  
x, y: Tọa độ điểm ban đầu.  
x', y': Tọa độ điểm sau tịnh tiến.  
dx: Tịnh tiến theo chiều ngang.  
dy: Tịnh tiến theo chiều dọc.  
Code chính:  
![image](https://github.com/user-attachments/assets/54953ce4-6d16-446b-bb97-01fc49bc2603)  
Giải thích:  
- Dịch chuyển 100 pixel xuống dưới.
- Dịch chuyển 25 pixel sang phải.  






