# Hướng dẫn chạy và kiểm thử hệ thống với Docker Compose

Tài liệu này hướng dẫn các bước để khởi chạy và kiểm thử toàn bộ stack dịch vụ bao gồm API, Database và AI service thông qua Docker Compose.

## Yêu cầu trước khi chạy
- Cài đặt và bật [Docker Desktop](https://www.docker.com/products/docker-desktop/) hoặc Docker Engine trên máy.
- Cài đặt Node.js và NPM (để chạy Newman kiểm thử tự động).

## Các bước khởi chạy

1. **Chuẩn bị biến môi trường (Environment Variables)**:
   Mở terminal tại thư mục gốc của dự án và chạy lệnh sau để copy file cấu hình mặc định:
   ```bash
   cp .env.example .env
   ```
   *(File `.env` sẽ cung cấp các thông tin cần thiết như POSTGRES_USER, APP_PORT, AUTH_TOKEN... cho các container).*

2. **Khởi chạy hệ thống**:
   Sử dụng Makefile để tự động build và chạy toàn bộ Docker Compose stack:
   ```bash
   make compose-up
   ```
   *Lệnh này sẽ tải các image cần thiết, build image cho API và AI Service, thiết lập mạng `team-internal` và chạy các container ở chế độ background.*

3. **Kiểm tra trạng thái (Health Check)**:
   Sau khi các container đã được tạo, hãy theo dõi log để đảm bảo mọi thứ đã khởi động xong:
   ```bash
   make logs
   ```
   Bạn cũng có thể kiểm tra sức khỏe của từng dịch vụ bằng lệnh:
   - **API**: `curl http://localhost:8000/health`
   - **AI**: `curl http://localhost:9000/health`
   - **DB**: `docker exec -it fit4110-db-lab05 pg_isready -U lab05`

4. **Chạy kiểm thử End-to-End với Postman/Newman**:
   Khi các dịch vụ đã trong trạng thái Ready, hãy cài đặt các Node dependencies và chạy bài kiểm thử:
   ```bash
   npm install
   make test-compose
   ```
   *Báo cáo test sẽ được lưu dưới dạng file HTML trong thư mục `reports/`.*

5. **Dừng hệ thống**:
   Sau khi hoàn tất, bạn có thể tắt và xóa các container thông qua lệnh:
   ```bash
   make compose-down
   ```