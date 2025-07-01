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
Otsu là một phương pháp tự động tìm ngưỡng để chuyển ảnh xám thành ảnh nhị phân.  
##### Công thức  
![image](https://github.com/user-attachments/assets/3485110b-3a2c-4b0b-af71-81265f54b86d)  
t: Ngưỡng phân tích mức xám.  
ω₀(t): Tỷ lệ số điểm ảnh thuộc lớp 0.  
ω₁(t): Tỷ lệ số điểm ảnh thuộc lớp 1.  
σ₀²(t): Phương sai của lớp 0.  
σ₁²(t): Phương sai của lớp 1.  
σw²(t): Phương sai trong lớp (mục tiêu cần giảm).  

##### Code chính  
![image](https://github.com/user-attachments/assets/fd3759a1-8746-4c6e-a257-b52bd36eb670)  
Trong đó:  
- a: Ảnh gốc đã chuyển sang ảnh xám.
- threshold_otsu(a): Áp dụng thuật toán Otsu để tự động tìm ngưỡng tối ưu thres.
- thres: Là ngưỡng xám mà Otsu chọn.  

#### 2.1.2 Phương pháp Adaptive Thresholding  
Cải tiến phân vùng chính xác hơn Otsu. Chia ảnh thành nhiều ảnh nhỏ và tính threshold cho từng ảnh nhỏ.  
##### Công thức  
T(x, y) = mean(Nₓ,ᵧ) - C.  

T(x, y): Ngưỡng được đặt tại vị trí pixel.  
Nₓ,ᵧ: Vùng lân cận xung quanh điểm (x, y).  
mean(Nₓ,ᵧ): Trung bình giá trị xám vùng lân cận.  
C: giá trị offset để điều chỉnh ngưỡng.  

##### Code chính
![image](https://github.com/user-attachments/assets/75f4bb99-44f7-404c-b6b8-d7b636898b01)  
Trong đó:  
- a: Ảnh đầu vào.
- 39: Kích thước pixel dùng để tính ngưỡng tại mỗi điểm.  
- offset = 10: trừ thêm 10 để làm ngưỡng nhạy hơn.
- b: ma trận ngưỡng cục bộ tại từng vị trí ảnh.

### 2.2 Phân vùng theo region  
Một region là một nhóm các pixel có cùng thuộc tính.  
##### Ý tưởng  
Xem ảnh như một hàm cường độ sáng f(x, y):
- f(x, y) càng nhỏ -> điểm ảnh càng thấp.
- f(x, y) càng lớn -> điểm ảnh càng cao.  
##### Thuật toán  
- Tìm các minima địa phương trong ảnh xám hoặc ảnh biến đổi khoảng cách (distanceTransform).  
- Mỗi minima được gán nhãn như một "hạt giống" (marker).  
- Từ các marker đó, thuật toán lan rộng vùng lân cận:  
- + Với mỗi điểm ảnh chưa được gán nhãn, xét điểm ảnh lân cận đã gán nhãn với giá trị thấp nhất.  
- + Gán theo hướng tăng dần độ cao.
- Khi vùng lan ra và chạm nhau, đánh dấu biên vùng.
##### Code chính  
![image](https://github.com/user-attachments/assets/ba67cba3-f15d-4125-8430-db19c21e238c)  
Đây là nơi thuật toán thực sự phân vùng ảnh dựa vào các marker đã chuẩn bị.  

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










