# THỰC HÀNH TĂNG CƯỜNG  
## Thông tin:  
Sinh viên: Trần Đại Phát  
MSSV: 2374802010379  
Môn học: Nhập môn Xử lý ảnh số  
GVHD: Đỗ Hữu Quân  
Năm học: 2024 - 2025  

### Bài 1:  
Trong bài này, chọn ảnh quả kiwi bất kì. Tịnh tiến quả kiwi 50 pixel sang phải và 30 pixel xuống dưới. Áp dụng hiệu ứng sóng (wave effect) lên quả kiwi bằng cách sử dụng biến đổi tọa độ (map_coordinates) với hàm sin. Lưu ảnh kết quả vào file kiwi_wave.jpg ta làm như sau:  
![image](https://github.com/user-attachments/assets/e4b3e587-86cc-4655-bc4a-5edbff88afbd)  
Chọn ảnh kiwi và tịnh tiến ảnh 50 pixel sang phải và 30 pixel xuống dưới.  
![image](https://github.com/user-attachments/assets/f7c1e813-34c1-4609-adab-a96769f4a2a0)  
Tạo hiệu ứng sóng bằng biến đổi tọa độ, Y và X có kích thước h, w dùng để biểu diễn vị trí từng pixel trong ảnh.  
![image](https://github.com/user-attachments/assets/d65665e0-6b73-4596-86b7-4741e401ad1f)  
Áp dụng biến dạng bằng map_coordinates.  

### Bài 2:  
Trong bài này, chọn quả đu đủ và dưa hấu từ google. Đổi màu đu đủ thành gradient từ đỏ sang xanh lá, và dưa hấu thành gradient từ vàng sang tím. Ghép hai quả lên một nền trong suốt (alpha channel) và lưu dưới dạng PNG ta làm như sau:  
![image](https://github.com/user-attachments/assets/2e152053-f336-4293-9844-dafe87a8e0d5)  
Chọn ảnh đu đủ và dưa hấu trong ảnh gốc.  
![image](https://github.com/user-attachments/assets/7046e6b9-0d12-4bf3-845a-59817f18a5e2)  
Tạo gradient màu đỏ -> xanh lá cho đu đủ:  
- Tạo gradient theo chiều dọc.  
- Đỏ -> xanh lá: đỏ giảm dần, xanh lá tăng dần từ trên xuống dưới.  
- Áp dụng gradient bằng cách nhân từng pixel của đu đủ với màu tương ứng trong gradient1.  

![image](https://github.com/user-attachments/assets/f8fa5b22-1ed2-4d03-967e-fbfcf8f76769)  
Tạo gradient vàng -> tím cho dưa hấu:  
- Tạo gradient theo chiều ngang.  
- Vàng (255,255,0) → Tím (128,0,255).
- Áp dụng gradient bằng cách nhân từng pixel của dưa hấu với màu tương ứng trong gradient2.

![image](https://github.com/user-attachments/assets/8a1da8fb-bc2d-46f4-a7a6-127eaa335fb3)  
Tạo nền trong suốt và ghép ảnh.  
![image](https://github.com/user-attachments/assets/ea3e9ed1-e810-482e-8deb-ac17c8611674)  
Tạo 1 ảnh nền có kích thước lớn để chứa đủ 2 quả:  
- Cả 2 được dán lên nền trong suốt alpha = 255.
- Dưa hấu nằm bên phải, cách đu đủ 50px.














