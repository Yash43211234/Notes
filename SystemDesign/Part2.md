# 🌐 System Design – Networking & Communication (Detailed Easy Notes)

---

## 1. HTTP/HTTPS Basics  

🔹 **HTTP (HyperText Transfer Protocol):**  
- A protocol for communication between client (browser/app) and server.  
- Works in a request–response model.  
- Example: Browser requests a page → server responds with HTML.  

🔹 **HTTPS (HTTP Secure):**  
- Same as HTTP, but encrypted with **SSL/TLS**.  
- Ensures:  
  - **Encryption** (data hidden from attackers).  
  - **Authentication** (server identity is verified).  
  - **Integrity** (data not modified in between).  

👉 Always use HTTPS in modern systems.  

---

## 2. WebSockets, REST vs GraphQL  

🔹 **WebSockets:**  
- Provides **two-way real-time communication** between client and server.  
- Once a connection is open, both sides can send messages anytime.  
- Example: Chat apps, live scores, stock prices.  

🔹 **REST (Representational State Transfer):**  
- Standard API style using HTTP methods (GET, POST, PUT, DELETE).  
- Each resource has a unique URL.  
- Example:  
  - `GET /users/101` → fetch user with ID 101.  
  - `POST /users` → create new user.  

🔹 **GraphQL:**  
- Query language for APIs.  
- Client asks exactly what it needs (not too much, not too little).  
- Example: Instead of making multiple API calls, one query can fetch **user + posts + comments** together.  

👉 REST is simple & widely used. GraphQL is powerful when data needs are complex.  

---

## 3. APIs – Rate Limiting & Authentication  

🔹 **Rate Limiting:**  
- Limits how many requests a client can make in a time period.  
- Protects system from abuse (DDOS attacks, too many requests).  
- Example: GitHub API → 5000 requests per hour per user.  

🔹 **Authentication:**  
Verifying the identity of a user/client.  

- **OAuth (Open Authorization):**  
  - Allows apps to access user data without sharing passwords.  
  - Example: Login with Google/Facebook.  

- **JWT (JSON Web Token):**  
  - A secure token format containing user info.  
  - Sent with each request (usually in headers).  
  - Example: After login, server gives a token → client uses it for future requests.  

👉 Most modern APIs use **OAuth + JWT** together.  

---

## 4. gRPC Basics  

- gRPC = **Google Remote Procedure Call**.  
- Faster and more efficient than REST (uses HTTP/2 and Protobuf).  
- Supports **bi-directional streaming**.  
- Example: Microservices inside Google, Netflix, etc. use gRPC to talk with each other.  

👉 Use gRPC when services need **fast internal communication**, REST/GraphQL for external clients.  

---

## 5. DNS & CDN Working  

🔹 **DNS (Domain Name System):**  
- Converts domain names into IP addresses.  
- Example: `www.google.com` → `142.250.183.110`.  
- Works like a phonebook of the internet.  

Steps:  
1. Browser asks DNS resolver for IP.  
2. Resolver queries root → TLD → authoritative servers.  
3. Gets IP and returns it to the browser.  

---

🔹 **CDN (Content Delivery Network):**  
- A network of servers placed globally.  
- Stores copies of static content (images, videos, CSS, JS).  
- Delivers data from the **nearest server** to user → reduces latency.  

Example: Netflix, YouTube, Amazon → videos load faster using CDN.  

👉 Popular CDNs: Cloudflare, Akamai, AWS CloudFront.  

---

## ✅ Summary of Concepts  

- **HTTP/HTTPS:** Request–response protocol (HTTPS is encrypted & secure).  
- **WebSockets:** Real-time 2-way communication.  
- **REST vs GraphQL:** REST = simple, GraphQL = flexible queries.  
- **Rate Limiting:** Prevents abuse.  
- **OAuth, JWT:** Secure authentication.  
- **gRPC:** High-performance internal service communication.  
- **DNS:** Converts domain → IP.  
- **CDN:** Delivers content from nearest server for speed.  
