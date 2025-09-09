# 🧪 System Design Case Studies (Must Practice)

> Flow to follow in interviews: **clarify requirements → list constraints → rough scale → draw HLD → walk through components & data → discuss scaling & trade-offs**.

---

## 1) Design a URL Shortener (Bitly)

### Requirements
- Shorten long URL → short code (e.g., `abc123`).
- Redirect fast.
- Optional: custom alias, link expiry, click analytics, rate limit.

### Constraints / Scale (assume)
- 100M links total, 1B redirects/day, read-heavy.
- Low latency (< 50ms), high availability.

### High-Level
Client → API → App Service → Cache → DB (primary) → Analytics pipeline (async)
+ Background workers for expiry/cleanup.

### Core Components
- API service (create/resolve).
- ID/Code generator (hash + base62, or counter + base62).
- Cache (Redis) for hot redirects.
- DB: Key-Value / NoSQL for `code → longURL, meta`.
- Analytics: Kafka → Stream processor → OLAP store.

### Data Model (NoSQL doc)
- `Link { code, longUrl, createdAt, expiresAt?, ownerId?, clickCount }`
- `ClickEvent { code, ts, ip, ua, ref }` (append-only stream)

### APIs
- `POST /shorten { longUrl, custom?, expiresAt? } -> { code, shortUrl }`
- `GET /:code -> 302 longUrl`
- `GET /stats/:code -> { clicks, ... }`

### Scaling
- Cache hot codes (TTL).
- Read replicas; CDN for redirect response if static 302 allowed.
- Partition by code; pre-generate codes if needed.
- Rate limiting per IP/user.

### Trade-offs
- Hash collisions vs sequential IDs (guessability).
- Strong vs eventual consistency for click counts.
- Cache freshness vs write complexity.

---

## 2) Design a Chat App (WhatsApp/Messenger)

### Requirements
- 1:1 and group chat, delivery & read receipts, online status.
- Mobile first, unreliable networks, end-to-end encryption (optional).

### Constraints
- High fan-out for groups; typing indicators near-real-time.
- Message ordering per conversation.

### High-Level
Client ↔ Gateway (WebSockets/GRPC) ↔ Chat Service ↔ Message Store
Presence Service, Notification Service, Media Service (S3+CDN),
Queue/Stream (Kafka), Push (FCM/APNs).

### Components
- Connection/Gateway (sticky, token auth).
- Message service (persist, route, ACKs).
- Presence service (last seen, online).
- Delivery worker (fan-out to recipients).
- Media upload (signed URLs → Object storage).

### Data Model
- `Conversation { id, type, members[] }`
- `Message { id, convId, senderId, ts, text|mediaRef, status }`
- `UserPresence { userId, lastSeen, state }`

### APIs/Protocols
- WebSocket events: `SendMessage`, `Delivered`, `Read`, `Typing`.
- REST for history: `GET /conversations/:id/messages?cursor`.
- Signed upload URLs for media.

### Scaling
- Shard by `convId`; ordered writes within shard.
- Write-ahead log; CQRS for search/analytics.
- Fan-out on write vs on read (trade-off based on read patterns).
- Cache recent messages; cold storage for old media.

### Trade-offs
- E2EE vs server-side features (search, moderation).
- Delivery latency vs durability (sync/async replication).

---

## 3) Design a News Feed (Facebook/Instagram)

### Requirements
- Personalized feed from follow graph.
- Ads/injection, ranking, freshness, infinite scroll.

### Constraints
- Heavy read, high fan-out; low tail latency.

### High-Level
Ingestion (posts) → Fanout (write/read hybrid) → Feed Store
Ranking Service (features + model) → API → Cache/CDN (images).

### Components
- Post service, Social graph, Fanout workers.
- Feed generator (per user feed lists).
- Ranking (features: recency, affinity, quality; ML model).
- Search/Hashtags, Notifications.

### Data Model
- `Post { id, authorId, ts, text, mediaRef, metrics }`
- `Edge { followerId, followeeId }`
- `FeedItem { userId, postId, score, ts }`

### APIs
- `GET /feed?cursor` (returns ranked feed items).
- `POST /post`, `POST /follow`.

### Scaling
- Hot author optimization (celebs): fan-out on read + cache.
- Precompute top-K per user; incremental merges.
- Denormalized counters via streams.
- Media on CDN.

### Trade-offs
- Fan-out on write (fast read, expensive write) vs read.
- Freshness vs ranking compute cost.

---

## 4) Design Video Streaming (YouTube/Netflix)

### Requirements
- Upload, transcode multi-bitrates, playback on many devices.
- Adaptive bitrate streaming (HLS/DASH), DRM, CDN delivery.
- Search, recommendations.

### High-Level
Upload → Object Store → Transcoding Pipeline → Manifest (HLS/DASH)
CDN edge delivery; Playback Service; Analytics stream.

### Components
- Upload service (signed URLs).
- Transcoder (workers, queue).
- Metadata service (title, tags).
- Playback (serves manifests, DRM keys).
- Recommendation pipeline (batch + real-time).

### Data Model
- `Video { id, ownerId, metadata, status }`
- `Variant { videoId, bitrate, resolution, segmentRefs }`
- `PlayEvent { videoId, ts, position, device }`

### Scaling
- Massive CDN offload; origin shield.
- Chunked segments; prefetch manifests.
- Parallel transcodes; retry/idempotency.

### Trade-offs
- Storage cost vs quality ladder depth.
- Latency to first frame vs encryption/DRM overhead.

---

## 5) Design E-commerce (Cart, Inventory)

### Requirements
- Browse/search, cart, checkout, orders, payments, inventory.
- Consistency of stock; promotions; order tracking.

### High-Level
API Gateway → Services: Catalog, Search, Cart, Order, Payment, Inventory, User
DBs per service; Cache; Message bus for events; Object store for images; CDN.

### Components
- Catalog (read-heavy; cache, search index).
- Cart (session or user-bound; Redis + DB).
- Inventory (atomic reservations).
- Order service (saga/orchestration with Payment, Inventory, Shipping).
- Payment gateway integration; webhooks.

### Data Model
- `Product { id, title, price, stock, attrs }`
- `Cart { userId, items[{productId, qty}] }`
- `Order { id, userId, items, amount, status }`
- `Inventory { productId, available, reserved }`

### APIs
- `GET /products?query`, `POST /cart/items`, `POST /checkout`.
- Webhooks: payment success/failure.

### Scaling
- Read replicas + cache for catalog.
- Inventory reservations via atomic ops / pessimistic locks / queue.
- Event-driven order pipeline (saga, outbox).

### Trade-offs
- Strong stock consistency vs cart UX.
- Denormalization for speed vs write complexity.

---

## 6) Design Ride Sharing (Uber/Ola)

### Requirements
- Rider app, driver app, matching, live location, ETA, pricing, surge.
- Real-time maps; trip states; payments.

### High-Level
Location stream (drivers) → Spatial index (geo-grid) → Matcher
Trip Service, Pricing Service, Routing (maps), Notification, Payments.

### Components
- Realtime gateway (WebSockets/GRPC).
- Geo-index (quad-tree/geo-hash buckets in Redis/Elastic).
- Matching engine (nearest drivers + constraints).
- Trip lifecycle FSM; fare calculation; receipts.

### Data Model
- `DriverLocation { driverId, lat, lon, ts, state }`
- `Trip { id, riderId, driverId?, status, route, fare }`

### APIs
- `POST /requestRide { pickup, drop } -> tripId`
- Streaming updates: driver positions, trip status.

### Scaling
- Partition by city/region; local affinity.
- Rate limit location updates; delta compression.
- Caching static map tiles via CDN.

### Trade-offs
- Optimal matching vs latency.
- Surge transparency vs gaming.

---

## 7) Design File Storage (Google Drive/Dropbox)

### Requirements
- Upload/download/sync, sharing, permissions, versioning, previews.

### High-Level
Client Sync ↔ Metadata Service ↔ Object Storage (chunks) ↔ Index/Search
Sharing/ACL service; Preview service; Event stream for sync.

### Components
- Chunked uploads with resumable sessions.
- Deduplication (content-hash).
- Versioning; trash/restore; sharing links with scopes.

### Data Model
- `File { id, ownerId, name, size, hashes[], version, parents[] }`
- `Chunk { fileId, idx, hash, location }`
- `ACL { resourceId, subject, role }`

### APIs
- `POST /files`, `PATCH /files/:id`, `GET /files/:id/content` (signed URLs).
- Webhooks for sync clients.

### Scaling
- Hot files cached at edge; multipart uploads.
- Background GC for orphaned chunks.
- Consistent hashing for chunk placement.

### Trade-offs
- Strong metadata consistency vs sync speed.
- Storage cost vs dedupe/erasure coding complexity.

---

## 8) Design a Rate Limiter (API Protection)

### Requirements
- Limit requests per key/IP (e.g., 100 req/min).
- Global + per-endpoint limits; sliding window fairness.
- Low latency, distributed.

### High-Level
Client → API Gateway → Rate-Limiter (Redis) → Upstream services
Counters/Token buckets stored in Redis/Memory with TTL.

### Algorithms
- **Token Bucket** (burst friendly).
- **Leaky Bucket** (steady outflow).
- **Fixed Window / Sliding Window** (accuracy vs cost).

### Data Model (in Redis)
- Keys like `rate:{apiKey}:{windowStart}` → count.
- Or `token:{apiKey}` → remaining tokens + refill rate.

### APIs
- Middleware check before routing.
- `429 Too Many Requests` with `Retry-After` header.

### Scaling
- Shard by `apiKey` via consistent hashing.
- Lua scripts for atomic ops; pipelining.
- Local LRU cache for ultra-hot keys; sync via pub/sub.

### Trade-offs
- Exactness vs performance (sliding window is costlier).
- Centralized vs decentralized limits (edge vs core).
