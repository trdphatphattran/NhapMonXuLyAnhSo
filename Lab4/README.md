# THỰC HÀNH 4: PHÂN VÙNG ẢNH  
## Thông tin  
Sinh viên: Trần Đại Phát  
MSSV: 2374802010379  
Môn học: Nhập môn Xử lý ảnh số  
GVHD: Đỗ Hữu Quân  
Năm học: 2024 - 2025  
## Mục tiêu bài học   
- Viết được chương trình phân vùng ảnh theo histogram.
- Viết được chương trình phân vùng ảnh theo region.
- Viết được chương trình thay đổi ảnh.
## Giới thiệu  
Phân vùng ảnh là quá trình chia ảnh thành nhiều vùng có chung đặc tính.  
## Phần 1: Viết chương trình phân vùng ảnh  
### 2.1 Phân vùng theo histogram  
Một ngưỡng được xác định dựa theo histogram của ảnh. Mỗi pixel trong ảnh được so sánh với ngưỡng, nếu giá trị pixel nhỏ hơn ngưỡng, thì pixel trong phân vùng được gán giá trị 0. Ngược lại, gán giá trị 1.  
#### 2.1.1 Phương pháp otsu  

#### 2.1.2 Phương pháp Adaptive Thresholding  
Cải tiến phân vùng chính xác hơn Otsu. Chia ảnh thành nhiều ảnh nhỏ và tính threshold cho từng ảnh nhỏ.  

### 2.2 Phân vùng theo region  
Một region là một nhóm các pixel có cùng thuộc tính.  

### 2.3 Biến đổi đối tượng trong ảnh  
Dilation cho phép các pixel ở foreground của 1 ảnh có thể соco giãn.  
#### 2.3.1  Sử dụng binary_dilation

#### 2.3.2  Sử dụng binary_opening  

#### 2.3.3 Sử dụng binary_erosion  

#### 2.3.4 Sử dụng binary_closing  

## Phần 2: Bài tập  
### Bài 1  

### Bài 2  

### Bài 3  

### Bài 4  

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

## Tài liệu tham khảo  
- Bài giảng nhập môn Xử lý ảnh số - Van Lang University.
- Chương 10 - Sách Digital Image Processing – Gonzalez & Woods.










