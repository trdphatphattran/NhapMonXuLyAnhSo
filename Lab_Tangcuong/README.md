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

### Bài 3:  
Trong bài này, Chọn ảnh núi và thuyền. Xoay cả hai đối tượng 45 độ, giữ kích thước ban đầu (reshape=False). Tạo hiệu ứng phản chiếu dọc (vertical mirror) cho cả hai đối tượng sau khi xoay. Ghép cả hai đối tượng lên một canvas trắng và lưu vào mountain_boat_mirror.jpg ta làm như sau:  
![image](https://github.com/user-attachments/assets/95496724-a36f-485d-9346-55bd7b004d48)  
Chọn ảnh núi và thuyền, xoay ảnh 45 độ không đổi kích thước.  
![image](https://github.com/user-attachments/assets/b9b29ba9-8d61-42f6-91a9-8a8858ecf86d)  
Phản chiếu dọc.  
![image](https://github.com/user-attachments/assets/113e483f-2dc2-4c06-bc29-b24288065e1b)  
Tinh kích thước và tạo nền trắng:  
- H: chiều cao canvas là lớn nhất giữa 2 ảnh.
- W: tổng chiều rộng 2 ảnh + 50px khoảng cách.

![image](https://github.com/user-attachments/assets/b3b35e60-f47b-48d8-8007-daa3cb0a65f1)  
Ghép ảnh vào canvas, mountain_mirror vào góc bên trái, boat_mirror vào bên phải.  

### Bài 4:  
Trong bài này, chọn ngôi chùa bất kì. Phóng to ngôi chùa lên 5 lần. Áp dụng một biến đổi hình học tùy chỉnh (geometric transform) để tạo hiệu ứng "uốn cong" (warping) ngôi chùa. Lưu ảnh kết quả vào pagoda_warped.jpg ta làm như sau:  
![image](https://github.com/user-attachments/assets/6a6f4f20-7fb6-4ab4-84e3-a3c1190372e3)  
Chọn ảnh và phóng to: chiều dài và rộng tăng 5, kênh màu giữ nguyên.  
![image](https://github.com/user-attachments/assets/af30d8ad-1e43-47d6-a35c-3b5a97aef6ea)  
Uốn cong ảnh:  
- h: Chiều cao.
- w: Chiều rộng.
- c: Kênh màu.
- Y: Chứa các chỉ số dòng.
- X: Chứa các chỉ số cột.
- Y += 10 * np.sin(X / 30.0): làm cong toàn bộ ảnh theo chiều dọc bằng sóng hình sin.

### Bài 5:  
Trong bài này, Tạo một chương trình menu tương tác cho phép người dùng chọn các phép biến đổi sau:  
- Tịnh tiến (hỏi số pixel di chuyển theo x và y).  
- Xoay (hỏi góc xoay và chọn reshape=True/False).  
- Phóng to/thu nhỏ (hỏi hệ số zoom).  
- Làm mờ Gaussian (hỏi giá trị sigma).  
- Biến đổi sóng (hỏi biên độ sóng).   
Người dùng chọn ảnh từ 3 ảnh bất kì  
![image](https://github.com/user-attachments/assets/e7e6135e-99ec-48fb-897f-24b4969a883f)  
Chọn thư mục chứa ảnh và các phép biến đổi ảnh.  
![image](https://github.com/user-attachments/assets/e4d61f36-8bf0-4e8a-befa-8451d0c9fd27)  
Hình phải có sẵn trong thư mục, nếu không thì không thể biến đổi ảnh.  
![image](https://github.com/user-attachments/assets/4acf564e-e1c1-48d2-9e6d-31a0b64fa0d5)  
Đây là các phép biến đổi ảnh cho người dùng lựa chọn.  
Ví dụ: Người dùng chọn W (uốn cong ảnh), sau đó nhập vào biên độ sóng muốn uốn cong, sau khi nhập xong sẽ xử lý và trả về hình sau biến đổi.

## Hướng dẫn  
### 1. Cài đặt môi trường  
Cài python, sau đó cài các thư viện:  
Dùng tổ hợp phím: Windows + R + cmd.  
- pip install imageio.
- pip install matplotlib.
- pip install scipy.

### 2. Chạy notebook  
- Mở Jupyter Notebook trên VSCode.
- Code từng bài và chạy để xem kết quả.
- Nếu xảy ra lỗi như code sai, không có ảnh, chưa tải thư viện -> Không hiển thị kết quả.

### 3. Tùy chỉnh tham số  
Ví dụ:  
- Nhập tọa độ cắt ảnh bất kỳ trong ảnh lớn.
- Nhập tọa độ tịnh tiến ảnh.
- Nhập tỉ lệ thay đổi kích thước ảnh.
- Nhập góc xoay ảnh.

## Tài liệu tham khảo  
- Bài giảng Nhập môn Xử lý ảnh số - Van Lang University.
- Chương 6 - Sách Digital Image Processing – Gonzalez & Woods.































