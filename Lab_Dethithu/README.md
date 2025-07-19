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

