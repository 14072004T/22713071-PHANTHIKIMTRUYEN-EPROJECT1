

📘 Giới thiệu
EProject - Phase 1 là một hệ thống microservices mô phỏng quy trình kinh doanh của một ứng dụng thương mại điện tử đơn giản.
Dự án được xây dựng để thực hành kiến trúc microservices, quản lý giao tiếp giữa các service thông qua RabbitMQ, và triển khai toàn bộ hệ thống bằng Docker Compose.

🧩 Các microservice chính

Auth Service: Quản lý người dùng, đăng ký và đăng nhập, cấp token JWT.

Product Service: Quản lý sản phẩm, lưu trữ thông tin sản phẩm trong MongoDB.

Order Service: Quản lý đơn hàng, nhận thông tin sản phẩm và người dùng để tạo đơn hàng.

API Gateway: Trung gian nhận request từ client và chuyển tiếp đến các service tương ứng.

RabbitMQ: Hàng đợi tin nhắn, đảm bảo truyền thông không đồng bộ giữa các service.

MongoDB: Cơ sở dữ liệu chính của hệ thống.

⚙️ Công nghệ sử dụng
Công nghệ	Mô tả
Node.js	Nền tảng JavaScript phía server
Express.js	Framework cho RESTful API
MongoDB	Cơ sở dữ liệu NoSQL
Mongoose	ORM cho MongoDB
RabbitMQ	Message Broker dùng cho giao tiếp giữa các service
Docker & Docker Compose	Dùng để container hóa và quản lý toàn bộ hệ thống

🚀 Cách cài đặt & chạy dự án
1️⃣ Clone source code

2️⃣ Cài đặt dependencies cho từng service

Chạy trong từng thư mục con:

cd auth && npm install
cd ../product && npm install
cd ../order && npm install
cd ../api-gateway && npm install

3️⃣ Chạy dự án bằng Docker Compose
docker compose up -d --build


📦 Docker sẽ tự động:

Tạo và khởi động tất cả containers (auth, product, order, api-gateway, rabbitmq, mymongodb)

Tạo network nội bộ để các service có thể giao tiếp

Expose các cổng như:

API Gateway: 3003

Auth: 3000

Product: 3001

Order: 3002

MongoDB: 27017

RabbitMQ UI: 15672

🧠 Kiểm thử API với Postman
🔑 Auth Service

Đăng ký người dùng

POST http://localhost:3003/auth/register
{
  "email": "example@gmail.com",
  "password": "123456"
}


Đăng nhập

POST http://localhost:3003/auth/login

🛍️ Product Service

Thêm sản phẩm

POST http://localhost:3003/products/api/products
{
  "name": "Laptop Dell XPS",
  "price": 2500,
  "description": "High-end ultrabook"
}


Lấy danh sách sản phẩm

GET http://localhost:3003/products/api/products

📦 Order Service

Tạo đơn hàng

POST http://localhost:3003/products/api/products/buy
{
 
  "productId": "ID_PRODUCT"
  
}

🧰 Các lệnh Docker hữu ích
Lệnh	Chức năng
docker compose up -d	Khởi động toàn bộ dự án
docker compose down -v	Dừng và xóa containers + volumes
docker compose ps	Kiểm tra trạng thái các container
docker logs api-gateway -f	Xem log của API Gateway
docker exec -it mymongodb mongosh	Truy cập vào Mongo shell
🧩 Cấu trúc dự án
EProject-Phase-1/
│
├── auth/               # Service quản lý người dùng
├── product/            # Service quản lý sản phẩm
├── order/              # Service quản lý đơn hàng
├── api-gateway/        # Gateway điều phối request
├── docker-compose.yml  # Cấu hình Docker Compose
└── README.md           # Tài liệu dự án

🧑‍💻 Tác giả

👩 Phan Thị Kim Truyền
📚 Trường Đại học Công nghiệp TP.HCM (IUH)
📧 Email: kimtruyen1407@gmail.com
]
🌐 GitHub: 14072004T

🏁 Ghi chú

Đảm bảo đã cài Docker Desktop và Node.js (nếu muốn chạy local không qua Docker).

Khi test với Postman, hãy kiểm tra kỹ URL và cổng của API Gateway.

Nếu thấy lỗi socket hang up, kiểm tra Gateway route và biến môi trường trong docker-compose.yml.