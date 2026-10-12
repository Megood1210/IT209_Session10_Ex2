## 1. Các bước thực hiện & Kiểm tra

### Bước 1: Build Docker Image
```bash
docker build -t hw-backend:v1 .
```
**Kết quả:**
```text
[+] Building 17.4s (10/10) FINISHED
 => [1/5] FROM docker.io/library/node:18-alpine
 => [2/5] WORKDIR /app
 => [3/5] COPY package*.json ./
 => [4/5] RUN npm install --only=production
 => [5/5] COPY . .
 => exporting to image
 => => naming to docker.io/library/hw-backend:v1
```

### Bước 2: Khởi chạy Container từ Image đã build
```bash
docker run -d --name app-single-stage -p 8080:3000 hw-backend:v1
```
**Kết quả:**
```text
35c6bcf6790fe4a9d06a49c34c977f248c73a0d70ce75384ed26c24542b5c26a
```

### Bước 3: Kiểm tra trạng thái Container
```bash
docker ps
```
**Kết quả:**
```text
CONTAINER ID   IMAGE           COMMAND                  CREATED          STATUS          PORTS                                         NAMES
35c6bcf6790f   hw-backend:v1   "docker-entrypoint.s…"   11 seconds ago   Up 10 seconds   0.0.0.0:8080->3000/tcp, [::]:8080->3000/tcp   app-single-stage
```

### Bước 4: Kiểm tra Logs của Container
```bash
docker logs app-single-stage
```
**Kết quả:**
```text
Server listening on port 3000
```

### Bước 5: Kiểm tra phản hồi của ứng dụng qua curl
```bash
curl -i http://localhost:8080/
```
**Kết quả:**
```text
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 64
ETag: W/"40-upZb7Fps+hszzRU9BoKtiCsmGCQ"
Date: Fri, 09 Oct 2026 13:47:15 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{"status":"success","message":"Hello from Docker Single-stage!"}
```
*(Ứng dụng phản hồi HTTP Status 200 OK và trả về JSON chính xác).*
