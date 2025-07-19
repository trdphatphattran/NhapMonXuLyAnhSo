# THỰC HÀNH 6: ĐỀ THI THỬ  
## Thông tin  
- Sinh viên: Trần Đại Phát
- MSSV: 2374802010379
- Môn học: Nhập môn Xử lý ảnh số
- GVHD: Đỗ Hữu Quân
- Năm học: 2024 - 2025
## Mục tiêu bài học  
- Ôn tập, hệ thống lại các kiến thức đã học.
- Xử lý nhiều dạng bài tập từ dễ đến khó.

## Câu 1: 
Cho ảnh a.jpg, thực hiện các yêu cầu sau:  
- Viết chương trình sử dụng mean filter cho ảnh.
<img width="295" height="57" alt="image" src="https://github.com/user-attachments/assets/9ff5acae-5b96-4cd5-a48b-bf92301e0c3f" />

Khởi tạo bộ lọc trung bình 5x5, mỗi phần tử có giá trị 1/25, thực hiện phép tính và lưu ảnh mới.  

- Viết chương trình sử dụng filter để xác định biên của ảnh trên.
<img width="370" height="40" alt="image" src="https://github.com/user-attachments/assets/93cd8da8-7c56-4fea-a26e-0c543d78c15e" />

Dùng phương pháp Canny để xác dịnh biên, sigma = 3 là tham số xác định độ làm mờ Gaussian trước khi phát hiện biên, thực hiện phép tính và lưu lại ảnh mới.  

- Viết chương trình đổi màu ảnh từ không gian màu BGR sang một màu ngẫu nhiên (RGB) bằng cách thay đổi các kênh màu một cách ngẫu nhiên, sau đó lưu hình mới vào file a_random_color.jpg.
<img width="298" height="78" alt="image" src="https://github.com/user-attachments/assets/7818175c-10e5-4e07-8f8e-89b89b9c3e20" />

Gán số thứ tự cho từng kênh màu trong ảnh RGB --> Tạo danh sách chứa các kênh màu theo thứ tự chuyển --> Trộn kênh màu một cách ngẫu nhiên --> Áp dụng thứ tự mới vào ảnh đầu vào, đổi vị trí các kênh màu RGB.  


- Chuyển ảnh sang không gian màu HSV và tách riêng kênh Hue, Saturation, Value để  lưu  thành  ba  ảnh  grayscale  tương  ứng  (a_hue.jpg, a_saturation.jpg, a_value.jpg).
<img width="579" height="147" alt="image" src="https://github.com/user-attachments/assets/8bbe7615-3848-44a9-a517-cf568f500b82" />

h_img: giữ nguyên Hue, còn Saturation và Value đặt là 1, giúp cho rõ kênh Hue. Tương tự với Saturation và Value.  
h_img: ảnh thể hiện màu chủ đạo.  
s_img: ảnh thể hiện độ bão hòa màu.  
v_img: ảnh thể hiện độ sáng.  

## Câu 2:  
<img width="786" height="728" alt="image" src="https://github.com/user-attachments/assets/63fd222c-1071-4483-8988-3a9ae6adda12" />  

<img width="776" height="103" alt="image" src="https://github.com/user-attachments/assets/d29367cf-718a-4e87-a264-b377b91bb3f6" />  

Trong bài này, khi người dùng ấn phím I, G, L, H, C, A thì chương trình sẽ thực hiện hàm tương ứng cho các hình  image1.jpg, image2.jpg, và 
image3.jpg. Lưu và hiển thị các ảnh đã biến đổi, ta làm như sau:  
<img width="441" height="42" alt="image" src="https://github.com/user-attachments/assets/0ddec666-85ba-4b1c-a6f4-5e281324adad" />  

Khai báo thư mục và tạo folder chứa ảnh sau biến đổi.  
<img width="599" height="397" alt="image" src="https://github.com/user-attachments/assets/33f35ee2-5a41-4ed2-af07-fed5828f475e" />  

Đây là các hàm biến đổi ảnh:  
- image_inverse giúp biến đổi cường độ ảnh, tức sáng thành tối và ngược lại.  
- gamma_correction làm tăng chất lượng của ảnh tùy thuộc vào giá trị gamma.
- log_transformation giúp làm sáng những vùng tối.
- histogram_equalization cải thiện độ tương phản hai vùng sáng tối của ảnh.
- contrast_stretch cải thiện độ tương phản tổng thể của ảnh.
- adaptive_histogram_equalization làm tăng độ rõ nét và chi tiết ở các vùng tối hoặc vùng sáng quá mức trong ảnh.

<img width="410" height="151" alt="image" src="https://github.com/user-attachments/assets/167a6f04-eb95-420b-aca3-1f7b30efaff4" />  

Sau biến đổi, ảnh được lưu vào thư mục output.  

<img width="470" height="152" alt="image" src="https://github.com/user-attachments/assets/5d7f13ea-ea8d-4bb5-97b7-d3d66209a8f6" />  

Cho người dùng nhập vào lựa chọn họ muốn biến đổi ảnh.  

<img width="606" height="561" alt="image" src="https://github.com/user-attachments/assets/174d8264-5e10-4d04-8e51-12748af974b0" />  

Sau khi chọn xong, ảnh sẽ được biến đổi và hiển thị ra màn hình.  

## Câu 3:  
Viết một chương trình Python sử dụng OpenCV để xử lý ba ảnh: colorful-ripe-tropical-fruits.jpg,  quang-ninh.jpg,  và  pagoda.jpg  với  các  phương  pháp biến đổi và tiền xử lý nâng cao.  
- Tăng kích thước ảnh colorful-ripe-tropical-fruits.jpg thêm 30 pixel ở cả chiều rộng và chiều cao.
<img width="498" height="57" alt="image" src="https://github.com/user-attachments/assets/650e026f-39e5-4f3a-82a4-5c096c53364b" />

Đoạn code trên tăng chiều rộng 15px trái và 15px phải; tăng chiều cao 15px trên và 15px dưới. Kênh màu vẫn giữ nguyên.  

- Xoay ảnh quang-ninh.jpg 45 độ theo chiều kim đồng hồ và lật ngang
<img width="259" height="131" alt="image" src="https://github.com/user-attachments/assets/58265e8a-dd54-4627-b942-6c5b4f5f6ca5" />

Dùng nd.rotate để xoay ảnh sang 45 độ.  
Dùng nd.fliplr để lật ảnh sang ngang (flip left right).  

- Tăng kích thước ảnh pagoda.jpg lên 5 lần và áp dụng Gaussian blur với kernel 7x7 để làm mịn.
<img width="416" height="166" alt="image" src="https://github.com/user-attachments/assets/6902028b-fb04-4412-9e30-3e37fd18944d" />

Dùng nd.zoom để phóng to ảnh lên 5 lần ở chiều rộng và chiều cao, kênh màu giữ nguyên.  
Dùng nd.gaussian_filter để làm mịn ảnh bằng Gaussian Blur. Sigma = (1.1, 1.1, 0) là độ lệch chuẩn của Gaussian theo chiều rộng và chiều cao, không làm biến đổi kênh màu.  

- Ứng dụng công thức bên dưới cho ảnh pagoda.jpg
<img width="620" height="432" alt="image" src="https://github.com/user-attachments/assets/9fe11cc0-0306-4f69-93ed-1877227cbcf6" />

<img width="480" height="148" alt="image" src="https://github.com/user-attachments/assets/9d3ab16c-19e1-4fbe-b3df-acd0ffc5c1c1" />  

Cho người dùng nhập vào giá trị alpha và beta (0.5 <= alpha <= 2.0 và -50 <= beta <= 50).  
Sau đó áp dụng công thức biến đổi tuyến tính được sử dụng để điều chỉnh độ sáng và tương phản của ảnh (lưu ý giới hạn giá trị trong khoảng [0, 255] hợp với ảnh 8-bit).  





























