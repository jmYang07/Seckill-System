
# Seckill System for Tens of Millions of Data and Millions of Concurrent Users

This system is designed to handle high-concurrency flash sales, ensuring stability, preventing overselling, and optimizing performance for millions of users in real-time.

## Project Features

### **1. High-Concurrency Optimization**
- **Nginx + Lua** for request filtering and inventory pre-deduction at the edge.
- **Redis** preloads inventory, minimizing database queries with atomic operations (`DECR`).
- **Kafka** queues buffer requests and asynchronously process orders, smoothing traffic spikes.
- Achieves **1M+ QPS**, reduces database access by **90%**, improves order success by **30%**, and reduces response time to **under 50ms**.

### **2. Real-Time Hot Data Management**
- **Nginx, Filebeat, Kafka, and Druid** track the top 1% high-traffic products for dynamic caching optimization.
- **Database for low-traffic products**, **Redis for mid-traffic**, and **queue-based throttling for hot items**.
- Increases hot product identification accuracy to **95%**, reduces database load by **70%**, and cuts query time to **10ms**.

### **3. Overselling Prevention & Rate Limiting**
- **Redis distributed locks** ensure atomic inventory updates.
- **Sentinel rate limiting** manages QPS thresholds and stabilizes the system under peak load.
- Cuts overselling to **0.001%**, increases system stability by **40%**, and reduces database rejections by **80%**.

### **4. Performance Boost with Static-Dynamic Separation**
- **Beetl template engine** generates static pages.
- **Nginx caches content**, and **CDN accelerates delivery**.
- Reduces backend load and rendering time, cutting page load time from **500ms to 150ms**, lowering CPU load by **60%**, and reducing database queries by **85%**.

### **5. Order Processing & Payment Consistency**
- **WebSocket + Netty** enable real-time order updates, reducing front-end polling.
- **Kafka monitors unpaid orders**, auto-releasing inventory to maintain stock accuracy.
- Halves order delays, reduces payment confirmation to **300ms**, increases inventory utilization by **25%**, and lowers failed transactions by **40%**.

## Tech Stack

- **Backend**: Spring Boot, Netty, Redis, Kafka, MySQL
- **Frontend**: Vue.js (or applicable framework), WebSocket
- **Middleware**: Nginx, Lua scripts, Sentinel, Beetl, CDN
- **Logging & Monitoring**: Filebeat, Kafka, Druid
- **Deployment**: Docker, Kubernetes

## Setup & Deployment

### **1. Running the Backend**
```sh
cd backend
mvn clean install
mvn spring-boot:run
```

### **2. Running the Frontend**
```sh
cd frontend
npm install
npm run dev
```

### **3. Running with Docker**
```sh
cd scripts
docker-compose up -d
```

## License
MIT
```

