# THỰC HÀNH 5: XÁC ĐỊNH ĐỐI TƯỢNG TRONG ẢNH  
## Thông tin  
Sinh viên: Trần Đại Phát  
MSSV: 2374802010379  
Môn học: Nhập môn Xử lý ảnh số  
GVHD: Đỗ Hữu Quân  
Năm học: 2024 - 2025  
## Mục tiêu bài học  
- Viết được chương trình gán nhãn cho phân vùng ảnh.
- Viết được chương trình phân vùng ảnh theo Region.
- Viết được chương trình thay đổi ảnh.
## Giới thiệu  
Gán nhãn dùng để phân biệt các đối tượng khác nhau trong ảnh. Trong 1 ảnh đã được gán nhãn, tất cả các pixel của một đối tượng có giá trị như nhau.  
## Phần 1: Cài đặt thư viện  
- pip install opencv-python.
## Phần 2: Viết chương trình gán nhãn ảnh  
### 2.1 Gán nhãn ảnh  
Gán nhãn ảnh là quá trình gắn thông tin mô tả cho một hoặc nhiều đối tượng trong ảnh.  
Gán nhãn ảnh nhầm mục đích:  
- Cải thiện độ chính xác của AI.
- Tăng tốc độ học máy.
- Đảm bảo tính nhất quán.
- Phát hiện lỗi sớm.

#### Code chính:  
![image](https://github.com/user-attachments/assets/24a2302b-b884-4ee4-9f1f-dd3b3b33479a)  
- Tìm ngưỡng nhị phân tự động bằng phương pháp Otsu.
- Gán nhãn cho từng vùng liên thông trong ảnh nhị phân b.  
- d là danh sách các vùng (region), mỗi vùng có thông tin riêng như "Area, Centroid, BoundingBox".

### 2.2 Dò tìm cạnh theo chiều dọc  
Dò tìm cạnh theo chiều dọc là quá trình xác định các điểm trong ảnh nơi cường độ pixel thay đổi mạnh theo chiều ngang (tức biên theo chiều dọc).  
Mục đích:  
- Làm nổi bật ranh giới.  
- Giảm thông tin dư thừa, giữ lại các vùng có thay đổi.

#### Code chính:  
![image](https://github.com/user-attachments/assets/27b1f3de-0116-415e-be08-3dafc596de83)  
- Dịch toàn bộ ảnh sang phải 1 pixel.
- abs(data - shifted()): Tính hiệu độ sáng giữa ảnh gốc và ảnh đã dịch -> Làm nổi bật các vị trí có sự thay đổi chiều ngang.  

### 2.3 Dò tìm cạnh Sobel Filter  
Dò tìm cạnh Sobel Filter nhằm phát hiện các cạnh, tức là nơi cường độ pixel thay đổi mạnh, bằng cách áp dụng toán tử Sobel theo hai hướng ngang và dọc.  
Mục đích:  
- Phát hiện hình dạng vật thể.  
- Phân đoạn đối tượng.  
- Hỗ trợ nhận dạng và theo dõi.  

#### Code chính:  
![image](https://github.com/user-attachments/assets/0f280473-26c5-45b9-b995-ed498388a2b1)  
Tính đạo hàm Sobel theo 2 trục:  
- axis = 0: Tính độ biến thiên theo chiều dọc (đạo hàm theo hàng) -> phát hiện biên ngang.
- axis = 1: Tính độ biến thiên theo chiều ngang (đạo hàm theo cột) -> phát hiện biên dọc.  

### 2.4 Xác định góc của đối tượng  
Xác định góc của đối tượng là quá trình tìm ra các điểm đặc trưng nằm tại góc trong ảnh, nơi có sự thay đổi mạnh về hướng hoặc giao nhau giữa hai biên.  
Mục đích:  
- Nhận diện đối tượng trong ảnh.
- So khớp ảnh.
- Theo dõi đối tượng.

#### Code chính:  
![image](https://github.com/user-attachments/assets/1fc56483-5e55-4b45-ad6d-f7306edada35)  
- Đạo hàm theo trục y và x.

![image](https://github.com/user-attachments/assets/1faf78f0-f68d-40de-bd8a-f73fa0e51c7c)  
- Tạo các phần tử ma trận của cấu trúc.

![image](https://github.com/user-attachments/assets/439077c9-5e23-4d16-9629-4cf5b89439f9)  
- Làm mượt các thành phần để ổn định hơn.

![image](https://github.com/user-attachments/assets/9cbf0dee-5b22-4966-b5fe-6c1db7acc28e)  
- Tính giá trị R cho mỗi pixel -> pixel có R cao là các điểm góc.  

### 2.5 Dò tìm hình dạng cụ thể trong ảnh với Hough Transform  
#### 2.5.1 Dò tìm đường thẳng trong ảnh  
Dò tìm ảnh thẳng trong ảnh là quá trình xác định các đường thẳng xuất hiện trong ảnh.  
Mục đích:  
- Phát hiện biên, lằn đường.
- Phát hiện hình học: Hình vuông, tam giác, ...

#### Công thức:  
ρ = x · cos(θ) + y · sin(θ)  
Trong đó:  
- x, y: Tọa độ điểm ảnh.
- θ: Góc quay.
- ρ: Khoảng cách từ tọa độ đến đường thẳng.

#### Code chính:  
![image](https://github.com/user-attachments/assets/1b97e48f-b049-4b27-b677-1f3e182d601b)  
R: Bán kính tối đa.  
90: Số góc.  

![image](https://github.com/user-attachments/assets/7458939c-0a47-4f8b-bb06-53d5a64eb862)  
Đây là vị trí thuât toán dò đường thẳng.  

#### 2.5.2 Dò tìm đường tròn trong ảnh

### 2.6 Image matching  

## Hướng dẫn  
### 1. Cài đặt môi trường  
Cài python, sau đó cài các thư viện:  
Dùng tổ hợp phím: Windows + R + cmd.  
- pip install imageio.
- pip install matplotlib.
- pip install scipy.
- pip install opencv-python.
- pip install scikit-image.
### 2. Chạy notebook  
- Mở Jupyter Notebook trên VSCode.
- Code từng bài và chạy để xem kết quả.
- Nếu xảy ra lỗi như code sai, không có ảnh, chưa tải thư viện -> Không hiển thị kết quả.
### 3. Tùy chỉnh tham số  
- Có thể thay đổi iterations, offset, hình ảnh,... để xem các kết quả khác nhau.  

## Tài liệu tham khảo  
- Bài giảng nhập môn Xử lý ảnh số - Van Lang University.
- Chương 10, 11, 12 - Sách Digital Image Processing – Gonzalez & Woods.


