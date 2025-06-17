# THỰC HÀNH 2:  ẢNH KỸ THUẬT SỐ & MÀU  

## Mục tiêu bài học  
- Xử lý điểm ảnh sử dụng kĩ thuật biến đổi logarith
- Xử lý điểm ảnh sử dụng kĩ thuật biến đổi power law
- Xử lý điểm ảnh sử dụng kĩ thuật ảnh ngược
- Xử lý điểm ảnh sử dụng kĩ thuật histogram equalization
- Xử lý điểm ảnh sử dụng kĩ thuật contrasting stretching

## Thuật toán sử dụng:  
Trong bài lab này có các thuật toán chính như: Image inverse transformation, Power law, Log transformation, Histogram equalization, Contrast stretching.  

## Cách hoạt động:  
### 1. Image inverse transformation (Biến đổi cường độ ảnh)
Là biến đổi cường độ ảnh từ tối sang sáng và ngược lại.  
Trong bài này, công thức chính là im_2 = 255 - im_1. 
  
![image](https://github.com/user-attachments/assets/5e53daab-6b45-4375-9f08-d0035709af36)  
Đầu tiên mở ảnh mức xám bird.png, chuyển ảnh sang ndarray để thao tác pixel (im_1 = np.asarray(img)), sau đó biến đổi ảnh tại dòng im_2 = 255 - im_1.  

### 2. Power law (Thay đổi chất lượng ảnh)
Là dùng để tăng chất lượng của một bức ảnh.  
Trong bài này, với gamma = 0.5 thì sẽ làm ảnh sáng hơn với công thức chính là b2 = np.log (b3) * gamma và c= np.exp (b2) * 255.0. 

![image](https://github.com/user-attachments/assets/d839ccf8-96aa-4f5c-8659-cfed5bd5c609)  
Trước tiên khởi tạo gamma = 0.5, sau đó chuyển ảnh từ kiểu int sang float để thực hiện tính toán số mũ (b1 = im_1.astype (float)). Tiếp theo tìm giá trị lớn nhất của b1 (b2 = np.max (b1)) để chuẩn hóa ảnh, sau đó chuẩn hóa pixel về khoảng [0, 1] (b3 = b1/b2). Tính pixel bằng cách lấy gamma * log(pixel) (b2 = np.log (b3) * gamma). Cuối cùng khi ra kết quả trên, lấy hàm mũ và nhân tiếp với 255 (c= np.exp (b2) * 255.0) sẽ cho ra ảnh sáng hơn.  

Tương tự với gamma = 5 thì sẽ cho ra ảnh tối hơn.  
![image](https://github.com/user-attachments/assets/0fe907e2-01a9-4887-a223-53154f1f1eeb).  

### 3. Log Transformation (Thay đổi cường độ điểm ảnh)  
Là biến đổi độ sáng của ảnh nhằm làm sáng những vùng tối và giảm độ chói những vùng sáng.  
Trong bài này, công thức chính là c = (128.0 * np.log(1 + b1))/np.log (1 + b2).  
![image](https://github.com/user-attachments/assets/014e5521-365f-49c8-9988-9bc373829b6b)  
Trước tiên chuyển ảnh sang kiếu float để thực hiện tính toán logarith (b1 = im_1.astype (float)), tiếp theo tìm giá trị lớn nhất của b1 (b2 = np.max (b1)), sau cùng là thay đổi cường độ điểm ảnh (c = (128.0 * np.log(1 + b1))/np.log (1 + b2)). Chọn 128 giúp cho cường độ ảnh sau biến đổi không bị quá chói so với ảnh gốc và chia cho np.log(1 + b2) giúp cho pixel sau biến đổi nằm trong khoảng hợp lý [0, 128].  

### 4. Histogram equalization  
Là biểu đồ tần suất thống kê số lần xuất hiện các mức sáng trong ảnh, mục đích là cải tiến độ tương phản hai vùng sáng tối của ảnh.  
Trong bài này, công thức chính là  
![image](https://github.com/user-attachments/assets/de9d2792-3cbd-4c1b-a869-8ef5644b06ce)  
cdf_m là hàm phân phối tích lũy (CDF) đã loại bỏ giá trị 0.  
![image](https://github.com/user-attachments/assets/d0ebfaac-a911-43e4-901e-8b89f169fe0f)  
Trước tiên chuyển mảng 2 chiều thành 1 chiều chứa toàn bộ pixel của ảnh (b1 = im1.flatten()), sau đó tính histogram và biên của các mức xám (histogram chứa số pixel ứng với các mức xám từ 0 -> 255) (hist, bins = np.histogram(im1, 256, [0, 255])), tính hàm phân phối tích lũy và loại bỏ giá trị 0 (cdf = hist.cumsum() và cdf_m = np.ma.masked_equal (cdf, 0)). Tiếp theo chuẩn hóa ảnh về 0 -> 255 (num_cdf_m giúp trải đều mức xám của ảnh, den_cdf_m giúp trải đều giá trị của ảnh từ 0 -> 255). Sau chuẩn hóa, thay giá trị mask = 0 và chuyển sang kiểu số nguyên (cdf = np.ma.filled (cdf_m, 0).astype('uint8')), tương tự biến đổi cdf lên mảng 1 chiều và đưa mảng trở về 2 chiều ((im2 = cdf[b1] và im3 = np.reshape (im2, im1.shape)).  

### 5. Contrast stretching  
Là mở rộng giá trị pixel của ảnh sao cho độ tương phản của ảnh được cải thiện.  
Trong bài này, công thức chính là im2 = 255* (c - a)/(b - a)  
![image](https://github.com/user-attachments/assets/0a8d38fd-4d75-4498-8754-a48b786777ef)  
Trước tiên lấy pixel lớn nhất b và nhỏ nhất a (255 và 0), biến đổi pixel sang kiểu float để thực hiện toán chia (C = im1.astype (float)) và thực hiện theo công thức 255* (c - a)/(b - a) để cải thiện ảnh.  

### 6. Biến đổi Fourier  
Là biến đổi ảnh theo miền tần suất, được sử dụng trong image filter, image compression, image enhancement, image restoration, image analysis, image reconstruction.  
#### 6.1 Biến đổi với Fast Fourier  
Là biến đổi ảnh từ miền không gian sang miền tần số.  
Trong bài này, công thức chính là c = abs (scipy.fftpack.fft2 (im1))  
![image](https://github.com/user-attachments/assets/faede7ae-fc09-48d2-bd2d-1129f69c7c6a)  
Thực hiện biến đổi Fourier trên ảnh im1 bằng thư viện scipy.fftpack, abs sẽ lấy biên độ của kết quả biến đổi Fourier (c = abs (scipy.fftpack.fft2 (im1))). Sau đó fftshift giúp đưa tần số thấp vào giữa khung hình, tần số cao ra rìa giúp thuận tiện quan sát (d= scipy.fftpack.fftshift (c)).  
#### 6.2 Lọc ảnh trong miền tần suất  
Có 2 dạng là Lowpass và Highpass  
##### Butterworth Lowpass Filter  
Sử dụng những điểm ảnh có tần suất thấp từ biến đổi Fourier, lowpass dùng để làm mịn và khử nhiễu ảnh. 
![image](https://github.com/user-attachments/assets/b34b71cd-b686-48d4-83b5-481b9c4eea3d)  
Đoạn code trên là nơi giữ lại tần số thấp, giảm biên độ tần số cao. Sau giai đoạn lọc thì biến ảnh từ miền tần số về miền không gian (e = abs (scipy.fftpack.ifft2 (con)))  
##### Butterworth highpass Filter  
Sử dụng những điểm ảnh có tần suất cao từ biến đổi Fourier, highpass dùng để làm sắc biên của ảnh.  
![image](https://github.com/user-attachments/assets/00ee8567-4365-4b43-bfc5-c74d36ffad87)  
Đoạn code trên là nơi giữ lại tần số cao, giảm tần số thấp. Sau giai đoạn lọc thì biến ảnh từ miền không gian về miền tần số (e = abs (scipy.fftpack.ifft2(con))).  

### BÀI TẬP  
#### Bài 1  
Trong bài này, khi người dùng ấn phím I, G, L, H, C thì chương trình sẽ thực hiện hàm tương ứng cho các hình trong thư mục exercise. Lưu và hiển thị các ảnh đã biến đổi, ta làm như sau:  
![image](https://github.com/user-attachments/assets/ef97d5fd-5634-4fff-ab38-6ceffab5d5d0)  
Khai báo thư mục exercise chứa ảnh gốc và tạo thư mục output để chứa ảnh sau biến đổi.  
![image](https://github.com/user-attachments/assets/5f10f3f1-4f41-4273-84ee-315bbe052b67)  
Đây là hàm đọc ảnh ở chế độ Grayscale.  
![image](https://github.com/user-attachments/assets/71bf377d-b23f-416d-8131-50b20b681655)  
Đây là các hàm biến đổi ảnh:  
- image_inverse giúp biến đổi cường độ ảnh, tức sáng thành tối và ngược lại.
- power_law làm tăng chất lượng của ảnh tùy thuộc vào giá trị gamma.
- log_transformation giúp làm sáng những vùng tối.
- histogram_equalization cải thiện độ tương phản hai vùng sáng tối của ảnh.
- contrast_stretch cải thiện độ tương phản tổng thể của ảnh.

![image](https://github.com/user-attachments/assets/37dcd3b5-b5c2-4f22-9986-9e817231e197)

Sau biến đổi, lưu ảnh vào thư mục output và hiển thị ảnh ra màn hình.  
![image](https://github.com/user-attachments/assets/50344b01-2bd7-45ad-99a0-5f20e71a7017)  
Cho người dùng nhập vào lựa chọn họ muốn biến đổi ảnh.  
![image](https://github.com/user-attachments/assets/60297e26-6127-46ed-b1a1-b4700cd93f39)
  
Sau khi người dùng chọn xong, ảnh sẽ được xử lý và hiển thị ra màn hình.  

#### Bài 2  
Trong bài này, khi người dùng ấn phím F, L, H  thì chương trình sẽ thực hiện hàm tương ứng cho các hình trong thư mục exercise. Lưu và hiển thị các ảnh đã biến đổi, ta làm như sau:  
![image](https://github.com/user-attachments/assets/06d771eb-0773-4847-90cd-c365a12dcfe4)  
Khai báo thư mục exercise chứa ảnh gốc và tạo thư mục output để chứa ảnh sau biến đổi.  
![image](https://github.com/user-attachments/assets/409fc8ea-9537-4508-8434-711a07f960e2)  
Đây là hàm đọc ảnh ở chế độ Grayscale.  
##### Fast Fourier  
![image](https://github.com/user-attachments/assets/3ab72261-a6ac-40d2-b3ee-a735e5dcc883)  
Thực hiện biến đổi Fourier 2 chiều trên ảnh xám (f = np.fft.fft2(img))  
Dịch chuyển tần số 0 vào giữa ảnh để dễ quan sát (fshift = np.fft.fftshift(f))  
Tính phổ biên độ (magnitude_spectrum = 20 * np.log(np.abs(fshift) + 1))  
Chuẩn hóa phổ biên độ về [0, 255] (return np.uint8(255 * magnitude_spectrum / np.max(magnitude_spectrum))).  
##### Butterworth Lowpass Filter  
![image](https://github.com/user-attachments/assets/7713859e-a1dd-4394-9fed-bb9a9a58df4a)  
Lấy kích thước ảnh và tọa độ trung tâm  
![image](https://github.com/user-attachments/assets/4650c9f2-427a-45ea-84a7-0993b2c65ee5)  
Tạo ma trận khoảng cách từ mỗi điểm đến tâm ảnh.  
Tạo bộ lọc Butterworth Lowpass (H = 1 / (1 + (d / cutoff)**(2 * order)))  
![image](https://github.com/user-attachments/assets/53f89930-a3a1-4320-bfe6-c828bf3d9b7c)  
Biến đổi Fourier -> dịch tâm về giữa -> nhân với bộ lọc H trog miền tần số  
Biến đổi ngược Fourier về miền không gian (img_back = np.fft.ifft2(np.fft.ifftshift(f_filtered)))  
##### Butterworth Highpass Filter  
![image](https://github.com/user-attachments/assets/7713859e-a1dd-4394-9fed-bb9a9a58df4a)  
Lấy kích thước ảnh và tọa độ trung tâm  
![image](https://github.com/user-attachments/assets/4650c9f2-427a-45ea-84a7-0993b2c65ee5)  
Tạo ma trận khoảng cách từ mỗi điểm đến tâm ảnh.  
Tạo bộ lọc Butterworth Lowpass (H = 1 / (1 + (cutoff / (d + 1e-5))**(2 * order)))    
![image](https://github.com/user-attachments/assets/53f89930-a3a1-4320-bfe6-c828bf3d9b7c)  
Biến đổi Fourier -> dịch tâm về giữa -> nhân với bộ lọc H trog miền tần số  
Biến đổi ngược Fourier về miền không gian (img_back = np.fft.ifft2(np.fft.ifftshift(f_filtered)))  
![image](https://github.com/user-attachments/assets/627523e9-c745-4d7a-bfc8-a4b2a4efd9f5)  
Sau biến đổi, lưu ảnh vào thư mục output và hiển thị ảnh ra màn hình.  
![image](https://github.com/user-attachments/assets/b002597a-4b07-4aab-8812-9612c8d22ddc)  
Cho người dùng nhập vào lựa chọn  
![image](https://github.com/user-attachments/assets/5705e1b7-36f5-42de-9b0c-8f392dad48c3)  
Sau khi chịn, ảnh sẽ được xử lý và hiển thị  





















































 















  
 
  




