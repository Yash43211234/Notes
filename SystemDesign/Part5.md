# 📘 High-Level Design Concepts

## 1. Monolith vs Microservices

- **Monolith:**
  - All features in a single codebase.
  - Simple to build, deploy, and debug initially.
  - Hard to scale and maintain as the project grows.
  - Example: Early versions of Twitter, Instagram.

- **Microservices:**
  - System is divided into smaller independent services.
  - Each service handles one responsibility (user service, payment service, etc.).
  - Easier scaling and independent deployments.
  - Needs service discovery, API gateway, and monitoring.
  - Example: Netflix, Amazon.

---

## 2. Service Discovery & API Gateways

- **Service Discovery:**
  - Helps microservices find each other dynamically.
  - Example: When a service starts, it registers itself to a registry.
  - Tools: **Consul, Eureka, Zookeeper**.

- **API Gateway:**
  - Acts as a single entry point for all client requests.
  - Handles authentication, routing, load balancing, caching, rate limiting.
  - Examples: **Kong, Nginx, AWS API Gateway**.

---

## 3. Event-Driven Architecture

- **Concept:**
  - Instead of direct requests, services communicate via events.
  - Producer emits events → Consumers listen & react.
  - Decouples services and improves scalability.

- **Examples:**
  - Kafka, RabbitMQ, AWS SNS/SQS.
  - Use cases: Order placed → Payment service, inventory service, and notification service all react independently.

---

## 4. Rate Limiting & Throttling

- **Why?**
  - Protects system from being overloaded by too many requests.
  - Ensures fair usage of resources.

- **Rate Limiting:**
  - Restrict number of requests per user/IP in a given time.
  - Example: API allows only 100 requests per minute.

- **Throttling:**
  - Slows down requests instead of blocking completely.
  - Example: After 100 requests, additional requests are delayed.

- **Techniques:**
  - Token Bucket, Leaky Bucket, Fixed Window, Sliding Window.

---

## 5. Consistency Models (Strong, Eventual)

- **Strong Consistency:**
  - Every read returns the latest write.
  - Good for banking, payments, critical systems.
  - Example: Traditional SQL databases.

- **Eventual Consistency:**
  - Data may take time to sync across servers.
  - Reads might be slightly outdated, but eventually consistent.
  - Good for large distributed systems.
  - Example: DynamoDB, Cassandra.

---

## 6. Fault Tolerance & Replication

- **Fault Tolerance:**
  - System continues to work even if parts fail.
  - Achieved using redundancy, retries, failover.

- **Replication:**
  - Copying data across multiple machines/regions.
  - Ensures high availability and disaster recovery.
  - Types:
    - **Synchronous:** Write confirmed only after all replicas update (slower but safer).
    - **Asynchronous:** Write confirmed after master, replicas update later (faster but risk of data loss).
