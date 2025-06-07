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















 















  
 
  




