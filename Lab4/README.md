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
  + Với mỗi điểm ảnh chưa được gán nhãn, xét điểm ảnh lân cận đã gán nhãn với giá trị thấp nhất.  
  + Gán theo hướng tăng dần độ cao.
- Khi vùng lan ra và chạm nhau, đánh dấu biên vùng.
##### Code chính  
![image](https://github.com/user-attachments/assets/ba67cba3-f15d-4125-8430-db19c21e238c)  
Đây là nơi thuật toán thực sự phân vùng ảnh dựa vào các marker đã chuẩn bị.  

### 2.3 Biến đổi đối tượng trong ảnh  
Dilation cho phép các pixel ở foreground của 1 ảnh có thể соco giãn.  
#### 2.3.1  Sử dụng binary_dilation  
Binary_dilation là phép dãn cho phép mở rộng vùng trắng trong ảnh nhị phân.  
##### Công thức  
![image](https://github.com/user-attachments/assets/d2c1ed7c-1c8e-4c26-b8ca-6969f27d1c4d)  
A: Ảnh nhị phân gốc.  
B: Structuring element (nhân).  
A ⊕ B: Kết quả của phép dãn A theo nhân B.  
Aᵦ: Tập A được tịnh tiến bởi phần tử b trong nhân B.  
U: Hợp tất cả các tập con Aᵦ.  
b ∈ B: Duyệt qua tất cả các phần tử trong nhân B.  
##### Code chính  
![image](https://github.com/user-attachments/assets/08d2a6e7-6d2d-4967-8149-36c44ea654a0)  
Đây là phép dãn ảnh với số lần lặp là 50.  

#### 2.3.2  Sử dụng binary_opening  
Binary_opening là sự kết hợp giữa dilation và erosion.  
##### Công thức  
![image](https://github.com/user-attachments/assets/1cf83fd3-2445-48e3-bfc8-cb3bf6d4c7d2)  
A: Ảnh nhị phân gốc.  
B: Structuring element (nhân).  
⊖: phép erosion – thu nhỏ vùng trắng.  
⊕: phép dilation – dãn vùng trắng.  
∘: phép opening.  
##### Code chính  
![image](https://github.com/user-attachments/assets/d0fdd1fb-6cdb-48b3-9dcb-84a0e337085b)  
Đây là phép mở ảnh với số lần lặp là 25 trên ma trận 3x3 có hình dấu cộng.  

#### 2.3.3 Sử dụng binary_erosion  
Binary_erosion là thu nhỏ vùng trắng, xóa nhiễu trắng nhỏ và tách các vật thể dính nhau trong ảnh nhị phân.  
##### Công thức  
![image](https://github.com/user-attachments/assets/6deedfc3-5939-4ffb-be09-f21f6f139eff)  
A: Ảnh nhị phân gốc.  
B: Structuring element (nhân).  
B_z: Dịch nhân B đến vị trí z.  
A ⊖ B: Tập hợp tất cả điểm z mà khi đặt nhân B tại z, nó hoàn toàn nằm trong vùng trắng của A.  
##### Code chính  
![image](https://github.com/user-attachments/assets/8f04571d-c867-4f8a-a563-2d564753910c)  
Đây là phép ăn mòn ảnh với số lần lặp là 50 (làm co vùng trắng mạnh).  

#### 2.3.4 Sử dụng binary_closing  
Binary_closing là phép đóng ảnh (ngược lại với binary_opening).  
##### Công thức  
![image](https://github.com/user-attachments/assets/e2151ec2-38b9-42e9-b41e-58ea5c55c44a)  
A: Ảnh nhị phân gốc.  
B: Structuring element (nhân).  
⊕: phép dilation – dãn.  
⊖: phép erosion – ăn mòn.  
A ∙ B: kết quả của phép closing (đóng ảnh).  
##### Code chính  
![image](https://github.com/user-attachments/assets/e2a6f350-a5a6-497c-b59f-17ddb15f32e1)  
Đây là phép đóng ảnh với số lần lặp là 50.  

## Phần 2: Bài tập  
### Bài 1  
Trong bài này, chọn ảnh Langbiang trong ảnh dalat.jpg. Tịnh tiến sang phải 100px, sử dụng phương pháp otsu để phân vùng Langbiang theo ngưỡng 0.3 và lưu ảnh vào máy ta làm như sau:  

![image](https://github.com/user-attachments/assets/c2e1b51c-c924-4273-8ab5-f76b5202d0ba)  
Chọn ảnh từ thư mục exercise.  
![image](https://github.com/user-attachments/assets/e53b6a7a-58de-4262-8a22-bea4448d9da9)  
Cắt ảnh Langbiang trong ảnh lớn dalat.  
![image](https://github.com/user-attachments/assets/3a53fc0c-3838-42c5-b094-30dd14d040c4)  
Dịch ảnh sang phải 100px.  
![image](https://github.com/user-attachments/assets/ff5f8ce0-7643-43c2-8978-9ffb031ff966)  
Chuyển các pixel về khoảng [0, 1], sau đó so sánh với 0.3. Nếu pixel nào sáng hơn 0.3 thì là trắng, còn lại đen.  

### Bài 2  
Trong bài này, chọn ảnh Hồ Xuân Hương trong dalat.jpg. Xoay ảnh 1 góc 45 độ, dùng phương pháp Adaptive Thresholding với ngưỡng 60 và lưu ảnh vào máy ta làm như sau:  

![image](https://github.com/user-attachments/assets/c4269296-03b9-4b1c-a768-89c077cfc12f)  
Chọn ảnh từ thư mục exercise.  
![image](https://github.com/user-attachments/assets/7c5c757f-c83d-4ddf-a068-4abe915f7f10)  
Cắt ảnh Hồ Xuân Hương trong ảnh lớn dalat và xoay ảnh 45 độ.  
![image](https://github.com/user-attachments/assets/040cf540-47ee-4457-ad79-4a9966a23203)  
Tính ngưỡng riêng cho từng pixel, dịch ngương xuống 10 đơn vị để làm rõ ảnh hơn.  
![image](https://github.com/user-attachments/assets/58ba5bb0-6e30-4b18-bfaf-db411a1065f9)  
Nếu giá trị > ngưỡng thì ảnh trắng, ngược lại ảnh đen.  





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
- Có thể thay đổi iterations, offset, hình ảnh,... để xem các kết quả khác nhau.  

## Tài liệu tham khảo  
- Bài giảng nhập môn Xử lý ảnh số - Van Lang University.
- Chương 10 - Sách Digital Image Processing – Gonzalez & Woods.










