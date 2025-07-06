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

### 2.3 Dò tìm cạnh với Sobel Filter  

### 2.4 Xác định góc của đối tượng  

### 2.5 Dò tìm hình dạng cụ thể trong ảnh với Hough Transform  
#### 2.5.1 Dò tìm đường thẳng trong ảnh  

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


