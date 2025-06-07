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
Công thức: s = L - 1 - r. 
  
![image](https://github.com/user-attachments/assets/5e53daab-6b45-4375-9f08-d0035709af36)  
Đầu tiên mở ảnh mức xám bird.png, chuyển ảnh sang ndarray để thao tác pixel (im_1 = np.asarray(img)), sau đó biến đổi ảnh tại dòng im_2 = 255 - im_1.  

### 2. Power law (Thay đổi chất lượng ảnh)

Là dùng để tăng chất lượng của một bức ảnh.  
Trong bài này, với gamma = 0.5 thì sẽ làm ảnh sáng hơn.  
![image](https://github.com/user-attachments/assets/d839ccf8-96aa-4f5c-8659-cfed5bd5c609)  

 















  
 
  




