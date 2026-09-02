Bài 4: Tích hợp CI/CD tự động Pull Image từ GHCR

 
1. Mục tiêu học tập

- Khai thác biến môi trường mặc định của GitHub Actions (`secrets.GITHUB_TOKEN`) để đơn giản hóa bảo mật.

- Thiết lập quyền (permissions) truy xuất tài nguyên container.

- Chủ động rà soát tài liệu hệ thống CI/CD để khắc phục các lỗi về quyền hạn và định dạng chuỗi.

 
2. Bối cảnh tình huống

Sau khi image đã được lưu trữ an toàn trên GHCR, luồng CI/CD (GitHub Actions) hiện cần được cấu hình để tự động kéo image về chạy verify. Khi bạn thử viết kịch bản kéo ảnh, workflow liên tục thất bại ở bước `docker pull` vì chưa được xác thực (unauthenticated). 

Giảng viên môn DevOps xem qua lỗi và hướng dẫn: "Hệ thống CI/CD có sẵn biến `GITHUB_TOKEN` để đăng nhập mà không cần lấy PAT cá nhân của em. Nhưng em phải thiết lập thêm khối `permissions` khai báo quyền cho file YAML thì nó mới truy cập được package. Thêm nữa, kiểm tra xem tên repo có dính chữ viết hoa không nhé. Em tự tra tài liệu GitHub Actions đi, thử vài lần là ra ngay!"

 
3. Yêu cầu bài tập

- Viết file Workflow (`.github/workflows/ci.yml`) để tự động đăng nhập vào GHCR sử dụng `secrets.GITHUB_TOKEN` và tên người dùng hệ thống mặc định.

- Bổ sung cấu hình quyền `permissions` trong file YAML để workflow có thể đọc packages.

- Khắc phục rủi ro tên repo chứa chữ hoa (nếu có) bằng cách chuyển tên thành chữ thường, sau đó pull image và khởi chạy container verify ở chế độ nền (detached).
4. Kết quả cần đạt được

- Tệp Workflow YAML hoàn chỉnh không có lỗi cú pháp.

- Log quá trình chạy trên tab Actions màu xanh, xác nhận đăng nhập thành công, kéo ảnh thành công.

- Thời gian chạy của job rất ngắn (dưới 20 giây), thể hiện sự ưu việt của việc chỉ kéo image thay vì biên dịch lại mã nguồn.

 
5. Hướng dẫn nộp bài

Nộp trực tiếp file `.github/workflows/ci.yml` của bạn và một đường link dẫn tới màn hình kết quả chạy Workflow thành công lên Portal.