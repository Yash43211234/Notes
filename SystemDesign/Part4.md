# 📘 Core Components in Systems

## 1. Load Balancers (Nginx, HAProxy)

- **What is Load Balancer?**
  - A traffic manager that distributes requests across multiple servers.
  - Prevents overload, improves performance, ensures high availability.

- **Types:**
  - **Layer 4 (Transport):** Works on TCP/UDP (faster, less flexible).
  - **Layer 7 (Application):** Works on HTTP/HTTPS (can inspect requests, smart routing).

- **Popular Tools:**
  - **Nginx:** High-performance web server + reverse proxy + load balancer.
  - **HAProxy:** Specialized in load balancing, widely used for high-traffic websites.

---

## 2. Caching Systems (Redis, CDN)

- **Why Caching?**
  - Stores frequently used data closer to users.
  - Reduces latency, improves speed, decreases database load.

- **Types:**
  - **Redis:** In-memory data store, supports lists, sets, pub/sub. Used for session storage, leaderboards, API caching.
  - **CDN (Content Delivery Network):**
    - Distributes static content (images, CSS, JS, videos) to servers across the globe.
    - Delivers content from nearest server → reduces latency.
    - Examples: Cloudflare, Akamai, AWS CloudFront.

---

## 3. Message Queues (Kafka, RabbitMQ, SQS)

- **Why Message Queues?**
  - Allow asynchronous communication between services.
  - Help decouple systems (producer and consumer don’t need to run at the same time).
  - Improve reliability and fault tolerance.

- **Examples:**
  - **Kafka:** Distributed, high-throughput system for event streaming.
  - **RabbitMQ:** Traditional message broker, supports complex routing.
  - **AWS SQS (Simple Queue Service):** Fully managed queue service on AWS.

---

## 4. Object Storage (S3, Google Cloud Storage)

- **What is Object Storage?**
  - Stores unstructured data (files, images, backups, logs) as **objects**.
  - Each object = data + metadata + unique ID.
  - Scales easily, cheap for storing large amounts of data.

- **Examples:**
  - **Amazon S3:** Industry standard for cloud storage.
  - **Google Cloud Storage (GCS):** Similar to S3, used for storing and serving data globally.

---

## 5. Logging & Monitoring (ELK, Prometheus, Grafana)

- **Why Logging & Monitoring?**
  - Helps track errors, system health, and performance.
  - Critical for debugging and maintaining uptime.

- **Tools:**
  - **ELK Stack (Elasticsearch, Logstash, Kibana):**
    - Collect, process, and visualize logs.
  - **Prometheus:**
    - Open-source monitoring tool, great for metrics and alerting.
  - **Grafana:**
    - Visualization tool, integrates with Prometheus, Elasticsearch, and others for dashboards.
