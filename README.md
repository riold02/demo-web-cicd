# 🚀 Demo Web Application - CI/CD với GitHub Actions và Docker

Ứng dụng web demo cơ bản để thực hành CI/CD với GitHub Actions và triển khai qua Docker.

## 📋 Mô tả

Đây là một ứng dụng web tĩnh đơn giản được xây dựng với HTML, CSS và JavaScript, được containerize bằng Docker và tự động build/deploy thông qua GitHub Actions.

## 🛠️ Công nghệ sử dụng

- **Frontend**: HTML5, CSS3, JavaScript
- **Web Server**: Nginx (Alpine Linux)
- **Container**: Docker
- **CI/CD**: GitHub Actions
- **Orchestration**: Docker Compose

## 📁 Cấu trúc thư mục

```
QTDA/
├── .github/
│   └── workflows/
│       └── ci-cd.yml          # GitHub Actions workflow
├── index.html                  # Trang chủ
├── styles.css                  # File CSS
├── script.js                   # JavaScript
├── Dockerfile                  # Docker configuration
├── docker-compose.yml          # Docker Compose configuration
├── .dockerignore              # Docker ignore file
└── README.md                   # File này
```

## 🚀 Cách sử dụng

### 1. Chạy local với Docker

#### Build và chạy với Docker:
```bash
# Build image
docker build -t demo-web-app .

# Chạy container
docker run -d -p 8080:80 --name demo-web-app demo-web-app

# Mở trình duyệt tại: http://localhost:8080
```

#### Hoặc sử dụng Docker Compose:
```bash
# Chạy ứng dụng
docker-compose up -d

# Xem logs
docker-compose logs -f

# Dừng ứng dụng
docker-compose down
```

### 2. Triển khai lên GitHub

#### Bước 1: Khởi tạo Git repository
```bash
git init
git add .
git commit -m "Initial commit: Demo web app with CI/CD"
```

#### Bước 2: Tạo repository trên GitHub
1. Truy cập https://github.com/new
2. Tạo repository mới (ví dụ: `demo-web-cicd`)
3. Không khởi tạo với README, .gitignore hay license

#### Bước 3: Push code lên GitHub
```bash
git remote add origin https://github.com/YOUR_USERNAME/demo-web-cicd.git
git branch -M main
git push -u origin main
```

### 3. Cấu hình CI/CD với GitHub Actions

GitHub Actions workflow sẽ tự động chạy khi bạn push code lên nhánh `main` hoặc `master`.

#### Workflow bao gồm:
- ✅ Build Docker image
- ✅ Test container
- ✅ Push lên Docker Hub (tùy chọn)
- ✅ Deploy notification

#### Cấu hình Docker Hub (Tùy chọn):

Nếu bạn muốn push image lên Docker Hub, cần thêm secrets trong GitHub:

1. Truy cập repository trên GitHub
2. Vào **Settings** → **Secrets and variables** → **Actions**
3. Thêm các secrets sau:
   - `DOCKER_USERNAME`: Tên đăng nhập Docker Hub
   - `DOCKER_PASSWORD`: Password hoặc access token của Docker Hub

### 4. Xem kết quả CI/CD

1. Truy cập tab **Actions** trong repository GitHub
2. Xem workflow đang chạy
3. Kiểm tra logs và kết quả của từng bước

## 🔧 Tùy chỉnh

### Thay đổi port
Sửa file `docker-compose.yml`:
```yaml
ports:
  - "3000:80"  # Thay 3000 bằng port bạn muốn
```

### Thêm biến môi trường
Sửa file `docker-compose.yml`:
```yaml
environment:
  - NODE_ENV=production
  - API_URL=https://api.example.com
```

## 📊 Kiểm tra trạng thái

```bash
# Xem các container đang chạy
docker ps

# Xem logs
docker logs demo-web-app

# Xem thông tin chi tiết container
docker inspect demo-web-app

# Kiểm tra resource usage
docker stats demo-web-app
```

## 🛡️ Dừng và xóa

```bash
# Dừng container
docker stop demo-web-app

# Xóa container
docker rm demo-web-app

# Xóa image
docker rmi demo-web-app

# Hoặc với docker-compose
docker-compose down
docker-compose down --rmi all  # Xóa cả images
```

## 🌐 Triển khai production

### Triển khai lên VPS/Cloud:

1. **Cài đặt Docker trên server**
```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

2. **Pull và chạy image từ Docker Hub**
```bash
docker pull YOUR_USERNAME/demo-web-app:latest
docker run -d -p 80:80 --name demo-web-app YOUR_USERNAME/demo-web-app:latest
```

3. **Hoặc clone repository và build**
```bash
git clone https://github.com/YOUR_USERNAME/demo-web-cicd.git
cd demo-web-cicd
docker-compose up -d
```

## 📝 Best Practices

- ✅ Luôn sử dụng `.dockerignore` để giảm image size
- ✅ Sử dụng Alpine Linux images cho kích thước nhỏ gọn
- ✅ Tag images với version cụ thể
- ✅ Sử dụng health checks
- ✅ Implement logging và monitoring
- ✅ Backup dữ liệu quan trọng
- ✅ Sử dụng secrets cho thông tin nhạy cảm

## 🐛 Troubleshooting

### Port đã được sử dụng
```bash
# Windows: Tìm process đang dùng port 8080
netstat -ano | findstr :8080
# Kill process
taskkill /PID <PID> /F
```

### Container không start
```bash
# Xem logs
docker logs demo-web-app

# Xem events
docker events
```

### Build fail
```bash
# Clear cache và rebuild
docker build --no-cache -t demo-web-app .
```

## 📚 Tài nguyên tham khảo

- [Docker Documentation](https://docs.docker.com/)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Nginx Documentation](https://nginx.org/en/docs/)

## 📄 License

MIT License - Tự do sử dụng cho mục đích học tập và thương mại.

## 👨‍💻 Phát triển tiếp

Một số ý tưởng để mở rộng:
- [ ] Thêm unit tests
- [ ] Tích hợp với database
- [ ] Thêm authentication
- [ ] Monitoring với Prometheus/Grafana
- [ ] Load balancing
- [ ] SSL/TLS certificates
- [ ] Kubernetes deployment

---

**Happy Coding! 🎉**
