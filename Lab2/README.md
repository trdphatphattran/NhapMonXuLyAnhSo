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
Công thức chính là im_2 = 255 - im_1. 
  
![image](https://github.com/user-attachments/assets/5e53daab-6b45-4375-9f08-d0035709af36)  
Đầu tiên mở ảnh mức xám bird.png, chuyển ảnh sang ndarray để thao tác pixel (im_1 = np.asarray(img)), sau đó biến đổi ảnh tại dòng im_2 = 255 - im_1.  

### 2. Power law (Thay đổi chất lượng ảnh)

Là dùng để tăng chất lượng của một bức ảnh.  
Trong bài này, với gamma = 0.5 thì sẽ làm ảnh sáng hơn với công thức chính là b2 = np.log (b3) * gamma và c= np.exp (b2) * 255.0. 

![image](https://github.com/user-attachments/assets/d839ccf8-96aa-4f5c-8659-cfed5bd5c609)  
Trước tiên khởi tạo gamma = 0.5, sau đó chuyển ảnh từ kiểu int sang float để thực hiện tính toán số mũ (b1 = im_1.astype (float)). Tiếp theo tìm giá trị lớn nhất của b1 (b2 = np.max (b1)) để chuẩn hóa ảnh, sau đó chuẩn hóa pixel về khoảng [0, 1] (b3 = b1/b2). Tính pixel bằng cách lấy gamma * log(pixel) (b2 = np.log (b3) * gamma). Cuối cùng khi ra kết quả trên, lấy hàm mũ và nhân tiếp với 255 (c= np.exp (b2) * 255.0).  
Tương tự với gamma = 5 thì sẽ cho ra ảnh tối hơn.  
![image](https://github.com/user-attachments/assets/0fe907e2-01a9-4887-a223-53154f1f1eeb).  





 















  
 
  




