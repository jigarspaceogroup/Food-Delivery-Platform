# Technical Specification Outline

## Food Delivery Platform - White-Label Solution

| Field | Detail |
|---|---|
| **Project Name** | Food Delivery Platform |
| **Document Type** | Technical Specification |
| **Version** | v1.0 |
| **Date** | March 2026 |
| **Based On** | PROJECT_SCOPE.md v1.1 |
| **Target Market** | Saudi Arabia |
| **Phase** | Phase 1 (MVP) |

---

## Table of Contents

1. [Architecture Overview](#1-architecture-overview)
2. [Tech Stack Details](#2-tech-stack-details)
3. [Database Schema](#3-database-schema)
4. [API Endpoints](#4-api-endpoints)
5. [Authentication Flow](#5-authentication-flow)
6. [Real-Time Architecture](#6-real-time-architecture)
7. [Payment Architecture](#7-payment-architecture)
8. [Deployment Strategy](#8-deployment-strategy)
9. [Testing Strategy](#9-testing-strategy)
10. [Monitoring and Logging](#10-monitoring-and-logging)
11. [Security Considerations](#11-security-considerations)
12. [White-Label Architecture](#12-white-label-architecture)
13. [Localization and RTL Strategy](#13-localization-and-rtl-strategy)
14. [Third-Party Integration Details](#14-third-party-integration-details)
15. [Performance Requirements and Targets](#15-performance-requirements-and-targets)

---

## 1. Architecture Overview

### 1.1 System Architecture Diagram (Text Description)

```
+------------------------------------------------------------------+
|                        CLIENT LAYER                               |
|                                                                   |
|  +----------------+  +----------------+  +---------------------+  |
|  | Customer App   |  | Driver App     |  | Restaurant          |  |
|  | (React Native) |  | (React Native) |  | Dashboard           |  |
|  | Android Only   |  | Android Only   |  | (React.js SPA)      |  |
|  +-------+--------+  +-------+--------+  +----------+----------+  |
|          |                    |                       |            |
|  +-------+--------+          |                       |            |
|  | Customer Web   |          |                       |            |
|  | (React/Next.js)|          |                       |            |
|  | Lightweight    |          |                       |            |
|  +-------+--------+          |                       |            |
+---------|--------------------|------ ----------------|------------+
           |                    |                       |
+---------v--------------------v-----------------------v------------+
|                       API GATEWAY LAYER                           |
|                                                                   |
|  +-------------------------------------------------------------+ |
|  | AWS API Gateway / Nginx Reverse Proxy                        | |
|  | - Rate limiting          - Request routing                   | |
|  | - SSL termination        - Load balancing                    | |
|  | - API key validation     - Request/response logging          | |
|  +-------------------------------------------------------------+ |
+------------------------------------------------------------------+
           |                    |                       |
+----------v--------------------v-----------------------v-----------+
|                    MICROSERVICES LAYER                             |
|                   (Docker Containers on AWS ECS)                  |
|                                                                   |
|  +-------------+ +-------------+ +-------------+ +-------------+ |
|  | Auth        | | User        | | Menu        | | Order       | |
|  | Service     | | Service     | | Service     | | Service     | |
|  +-------------+ +-------------+ +-------------+ +-------------+ |
|  +-------------+ +-------------+ +-------------+ +-------------+ |
|  | Cart        | | Payment     | | Delivery    | | Notification| |
|  | Service     | | Service     | | Service     | | Service     | |
|  +-------------+ +-------------+ +-------------+ +-------------+ |
|  +-------------+ +-------------+ +-------------+ +-------------+ |
|  | Promo &     | | Analytics   | | Support     | | Config      | |
|  | Loyalty Svc | | Service     | | Service     | | Service     | |
|  +-------------+ +-------------+ +-------------+ +-------------+ |
+------------------------------------------------------------------+
           |                    |                       |
+----------v--------------------v-----------------------v-----------+
|                       DATA LAYER                                  |
|                                                                   |
|  +----------------+  +----------------+  +---------------------+  |
|  | PostgreSQL     |  | Redis          |  | AWS S3              |  |
|  | (AWS RDS)      |  | (ElastiCache)  |  | File Storage        |  |
|  | Primary DB     |  | Cache + Queues |  | Images, Docs        |  |
|  +----------------+  +----------------+  +---------------------+  |
+------------------------------------------------------------------+
           |                    |                       |
+----------v--------------------v-----------------------v-----------+
|                  EXTERNAL INTEGRATIONS                            |
|                                                                   |
|  +----------+ +----------+ +----------+ +----------+ +----------+ |
|  | Stripe   | | Google   | | Firebase | | Firebase | | STC Pay  | |
|  | Payments | | Maps API | | Auth     | | FCM      | | API      | |
|  +----------+ +----------+ +----------+ +----------+ +----------+ |
+------------------------------------------------------------------+
```

### 1.2 Microservices Breakdown

#### 1. Auth Service

| Attribute | Detail |
|---|---|
| **Responsibility** | Firebase Auth integration, JWT token issuance and validation, OTP verification orchestration, social login (Google, Facebook), session management, token refresh |
| **Tech** | Node.js + Express.js, Firebase Admin SDK, jsonwebtoken |
| **Database Schema Ownership** | `auth_sessions`, `refresh_tokens`, `social_accounts` |
| **API Prefix** | `/api/v1/auth` |
| **Dependencies** | Firebase Authentication (external), User Service (for profile creation on registration) |
| **Port** | 3001 |

#### 2. User Service

| Attribute | Detail |
|---|---|
| **Responsibility** | Customer profiles, driver profiles, restaurant admin accounts, address management, dietary preferences, avatar/document uploads, user status management |
| **Tech** | Node.js + Express.js, Prisma ORM |
| **Database Schema Ownership** | `users`, `customers`, `drivers`, `restaurant_admins`, `addresses`, `notification_preferences` |
| **API Prefix** | `/api/v1/users`, `/api/v1/addresses` |
| **Dependencies** | Auth Service (token validation), File Service (avatar/document uploads to S3) |
| **Port** | 3002 |

#### 3. Menu Service

| Attribute | Detail |
|---|---|
| **Responsibility** | Menu item CRUD, category management (hierarchical), item variants (size, toppings, modifications), nutrition/allergy info, availability toggling, favorites, multi-branch menu support, popular items tracking, menu search with auto-suggest |
| **Tech** | Node.js + Express.js, Prisma ORM, PostgreSQL full-text search |
| **Database Schema Ownership** | `menu_categories`, `menu_items`, `menu_item_variants`, `favorites` |
| **API Prefix** | `/api/v1/menu` |
| **Dependencies** | Config Service (branch validation), File Service (menu item images) |
| **Port** | 3003 |

#### 4. Order Service

| Attribute | Detail |
|---|---|
| **Responsibility** | Order creation from cart, order lifecycle management (status transitions), order status history, order history retrieval, reordering, order cancellation, VAT-compliant receipt generation, scheduled orders |
| **Tech** | Node.js + Express.js, Prisma ORM, BullMQ (async order processing) |
| **Database Schema Ownership** | `orders`, `order_items`, `order_status_history` |
| **API Prefix** | `/api/v1/orders` |
| **Dependencies** | Cart Service (cart-to-order conversion), Payment Service (payment processing), Delivery Service (driver assignment), Notification Service (order status notifications), Menu Service (item validation and pricing) |
| **Port** | 3004 |

#### 5. Cart Service

| Attribute | Detail |
|---|---|
| **Responsibility** | Cart management (add/remove/update items), promo code validation and application, VAT calculation (15%), delivery fee inclusion, upsell rule execution, cart-to-order preparation |
| **Tech** | Node.js + Express.js, Prisma ORM, Redis (cart caching for performance) |
| **Database Schema Ownership** | `carts`, `cart_items` |
| **API Prefix** | `/api/v1/cart` |
| **Dependencies** | Menu Service (item validation, pricing), Promo & Loyalty Service (promo code validation), Delivery Service (delivery fee calculation), Config Service (VAT rate) |
| **Port** | 3005 |

#### 6. Payment Service

| Attribute | Detail |
|---|---|
| **Responsibility** | Stripe payment intent creation and confirmation, Mada card processing (via Stripe), Google Pay processing (via Stripe), STC Pay integration, COD order handling, saved card management, refund processing (technical failures only), transaction record keeping, Stripe webhook handling |
| **Tech** | Node.js + Express.js, Stripe SDK, Prisma ORM |
| **Database Schema Ownership** | `payments`, `saved_cards`, `refunds` |
| **API Prefix** | `/api/v1/payments` |
| **Dependencies** | Order Service (order total verification), Stripe (external), STC Pay API (external) |
| **Port** | 3006 |

#### 7. Delivery Service

| Attribute | Detail |
|---|---|
| **Responsibility** | Driver assignment (manual by restaurant + auto-suggest nearest available), GPS location tracking and broadcasting, route management, delivery zone definition and management (polygon-based), zone-based delivery fee calculation, ETA estimation using Google Maps Distance Matrix API, driver availability management |
| **Tech** | Node.js + Express.js, Prisma ORM, Socket.io (GPS broadcasting), PostGIS (geospatial queries) |
| **Database Schema Ownership** | `delivery_zones`, `driver_locations` (Redis for real-time, PostgreSQL for historical), `delivery_assignments` |
| **API Prefix** | `/api/v1/delivery` |
| **Dependencies** | User Service (driver profiles), Google Maps API (external), Order Service (order details), Notification Service (driver notifications) |
| **Port** | 3007 |

#### 8. Notification Service

| Attribute | Detail |
|---|---|
| **Responsibility** | Push notification dispatch via FCM, email campaign sending, in-app notification storage and retrieval, notification preference management, notification template management (Arabic/English), segmented notification targeting |
| **Tech** | Node.js + Express.js, Firebase Admin SDK (FCM), BullMQ (async dispatch), Prisma ORM |
| **Database Schema Ownership** | `notifications`, `notification_templates`, `notification_preferences`, `email_campaigns` |
| **API Prefix** | `/api/v1/notifications` |
| **Dependencies** | Firebase Cloud Messaging (external), Email Service Provider (external, [TBD - AWS SES recommended]), User Service (user tokens and preferences) |
| **Port** | 3008 |

#### 9. Promo & Loyalty Service

| Attribute | Detail |
|---|---|
| **Responsibility** | Promo code CRUD and validation, discount campaign management, loyalty points framework (earn/redeem), loyalty account management, redemption processing, loyalty configuration per restaurant (points per SAR, redemption rate) |
| **Tech** | Node.js + Express.js, Prisma ORM |
| **Database Schema Ownership** | `promo_codes`, `promo_usage`, `loyalty_accounts`, `loyalty_transactions`, `loyalty_config` |
| **API Prefix** | `/api/v1/promos`, `/api/v1/loyalty` |
| **Dependencies** | Order Service (order total for points calculation), User Service (customer identification), Config Service (restaurant-specific loyalty rules) |
| **Port** | 3009 |

#### 10. Analytics Service

| Attribute | Detail |
|---|---|
| **Responsibility** | Sales reports (daily, weekly, monthly, custom range), customer analytics (new vs returning, order frequency, average order value), popular items analysis, driver performance metrics (delivery times, completion rates, ratings), revenue tracking, export capabilities (CSV, PDF) |
| **Tech** | Node.js + Express.js, Prisma ORM (read replicas for heavy queries) |
| **Database Schema Ownership** | `analytics_snapshots` (pre-aggregated data), reads from Order, User, Delivery schemas |
| **API Prefix** | `/api/v1/analytics` |
| **Dependencies** | Order Service (order data), User Service (customer data), Delivery Service (driver performance data) |
| **Port** | 3010 |

#### 11. Support Service

| Attribute | Detail |
|---|---|
| **Responsibility** | Support ticket creation and management, customer-restaurant communication, issue categorization and prioritization, ticket status tracking, attachment handling |
| **Tech** | Node.js + Express.js, Prisma ORM |
| **Database Schema Ownership** | `support_tickets`, `support_messages` |
| **API Prefix** | `/api/v1/support` |
| **Dependencies** | User Service (user identification), Order Service (order reference), File Service (attachment uploads), Notification Service (ticket update notifications) |
| **Port** | 3011 |

#### 12. Config Service

| Attribute | Detail |
|---|---|
| **Responsibility** | White-label branding configuration (colors, logos, app name), system settings management, operating hours configuration, branch management (multi-branch CRUD), delivery zone management (polygon drawing on map), VAT/tax rate configuration, minimum order amount settings |
| **Tech** | Node.js + Express.js, Prisma ORM, Redis (config caching) |
| **Database Schema Ownership** | `restaurants`, `branches`, `system_settings`, `branding_config` |
| **API Prefix** | `/api/v1/config`, `/api/v1/branches` |
| **Dependencies** | File Service (logo/asset uploads) |
| **Port** | 3012 |

#### 13. File Service (Lightweight / Shared Utility)

| Attribute | Detail |
|---|---|
| **Responsibility** | File upload to AWS S3, image resizing/optimization, presigned URL generation, file deletion, file type validation |
| **Tech** | Node.js + Express.js, AWS SDK (S3), Sharp (image processing) |
| **Database Schema Ownership** | None (files tracked by owning services) |
| **API Prefix** | `/api/v1/files` |
| **Dependencies** | AWS S3 (external) |
| **Port** | 3013 |

### 1.3 Communication Patterns

#### Synchronous Communication (REST APIs)
- All client-to-service communication uses REST over HTTPS
- Inter-service synchronous calls use internal HTTP with service discovery
- Request/response pattern for CRUD operations, queries, and commands that need immediate confirmation

#### Real-Time Communication (Socket.io)
- Dedicated Socket.io server running alongside the Delivery Service
- Namespaces: `/tracking`, `/orders`, `/notifications`
- Used for: live GPS updates, order status changes, new order alerts for restaurant dashboard, driver assignment notifications

#### Asynchronous Communication (BullMQ + Redis)
- Event-driven architecture for decoupled service communication
- Key async flows:
  - `order.placed` -> Notification Service (notify restaurant), Delivery Service (prepare for assignment)
  - `order.accepted` -> Notification Service (notify customer), Delivery Service (suggest driver)
  - `order.status_changed` -> Notification Service (push to customer), Analytics Service (record event)
  - `payment.confirmed` -> Order Service (update order status)
  - `payment.failed` -> Order Service (mark order failed), Notification Service (notify customer)
  - `driver.assigned` -> Notification Service (notify driver + customer)
  - `driver.location_updated` -> Delivery Service (broadcast via Socket.io)
  - `loyalty.order_completed` -> Promo & Loyalty Service (calculate and credit points)

#### Message Queue Topics

| Queue Name | Producer | Consumer(s) | Description |
|---|---|---|---|
| `order-events` | Order Service | Notification, Delivery, Analytics, Loyalty | Order lifecycle events |
| `payment-events` | Payment Service | Order Service, Notification | Payment status changes |
| `delivery-events` | Delivery Service | Notification, Order, Analytics | Delivery assignment and status |
| `notification-dispatch` | Any Service | Notification Service | Notification send requests |
| `analytics-events` | Multiple Services | Analytics Service | Events for analytics aggregation |
| `file-processing` | File Service | File Service (workers) | Image resize/optimization jobs |

### 1.4 Service Discovery and Routing

- **API Gateway**: Nginx reverse proxy routes requests to appropriate services based on URL prefix
- **Internal Communication**: Services communicate via internal Docker network using service names
- **Health Checks**: Each service exposes `GET /health` endpoint returning service status, version, and uptime
- **Service Registry**: Docker Compose (development), AWS ECS Service Discovery (staging/production)

---

## 2. Tech Stack Details

### 2.1 Frontend

#### Customer App (Android)

| Component | Technology | Version | Notes |
|---|---|---|---|
| Framework | React Native | 0.76+ (latest stable) | Android only, no iOS builds |
| Language | TypeScript | 5.x | Strict mode enabled |
| Navigation | React Navigation | 7.x | Stack, Tab, Drawer navigators |
| State Management | Redux Toolkit | 2.x | With RTK Query for API caching |
| UI Component Library | React Native Paper | 5.x | Material Design 3, RTL support built-in |
| Maps | react-native-maps | latest | Google Maps provider |
| Real-time | socket.io-client | 4.x | Live tracking, order updates |
| Forms | React Hook Form | 7.x | With Zod schema validation |
| i18n | react-i18next | 14.x | Arabic/English, RTL auto-detection |
| HTTP Client | Axios | 1.x | With interceptors for auth tokens |
| Push Notifications | @react-native-firebase/messaging | latest | FCM integration |
| Auth | @react-native-firebase/auth | latest | Phone OTP, social login |
| Storage | @react-native-async-storage/async-storage | latest | Local persistence |
| Image Loading | react-native-fast-image | latest | Cached image loading |
| Payments | @stripe/stripe-react-native | latest | Stripe SDK for Android |
| Geolocation | react-native-geolocation-service | latest | GPS for address pin-drop |
| Animations | react-native-reanimated | 3.x | Smooth UI transitions |
| Build Tool | Gradle | latest | Android build system |

#### Customer Web (Lightweight)

| Component | Technology | Version | Notes |
|---|---|---|---|
| Framework | Next.js | 14+ (latest stable) | SSR for SEO (menu pages), App Router |
| Language | TypeScript | 5.x | Strict mode |
| State Management | Redux Toolkit | 2.x | Shared logic with mobile via RTK Query |
| UI Component Library | Tailwind CSS + Headless UI | latest | Custom components, RTL via `dir="rtl"` |
| Maps | @react-google-maps/api | latest | Address selection, branch map |
| Real-time | socket.io-client | 4.x | Order tracking |
| Forms | React Hook Form + Zod | latest | Validation |
| i18n | next-intl | latest | Arabic/English with SSR support |
| HTTP Client | Axios | 1.x | API communication |
| Payments | @stripe/stripe-js + @stripe/react-stripe-js | latest | Stripe Elements for PCI compliance |
| Analytics | Google Analytics 4 | latest | User behavior tracking |

#### Driver App (Android)

| Component | Technology | Version | Notes |
|---|---|---|---|
| Framework | React Native | 0.76+ (latest stable) | Android only |
| Language | TypeScript | 5.x | Strict mode |
| Navigation | React Navigation | 7.x | Simplified navigation (fewer screens) |
| State Management | Redux Toolkit | 2.x | Driver-specific state |
| UI Component Library | React Native Paper | 5.x | Material Design 3, RTL support |
| Maps | react-native-maps | latest | Navigation, route display |
| Real-time | socket.io-client | 4.x | Location broadcasting, order updates |
| Background Location | react-native-background-geolocation | latest | GPS tracking while app is backgrounded |
| Forms | React Hook Form + Zod | latest | Issue reporting, profile forms |
| i18n | react-i18next | 14.x | Arabic/English |
| HTTP Client | Axios | 1.x | API communication |
| Push Notifications | @react-native-firebase/messaging | latest | Order assignment alerts |
| Phone/SMS | react-native-communications | latest | Direct call/message to customer |

#### Restaurant Web Dashboard

| Component | Technology | Version | Notes |
|---|---|---|---|
| Framework | React.js | 18+ | SPA with client-side routing |
| Build Tool | Vite | 5.x | Fast dev server and builds |
| Language | TypeScript | 5.x | Strict mode |
| Routing | React Router | 6.x | Nested routes for dashboard sections |
| State Management | Redux Toolkit | 2.x | Complex dashboard state |
| UI Component Library | Ant Design | 5.x | Enterprise dashboard components, RTL support |
| Charts | Recharts | 2.x | Sales reports, analytics visualizations |
| Maps | @react-google-maps/api | latest | Delivery zones (polygon drawing), driver tracking |
| Real-time | socket.io-client | 4.x | Live order board, driver tracking |
| Forms | React Hook Form + Zod | latest | Menu management, settings forms |
| i18n | react-i18next | 14.x | Arabic/English, RTL |
| HTTP Client | Axios | 1.x | API communication |
| Table/Data Grid | Ant Design Table | 5.x | Order lists, customer database, reports |
| Date Handling | date-fns | 3.x | Date formatting, Hijri calendar support via plugin |
| Export | xlsx + jspdf | latest | Report export (CSV, PDF) |
| Rich Text | React Quill | latest | Email campaign editor |
| Image Upload | react-dropzone | latest | Menu item images, branding assets |

### 2.2 Backend

| Component | Technology | Version | Notes |
|---|---|---|---|
| Runtime | Node.js | 20 LTS (v20.x) | Long-term support release |
| Language | TypeScript | 5.x | Strict mode, all services |
| Framework | Express.js | 4.x | REST API framework |
| ORM | Prisma | 5.x | Type-safe PostgreSQL queries, migrations |
| Validation | Zod | 3.x | Request/response schema validation |
| Auth - Firebase | firebase-admin | 12.x | OTP verification, social login validation |
| Auth - JWT | jsonwebtoken | 9.x | Token issuance, validation |
| Real-time | socket.io | 4.x | WebSocket server |
| Message Queue | BullMQ | 5.x | Async job processing, event dispatch |
| Cache Client | ioredis | 5.x | Redis connection for caching, queues |
| Logging | Winston | 3.x | Structured logging with log levels |
| HTTP Logging | Morgan | 1.x | HTTP request logging middleware |
| API Documentation | Swagger (swagger-jsdoc + swagger-ui-express) | latest | OpenAPI 3.0 spec |
| Testing | Jest | 29.x | Unit and integration tests |
| API Testing | Supertest | 6.x | HTTP assertion library |
| Payment | stripe | latest | Stripe Node.js SDK |
| Email | @aws-sdk/client-ses | latest | AWS SES for transactional and marketing emails |
| File Upload | multer | 1.x | Multipart form data handling |
| AWS S3 | @aws-sdk/client-s3 | latest | File storage operations |
| Image Processing | sharp | 0.33.x | Image resize, format conversion |
| Rate Limiting | express-rate-limit | 7.x | API rate limiting |
| CORS | cors | 2.x | Cross-origin resource sharing |
| Helmet | helmet | 7.x | Security headers |
| Compression | compression | 1.x | Response compression |
| Geospatial | PostGIS via Prisma raw queries | N/A | Polygon containment, distance calculations |
| Scheduler | node-cron | 3.x | Scheduled tasks (analytics aggregation, promo expiry) |
| UUID | uuid | 9.x | Unique identifier generation |

### 2.3 Database

| Component | Technology | Version | Notes |
|---|---|---|---|
| Primary Database | PostgreSQL | 16.x | All transactional data, PostGIS extension for geospatial |
| Cache / Queue Backend | Redis | 7.x | Session cache, BullMQ backend, real-time data (driver locations), rate limiting counters |
| File Storage | AWS S3 | N/A | Menu images, driver documents, branding assets, receipts |
| Search | PostgreSQL Full-Text Search + pg_trgm | Built-in | Menu search, auto-suggest (trigram similarity for fuzzy matching) |

### 2.4 Infrastructure

| Component | Technology | Notes |
|---|---|---|
| Cloud Provider | AWS (me-south-1, Bahrain) | Saudi market proximity, data residency |
| Compute | AWS ECS Fargate | Serverless container orchestration, no EC2 management |
| Container Registry | AWS ECR | Private Docker image registry |
| Database Hosting | AWS RDS (PostgreSQL 16) | Multi-AZ deployment for high availability, automated backups |
| Cache Hosting | AWS ElastiCache (Redis 7) | Cluster mode, encryption at rest and in transit |
| Object Storage | AWS S3 | Versioning enabled, lifecycle policies for cost optimization |
| CDN | AWS CloudFront | Static assets, menu images, web app hosting |
| DNS | AWS Route 53 | Domain management, health check routing |
| SSL/TLS | AWS Certificate Manager | Free SSL certificates, auto-renewal |
| API Gateway | Nginx on ECS | Reverse proxy, rate limiting, SSL termination |
| Load Balancer | AWS Application Load Balancer (ALB) | HTTPS listener, path-based routing to ECS services |
| Monitoring | AWS CloudWatch | Logs, metrics, alarms |
| APM | Sentry | Application performance monitoring, error tracking |
| Log Aggregation | AWS CloudWatch Logs | Centralized log storage with log groups per service |
| Secrets Management | AWS Secrets Manager | API keys, database credentials, third-party secrets |
| Parameter Store | AWS Systems Manager Parameter Store | Non-sensitive configuration values |
| CI/CD | GitHub Actions | Build, test, deploy pipelines |
| IaC | AWS CDK (TypeScript) | Infrastructure as Code for reproducible environments |
| Email | AWS SES | Transactional emails, marketing campaigns |

---

## 3. Database Schema

### 3.1 Schema Overview

The database uses PostgreSQL 16 with the PostGIS extension for geospatial operations. Each microservice owns its schema tables but shares a single PostgreSQL instance (with logical separation via schemas) in Phase 1. Services access only their owned tables directly; cross-service data is accessed via API calls.

**Database Schemas (logical separation):**
- `auth` - Authentication and session data
- `users` - User profiles and addresses
- `menu` - Menu items, categories, variants
- `orders` - Orders, cart, order items
- `payments` - Payment transactions
- `delivery` - Delivery zones, driver locations
- `notifications` - Notification records and templates
- `promos` - Promo codes and loyalty
- `support` - Support tickets
- `config` - Restaurant and branch configuration
- `analytics` - Pre-aggregated analytics data

### 3.2 Detailed Table Definitions

#### Auth Schema

**Table: `auth.sessions`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | Session identifier |
| user_id | UUID | NOT NULL, FK -> users.users.id | Associated user |
| refresh_token | VARCHAR(512) | NOT NULL, UNIQUE | Hashed refresh token |
| device_info | JSONB | DEFAULT '{}' | Device metadata (OS, app version, device model) |
| ip_address | INET | | Last known IP |
| is_active | BOOLEAN | DEFAULT true | Session validity |
| expires_at | TIMESTAMPTZ | NOT NULL | Token expiration |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_sessions_user_id`, `idx_sessions_refresh_token`, `idx_sessions_expires_at`

**Table: `auth.social_accounts`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| user_id | UUID | NOT NULL, FK -> users.users.id | Associated user |
| provider | VARCHAR(20) | NOT NULL | 'google', 'facebook' |
| provider_user_id | VARCHAR(255) | NOT NULL | Provider's user identifier |
| email | VARCHAR(255) | | Email from provider |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_social_provider_uid` (UNIQUE on provider + provider_user_id)

#### Users Schema

**Table: `users.users`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| firebase_uid | VARCHAR(128) | UNIQUE | Firebase Authentication UID |
| type | VARCHAR(20) | NOT NULL | 'customer', 'driver', 'restaurant_admin', 'super_admin' |
| email | VARCHAR(255) | UNIQUE (nullable) | Email address |
| phone | VARCHAR(20) | UNIQUE (nullable) | Phone number (E.164 format, e.g., +966XXXXXXXXX) |
| name_en | VARCHAR(100) | | Full name in English |
| name_ar | VARCHAR(100) | | Full name in Arabic |
| avatar_url | VARCHAR(500) | | Profile picture S3 URL |
| language_pref | VARCHAR(5) | DEFAULT 'ar' | 'ar' or 'en' |
| status | VARCHAR(20) | DEFAULT 'active' | 'active', 'suspended', 'deactivated' |
| last_login_at | TIMESTAMPTZ | | |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_users_firebase_uid`, `idx_users_email`, `idx_users_phone`, `idx_users_type_status`

**Table: `users.customers`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| user_id | UUID | NOT NULL, UNIQUE, FK -> users.users.id ON DELETE CASCADE | |
| default_address_id | UUID | FK -> users.addresses.id | Default delivery address |
| dietary_preferences | JSONB | DEFAULT '[]' | Array of dietary tags (halal, vegetarian, etc.) |
| fcm_token | VARCHAR(500) | | Firebase Cloud Messaging token |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

**Table: `users.drivers`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| user_id | UUID | NOT NULL, UNIQUE, FK -> users.users.id ON DELETE CASCADE | |
| restaurant_id | UUID | NOT NULL, FK -> config.restaurants.id | Restaurant this driver belongs to |
| vehicle_type | VARCHAR(50) | | 'car', 'motorcycle', 'bicycle' |
| vehicle_number | VARCHAR(20) | | License plate |
| license_doc_url | VARCHAR(500) | | Driver license document S3 URL |
| id_doc_url | VARCHAR(500) | | National ID document S3 URL |
| is_available | BOOLEAN | DEFAULT false | Online/offline toggle |
| current_lat | DECIMAL(10, 8) | | Last known latitude |
| current_lng | DECIMAL(11, 8) | | Last known longitude |
| status | VARCHAR(20) | DEFAULT 'active' | 'active', 'suspended', 'inactive' |
| fcm_token | VARCHAR(500) | | Firebase Cloud Messaging token |
| rating_avg | DECIMAL(3, 2) | DEFAULT 0.00 | Average customer rating |
| total_deliveries | INTEGER | DEFAULT 0 | Lifetime delivery count |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_drivers_restaurant_id`, `idx_drivers_available` (WHERE is_available = true), `idx_drivers_location` (GiST index on point(current_lng, current_lat))

**Table: `users.restaurant_admins`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| user_id | UUID | NOT NULL, UNIQUE, FK -> users.users.id ON DELETE CASCADE | |
| restaurant_id | UUID | NOT NULL, FK -> config.restaurants.id | |
| role | VARCHAR(20) | DEFAULT 'admin' | 'owner', 'admin', 'manager', 'staff' |
| branch_id | UUID | FK -> config.branches.id (nullable) | If scoped to a specific branch |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_restaurant_admins_restaurant_id`

**Table: `users.addresses`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| customer_id | UUID | NOT NULL, FK -> users.customers.id ON DELETE CASCADE | |
| label | VARCHAR(50) | | 'Home', 'Work', 'Other', or custom label |
| address_line_1 | VARCHAR(255) | NOT NULL | Street address |
| address_line_2 | VARCHAR(255) | | Apartment, floor, building |
| city | VARCHAR(100) | | City name |
| district | VARCHAR(100) | | District/neighborhood |
| postal_code | VARCHAR(10) | | Saudi postal code |
| lat | DECIMAL(10, 8) | NOT NULL | Latitude from map pin-drop |
| lng | DECIMAL(11, 8) | NOT NULL | Longitude from map pin-drop |
| is_default | BOOLEAN | DEFAULT false | |
| additional_info | TEXT | | Delivery instructions, landmarks |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_addresses_customer_id`, `idx_addresses_location` (GiST index)

**Table: `users.notification_preferences`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| user_id | UUID | NOT NULL, UNIQUE, FK -> users.users.id ON DELETE CASCADE | |
| order_updates | BOOLEAN | DEFAULT true | Order status push notifications |
| promotions | BOOLEAN | DEFAULT true | Promotional push notifications |
| delivery_alerts | BOOLEAN | DEFAULT true | Delivery-related alerts |
| email_marketing | BOOLEAN | DEFAULT false | Email marketing campaigns |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

#### Config Schema

**Table: `config.restaurants`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| name_en | VARCHAR(200) | NOT NULL | Restaurant name in English |
| name_ar | VARCHAR(200) | NOT NULL | Restaurant name in Arabic |
| slug | VARCHAR(100) | NOT NULL, UNIQUE | URL-friendly identifier |
| logo_url | VARCHAR(500) | | Primary logo S3 URL |
| logo_dark_url | VARCHAR(500) | | Dark mode logo S3 URL |
| branding_config | JSONB | DEFAULT '{}' | See White-Label Architecture (Section 12) |
| default_language | VARCHAR(5) | DEFAULT 'ar' | 'ar' or 'en' |
| currency | VARCHAR(3) | DEFAULT 'SAR' | ISO currency code |
| vat_rate | DECIMAL(5, 2) | DEFAULT 15.00 | VAT percentage |
| vat_number | VARCHAR(50) | | Saudi VAT registration number |
| commercial_registration | VARCHAR(50) | | CR number |
| contact_email | VARCHAR(255) | | |
| contact_phone | VARCHAR(20) | | |
| status | VARCHAR(20) | DEFAULT 'active' | 'active', 'suspended', 'setup' |
| stripe_account_id | VARCHAR(255) | | Stripe Connect account ID |
| stc_pay_merchant_id | VARCHAR(255) | | STC Pay merchant identifier |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_restaurants_slug`

**Table: `config.branches`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| restaurant_id | UUID | NOT NULL, FK -> config.restaurants.id ON DELETE CASCADE | |
| name_en | VARCHAR(200) | NOT NULL | Branch name in English |
| name_ar | VARCHAR(200) | NOT NULL | Branch name in Arabic |
| address_en | VARCHAR(500) | | Address in English |
| address_ar | VARCHAR(500) | | Address in Arabic |
| lat | DECIMAL(10, 8) | NOT NULL | Branch latitude |
| lng | DECIMAL(11, 8) | NOT NULL | Branch longitude |
| phone | VARCHAR(20) | | Branch phone number |
| operating_hours | JSONB | NOT NULL | `{ "sun": { "open": "09:00", "close": "23:00" }, ... }` |
| is_accepting_orders | BOOLEAN | DEFAULT true | Can toggle orders on/off |
| is_active | BOOLEAN | DEFAULT true | Branch visibility |
| min_order_amount | DECIMAL(10, 2) | DEFAULT 0.00 | Minimum order in SAR |
| avg_preparation_time | INTEGER | DEFAULT 20 | Average prep time in minutes |
| supports_pickup | BOOLEAN | DEFAULT true | Pickup available |
| supports_delivery | BOOLEAN | DEFAULT true | Delivery available |
| sort_order | INTEGER | DEFAULT 0 | Display ordering |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_branches_restaurant_id`, `idx_branches_location` (GiST), `idx_branches_active` (WHERE is_active = true)

**Table: `config.system_settings`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| restaurant_id | UUID | NOT NULL, FK -> config.restaurants.id | |
| key | VARCHAR(100) | NOT NULL | Setting key |
| value | JSONB | NOT NULL | Setting value |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_settings_restaurant_key` (UNIQUE on restaurant_id + key)

#### Menu Schema

**Table: `menu.menu_categories`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| branch_id | UUID | NOT NULL, FK -> config.branches.id ON DELETE CASCADE | |
| parent_id | UUID | FK -> menu.menu_categories.id (nullable) | For subcategories |
| name_en | VARCHAR(100) | NOT NULL | Category name in English |
| name_ar | VARCHAR(100) | NOT NULL | Category name in Arabic |
| description_en | VARCHAR(500) | | |
| description_ar | VARCHAR(500) | | |
| image_url | VARCHAR(500) | | Category image S3 URL |
| sort_order | INTEGER | DEFAULT 0 | Display ordering |
| is_active | BOOLEAN | DEFAULT true | |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_categories_branch_id`, `idx_categories_parent_id`, `idx_categories_sort`

**Table: `menu.menu_items`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| category_id | UUID | NOT NULL, FK -> menu.menu_categories.id ON DELETE CASCADE | |
| branch_id | UUID | NOT NULL, FK -> config.branches.id | Denormalized for query performance |
| name_en | VARCHAR(200) | NOT NULL | Item name in English |
| name_ar | VARCHAR(200) | NOT NULL | Item name in Arabic |
| description_en | TEXT | | Full description English |
| description_ar | TEXT | | Full description Arabic |
| price | DECIMAL(10, 2) | NOT NULL | Base price in SAR |
| image_url | VARCHAR(500) | | Item image S3 URL |
| nutrition_info | JSONB | DEFAULT '{}' | `{ "calories": 450, "protein": 25, "carbs": 40, "fat": 15 }` |
| allergy_info | JSONB | DEFAULT '[]' | `["gluten", "dairy", "nuts"]` |
| dietary_tags | JSONB | DEFAULT '[]' | `["halal", "spicy", "vegetarian"]` |
| is_available | BOOLEAN | DEFAULT true | Real-time availability toggle |
| is_popular | BOOLEAN | DEFAULT false | Featured in popular section |
| order_count | INTEGER | DEFAULT 0 | Total times ordered (for popularity ranking) |
| sort_order | INTEGER | DEFAULT 0 | Display ordering within category |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_items_category_id`, `idx_items_branch_id`, `idx_items_available` (WHERE is_available = true), `idx_items_popular` (WHERE is_popular = true), GIN index on `name_en`, `name_ar` for full-text search, GIN index on `dietary_tags` for filter queries

**Table: `menu.menu_item_variants`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| menu_item_id | UUID | NOT NULL, FK -> menu.menu_items.id ON DELETE CASCADE | |
| group_name_en | VARCHAR(100) | NOT NULL | Variant group (e.g., "Size", "Toppings") |
| group_name_ar | VARCHAR(100) | NOT NULL | |
| name_en | VARCHAR(100) | NOT NULL | Option name (e.g., "Large", "Extra Cheese") |
| name_ar | VARCHAR(100) | NOT NULL | |
| type | VARCHAR(20) | NOT NULL | 'size', 'topping', 'modification', 'addon' |
| price_modifier | DECIMAL(10, 2) | DEFAULT 0.00 | Added to base price (can be 0 for free options) |
| is_default | BOOLEAN | DEFAULT false | Pre-selected option |
| is_available | BOOLEAN | DEFAULT true | |
| max_selection | INTEGER | DEFAULT 1 | Max selections within this group |
| sort_order | INTEGER | DEFAULT 0 | |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_variants_item_id`, `idx_variants_type`

**Table: `menu.favorites`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| customer_id | UUID | NOT NULL, FK -> users.customers.id ON DELETE CASCADE | |
| menu_item_id | UUID | NOT NULL, FK -> menu.menu_items.id ON DELETE CASCADE | |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_favorites_customer_item` (UNIQUE on customer_id + menu_item_id)

#### Orders Schema

**Table: `orders.carts`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| customer_id | UUID | NOT NULL, FK -> users.customers.id | |
| branch_id | UUID | NOT NULL, FK -> config.branches.id | Cart is scoped to a single branch |
| promo_code_id | UUID | FK -> promos.promo_codes.id (nullable) | Applied promo code |
| subtotal | DECIMAL(10, 2) | DEFAULT 0.00 | Sum of cart items |
| discount_amount | DECIMAL(10, 2) | DEFAULT 0.00 | Promo discount |
| vat_amount | DECIMAL(10, 2) | DEFAULT 0.00 | Calculated VAT |
| delivery_fee | DECIMAL(10, 2) | DEFAULT 0.00 | Zone-based delivery fee |
| total | DECIMAL(10, 2) | DEFAULT 0.00 | Grand total |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_carts_customer_id` (most recent cart per customer)

**Table: `orders.cart_items`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| cart_id | UUID | NOT NULL, FK -> orders.carts.id ON DELETE CASCADE | |
| menu_item_id | UUID | NOT NULL, FK -> menu.menu_items.id | |
| quantity | INTEGER | NOT NULL, CHECK (quantity > 0) | |
| selected_variants | JSONB | DEFAULT '[]' | `[{ "variant_id": "...", "name": "Large", "price_modifier": 5.00 }]` |
| special_instructions | TEXT | | Customer notes for this item |
| unit_price | DECIMAL(10, 2) | NOT NULL | Base price + variant modifiers |
| total_price | DECIMAL(10, 2) | NOT NULL | unit_price * quantity |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_cart_items_cart_id`

**Table: `orders.orders`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| customer_id | UUID | NOT NULL, FK -> users.customers.id | |
| branch_id | UUID | NOT NULL, FK -> config.branches.id | |
| driver_id | UUID | FK -> users.drivers.id (nullable) | Assigned after acceptance |
| order_number | VARCHAR(20) | NOT NULL, UNIQUE | Human-readable order number (e.g., ORD-20260316-001) |
| status | VARCHAR(30) | NOT NULL, DEFAULT 'pending_payment' | See status enum below |
| type | VARCHAR(10) | NOT NULL | 'delivery', 'pickup' |
| subtotal | DECIMAL(10, 2) | NOT NULL | Items total before discounts |
| vat_amount | DECIMAL(10, 2) | NOT NULL | 15% VAT |
| delivery_fee | DECIMAL(10, 2) | DEFAULT 0.00 | Zone-based fee (0 for pickup) |
| discount_amount | DECIMAL(10, 2) | DEFAULT 0.00 | Applied promo discount |
| total | DECIMAL(10, 2) | NOT NULL | Final charge amount |
| promo_code_id | UUID | FK -> promos.promo_codes.id (nullable) | |
| scheduled_at | TIMESTAMPTZ | | For scheduled orders (null = ASAP) |
| estimated_prep_time | INTEGER | | Restaurant-set prep time in minutes |
| estimated_delivery_at | TIMESTAMPTZ | | ETA for customer |
| actual_delivery_at | TIMESTAMPTZ | | When delivery was confirmed |
| delivery_address | JSONB | | Snapshot of delivery address at order time |
| special_instructions | TEXT | | Order-level notes |
| cancellation_reason | TEXT | | If order was cancelled |
| cancelled_by | VARCHAR(20) | | 'customer', 'restaurant', 'system' |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

**Order Status Enum Values:**
- `pending_payment` - Order created, awaiting payment confirmation
- `payment_confirmed` - Payment successful, awaiting restaurant acceptance
- `accepted` - Restaurant accepted the order
- `preparing` - Kitchen is preparing the order
- `ready_for_pickup` - Order ready (for pickup orders, customer notified)
- `ready_for_delivery` - Order ready for driver pickup
- `driver_assigned` - Driver assigned to the delivery
- `driver_at_restaurant` - Driver arrived at restaurant
- `picked_up` - Driver picked up the order
- `on_the_way` - Driver en route to customer
- `delivered` - Order delivered successfully
- `completed` - Order completed (after delivery confirmation + rating window)
- `cancelled` - Order cancelled

Indexes: `idx_orders_customer_id`, `idx_orders_branch_id`, `idx_orders_driver_id`, `idx_orders_status`, `idx_orders_created_at`, `idx_orders_order_number`, `idx_orders_scheduled` (WHERE scheduled_at IS NOT NULL)

**Table: `orders.order_items`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| order_id | UUID | NOT NULL, FK -> orders.orders.id ON DELETE CASCADE | |
| menu_item_id | UUID | NOT NULL | Reference (not FK, item may be deleted later) |
| name_en | VARCHAR(200) | NOT NULL | Snapshot of item name |
| name_ar | VARCHAR(200) | NOT NULL | Snapshot of item name |
| quantity | INTEGER | NOT NULL | |
| selected_variants | JSONB | DEFAULT '[]' | Snapshot of selected variants |
| special_instructions | TEXT | | |
| unit_price | DECIMAL(10, 2) | NOT NULL | Price at order time |
| total_price | DECIMAL(10, 2) | NOT NULL | |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_order_items_order_id`

**Table: `orders.order_status_history`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| order_id | UUID | NOT NULL, FK -> orders.orders.id ON DELETE CASCADE | |
| status | VARCHAR(30) | NOT NULL | Status value |
| changed_by_user_id | UUID | | User who triggered the change |
| changed_by_role | VARCHAR(20) | | 'customer', 'restaurant', 'driver', 'system' |
| notes | TEXT | | Optional notes on status change |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_status_history_order_id`, `idx_status_history_created_at`

**Table: `orders.reviews`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| order_id | UUID | NOT NULL, FK -> orders.orders.id | |
| customer_id | UUID | NOT NULL, FK -> users.customers.id | |
| menu_item_id | UUID | FK -> menu.menu_items.id (nullable) | For item-level reviews |
| driver_id | UUID | FK -> users.drivers.id (nullable) | For driver ratings |
| rating | SMALLINT | NOT NULL, CHECK (rating BETWEEN 1 AND 5) | Star rating |
| comment | TEXT | | Review text |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_reviews_order_id`, `idx_reviews_customer_id`, `idx_reviews_menu_item_id`, `idx_reviews_driver_id`

#### Payments Schema

**Table: `payments.payments`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| order_id | UUID | NOT NULL, FK -> orders.orders.id | |
| method | VARCHAR(20) | NOT NULL | 'card', 'mada', 'google_pay', 'stc_pay', 'cod' |
| stripe_payment_intent_id | VARCHAR(255) | | Stripe PI ID |
| stc_pay_transaction_ref | VARCHAR(255) | | STC Pay reference |
| amount | DECIMAL(10, 2) | NOT NULL | Amount charged |
| currency | VARCHAR(3) | DEFAULT 'SAR' | |
| status | VARCHAR(20) | NOT NULL | 'pending', 'processing', 'succeeded', 'failed', 'refunded', 'partially_refunded' |
| card_brand | VARCHAR(20) | | 'visa', 'mastercard', 'mada' |
| card_last4 | VARCHAR(4) | | Last 4 digits |
| failure_reason | TEXT | | If payment failed |
| metadata | JSONB | DEFAULT '{}' | Additional payment data |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_payments_order_id`, `idx_payments_stripe_pi`, `idx_payments_status`, `idx_payments_created_at`

**Table: `payments.saved_cards`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| customer_id | UUID | NOT NULL, FK -> users.customers.id ON DELETE CASCADE | |
| stripe_payment_method_id | VARCHAR(255) | NOT NULL | Stripe PM ID |
| brand | VARCHAR(20) | NOT NULL | 'visa', 'mastercard', 'mada' |
| last4 | VARCHAR(4) | NOT NULL | |
| exp_month | SMALLINT | NOT NULL | |
| exp_year | SMALLINT | NOT NULL | |
| is_default | BOOLEAN | DEFAULT false | |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_saved_cards_customer_id`

**Table: `payments.refunds`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| payment_id | UUID | NOT NULL, FK -> payments.payments.id | |
| order_id | UUID | NOT NULL, FK -> orders.orders.id | |
| stripe_refund_id | VARCHAR(255) | | Stripe refund ID |
| amount | DECIMAL(10, 2) | NOT NULL | Refund amount |
| reason | VARCHAR(50) | NOT NULL | 'payment_stuck', 'double_charge', 'technical_failure' |
| notes | TEXT | | Admin notes |
| status | VARCHAR(20) | NOT NULL | 'pending', 'succeeded', 'failed' |
| processed_by | UUID | | Admin user who initiated |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_refunds_payment_id`, `idx_refunds_order_id`

#### Delivery Schema

**Table: `delivery.delivery_zones`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| branch_id | UUID | NOT NULL, FK -> config.branches.id ON DELETE CASCADE | |
| name_en | VARCHAR(100) | NOT NULL | Zone name (e.g., "Zone 1 - Nearby") |
| name_ar | VARCHAR(100) | NOT NULL | |
| polygon | GEOMETRY(POLYGON, 4326) | NOT NULL | PostGIS polygon defining the zone boundary |
| delivery_fee | DECIMAL(10, 2) | NOT NULL | Fee for this zone in SAR |
| min_order_amount | DECIMAL(10, 2) | DEFAULT 0.00 | Minimum order for this zone |
| estimated_delivery_minutes | INTEGER | | Base ETA estimate for this zone |
| is_active | BOOLEAN | DEFAULT true | |
| sort_order | INTEGER | DEFAULT 0 | Priority (checked in order for overlapping zones) |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_zones_branch_id`, GIST index on `polygon`

**Table: `delivery.delivery_assignments`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| order_id | UUID | NOT NULL, FK -> orders.orders.id | |
| driver_id | UUID | NOT NULL, FK -> users.drivers.id | |
| status | VARCHAR(20) | NOT NULL | 'assigned', 'accepted', 'declined', 'picked_up', 'delivered', 'failed' |
| assigned_at | TIMESTAMPTZ | DEFAULT NOW() | |
| accepted_at | TIMESTAMPTZ | | |
| picked_up_at | TIMESTAMPTZ | | |
| delivered_at | TIMESTAMPTZ | | |
| decline_reason | TEXT | | If driver declined |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_assignments_order_id`, `idx_assignments_driver_id`, `idx_assignments_status`

#### Notifications Schema

**Table: `notifications.notifications`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| user_id | UUID | NOT NULL, FK -> users.users.id ON DELETE CASCADE | |
| type | VARCHAR(30) | NOT NULL | 'order_update', 'promo', 'delivery', 'system', 'marketing' |
| title_en | VARCHAR(200) | NOT NULL | |
| title_ar | VARCHAR(200) | NOT NULL | |
| body_en | TEXT | NOT NULL | |
| body_ar | TEXT | NOT NULL | |
| data | JSONB | DEFAULT '{}' | Deep link data, order_id, etc. |
| is_read | BOOLEAN | DEFAULT false | |
| sent_via | VARCHAR(20) | DEFAULT 'push' | 'push', 'email', 'in_app', 'sms' |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_notifications_user_id`, `idx_notifications_read` (WHERE is_read = false), `idx_notifications_created_at`

**Table: `notifications.notification_templates`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| restaurant_id | UUID | NOT NULL, FK -> config.restaurants.id | |
| event_type | VARCHAR(50) | NOT NULL | 'order_placed', 'order_accepted', 'driver_assigned', etc. |
| title_en | VARCHAR(200) | NOT NULL | Template with {{variables}} |
| title_ar | VARCHAR(200) | NOT NULL | |
| body_en | TEXT | NOT NULL | |
| body_ar | TEXT | NOT NULL | |
| is_active | BOOLEAN | DEFAULT true | |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_templates_restaurant_event` (UNIQUE on restaurant_id + event_type)

#### Promos Schema

**Table: `promos.promo_codes`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| restaurant_id | UUID | NOT NULL, FK -> config.restaurants.id | |
| code | VARCHAR(50) | NOT NULL | Promo code string (uppercase) |
| type | VARCHAR(20) | NOT NULL | 'percentage', 'fixed_amount', 'free_delivery' |
| value | DECIMAL(10, 2) | NOT NULL | Discount value (% or SAR amount) |
| min_order_amount | DECIMAL(10, 2) | DEFAULT 0.00 | Minimum order to apply |
| max_discount_amount | DECIMAL(10, 2) | | Cap on percentage discounts |
| usage_limit_total | INTEGER | | Total uses allowed (null = unlimited) |
| usage_limit_per_user | INTEGER | DEFAULT 1 | Uses per customer |
| used_count | INTEGER | DEFAULT 0 | Total times used |
| applicable_branches | JSONB | DEFAULT '[]' | Empty = all branches |
| applicable_categories | JSONB | DEFAULT '[]' | Empty = all categories |
| start_date | TIMESTAMPTZ | NOT NULL | Promo start |
| end_date | TIMESTAMPTZ | NOT NULL | Promo expiry |
| is_active | BOOLEAN | DEFAULT true | |
| is_first_order_only | BOOLEAN | DEFAULT false | Only for new customers |
| description_en | VARCHAR(500) | | |
| description_ar | VARCHAR(500) | | |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_promos_restaurant_id`, `idx_promos_code` (UNIQUE on restaurant_id + code), `idx_promos_active_dates`

**Table: `promos.promo_usage`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| promo_code_id | UUID | NOT NULL, FK -> promos.promo_codes.id | |
| customer_id | UUID | NOT NULL, FK -> users.customers.id | |
| order_id | UUID | NOT NULL, FK -> orders.orders.id | |
| discount_amount | DECIMAL(10, 2) | NOT NULL | Actual discount applied |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_promo_usage_promo_customer` (for per-user usage count)

**Table: `promos.loyalty_accounts`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| customer_id | UUID | NOT NULL, FK -> users.customers.id | |
| restaurant_id | UUID | NOT NULL, FK -> config.restaurants.id | |
| points_balance | INTEGER | DEFAULT 0 | Current available points |
| total_earned | INTEGER | DEFAULT 0 | Lifetime earned points |
| total_redeemed | INTEGER | DEFAULT 0 | Lifetime redeemed points |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_loyalty_customer_restaurant` (UNIQUE on customer_id + restaurant_id)

**Table: `promos.loyalty_transactions`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| loyalty_account_id | UUID | NOT NULL, FK -> promos.loyalty_accounts.id | |
| type | VARCHAR(10) | NOT NULL | 'earn', 'redeem', 'expire', 'adjust' |
| points | INTEGER | NOT NULL | Positive for earn, negative for redeem |
| order_id | UUID | FK -> orders.orders.id (nullable) | |
| description_en | VARCHAR(200) | | |
| description_ar | VARCHAR(200) | | |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_loyalty_tx_account_id`, `idx_loyalty_tx_created_at`

**Table: `promos.loyalty_config`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| restaurant_id | UUID | NOT NULL, UNIQUE, FK -> config.restaurants.id | |
| points_per_sar | DECIMAL(5, 2) | DEFAULT 1.00 | Points earned per 1 SAR spent |
| redemption_rate | DECIMAL(5, 2) | DEFAULT 0.01 | SAR value per point (100 points = 1 SAR default) |
| min_points_redeem | INTEGER | DEFAULT 100 | Minimum points to redeem |
| max_points_per_order | INTEGER | | Max points redeemable per order (null = no limit) |
| is_active | BOOLEAN | DEFAULT false | Loyalty program on/off |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

#### Support Schema

**Table: `support.support_tickets`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| ticket_number | VARCHAR(20) | NOT NULL, UNIQUE | Human-readable (e.g., TKT-20260316-001) |
| customer_id | UUID | NOT NULL, FK -> users.customers.id | |
| restaurant_id | UUID | NOT NULL, FK -> config.restaurants.id | |
| order_id | UUID | FK -> orders.orders.id (nullable) | Related order |
| subject | VARCHAR(200) | NOT NULL | |
| category | VARCHAR(50) | DEFAULT 'general' | 'order_issue', 'payment_issue', 'delivery_issue', 'menu_feedback', 'general' |
| status | VARCHAR(20) | DEFAULT 'open' | 'open', 'in_progress', 'waiting_customer', 'resolved', 'closed' |
| priority | VARCHAR(10) | DEFAULT 'normal' | 'low', 'normal', 'high', 'urgent' |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_tickets_customer_id`, `idx_tickets_restaurant_id`, `idx_tickets_status`, `idx_tickets_order_id`

**Table: `support.support_messages`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| ticket_id | UUID | NOT NULL, FK -> support.support_tickets.id ON DELETE CASCADE | |
| sender_type | VARCHAR(20) | NOT NULL | 'customer', 'restaurant_admin', 'system' |
| sender_id | UUID | NOT NULL | User ID of sender |
| message | TEXT | NOT NULL | Message body |
| attachments | JSONB | DEFAULT '[]' | `[{ "url": "s3://...", "filename": "photo.jpg", "type": "image/jpeg" }]` |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_messages_ticket_id`, `idx_messages_created_at`

#### Analytics Schema

**Table: `analytics.daily_snapshots`**

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | UUID | PK, DEFAULT gen_random_uuid() | |
| branch_id | UUID | NOT NULL, FK -> config.branches.id | |
| date | DATE | NOT NULL | Snapshot date |
| total_orders | INTEGER | DEFAULT 0 | |
| completed_orders | INTEGER | DEFAULT 0 | |
| cancelled_orders | INTEGER | DEFAULT 0 | |
| total_revenue | DECIMAL(12, 2) | DEFAULT 0.00 | |
| total_vat | DECIMAL(12, 2) | DEFAULT 0.00 | |
| total_delivery_fees | DECIMAL(12, 2) | DEFAULT 0.00 | |
| total_discounts | DECIMAL(12, 2) | DEFAULT 0.00 | |
| avg_order_value | DECIMAL(10, 2) | DEFAULT 0.00 | |
| new_customers | INTEGER | DEFAULT 0 | |
| returning_customers | INTEGER | DEFAULT 0 | |
| avg_delivery_time_minutes | DECIMAL(6, 2) | | |
| avg_preparation_time_minutes | DECIMAL(6, 2) | | |
| popular_items | JSONB | DEFAULT '[]' | Top 10 items for the day |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

Indexes: `idx_snapshots_branch_date` (UNIQUE on branch_id + date)

### 3.3 Database Extensions Required

```sql
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";     -- UUID generation
CREATE EXTENSION IF NOT EXISTS "postgis";         -- Geospatial operations
CREATE EXTENSION IF NOT EXISTS "pg_trgm";         -- Trigram similarity for fuzzy search
CREATE EXTENSION IF NOT EXISTS "btree_gist";      -- GiST indexes for exclusion constraints
```

### 3.4 Key Database Design Decisions

1. **UUIDs for Primary Keys**: All tables use UUID v4 for primary keys to support distributed systems and prevent enumeration attacks.
2. **Soft Deletes**: Critical entities (users, restaurants, orders) use status fields rather than actual deletion.
3. **JSONB for Flexible Data**: Used for branding config, operating hours, nutrition info, variant selections, and delivery addresses (snapshot at order time).
4. **Denormalized Order Snapshots**: Order items store name and price at order time to preserve historical accuracy even if menu items change.
5. **PostGIS for Geospatial**: Delivery zone polygon containment queries and nearest-driver calculations.
6. **Bilingual Columns**: All user-facing text fields have `_en` and `_ar` variants rather than a separate translations table, for query simplicity.
7. **Schema Separation**: Logical schema per service for clear ownership boundaries.

---

## 4. API Endpoints

All endpoints are versioned under `/api/v1/`. Authentication is indicated as: **Public** (no auth), **Customer** (customer JWT), **Driver** (driver JWT), **Admin** (restaurant admin JWT), **Any Auth** (any authenticated user).

### 4.1 Auth Service (`/api/v1/auth`)

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| POST | `/auth/register` | Register new customer (phone + OTP via Firebase) | Public |
| POST | `/auth/verify-otp` | Verify OTP code from Firebase and issue JWT | Public |
| POST | `/auth/login/phone` | Send OTP to phone for login | Public |
| POST | `/auth/login/social` | Authenticate via Google/Facebook token | Public |
| POST | `/auth/login/driver` | Driver login with credentials (username + password) | Public |
| POST | `/auth/login/admin` | Restaurant admin login (email + password) | Public |
| POST | `/auth/refresh-token` | Refresh expired JWT using refresh token | Public (with refresh token) |
| POST | `/auth/logout` | Invalidate session and refresh token | Any Auth |
| GET | `/auth/me` | Get current authenticated user info | Any Auth |
| POST | `/auth/guest-upgrade` | Convert guest session to registered account | Public (with guest token) |

### 4.2 User Service (`/api/v1/users`, `/api/v1/addresses`)

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| GET | `/users/profile` | Get current user profile | Any Auth |
| PUT | `/users/profile` | Update profile (name, language, dietary prefs) | Any Auth |
| POST | `/users/avatar` | Upload profile avatar | Any Auth |
| DELETE | `/users/avatar` | Remove profile avatar | Any Auth |
| GET | `/users/dietary-preferences` | Get dietary preference options | Customer |
| PUT | `/users/dietary-preferences` | Update dietary preferences | Customer |
| GET | `/users/notification-preferences` | Get notification preferences | Any Auth |
| PUT | `/users/notification-preferences` | Update notification preferences | Any Auth |
| GET | `/addresses` | List customer addresses | Customer |
| POST | `/addresses` | Add new address (with lat/lng from map pin-drop) | Customer |
| PUT | `/addresses/:id` | Update address | Customer |
| DELETE | `/addresses/:id` | Delete address | Customer |
| PUT | `/addresses/:id/default` | Set address as default | Customer |

### 4.3 Menu Service (`/api/v1/menu`)

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| GET | `/menu/branches/:branchId/categories` | List categories for a branch (with subcategories) | Public |
| POST | `/menu/categories` | Create category | Admin |
| PUT | `/menu/categories/:id` | Update category | Admin |
| DELETE | `/menu/categories/:id` | Delete category (and reassign/delete items) | Admin |
| PUT | `/menu/categories/reorder` | Reorder categories (batch sort_order update) | Admin |
| GET | `/menu/branches/:branchId/items` | List menu items for a branch (with filters, pagination) | Public |
| GET | `/menu/items/:id` | Get item detail (with variants, nutrition, allergy) | Public |
| POST | `/menu/items` | Create menu item | Admin |
| PUT | `/menu/items/:id` | Update menu item | Admin |
| DELETE | `/menu/items/:id` | Delete menu item | Admin |
| PATCH | `/menu/items/:id/availability` | Toggle item availability | Admin |
| PATCH | `/menu/items/:id/popular` | Toggle popular flag | Admin |
| POST | `/menu/items/:id/image` | Upload item image | Admin |
| GET | `/menu/items/:itemId/variants` | List variants for an item | Public |
| POST | `/menu/items/:itemId/variants` | Add variant to item | Admin |
| PUT | `/menu/variants/:id` | Update variant | Admin |
| DELETE | `/menu/variants/:id` | Delete variant | Admin |
| GET | `/menu/branches/:branchId/search` | Search menu items (full-text, auto-suggest) | Public |
| GET | `/menu/branches/:branchId/popular` | Get popular items for a branch | Public |
| GET | `/menu/favorites` | Get customer's favorite items | Customer |
| POST | `/menu/favorites/:itemId` | Add item to favorites | Customer |
| DELETE | `/menu/favorites/:itemId` | Remove item from favorites | Customer |

### 4.4 Cart Service (`/api/v1/cart`)

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| GET | `/cart` | Get current cart (with items, totals, promo) | Customer |
| POST | `/cart/items` | Add item to cart (with variants, quantity) | Customer |
| PUT | `/cart/items/:id` | Update cart item (quantity, variants, instructions) | Customer |
| DELETE | `/cart/items/:id` | Remove item from cart | Customer |
| POST | `/cart/promo` | Apply promo code to cart | Customer |
| DELETE | `/cart/promo` | Remove applied promo code | Customer |
| DELETE | `/cart` | Clear entire cart | Customer |
| GET | `/cart/upsells` | Get upsell suggestions based on cart contents | Customer |
| GET | `/cart/summary` | Get cart summary (subtotal, VAT, delivery fee, discount, total) | Customer |

### 4.5 Order Service (`/api/v1/orders`)

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| POST | `/orders` | Create order from cart | Customer |
| GET | `/orders` | List orders (with filters: status, date range, pagination) | Customer, Admin |
| GET | `/orders/:id` | Get order detail (items, status history, payment, driver) | Customer, Admin, Driver |
| GET | `/orders/:id/receipt` | Get VAT-compliant receipt (PDF or JSON) | Customer, Admin |
| POST | `/orders/:id/reorder` | Create new cart from previous order items | Customer |
| POST | `/orders/:id/cancel` | Cancel order (with reason) | Customer, Admin |
| PATCH | `/orders/:id/status` | Update order status (accept, preparing, ready, etc.) | Admin, Driver |
| POST | `/orders/:id/review` | Rate and review order (overall + item-level) | Customer |
| GET | `/orders/:id/tracking` | Get real-time tracking info (status, driver location, ETA) | Customer |
| PATCH | `/orders/:id/prep-time` | Set estimated preparation time | Admin |
| GET | `/orders/active` | Get customer's active (in-progress) orders | Customer |
| GET | `/orders/board` | Get restaurant order board (incoming, preparing, ready) | Admin |

### 4.6 Payment Service (`/api/v1/payments`)

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| POST | `/payments/intent` | Create Stripe payment intent for order | Customer |
| POST | `/payments/confirm` | Confirm payment (after Stripe client-side confirmation) | Customer |
| POST | `/payments/stc-pay/initiate` | Initiate STC Pay payment | Customer |
| POST | `/payments/stc-pay/confirm` | Confirm STC Pay payment (after OTP) | Customer |
| POST | `/payments/cod` | Mark order as COD (cash on delivery) | Customer |
| GET | `/payments/methods` | Get customer's saved payment methods | Customer |
| POST | `/payments/methods` | Save a new payment method (Stripe setup intent) | Customer |
| DELETE | `/payments/methods/:id` | Delete saved payment method | Customer |
| PUT | `/payments/methods/:id/default` | Set default payment method | Customer |
| GET | `/payments/transactions` | List payment transactions (with filters) | Admin |
| GET | `/payments/transactions/:id` | Get transaction detail | Admin |
| POST | `/payments/refund` | Process refund (technical failures only) | Admin |
| POST | `/payments/webhook/stripe` | Stripe webhook handler | Public (Stripe signature verified) |
| POST | `/payments/webhook/stc-pay` | STC Pay webhook handler | Public (signature verified) |

### 4.7 Delivery Service (`/api/v1/delivery`)

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| POST | `/delivery/assign` | Assign driver to order | Admin |
| GET | `/delivery/suggest-driver/:orderId` | Get suggested available drivers for order (nearest) | Admin |
| PATCH | `/delivery/assignments/:id/accept` | Driver accepts delivery assignment | Driver |
| PATCH | `/delivery/assignments/:id/decline` | Driver declines delivery assignment | Driver |
| PATCH | `/delivery/assignments/:id/pickup` | Driver marks order picked up | Driver |
| PATCH | `/delivery/assignments/:id/deliver` | Driver confirms delivery | Driver |
| POST | `/delivery/location` | Update driver GPS location | Driver |
| GET | `/delivery/tracking/:orderId` | Get live tracking data (driver location, ETA) | Customer, Admin |
| GET | `/delivery/zones/:branchId` | List delivery zones for a branch | Public |
| POST | `/delivery/zones` | Create delivery zone (polygon + fee) | Admin |
| PUT | `/delivery/zones/:id` | Update delivery zone | Admin |
| DELETE | `/delivery/zones/:id` | Delete delivery zone | Admin |
| GET | `/delivery/fee` | Calculate delivery fee for address + branch | Customer |
| GET | `/delivery/eta` | Estimate delivery time for address + branch | Customer |
| GET | `/delivery/drivers` | List drivers with status and location | Admin |
| GET | `/delivery/drivers/:id/location` | Get specific driver location | Admin |
| PATCH | `/delivery/availability` | Toggle driver availability (online/offline) | Driver |
| GET | `/delivery/my-deliveries` | Get driver's assigned deliveries | Driver |
| GET | `/delivery/my-stats` | Get driver's performance statistics | Driver |

### 4.8 Notification Service (`/api/v1/notifications`)

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| GET | `/notifications` | List user notifications (paginated) | Any Auth |
| GET | `/notifications/unread-count` | Get unread notification count | Any Auth |
| PATCH | `/notifications/:id/read` | Mark notification as read | Any Auth |
| PATCH | `/notifications/read-all` | Mark all notifications as read | Any Auth |
| DELETE | `/notifications/:id` | Delete a notification | Any Auth |
| POST | `/notifications/push` | Send push notification (targeted or broadcast) | Admin |
| POST | `/notifications/email` | Send email campaign | Admin |
| GET | `/notifications/templates` | List notification templates | Admin |
| PUT | `/notifications/templates/:id` | Update notification template | Admin |
| POST | `/notifications/fcm-token` | Register/update FCM device token | Customer, Driver |

### 4.9 Promo & Loyalty Service (`/api/v1/promos`, `/api/v1/loyalty`)

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| GET | `/promos` | List active promo codes (customer-facing offers) | Customer |
| POST | `/promos/validate` | Validate promo code against cart | Customer |
| GET | `/promos/admin` | List all promo codes (with stats) | Admin |
| POST | `/promos` | Create promo code | Admin |
| PUT | `/promos/:id` | Update promo code | Admin |
| DELETE | `/promos/:id` | Deactivate promo code | Admin |
| GET | `/promos/:id/stats` | Get promo usage statistics | Admin |
| GET | `/loyalty/balance` | Get customer's loyalty points balance | Customer |
| GET | `/loyalty/history` | Get loyalty transaction history | Customer |
| POST | `/loyalty/redeem` | Redeem loyalty points on order | Customer |
| GET | `/loyalty/config` | Get loyalty program configuration | Admin |
| PUT | `/loyalty/config` | Update loyalty configuration (points/SAR, rates) | Admin |
| PATCH | `/loyalty/config/toggle` | Enable/disable loyalty program | Admin |

### 4.10 Analytics Service (`/api/v1/analytics`)

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| GET | `/analytics/dashboard` | Get dashboard summary (today's stats) | Admin |
| GET | `/analytics/sales` | Sales report (date range, branch filter, export) | Admin |
| GET | `/analytics/revenue` | Revenue breakdown (by payment method, by day) | Admin |
| GET | `/analytics/customers` | Customer analytics (new vs returning, segments) | Admin |
| GET | `/analytics/popular-items` | Popular items report (date range, ranking) | Admin |
| GET | `/analytics/orders` | Order analytics (volume, avg value, peak hours) | Admin |
| GET | `/analytics/drivers` | Driver performance report | Admin |
| GET | `/analytics/export/:reportType` | Export report as CSV or PDF | Admin |

### 4.11 Support Service (`/api/v1/support`)

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| POST | `/support/tickets` | Create support ticket | Customer |
| GET | `/support/tickets` | List tickets (filtered by status, paginated) | Customer, Admin |
| GET | `/support/tickets/:id` | Get ticket detail with messages | Customer, Admin |
| POST | `/support/tickets/:id/messages` | Add message to ticket | Customer, Admin |
| PATCH | `/support/tickets/:id/status` | Update ticket status | Admin |
| PATCH | `/support/tickets/:id/priority` | Update ticket priority | Admin |
| POST | `/support/tickets/:id/attachments` | Upload attachment to ticket | Customer, Admin |

### 4.12 Config Service (`/api/v1/config`, `/api/v1/branches`)

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| GET | `/config/restaurant` | Get restaurant configuration (public branding) | Public |
| PUT | `/config/restaurant` | Update restaurant settings | Admin |
| GET | `/config/branding` | Get branding configuration (colors, logos, theme) | Public |
| PUT | `/config/branding` | Update branding configuration | Admin |
| POST | `/config/branding/logo` | Upload restaurant logo | Admin |
| GET | `/config/settings` | Get system settings | Admin |
| PUT | `/config/settings` | Update system settings | Admin |
| GET | `/branches` | List restaurant branches | Public |
| GET | `/branches/:id` | Get branch detail (hours, location, zones) | Public |
| POST | `/branches` | Create new branch | Admin |
| PUT | `/branches/:id` | Update branch details | Admin |
| DELETE | `/branches/:id` | Deactivate branch | Admin |
| PUT | `/branches/:id/hours` | Update operating hours | Admin |
| PATCH | `/branches/:id/accepting` | Toggle order acceptance on/off | Admin |

### 4.13 File Service (`/api/v1/files`)

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| POST | `/files/upload` | Upload file to S3 (with type validation) | Any Auth |
| POST | `/files/upload/image` | Upload and resize image (returns multiple sizes) | Any Auth |
| GET | `/files/presigned-url` | Get presigned download URL | Any Auth |
| DELETE | `/files/:key` | Delete file from S3 | Admin |

### 4.14 Driver-Specific Endpoints (via User + Delivery Services)

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| GET | `/users/driver/profile` | Get driver profile with documents | Driver |
| PUT | `/users/driver/profile` | Update driver profile | Driver |
| POST | `/users/driver/documents` | Upload driver documents (license, ID) | Driver |
| GET | `/users/driver/shift` | Get current shift info | Driver |
| POST | `/users/driver/shift/start` | Start shift | Driver |
| POST | `/users/driver/shift/end` | End shift | Driver |
| POST | `/users/driver/leave-request` | Submit leave request | Driver |
| POST | `/delivery/issues` | Report delivery issue | Driver |
| GET | `/support/driver-channel` | Get driver-restaurant support channel | Driver |
| POST | `/support/driver-channel/message` | Send message to restaurant support | Driver |

### 4.15 Admin Driver Management Endpoints

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| GET | `/users/admin/drivers` | List all drivers for restaurant | Admin |
| POST | `/users/admin/drivers` | Create driver account (credentials provisioned by restaurant) | Admin |
| PUT | `/users/admin/drivers/:id` | Update driver account | Admin |
| PATCH | `/users/admin/drivers/:id/status` | Suspend/activate driver | Admin |
| GET | `/users/admin/drivers/:id/performance` | Get driver performance metrics | Admin |
| GET | `/users/admin/customers` | List customer database | Admin |
| GET | `/users/admin/customers/:id` | Get customer detail | Admin |

---

## 5. Authentication Flow

### 5.1 Customer Registration (OTP Flow with Firebase)

```
Customer App                 Auth Service              Firebase Auth
     |                            |                         |
     |-- 1. Enter phone number -->|                         |
     |                            |-- 2. verifyPhoneNumber ->|
     |                            |                         |
     |<-- 3. OTP sent to phone ---|<-- verificationId ------|
     |                            |                         |
     |-- 4. Enter OTP code ------>|                         |
     |                            |-- 5. signInWithCredential ->|
     |                            |                         |
     |                            |<-- 6. Firebase ID token -|
     |                            |                         |
     |                            |-- 7. Verify ID token    |
     |                            |   (firebase-admin SDK)  |
     |                            |                         |
     |                            |-- 8. Create/find user   |
     |                            |   in PostgreSQL         |
     |                            |                         |
     |                            |-- 9. Generate JWT       |
     |                            |   (access + refresh)    |
     |                            |                         |
     |<-- 10. Return JWT tokens --|                         |
     |   + user profile           |                         |
```

**Implementation Details:**
- Firebase Authentication handles the OTP SMS delivery (no separate SMS provider needed)
- Firebase free tier supports 10,000 phone verifications/month; monitor usage and plan for paid tier if needed
- The Auth Service validates the Firebase ID token server-side using `firebase-admin` SDK
- On successful verification, a local JWT is issued for all subsequent API calls
- User record is created in PostgreSQL with `firebase_uid` linking to Firebase

### 5.2 Customer Social Login (Google/Facebook)

```
Customer App                 Auth Service              Firebase Auth     Google/Facebook
     |                            |                         |                   |
     |-- 1. Tap "Login with      |                         |                   |
     |   Google/Facebook" ------->|                         |                   |
     |                            |                         |                   |
     |<-- 2. Open OAuth popup ----|                         |                   |
     |                            |                         |                   |
     |-- 3. User authorizes ----->|                         |                   |
     |                            |                         |                   |
     |-- 4. Firebase credential ->|                         |                   |
     |                            |-- 5. signInWithCredential ->|              |
     |                            |                         |                   |
     |                            |<-- 6. Firebase ID token -|                  |
     |                            |                         |                   |
     |                            |-- 7. Verify token,      |                   |
     |                            |   extract email/name    |                   |
     |                            |                         |                   |
     |                            |-- 8. Find/create user   |                   |
     |                            |   Link social account   |                   |
     |                            |                         |                   |
     |<-- 9. Return JWT tokens --|                          |                   |
     |   + user profile           |                         |                   |
```

**Implementation Details:**
- Uses `@react-native-firebase/auth` for mobile and Firebase JS SDK for web
- Social account linked in `auth.social_accounts` table
- If email already exists (registered via phone), accounts are merged
- Phone number may be requested on first social login for delivery contact purposes

### 5.3 Guest Browsing to Authenticated Upgrade Flow

```
Customer App                 Auth Service              Backend Services
     |                            |                         |
     |-- 1. Open app (no login) ->|                         |
     |                            |                         |
     |<-- 2. Guest token (limited |                         |
     |   claims, no user_id) -----|                         |
     |                            |                         |
     |-- 3. Browse menu --------->|                         |
     |   (guest token accepted    |                    Menu Service
     |    for read-only routes)   |                         |
     |                            |                         |
     |-- 4. Try to add to cart -->|                         |
     |                            |                         |
     |<-- 5. 401 + redirect to   |                         |
     |   registration prompt -----|                         |
     |                            |                         |
     |-- 6. Register/Login ------>|                         |
     |   (OTP or social)          |                         |
     |                            |                         |
     |<-- 7. Full JWT tokens ----|                          |
     |                            |                         |
     |-- 8. Retry add to cart --->|                    Cart Service
     |   (with full JWT)          |                         |
```

**Implementation Details:**
- Guest token is a JWT with `{ type: "guest", scope: "read" }` claims
- Menu browsing, search, and branch listing are accessible with guest token
- Cart, orders, payments, and profile require full authentication
- Registration prompt appears at the point of first write action (add to cart)
- Minimized signup form (phone number only, name optional initially)

### 5.4 Driver Login (Credentials)

```
Driver App                   Auth Service              PostgreSQL
     |                            |                         |
     |-- 1. Enter username/ID    |                         |
     |   + password ------------->|                         |
     |                            |                         |
     |                            |-- 2. Look up driver     |
     |                            |   by username/phone     |
     |                            |   in users + drivers -->|
     |                            |                         |
     |                            |<-- 3. User record ------|
     |                            |                         |
     |                            |-- 4. Verify password    |
     |                            |   (bcrypt compare)      |
     |                            |                         |
     |                            |-- 5. Check driver       |
     |                            |   status == 'active'    |
     |                            |                         |
     |                            |-- 6. Generate JWT       |
     |                            |   { role: 'driver',     |
     |                            |     restaurant_id }     |
     |                            |                         |
     |<-- 7. Return JWT tokens --|                          |
     |   + driver profile         |                         |
```

**Implementation Details:**
- Drivers do NOT use Firebase Auth; they use credentials provisioned by the restaurant admin
- Passwords are hashed with bcrypt (12 salt rounds)
- Driver JWT includes `restaurant_id` claim for scoping data access
- Driver accounts are created by restaurant admins via the dashboard

### 5.5 Restaurant Admin Login

```
Dashboard                    Auth Service              PostgreSQL
     |                            |                         |
     |-- 1. Enter email          |                         |
     |   + password ------------->|                         |
     |                            |                         |
     |                            |-- 2. Look up admin      |
     |                            |   by email in users +   |
     |                            |   restaurant_admins --->|
     |                            |                         |
     |                            |<-- 3. User record ------|
     |                            |   + restaurant_id       |
     |                            |   + role                |
     |                            |                         |
     |                            |-- 4. Verify password    |
     |                            |   (bcrypt compare)      |
     |                            |                         |
     |                            |-- 5. Generate JWT       |
     |                            |   { role: 'admin',      |
     |                            |     restaurant_id,      |
     |                            |     admin_role }        |
     |                            |                         |
     |<-- 6. Return JWT tokens --|                          |
     |   + admin profile          |                         |
```

### 5.6 JWT Token Structure and Refresh Flow

**Access Token Claims:**
```json
{
  "sub": "user-uuid",
  "type": "customer|driver|restaurant_admin",
  "restaurant_id": "restaurant-uuid (for driver/admin)",
  "admin_role": "owner|admin|manager|staff (for admin only)",
  "branch_id": "branch-uuid (if branch-scoped admin)",
  "iat": 1710576000,
  "exp": 1710579600
}
```

**Token Configuration:**
- Access Token: 1 hour expiry, signed with RS256 (asymmetric)
- Refresh Token: 30 days expiry, stored hashed in `auth.sessions` table
- Token signing key: RSA 2048-bit key pair, stored in AWS Secrets Manager

**Refresh Flow:**
```
Client                       Auth Service
  |                               |
  |-- 1. API call with expired    |
  |   access token (401) -------->|
  |                               |
  |<-- 2. 401 Unauthorized -------|
  |                               |
  |-- 3. POST /auth/refresh-token |
  |   { refresh_token } --------->|
  |                               |
  |                               |-- 4. Verify refresh token
  |                               |   exists in sessions table
  |                               |   and is not expired
  |                               |
  |                               |-- 5. Generate new access
  |                               |   + refresh token pair
  |                               |
  |                               |-- 6. Invalidate old refresh
  |                               |   token (rotation)
  |                               |
  |<-- 7. New access + refresh ---|
  |   tokens                      |
  |                               |
  |-- 8. Retry original request ->|
  |   with new access token       |
```

**Implementation Notes:**
- Refresh token rotation: each refresh generates a new pair, old refresh token is invalidated
- If a previously invalidated refresh token is used, all sessions for that user are terminated (security breach detection)
- Axios interceptor on clients automatically handles 401 -> refresh -> retry

### 5.7 Role-Based Access Control (RBAC) Matrix

| Resource | Customer | Driver | Admin (Owner) | Admin (Manager) | Admin (Staff) | Guest |
|---|---|---|---|---|---|---|
| Browse menu | Read | - | Read | Read | Read | Read |
| Search menu | Read | - | Read | Read | Read | Read |
| Manage menu | - | - | Full CRUD | Full CRUD | Read only | - |
| Cart operations | Full CRUD | - | - | - | - | - |
| Place order | Create | - | - | - | - | - |
| View own orders | Read | - | - | - | - | - |
| View all orders | - | - | Read | Read | Read | - |
| Manage order status | - | - | Update | Update | Update | - |
| Accept/decline delivery | - | Update | - | - | - | - |
| Driver location | - | Update | Read | Read | - | - |
| Driver management | - | - | Full CRUD | Read | - | - |
| Payment processing | Create | - | - | - | - | - |
| View transactions | Own only | - | Read | Read | - | - |
| Process refunds | - | - | Create | - | - | - |
| Promo codes | Apply | - | Full CRUD | Full CRUD | Read | - |
| Loyalty | Read/Redeem | - | Config | Config | Read | - |
| Analytics | - | - | Read | Read | - | - |
| Support tickets | Create/Read own | Create | Full CRUD | Read/Update | Read | - |
| Branding config | - | - | Full CRUD | Read | - | - |
| Branch management | - | - | Full CRUD | Read | - | - |
| System settings | - | - | Full CRUD | Read | - | - |
| Push notifications | - | - | Create | Create | - | - |
| Customer database | - | - | Read | Read | - | - |

### 5.8 Middleware Chain

```
Request -> Rate Limiter -> CORS -> Helmet -> Auth Middleware -> Role Middleware -> Validation -> Controller
```

**Auth Middleware** (`authMiddleware`):
1. Extract Bearer token from Authorization header
2. Verify JWT signature using public key
3. Check token expiry
4. Attach decoded user claims to `req.user`
5. For guest-allowed routes, generate guest context if no token

**Role Middleware** (`requireRole(...roles)`):
1. Check `req.user.type` against allowed roles
2. For admin routes, optionally check `admin_role` for granular permissions
3. For branch-scoped admins, verify access to the requested branch

---

## 6. Real-Time Architecture

### 6.1 Socket.io Server Design

The real-time system runs as part of the Delivery Service, with a dedicated Socket.io server accessible at `wss://api.{domain}/realtime`.

**Connection Authentication:**
- Clients connect with JWT token in handshake auth: `io({ auth: { token: "jwt_token" } })`
- Server validates JWT on connection, rejects unauthorized connections
- Token refresh handled via `socket.emit('refresh-token', newToken)`

### 6.2 Namespace Design

#### `/tracking` Namespace
Used for real-time GPS tracking and delivery status updates.

| Event | Direction | Emitter | Payload | Description |
|---|---|---|---|---|
| `driver:location-update` | Client -> Server | Driver App | `{ lat, lng, heading, speed, timestamp }` | Driver sends GPS position (every 10 seconds) |
| `tracking:location` | Server -> Client | Server | `{ driver_id, lat, lng, heading, eta_minutes }` | Broadcast driver position to order room |
| `tracking:eta-update` | Server -> Client | Server | `{ order_id, eta_minutes, distance_km }` | Updated ETA calculation |
| `driver:go-online` | Client -> Server | Driver App | `{ driver_id }` | Driver starts shift |
| `driver:go-offline` | Client -> Server | Driver App | `{ driver_id }` | Driver ends shift |

#### `/orders` Namespace
Used for order lifecycle real-time updates.

| Event | Direction | Emitter | Payload | Description |
|---|---|---|---|---|
| `order:new` | Server -> Client | Server | `{ order }` | New order notification to restaurant dashboard |
| `order:status-changed` | Server -> Client | Server | `{ order_id, old_status, new_status, timestamp }` | Order status update to all parties |
| `order:accepted` | Server -> Client | Server | `{ order_id, estimated_prep_time }` | Restaurant accepted order |
| `order:driver-assigned` | Server -> Client | Server | `{ order_id, driver_id, driver_name, eta }` | Driver assigned notification |
| `order:cancelled` | Server -> Client | Server | `{ order_id, reason, cancelled_by }` | Order cancellation |
| `order:ready` | Server -> Client | Server | `{ order_id }` | Order ready for pickup/delivery |

#### `/notifications` Namespace
Used for real-time in-app notification delivery.

| Event | Direction | Emitter | Payload | Description |
|---|---|---|---|---|
| `notification:new` | Server -> Client | Server | `{ notification }` | New in-app notification |
| `notification:count` | Server -> Client | Server | `{ unread_count }` | Updated unread count |

### 6.3 Room Strategy

```
Rooms:
  order:{orderId}        -> Customer + Driver + Restaurant admin (for specific order tracking)
  restaurant:{restaurantId}  -> All restaurant admins (for new order alerts, order board)
  branch:{branchId}      -> Branch-specific admins (for branch-scoped order board)
  driver:{driverId}      -> Individual driver room (for assignment notifications)
  customer:{customerId}  -> Individual customer room (for order updates, promos)
```

**Room Join Logic:**
- **Customer** joins `customer:{customerId}` on connect, and `order:{orderId}` when viewing order tracking
- **Driver** joins `driver:{driverId}` on connect, and `order:{orderId}` when assigned to delivery
- **Restaurant admin** joins `restaurant:{restaurantId}` (and optionally `branch:{branchId}`) on connect

### 6.4 Connection Management

**Reconnection Strategy:**
- Client: Exponential backoff (1s, 2s, 4s, 8s, max 30s)
- Max reconnection attempts: 50 (then show "connection lost" UI)
- On reconnect: re-authenticate, rejoin rooms, fetch missed events via REST API

**Scaling Strategy:**
- Socket.io with Redis adapter (`@socket.io/redis-adapter`) for multi-instance support
- Each ECS task runs a Socket.io instance; Redis Pub/Sub synchronizes events across instances
- Sticky sessions via ALB for WebSocket connections

**Driver Location Broadcasting Optimization:**
- Driver sends location every 10 seconds
- Server updates Redis (ephemeral) with latest position: `driver:location:{driverId}`
- Server broadcasts to order room only if driver has active delivery
- Location history written to PostgreSQL in batches (every 60 seconds) for route reconstruction
- When driver is idle (no active delivery), location updates are stored in Redis only (for nearest-driver queries)

**Heartbeat and Timeout:**
- Ping interval: 25 seconds
- Ping timeout: 20 seconds
- If driver disconnects without going offline, mark as unavailable after 2 minutes of no heartbeat

---

## 7. Payment Architecture

### 7.1 Payment Flow Overview

All payment processing uses Stripe as the primary gateway for card payments (Visa, Mastercard, Mada) and Google Pay. STC Pay requires a separate integration path. Cash on Delivery (COD) is handled locally without external gateway.

### 7.2 Stripe Payment Flow (Card / Mada / Google Pay)

```
Customer App/Web          Backend (Payment Service)         Stripe API
     |                            |                             |
     |-- 1. Checkout: select      |                             |
     |   payment method --------->|                             |
     |                            |                             |
     |                            |-- 2. Create PaymentIntent   |
     |                            |   { amount, currency: SAR,  |
     |                            |     payment_method_types:   |
     |                            |     ['card'],              |
     |                            |     metadata: { order_id }} |
     |                            |   ---------------------------->|
     |                            |                             |
     |                            |<-- 3. client_secret --------|
     |                            |                             |
     |<-- 4. Return client_secret |                             |
     |                            |                             |
     |-- 5. Confirm payment       |                             |
     |   (Stripe SDK handles      |                             |
     |    card input, 3DS, etc.)  |                             |
     |   -------------------------------------------------->|
     |                            |                             |
     |<-- 6. Payment result ------|<-- 7. Webhook:             |
     |   (success/failure)        |   payment_intent.succeeded  |
     |                            |   or .failed ---------------|
     |                            |                             |
     |                            |-- 8. Update payment record  |
     |                            |   Emit order.payment_confirmed |
     |                            |   or order.payment_failed   |
```

**Mada Integration (via Stripe):**
- Stripe supports Mada natively in Saudi Arabia
- Mada cards are detected automatically by Stripe when `card` payment method type is used
- No special integration needed; Stripe routes Mada transactions through the local network
- Mada transactions may have different authentication flows (handled by Stripe SDK)

**Google Pay Integration (via Stripe):**
- Stripe supports Google Pay through the Payment Request API
- Mobile: Use `@stripe/stripe-react-native` with Google Pay configuration
- Web: Use Stripe Payment Request Button element
- Configuration: Google Pay merchant ID registered with Google

### 7.3 STC Pay Integration

```
Customer App/Web          Backend (Payment Service)         STC Pay API
     |                            |                             |
     |-- 1. Select STC Pay ------>|                             |
     |                            |                             |
     |                            |-- 2. Create STC Pay         |
     |                            |   payment request           |
     |                            |   { amount, merchant_id,    |
     |                            |     order_ref, callback } ->|
     |                            |                             |
     |                            |<-- 3. Payment URL/OTP ref --|
     |                            |                             |
     |<-- 4. Redirect to STC Pay  |                             |
     |   or show OTP prompt       |                             |
     |                            |                             |
     |-- 5. Customer confirms     |                             |
     |   via STC Pay app/OTP ---->|                             |
     |                            |                             |
     |                            |<-- 6. Webhook: payment      |
     |                            |   status notification ------|
     |                            |                             |
     |                            |-- 7. Verify payment status  |
     |                            |   (callback validation) --->|
     |                            |                             |
     |                            |-- 8. Update payment record  |
     |                            |   Emit order.payment_confirmed |
```

**STC Pay Implementation Notes:**
- STC Pay does NOT currently integrate via Stripe; requires separate API integration
- STC Pay merchant account must be set up by the client
- Integration uses STC Pay's merchant API (REST-based)
- Payment confirmation via webhook + server-side verification
- STC Pay OTP flow is handled by STC Pay's own UI/SDK
- [TBD] Exact STC Pay API documentation and sandbox availability to be confirmed during development

### 7.4 Cash on Delivery (COD) Flow

```
Customer App              Backend (Payment Service)         Order Service
     |                            |                             |
     |-- 1. Select COD as         |                             |
     |   payment method --------->|                             |
     |                            |                             |
     |                            |-- 2. Create payment record  |
     |                            |   { method: 'cod',          |
     |                            |     status: 'pending' }     |
     |                            |                             |
     |                            |-- 3. Emit order.placed ---->|
     |                            |   (skip payment_confirmed   |
     |                            |    for COD orders)          |
     |                            |                             |
     |                            |   Order goes directly to    |
     |                            |   'accepted' status (pending |
     |                            |   restaurant confirmation)  |
     |                            |                             |
     |   ... delivery happens ... |                             |
     |                            |                             |
     |                            |<-- 4. Driver confirms       |
     |                            |   delivery (cash collected) |
     |                            |                             |
     |                            |-- 5. Update payment status  |
     |                            |   to 'succeeded'            |
```

### 7.5 Refund Flow (Technical Failures Only)

Per PROJECT_SCOPE.md, refunds are limited to technical/payment failures only (stuck payments, double charges). No general order refund workflow.

```
Dashboard (Admin)         Backend (Payment Service)         Stripe API
     |                            |                             |
     |-- 1. Admin identifies      |                             |
     |   technical failure        |                             |
     |   (double charge, stuck)   |                             |
     |                            |                             |
     |-- 2. POST /payments/refund |                             |
     |   { payment_id, amount,    |                             |
     |     reason: 'double_charge'|                             |
     |     or 'payment_stuck' } ->|                             |
     |                            |                             |
     |                            |-- 3. Validate:              |
     |                            |   - reason is allowed       |
     |                            |   - amount <= original      |
     |                            |   - not already refunded    |
     |                            |                             |
     |                            |-- 4. Stripe Refund API      |
     |                            |   { payment_intent,         |
     |                            |     amount } --------------->|
     |                            |                             |
     |                            |<-- 5. Refund result --------|
     |                            |                             |
     |                            |-- 6. Record refund in DB    |
     |                            |   Update payment status     |
     |                            |                             |
     |<-- 7. Refund confirmation -|                             |
```

**Allowed Refund Reasons (enforced in code):**
- `payment_stuck` - Payment processing timed out but amount was charged
- `double_charge` - Customer was charged twice for the same order
- `technical_failure` - Generic technical error in payment processing

### 7.6 Saved Cards (Stripe Setup Intent)

```
Customer App/Web          Backend (Payment Service)         Stripe API
     |                            |                             |
     |-- 1. Request to save       |                             |
     |   new card --------------->|                             |
     |                            |                             |
     |                            |-- 2. Create SetupIntent     |
     |                            |   { customer: stripe_cust } |
     |                            |   --------------------------->|
     |                            |                             |
     |                            |<-- 3. client_secret ---------|
     |                            |                             |
     |<-- 4. Return client_secret |                             |
     |                            |                             |
     |-- 5. Confirm setup         |                             |
     |   (Stripe SDK collects     |                             |
     |    card details securely)  |                             |
     |   -------------------------------------------------->|
     |                            |                             |
     |                            |<-- 6. Webhook:              |
     |                            |   setup_intent.succeeded    |
     |                            |   + payment_method ----------|
     |                            |                             |
     |                            |-- 7. Save card metadata     |
     |                            |   (brand, last4, expiry)    |
     |                            |   to saved_cards table      |
```

### 7.7 PCI Compliance Approach

- **No card data touches our servers**: Stripe Elements (web) and Stripe SDK (mobile) handle all card input
- Card numbers, CVV, and full expiry are never transmitted to or stored on our backend
- Only tokenized references (Stripe PaymentMethod IDs) are stored
- Stripe handles PCI DSS Level 1 compliance; our platform operates at SAQ-A level
- All communication over HTTPS/TLS 1.2+
- Stripe webhook signatures verified using shared secret

### 7.8 Webhook Handling

**Stripe Webhooks to Handle:**

| Event | Action |
|---|---|
| `payment_intent.succeeded` | Update payment status, confirm order, notify customer |
| `payment_intent.payment_failed` | Update payment status, notify customer, mark order as payment_failed |
| `charge.refunded` | Update refund status in DB |
| `charge.dispute.created` | Alert admin, log dispute |
| `customer.subscription.deleted` | N/A (no subscriptions in Phase 1) |

**Webhook Security:**
- Verify Stripe signature using `stripe.webhooks.constructEvent(body, sig, secret)`
- Idempotent processing using Stripe event ID (prevent duplicate handling)
- Failed webhook processing retried via BullMQ dead-letter queue
- Webhook endpoint: `POST /api/v1/payments/webhook/stripe` (no auth middleware, signature-verified)

### 7.9 Currency and VAT

- **Currency**: SAR (Saudi Riyal) only in Phase 1
- **VAT Rate**: 15% (configurable per restaurant in `config.restaurants.vat_rate`)
- **VAT Calculation**: Applied to subtotal (items + delivery fee)
- **VAT Display**: Shown upfront in cart, breakdown on receipt
- **VAT-Compliant Receipt Fields**: Restaurant name, VAT number, commercial registration, itemized amounts, VAT amount, total, date, order number

---

## 8. Deployment Strategy

### 8.1 Docker Containerization

Each microservice is containerized with its own Dockerfile. A shared base image is used for consistency.

**Base Dockerfile (Node.js services):**
```dockerfile
FROM node:20-alpine AS base
WORKDIR /app
RUN apk add --no-cache dumb-init

FROM base AS dependencies
COPY package.json package-lock.json ./
RUN npm ci --only=production

FROM base AS build
COPY package.json package-lock.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM base AS production
ENV NODE_ENV=production
COPY --from=dependencies /app/node_modules ./node_modules
COPY --from=build /app/dist ./dist
COPY --from=build /app/prisma ./prisma
RUN npx prisma generate
USER node
EXPOSE 3000
CMD ["dumb-init", "node", "dist/server.js"]
```

**Docker Compose (Development):**
- All 13 services + PostgreSQL + Redis + Nginx + pgAdmin
- Hot-reload via volume mounts
- Shared network for inter-service communication
- Environment variables via `.env` file

**Service Container List:**

| Container | Port | Replicas (Prod) | Memory | CPU |
|---|---|---|---|---|
| nginx-gateway | 80/443 | 2 | 256 MB | 0.25 vCPU |
| auth-service | 3001 | 2 | 512 MB | 0.5 vCPU |
| user-service | 3002 | 2 | 512 MB | 0.5 vCPU |
| menu-service | 3003 | 2 | 512 MB | 0.5 vCPU |
| order-service | 3004 | 3 | 1 GB | 1 vCPU |
| cart-service | 3005 | 2 | 512 MB | 0.5 vCPU |
| payment-service | 3006 | 2 | 512 MB | 0.5 vCPU |
| delivery-service | 3007 | 3 | 1 GB | 1 vCPU |
| notification-service | 3008 | 2 | 512 MB | 0.5 vCPU |
| promo-loyalty-service | 3009 | 2 | 512 MB | 0.5 vCPU |
| analytics-service | 3010 | 1 | 1 GB | 0.5 vCPU |
| support-service | 3011 | 1 | 256 MB | 0.25 vCPU |
| config-service | 3012 | 2 | 256 MB | 0.25 vCPU |
| file-service | 3013 | 2 | 512 MB | 0.5 vCPU |

### 8.2 AWS ECS Fargate Setup

**Cluster Architecture:**
- 1 ECS Cluster per environment (dev, staging, production)
- Services run as Fargate tasks (no EC2 instance management)
- Auto-scaling based on CPU/memory utilization (target 70%)
- Application Load Balancer (ALB) with path-based routing

**Networking:**
- VPC with public and private subnets across 2 AZs in me-south-1 (Bahrain)
- Services in private subnets (no direct internet access)
- ALB in public subnets
- NAT Gateway for outbound internet (external API calls)
- VPC Endpoints for AWS services (S3, ECR, CloudWatch, Secrets Manager)

**Service Discovery:**
- AWS Cloud Map for internal service-to-service DNS resolution
- Service names: `auth.internal`, `user.internal`, `menu.internal`, etc.
- Health checks via ALB target group health checks

### 8.3 Environment Strategy

| Environment | Purpose | AWS Account | Database | URL Pattern |
|---|---|---|---|---|
| **Development** | Local developer machines | N/A (Docker Compose) | Local PostgreSQL | `localhost:*` |
| **Staging** | Pre-production testing, QA | Shared AWS account | RDS (Single AZ) | `staging-api.{domain}` |
| **Production** | Live environment | Dedicated AWS account | RDS (Multi-AZ) | `api.{domain}` |

**Environment Variable Categories:**

| Category | Storage | Examples |
|---|---|---|
| Secrets | AWS Secrets Manager | DB passwords, Stripe secret key, JWT private key, Firebase service account |
| Config | AWS SSM Parameter Store | API URLs, feature flags, rate limits, VAT rate |
| Build-time | CI/CD pipeline | Node environment, build version, commit hash |

### 8.4 Database Migration Strategy

**Tool:** Prisma Migrate

**Migration Workflow:**
1. Developer creates/modifies `schema.prisma` file
2. Run `npx prisma migrate dev --name descriptive-name` locally
3. Migration SQL file committed to git in `prisma/migrations/` directory
4. CI/CD runs `npx prisma migrate deploy` on staging/production
5. Migrations are applied in order, tracked in `_prisma_migrations` table

**Migration Safety Rules:**
- Never delete columns in production without deprecation period
- Add columns as nullable first, then backfill, then add NOT NULL constraint
- Use shadow database for migration validation in CI
- Database backups taken before every production migration
- Rollback scripts prepared for every migration

### 8.5 Zero-Downtime Deployment

**Rolling Update Strategy (ECS):**
1. New Docker image built and pushed to ECR
2. ECS task definition updated with new image tag
3. ECS performs rolling update:
   - Start new tasks with new version
   - Wait for new tasks to pass health check
   - Drain connections from old tasks
   - Stop old tasks
4. Minimum healthy percent: 100% (no downtime)
5. Maximum percent: 200% (double capacity during deploy)

**Health Check Configuration:**
- Health check path: `GET /health`
- Interval: 30 seconds
- Healthy threshold: 2 consecutive successes
- Unhealthy threshold: 3 consecutive failures
- Timeout: 10 seconds
- Grace period: 60 seconds (for service startup)

**Database Migration During Deployment:**
- Migrations run as a separate ECS task (not part of service startup)
- Migration task runs before new service version is deployed
- Only backward-compatible migrations allowed (additive changes)
- Breaking changes require multi-step deployment:
  1. Deploy code that handles both old and new schema
  2. Run migration
  3. Deploy code that uses only new schema

### 8.6 CI/CD Pipeline (GitHub Actions)

**Pipeline Stages:**

```
Trigger (push to branch)
    |
    v
1. Lint & Type Check
    - ESLint
    - TypeScript compiler (tsc --noEmit)
    |
    v
2. Unit Tests
    - Jest (all services in parallel)
    - Coverage report (minimum 80%)
    |
    v
3. Integration Tests
    - Supertest with test database
    - Docker Compose for dependencies
    |
    v
4. Build Docker Images
    - Multi-stage build
    - Tag with commit SHA + branch name
    |
    v
5. Push to ECR
    - Push to staging ECR (for staging branch)
    - Push to production ECR (for main branch)
    |
    v
6. Deploy to Staging (automatic for staging branch)
    - Run database migrations
    - Update ECS services
    - Run smoke tests
    |
    v
7. Deploy to Production (manual approval for main branch)
    - Run database migrations
    - Rolling update ECS services
    - Post-deployment health verification
    - Rollback on failure
```

**Branch Strategy:**
- `main` - Production-ready code
- `staging` - Pre-production testing
- `develop` - Development integration
- `feature/*` - Feature branches (PR to develop)
- `hotfix/*` - Production hotfixes (PR to main + develop)

### 8.7 Mobile App Build and Distribution

**React Native Android Build:**
- Build tool: Gradle (via React Native CLI or EAS Build)
- Signing: Release keystore stored in AWS Secrets Manager
- Build variants: `debug`, `staging`, `release`
- Build automation: GitHub Actions with Android SDK

**Distribution:**
- Internal testing: Firebase App Distribution (staging builds)
- Production: Google Play Store
- App Bundle format (.aab) for Play Store submission
- [TBD] Google Play Store account management and submission process (client or vendor)

---

## 9. Testing Strategy

### 9.1 Unit Tests

**Framework:** Jest 29.x with TypeScript support

**Scope:** All business logic functions, utility functions, validators, middleware

**Coverage Target:** 80% line coverage minimum per service

**Conventions:**
- Test files co-located with source: `service.ts` -> `service.test.ts`
- Describe blocks mirror module/function names
- Mock external dependencies (database, APIs, Redis)
- Test both success and error paths

**Key Areas per Service:**
| Service | Unit Test Focus |
|---|---|
| Auth | Token generation/validation, password hashing, role checks |
| User | Profile validation, address formatting, preference logic |
| Menu | Price calculation (base + variants), search ranking, availability rules |
| Order | Status transition validation, order total calculation, VAT computation, order number generation |
| Cart | Item total calculation, promo application, upsell rule matching |
| Payment | Payment intent creation, refund validation (allowed reasons), webhook signature verification |
| Delivery | Zone containment (point-in-polygon), fee calculation, ETA estimation, nearest-driver selection |
| Notification | Template variable replacement, preference filtering, FCM payload construction |
| Promo & Loyalty | Promo validation (expiry, usage limits, min order), points calculation, redemption limits |
| Analytics | Data aggregation logic, report formatting, date range calculations |

### 9.2 Integration Tests

**Framework:** Jest + Supertest

**Scope:** API endpoint testing with real database (test database in Docker)

**Setup:**
- Docker Compose spins up PostgreSQL + Redis for tests
- Database migrations run before test suite
- Each test suite seeds its own data
- Transactions rolled back after each test (or truncate tables)

**Key Integration Test Scenarios:**
1. Full registration flow (OTP -> profile creation -> JWT)
2. Menu CRUD with category hierarchy
3. Cart -> Order -> Payment flow
4. Order status transitions (full lifecycle)
5. Promo code application and validation
6. Delivery zone fee calculation
7. Loyalty points earn and redeem
8. Webhook processing (Stripe payment events)
9. Multi-branch menu isolation

### 9.3 End-to-End Tests

**Mobile (React Native):** Detox
- Customer app: Full ordering flow (browse -> cart -> checkout -> track)
- Driver app: Login -> receive assignment -> navigate -> deliver
- Arabic/RTL layout verification

**Web (Dashboard + Customer Web):** Playwright
- Restaurant dashboard: Menu management, order processing, driver management
- Customer web: Browse menu, place order, track order
- Cross-browser testing: Chrome, Firefox, Edge

**Key E2E Scenarios:**

| Scenario | Apps Involved | Description |
|---|---|---|
| Happy path order | Customer + Dashboard + Driver | Complete order from browse to delivery |
| Guest to registered user | Customer | Browse as guest, register at checkout, complete order |
| COD order | Customer + Dashboard + Driver | Cash on delivery flow |
| Scheduled order | Customer + Dashboard | Place order for future time |
| Order cancellation | Customer + Dashboard | Cancel before preparation |
| Promo code flow | Customer | Apply promo, verify discount, checkout |
| Multi-branch | Customer | Switch between branches, verify separate menus |
| Driver shift management | Driver + Dashboard | Start shift, receive orders, end shift |
| Menu management | Dashboard | Add category, add item with variants, toggle availability |
| Arabic RTL | All | Verify all screens render correctly in Arabic/RTL |

### 9.4 Arabic/RTL Testing Approach

**Automated:**
- Playwright visual regression tests comparing LTR (English) and RTL (Arabic) screenshots
- Layout assertion tests verifying text alignment, margin/padding directions
- i18n key completeness check (ensure all English keys have Arabic translations)

**Manual QA Checklist:**
- Text truncation in Arabic (Arabic text is generally shorter than English)
- Number display (Arabic-Indic numerals vs Western Arabic numerals - use Western Arabic)
- Date formatting (Gregorian calendar, not Hijri, for order dates)
- Currency formatting: SAR amount (e.g., 45.00 SAR)
- Phone number display (LTR within RTL context)
- Map interaction (pin-drop, zone drawing) in RTL mode
- Form input direction (some fields like email remain LTR)
- Icons that imply direction (arrows, back buttons) are mirrored

### 9.5 Payment Testing

**Stripe Test Mode:**
- All development and staging environments use Stripe test API keys
- Test card numbers:
  - Visa: `4242 4242 4242 4242`
  - Mastercard: `5555 5555 5555 4444`
  - Mada: Use Stripe test Mada cards for Saudi Arabia
  - 3DS required: `4000 0025 0000 3155`
  - Decline: `4000 0000 0000 0002`
- Webhook testing: Stripe CLI (`stripe listen --forward-to localhost:3006/api/v1/payments/webhook/stripe`)
- Google Pay: Test environment with Stripe test mode

**STC Pay Testing:**
- [TBD] STC Pay sandbox environment availability to be confirmed
- Fallback: Mock STC Pay API for development, test with real sandbox when available

### 9.6 GPS and Real-Time Testing

**GPS Simulation:**
- Android Emulator: Mock location provider for simulated routes
- Detox: Programmatic location mocking
- Tools: GPX file replay for predefined routes in Riyadh

**Socket.io Testing:**
- Unit: `socket.io-client` mock for event emission/reception
- Integration: Real Socket.io server with test clients
- Load: Artillery with Socket.io plugin for concurrent connection testing

### 9.7 Load Testing

**Tool:** k6 (Grafana)

**Target Performance Metrics:**

| Metric | Target |
|---|---|
| API response time (p95) | < 500ms |
| API response time (p99) | < 1000ms |
| Concurrent users | 500 (Phase 1 launch target) |
| Orders per minute | 50 |
| Socket.io concurrent connections | 1000 |
| Driver location updates/second | 100 |

**Load Test Scenarios:**
1. Menu browsing (high read volume)
2. Concurrent order placement (peak lunch/dinner hours)
3. Real-time tracking (many simultaneous Socket.io connections)
4. Search with auto-suggest (rapid keystroke simulation)
5. Payment processing under load

### 9.8 Security Testing

**Automated:**
- OWASP ZAP: Automated security scanning of all API endpoints
- npm audit: Dependency vulnerability scanning in CI
- Snyk: Continuous dependency monitoring

**Manual/Periodic:**
- Authentication bypass attempts
- SQL injection testing (parameterized queries should prevent)
- XSS testing on user-generated content (reviews, support messages)
- Rate limit verification
- JWT token manipulation attempts
- File upload malicious payload testing

---

## 10. Monitoring and Logging

### 10.1 Centralized Logging

**Stack:** Winston (application) + Morgan (HTTP) -> AWS CloudWatch Logs

**Log Format (JSON structured):**
```json
{
  "timestamp": "2026-03-16T12:00:00.000Z",
  "level": "info",
  "service": "order-service",
  "traceId": "abc-123-def-456",
  "userId": "user-uuid",
  "method": "POST",
  "path": "/api/v1/orders",
  "statusCode": 201,
  "duration": 145,
  "message": "Order created successfully",
  "metadata": {
    "orderId": "order-uuid",
    "orderNumber": "ORD-20260316-001"
  }
}
```

**Log Levels:**
- `error` - Application errors, unhandled exceptions, payment failures
- `warn` - Degraded performance, retry attempts, rate limit hits
- `info` - Request/response logs, business events (order placed, payment confirmed)
- `debug` - Detailed debugging (disabled in production)

**Log Groups (CloudWatch):**
- `/fooddelivery/{env}/{service-name}` per service
- Retention: 30 days (staging), 90 days (production)

**Distributed Tracing:**
- Each request assigned a `traceId` (UUID) at the API gateway
- `traceId` propagated through all inter-service calls via `x-trace-id` header
- All log entries include `traceId` for cross-service request tracing

### 10.2 Application Performance Monitoring (APM)

**Primary Tool:** Sentry

**Configuration:**
- Sentry SDK integrated in all backend services and frontend apps
- Source maps uploaded for React Native and React.js builds
- Performance monitoring enabled (transaction tracing)
- Release tracking tied to Git commit SHA

**Tracked Metrics:**
- Transaction duration (per API endpoint)
- Error rate (per service)
- User-facing errors (with breadcrumbs)
- Slow queries (Prisma query instrumentation)

### 10.3 Infrastructure Monitoring

**AWS CloudWatch Dashboards:**

**Dashboard 1: Service Health**
- ECS task count per service (running vs desired)
- CPU utilization per service
- Memory utilization per service
- ALB healthy/unhealthy host count
- Request count per target group

**Dashboard 2: Database & Cache**
- RDS CPU utilization
- RDS connections count
- RDS read/write IOPS
- RDS storage space
- ElastiCache CPU, memory, connections
- ElastiCache cache hit rate

**Dashboard 3: Business Metrics**
- Orders per minute (from application logs)
- Payment success/failure rate
- Active Socket.io connections
- FCM notification delivery rate

### 10.4 Health Checks

Each service exposes a health check endpoint:

**`GET /health`** Response:
```json
{
  "status": "healthy",
  "service": "order-service",
  "version": "1.2.3",
  "uptime": 86400,
  "timestamp": "2026-03-16T12:00:00.000Z",
  "dependencies": {
    "database": "healthy",
    "redis": "healthy",
    "external_apis": {
      "stripe": "healthy",
      "firebase": "healthy"
    }
  }
}
```

**Health Check Types:**
- **Shallow** (ALB): Returns 200 if process is running (used for load balancer routing)
- **Deep** (monitoring): Checks database, Redis, and external API connectivity

### 10.5 Alerting Strategy

| Alert | Condition | Severity | Channel |
|---|---|---|---|
| Service down | Health check fails for 3 minutes | Critical | SMS + Slack |
| High error rate | >5% error rate for 5 minutes | High | Slack |
| High latency | p95 > 2s for 10 minutes | High | Slack |
| Database CPU > 80% | Sustained for 10 minutes | High | Slack |
| Database connections > 80% | Sustained for 5 minutes | High | Slack |
| Payment failure rate > 10% | For 5 minutes | Critical | SMS + Slack |
| Disk usage > 80% | Any service or RDS | Medium | Slack |
| Memory usage > 90% | Any ECS task | High | Slack |
| Socket.io disconnection spike | >20% drop in 5 minutes | High | Slack |
| Zero orders for 30 minutes | During operating hours | Medium | Slack |

### 10.6 Key Business Metrics to Monitor

| Metric | Source | Dashboard |
|---|---|---|
| Orders per hour/day | Order Service logs | Business Metrics |
| Average order value | Analytics Service | Business Metrics |
| Order completion rate | Order status events | Business Metrics |
| Average delivery time | Delivery Service | Business Metrics |
| Customer registration rate | Auth Service logs | Business Metrics |
| Payment method distribution | Payment Service | Business Metrics |
| Cart abandonment rate | Cart + Order comparison | Business Metrics |
| API error rate by endpoint | Application logs | Service Health |
| FCM delivery success rate | Notification Service | Service Health |

---

## 11. Security Considerations

### 11.1 Transport Security

- **HTTPS everywhere**: All client-server communication over TLS 1.2+
- **SSL certificates**: AWS Certificate Manager with auto-renewal
- **HSTS headers**: Strict-Transport-Security enabled via Helmet
- **WebSocket security**: WSS (WebSocket Secure) for all Socket.io connections

### 11.2 Authentication Security

- **JWT signing**: RS256 (asymmetric) with RSA 2048-bit key pair
- **Access token expiry**: 1 hour (short-lived)
- **Refresh token expiry**: 30 days
- **Refresh token rotation**: New pair issued on each refresh; old token invalidated
- **Breach detection**: If an invalidated refresh token is reused, all user sessions are terminated
- **Password hashing**: bcrypt with 12 salt rounds (for driver and admin accounts)
- **Firebase Auth**: Handles OTP security (rate limiting, fraud detection) for customer registration
- **Session management**: Active sessions tracked in database; user can view and revoke sessions

### 11.3 API Security

**Rate Limiting (per endpoint category):**

| Endpoint Category | Rate Limit | Window |
|---|---|---|
| Auth (login/register) | 5 requests | 1 minute |
| OTP verification | 3 attempts | 5 minutes |
| General API (authenticated) | 100 requests | 1 minute |
| Menu browsing (public) | 200 requests | 1 minute |
| Search | 30 requests | 1 minute |
| File upload | 10 requests | 1 minute |
| Payment creation | 5 requests | 1 minute |
| Webhook endpoints | 1000 requests | 1 minute |

**Implementation:** `express-rate-limit` with Redis store for distributed rate limiting across ECS instances

**Input Validation:**
- Zod schemas validate all request bodies, query parameters, and path parameters
- Type coercion disabled (strict validation)
- Maximum request body size: 10 MB (file uploads), 1 MB (JSON)
- SQL injection prevention: Prisma ORM with parameterized queries (no raw SQL except PostGIS functions with parameter binding)

**CORS Configuration:**
```javascript
{
  origin: [
    'https://{restaurant-domain}',     // Customer web
    'https://dashboard.{domain}',       // Restaurant dashboard
    'https://staging-*.{domain}'        // Staging environments
  ],
  methods: ['GET', 'POST', 'PUT', 'PATCH', 'DELETE'],
  allowedHeaders: ['Content-Type', 'Authorization', 'x-trace-id'],
  credentials: true,
  maxAge: 86400
}
```

### 11.4 Data Security

**Encryption at Rest:**
- AWS RDS: AES-256 encryption enabled (default for RDS)
- AWS S3: Server-side encryption (SSE-S3) for all stored files
- AWS ElastiCache: At-rest encryption enabled

**Encryption in Transit:**
- TLS 1.2+ for all connections
- RDS connections use SSL certificates
- Redis connections use TLS (ElastiCache in-transit encryption)

**Sensitive Data Handling:**
- No card numbers, CVVs, or full card details ever touch our servers (Stripe handles PCI)
- Phone numbers and emails stored in clear text (needed for operations) but access-controlled
- Driver documents (license, ID) stored in private S3 bucket with signed URL access
- Passwords (driver/admin) stored as bcrypt hashes only
- Firebase UIDs are opaque identifiers (no sensitive data)

### 11.5 File Upload Security

- **Allowed file types**: Images (JPEG, PNG, WebP), Documents (PDF) for driver documents
- **File type validation**: Check both MIME type and file magic bytes (not just extension)
- **Maximum file size**: 10 MB for images, 20 MB for documents
- **Image processing**: All uploaded images re-encoded via Sharp (strips EXIF data, prevents image-based exploits)
- **Filename sanitization**: Generate UUID-based filenames; never use user-provided filenames
- **S3 bucket policy**: Private by default; access only via presigned URLs with expiry
- **Virus scanning**: [TBD] Consider AWS S3 malware scanning or ClamAV integration

### 11.6 XSS and Injection Prevention

- **Output encoding**: All user-generated content (reviews, support messages, special instructions) encoded when rendered
- **React**: JSX auto-escapes rendered content by default
- **Helmet security headers**: Content-Security-Policy, X-Content-Type-Options, X-Frame-Options, X-XSS-Protection
- **No `dangerouslySetInnerHTML`** without sanitization (DOMPurify if needed for email campaign previews)

### 11.7 PCI DSS Compliance

- **SAQ-A eligibility**: No card data touches our servers; all payment UI handled by Stripe SDK/Elements
- **Stripe Elements** (web): PCI-compliant iframe-based card input
- **Stripe React Native SDK** (mobile): Secure card input via Stripe-hosted UI
- **No card storage**: Only Stripe PaymentMethod tokens (references) stored in our database
- **Audit trail**: All payment events logged (amount, status, timestamp) without sensitive card data

### 11.8 Saudi Regulatory Compliance

**PDPL (Personal Data Protection Law):**
- Data residency: All data stored in AWS Bahrain region (me-south-1)
- Data minimization: Collect only necessary personal data
- Consent: Clear privacy policy and consent at registration
- Data deletion: Ability to delete customer account and associated data upon request
- Data access: Customer can view and export their personal data

**VAT Compliance (ZATCA):**
- 15% VAT calculated and displayed on all orders
- VAT-compliant electronic receipts with required fields
- Restaurant VAT number displayed on receipts
- [TBD] ZATCA e-invoicing integration requirements (Phase 2 consideration)

**General:**
- Arabic language as primary interface language
- Commercial registration number on receipts
- Food safety and hygiene disclaimers as required

---

## 12. White-Label Architecture

### 12.1 Branding Configuration Schema

The `branding_config` JSONB field in `config.restaurants` stores the complete white-label configuration:

```json
{
  "brand": {
    "name_en": "Al Baik",
    "name_ar": "البيك",
    "tagline_en": "Delicious Fried Chicken",
    "tagline_ar": "دجاج مقلي لذيذ",
    "description_en": "Saudi Arabia's favorite fried chicken restaurant",
    "description_ar": "مطعم الدجاج المقلي المفضل في المملكة العربية السعودية"
  },
  "colors": {
    "primary": "#FF6B00",
    "primaryLight": "#FF8A33",
    "primaryDark": "#CC5500",
    "secondary": "#1A1A2E",
    "secondaryLight": "#33334D",
    "accent": "#FFD700",
    "background": "#FFFFFF",
    "backgroundSecondary": "#F5F5F5",
    "surface": "#FFFFFF",
    "text": "#1A1A2E",
    "textSecondary": "#666666",
    "textOnPrimary": "#FFFFFF",
    "success": "#28A745",
    "warning": "#FFC107",
    "error": "#DC3545",
    "info": "#17A2B8",
    "border": "#E0E0E0",
    "divider": "#F0F0F0"
  },
  "typography": {
    "fontFamilyEn": "Inter",
    "fontFamilyAr": "Noto Sans Arabic",
    "headingFontEn": "Inter",
    "headingFontAr": "Noto Sans Arabic"
  },
  "assets": {
    "logoUrl": "https://cdn.{domain}/restaurants/{slug}/logo.png",
    "logoDarkUrl": "https://cdn.{domain}/restaurants/{slug}/logo-dark.png",
    "faviconUrl": "https://cdn.{domain}/restaurants/{slug}/favicon.ico",
    "appIconUrl": "https://cdn.{domain}/restaurants/{slug}/app-icon.png",
    "splashScreenUrl": "https://cdn.{domain}/restaurants/{slug}/splash.png",
    "heroImageUrl": "https://cdn.{domain}/restaurants/{slug}/hero.jpg",
    "ogImageUrl": "https://cdn.{domain}/restaurants/{slug}/og-image.jpg"
  },
  "layout": {
    "menuStyle": "grid",
    "categoryStyle": "horizontal_scroll",
    "showNutritionInfo": true,
    "showAllergyInfo": true,
    "showPopularBadge": true,
    "showEstimatedDeliveryTime": true,
    "heroEnabled": true,
    "showBranchSelector": true
  },
  "features": {
    "loyaltyEnabled": true,
    "scheduledOrdersEnabled": true,
    "pickupEnabled": true,
    "codEnabled": true,
    "guestBrowsingEnabled": true,
    "reviewsEnabled": true,
    "socialLoginGoogle": true,
    "socialLoginFacebook": true
  },
  "social": {
    "instagram": "https://instagram.com/albaik",
    "twitter": "https://twitter.com/albaik",
    "facebook": "https://facebook.com/albaik",
    "website": "https://albaik.com"
  },
  "legal": {
    "privacyPolicyUrl_en": "https://{domain}/privacy",
    "privacyPolicyUrl_ar": "https://{domain}/ar/privacy",
    "termsOfServiceUrl_en": "https://{domain}/terms",
    "termsOfServiceUrl_ar": "https://{domain}/ar/terms"
  }
}
```

### 12.2 Theme System Implementation

**React Native (Customer App + Driver App):**

```typescript
// theme/ThemeProvider.tsx
interface BrandTheme {
  colors: {
    primary: string;
    primaryLight: string;
    primaryDark: string;
    secondary: string;
    // ... all color keys from branding_config
  };
  typography: {
    fontFamilyEn: string;
    fontFamilyAr: string;
  };
  assets: {
    logoUrl: string;
    splashScreenUrl: string;
  };
}

// Theme loaded from API on app launch and cached locally
// React Native Paper theme provider wraps the app with dynamic colors
// All components reference theme values, never hardcoded colors
```

**React.js (Dashboard + Customer Web):**

```typescript
// CSS custom properties approach
:root {
  --color-primary: #FF6B00;
  --color-primary-light: #FF8A33;
  --color-primary-dark: #CC5500;
  --color-secondary: #1A1A2E;
  --color-background: #FFFFFF;
  --color-text: #1A1A2E;
  --font-family-en: 'Inter', sans-serif;
  --font-family-ar: 'Noto Sans Arabic', sans-serif;
  // ... generated from branding_config on app load
}

// CSS variables injected dynamically based on restaurant branding
// Tailwind CSS config (Customer Web) or Ant Design theme (Dashboard)
// references these CSS variables
```

### 12.3 White-Label Deployment Model

**Single Codebase, Multi-Tenant:**
- One backend deployment serves multiple restaurant brands
- Restaurant identified by subdomain or custom domain: `albaik.{platform-domain}` or `order.albaik.com`
- API requests include restaurant context via subdomain resolution or `x-restaurant-id` header
- Branding configuration fetched once on app/web launch and cached

**Mobile App Strategy:**
- Single APK/AAB with dynamic branding (fetched from API on first launch)
- App icon and splash screen set per restaurant at build time (requires separate build per restaurant)
- Alternative: Generic app with restaurant selection screen (if serving multiple restaurants from one app)
- [TBD] Final decision on single-build vs per-restaurant builds depends on number of planned deployments

**Web Strategy:**
- Customer Web: Next.js app deployed to CloudFront, restaurant detected by domain
- Dashboard: React SPA deployed to CloudFront, restaurant detected by login credentials

### 12.4 Branding Management in Dashboard

The restaurant dashboard includes a "Branding" section under Platform Configuration:

1. **Logo Upload**: Upload primary logo, dark mode logo, favicon, app icon
2. **Color Picker**: Interactive color selection for all theme colors with live preview
3. **Typography Selection**: Choose from approved font pairs (EN + AR)
4. **Feature Toggles**: Enable/disable optional features (loyalty, scheduled orders, COD, etc.)
5. **Social Links**: Add social media profile URLs
6. **Legal Pages**: Upload/link privacy policy and terms of service
7. **Preview**: Live preview of customer app/web with current branding

### 12.5 Asset Management

**S3 Bucket Structure:**
```
s3://fooddelivery-assets-{env}/
  restaurants/
    {restaurant-slug}/
      branding/
        logo.png
        logo-dark.png
        favicon.ico
        app-icon.png
        splash.png
        hero.jpg
        og-image.jpg
      menu/
        items/
          {item-id}/
            original.jpg
            thumb_200x200.jpg
            medium_600x400.jpg
        categories/
          {category-id}/
            original.jpg
            thumb_200x200.jpg
      drivers/
        {driver-id}/
          license.pdf
          national-id.pdf
      support/
        {ticket-id}/
          {attachment-filename}
```

**Image Processing Pipeline:**
1. Original image uploaded to S3
2. BullMQ job queued for image processing
3. Sharp generates multiple sizes: thumbnail (200x200), medium (600x400), original (max 1920px)
4. WebP format generated alongside JPEG for modern browsers
5. CloudFront serves images with automatic format selection (WebP for supported browsers)

---

## 13. Localization and RTL Strategy

### 13.1 Language Support

**Supported Languages:** Arabic (ar), English (en)
**Default Language:** Arabic (configurable per restaurant)
**Direction:** RTL for Arabic, LTR for English

### 13.2 i18n Implementation

**React Native (react-i18next):**
```typescript
// Translation files structure
/locales
  /ar
    common.json       // Shared strings (buttons, labels)
    menu.json          // Menu-related strings
    orders.json        // Order-related strings
    checkout.json      // Checkout flow strings
    tracking.json      // Tracking strings
    profile.json       // Profile and settings
    notifications.json // Notification strings
    errors.json        // Error messages
  /en
    common.json
    menu.json
    // ... same structure
```

**Key Conventions:**
- Translation keys use dot notation: `orders.status.preparing`
- Pluralization handled via i18next plural rules
- Interpolation for dynamic values: `{{orderNumber}}`
- Numbers always displayed in Western Arabic numerals (0-9), not Arabic-Indic
- Currency: `45.00 SAR` format (not localized number format)
- Dates: Gregorian calendar, formatted per locale

### 13.3 RTL Layout Strategy

**React Native:**
- `I18nManager.forceRTL(true)` for Arabic
- `I18nManager.allowRTL(true)` enabled
- App restart required on language switch (React Native limitation)
- `writingDirection` style prop for mixed-direction content
- `react-native-paper` has built-in RTL support

**React.js (Web):**
- `dir="rtl"` on `<html>` element for Arabic
- CSS logical properties: `margin-inline-start` instead of `margin-left`
- Tailwind CSS RTL plugin for utility classes
- Ant Design has built-in RTL support (ConfigProvider `direction="rtl"`)

**Mixed-Direction Content Rules:**
- Phone numbers: Always LTR (`direction: ltr; unicode-bidi: embed`)
- Email addresses: Always LTR
- URLs: Always LTR
- Numbers and currency: LTR within RTL context
- Map components: Not affected by RTL
- Back/forward icons: Mirrored in RTL (use `scaleX(-1)` or RTL-specific icons)

### 13.4 Bilingual Data Strategy

- All user-facing database fields have `_en` and `_ar` columns
- API responses include both languages; client displays based on user preference
- Menu items require both Arabic and English names (enforced at creation)
- Notification templates stored in both languages
- Admin dashboard fully bilingual (admin can switch language)
- Search works across both language fields

### 13.5 Arabic Typography

**Font Selection:**
- Arabic: Noto Sans Arabic (Google Font, excellent Arabic rendering, multiple weights)
- English: Inter (clean, modern, pairs well with Noto Sans Arabic)
- Both fonts loaded from Google Fonts CDN or bundled in mobile apps

**Typography Scale:**
- Arabic text generally renders slightly larger than English at the same font size
- Line height for Arabic: 1.6-1.8 (slightly more than English 1.4-1.6)
- Minimum font size for Arabic body text: 14px (to ensure readability of Arabic characters)

---

## 14. Third-Party Integration Details

### 14.1 Firebase Authentication

**Purpose:** Customer registration and login via phone OTP, social login verification

**Configuration:**
- Firebase project created in GCP console
- Android app registered with SHA-1 fingerprint
- Web app registered with domain
- Phone Authentication enabled in Firebase console
- Google and Facebook sign-in methods enabled

**Usage Quotas:**
- Free tier: 10,000 phone verifications/month
- Beyond free tier: $0.01-$0.06 per verification (volume-based)
- Monitor usage; alert at 80% of budget threshold

**SDK Versions:**
- Mobile: `@react-native-firebase/auth` (latest)
- Web: `firebase/auth` (modular v9+)
- Backend: `firebase-admin` (for token verification)

### 14.2 Firebase Cloud Messaging (FCM)

**Purpose:** Push notifications to Android devices (Customer App + Driver App)

**Notification Types:**

| Type | Trigger | Target | Priority |
|---|---|---|---|
| Order Confirmation | Order placed | Customer | High |
| Order Accepted | Restaurant accepts | Customer | High |
| Order Ready | Preparation complete | Customer + Driver | High |
| Driver Assigned | Driver assignment | Customer | Normal |
| Driver Arriving | Driver near address | Customer | High |
| Order Delivered | Delivery confirmed | Customer | Normal |
| New Order Alert | Customer places order | Restaurant (web push) | High |
| Delivery Assignment | Order assigned | Driver | High |
| Promotional | Admin sends campaign | Segmented customers | Normal |

**Implementation:**
- FCM token stored per device in `customers.fcm_token` / `drivers.fcm_token`
- Token refresh handled on app launch and via `onTokenRefresh` listener
- Background notification handling for order status updates
- Notification channels (Android): `orders`, `promotions`, `delivery`
- Data-only messages for silent updates (e.g., order status change that updates UI)

### 14.3 Google Maps API

**APIs Used:**

| API | Purpose | Billing |
|---|---|---|
| Maps SDK for Android | Map display in mobile apps | $7 per 1,000 loads |
| Maps JavaScript API | Map display on web (dashboard, customer web) | $7 per 1,000 loads |
| Geocoding API | Convert address to lat/lng and vice versa | $5 per 1,000 requests |
| Places API | Address auto-complete, place search | $17 per 1,000 requests |
| Distance Matrix API | ETA calculation, delivery time estimation | $5 per 1,000 elements |
| Directions API | Driver navigation routes | $5 per 1,000 requests |

**Cost Optimization:**
- Cache geocoding results in Redis (24-hour TTL)
- Batch Distance Matrix requests where possible
- Use Places Autocomplete session tokens to reduce cost
- Free $200/month Google Maps credit covers approximately 28,000 map loads
- Set billing alerts at $100, $200, $500 thresholds

**Implementation Details:**
- API key restricted by Android app (SHA-1 + package name), HTTP referrer (web), and IP (backend)
- Separate API keys for frontend and backend usage
- Backend calls use server-side API key (for geocoding, distance matrix)
- Delivery zone polygon drawing uses Google Maps Drawing Library (dashboard)
- Point-in-polygon checks done via PostGIS (not Google Maps API) to avoid per-request costs

### 14.4 Stripe

**Stripe Products Used:**

| Product | Purpose |
|---|---|
| Stripe Payments | Payment processing (cards, Mada) |
| Stripe PaymentIntents API | Payment creation and confirmation |
| Stripe SetupIntents API | Saved card management |
| Stripe Payment Request API | Google Pay integration |
| Stripe Webhooks | Asynchronous payment status updates |
| Stripe Refunds API | Technical failure refunds |

**Stripe Configuration:**
- Account region: Saudi Arabia (SAR currency)
- Payment methods enabled: `card` (includes Visa, Mastercard, Mada), Google Pay
- Stripe Dashboard access for transaction monitoring
- Webhook endpoints registered for payment events
- API version pinned to specific date (e.g., `2025-12-01`) for stability

**Stripe Connect (if applicable):**
- If multiple restaurant brands use the platform, Stripe Connect can route payments to individual restaurant Stripe accounts
- Direct charges model: Platform creates PaymentIntent on behalf of connected account
- [TBD] Stripe Connect setup depends on final white-label business model

### 14.5 STC Pay

**Integration Type:** Direct API integration (not via Stripe)

**Integration Points:**
- Merchant registration with STC Pay
- Payment initiation API
- Payment status query API
- Webhook for payment confirmations
- Refund API

**Technical Details:**
- [TBD] Exact API documentation, SDK availability, and sandbox environment to be confirmed
- REST-based API expected
- OTP-based customer confirmation flow
- Webhook URL registration for payment status callbacks

**Risk Mitigation:**
- Begin STC Pay integration research early in development
- Prepare mock service for development if sandbox is not immediately available
- STC Pay can be launched as a Phase 1.1 addition if integration takes longer than expected

### 14.6 AWS Services

| Service | Configuration | Purpose |
|---|---|---|
| ECS Fargate | Cluster in me-south-1 | Container orchestration |
| RDS PostgreSQL | db.r6g.large, Multi-AZ, 100GB gp3 | Primary database |
| ElastiCache Redis | cache.r6g.large, 2 nodes | Caching, queues, real-time data |
| S3 | Standard storage, intelligent tiering | File storage |
| CloudFront | Global edge, custom domain | CDN for web apps and images |
| Route 53 | Hosted zone for platform domain | DNS management |
| ALB | 2 AZs, HTTPS listener | Load balancing |
| Secrets Manager | Per-environment secrets | Sensitive configuration |
| SSM Parameter Store | Per-environment params | Non-sensitive configuration |
| SES | Verified domain, production access | Transactional + marketing email |
| CloudWatch | Custom dashboards, log groups, alarms | Monitoring and logging |
| ECR | Private repositories per service | Docker image registry |
| Certificate Manager | Wildcard certificate for *.{domain} | SSL/TLS |
| VPC | 2 AZs, public + private subnets | Network isolation |

### 14.7 Email Service (AWS SES)

**Purpose:** Transactional emails (order confirmations, receipts) and marketing campaigns

**Email Types:**

| Type | Trigger | Template |
|---|---|---|
| Order Confirmation | Order placed | Bilingual order summary with items |
| Order Ready (Pickup) | Preparation complete | Pickup instructions |
| Delivery Confirmation | Order delivered | Delivery summary + rating prompt |
| Receipt | Order completed | VAT-compliant receipt |
| Welcome Email | Registration | Onboarding + first-order promo |
| Marketing Campaign | Admin initiated | Custom template |
| Password Reset | Admin/Driver request | Reset link |
| Support Ticket Update | Status change | Ticket status notification |

**SES Configuration:**
- Verified sending domain
- DKIM and SPF configured via Route 53
- Dedicated IP address for consistent deliverability (if volume justifies)
- Bounce and complaint handling via SNS notifications
- Email templates stored in notification_templates table (bilingual)

---

## 15. Performance Requirements and Targets

### 15.1 API Response Time Targets

| Endpoint Category | p50 Target | p95 Target | p99 Target |
|---|---|---|---|
| Auth (login, register) | < 200ms | < 500ms | < 1000ms |
| Menu browsing (cached) | < 100ms | < 200ms | < 500ms |
| Menu search | < 150ms | < 300ms | < 600ms |
| Cart operations | < 150ms | < 300ms | < 500ms |
| Order creation | < 300ms | < 700ms | < 1500ms |
| Payment intent creation | < 500ms | < 1000ms | < 2000ms |
| Real-time events (Socket.io) | < 100ms | < 200ms | < 500ms |
| File upload | < 1000ms | < 3000ms | < 5000ms |
| Analytics reports | < 500ms | < 2000ms | < 5000ms |
| Health checks | < 50ms | < 100ms | < 200ms |

### 15.2 Throughput Targets (Phase 1 Launch)

| Metric | Target |
|---|---|
| Concurrent authenticated users | 500 |
| Orders per minute (peak) | 50 |
| API requests per second | 200 |
| Socket.io concurrent connections | 1,000 |
| Driver location updates per second | 100 |
| Push notifications per minute | 500 |
| Database connections (pool) | 100 per service (1,300 total) |

### 15.3 Caching Strategy

**Redis Caching Layers:**

| Cache Key Pattern | Data | TTL | Invalidation |
|---|---|---|---|
| `menu:branch:{branchId}` | Full menu for branch | 5 minutes | On menu item CRUD |
| `menu:item:{itemId}` | Individual item detail | 5 minutes | On item update |
| `menu:categories:{branchId}` | Category tree | 10 minutes | On category CRUD |
| `menu:popular:{branchId}` | Popular items list | 15 minutes | On order completion |
| `config:restaurant:{id}` | Restaurant config | 30 minutes | On config update |
| `config:branding:{id}` | Branding config | 1 hour | On branding update |
| `config:branch:{id}` | Branch details + hours | 10 minutes | On branch update |
| `delivery:zones:{branchId}` | Delivery zones | 30 minutes | On zone CRUD |
| `driver:location:{driverId}` | Latest driver GPS | 30 seconds | On location update |
| `user:session:{userId}` | Active session data | 1 hour | On logout/refresh |
| `promo:active:{restaurantId}` | Active promo codes | 5 minutes | On promo CRUD |
| `analytics:dashboard:{branchId}` | Dashboard summary | 5 minutes | On new order |

**Cache Invalidation Strategy:**
- Write-through: Update cache when data is modified
- Event-driven: BullMQ events trigger cache invalidation across services
- TTL-based expiry as safety net
- Manual cache flush available via admin API (for emergencies)

### 15.4 Database Optimization

**Connection Pooling:**
- Prisma connection pool: 10-20 connections per service instance
- PgBouncer considered if connection count exceeds RDS limits

**Query Optimization:**
- Indexes on all foreign keys and frequently queried columns (defined in Section 3)
- Partial indexes for common WHERE clauses (e.g., `WHERE is_active = true`)
- GiST indexes for geospatial queries (PostGIS)
- GIN indexes for full-text search and JSONB queries
- `EXPLAIN ANALYZE` for all queries during development
- Slow query logging enabled (threshold: 200ms)

**Read Replicas:**
- RDS read replica for analytics queries (Phase 1 if needed, or Phase 2)
- Analytics Service routed to read replica to reduce primary DB load

### 15.5 Frontend Performance Targets

| Metric | Target | Tool |
|---|---|---|
| Customer Web - LCP | < 2.5s | Lighthouse |
| Customer Web - FID | < 100ms | Lighthouse |
| Customer Web - CLS | < 0.1 | Lighthouse |
| Customer Web - Lighthouse Score | > 90 (Performance) | Lighthouse |
| Customer App - Cold Start | < 3s | Manual measurement |
| Customer App - Hot Start | < 1s | Manual measurement |
| Dashboard - Initial Load | < 4s | Lighthouse |
| App Bundle Size (Customer) | < 25 MB APK | Android Studio |
| App Bundle Size (Driver) | < 20 MB APK | Android Studio |

**Frontend Optimization Techniques:**
- Code splitting and lazy loading (React.lazy, Next.js dynamic imports)
- Image optimization (WebP, responsive sizes via CloudFront)
- Menu data prefetching and caching (RTK Query)
- Skeleton screens during data loading
- Infinite scroll for long lists (menu items, order history)
- Service worker for Customer Web (offline menu browsing)

---

## Appendix A: Open Items and TBD Decisions

| Item | Context | Decision Needed By |
|---|---|---|
| STC Pay API documentation and sandbox | Payment integration | Before Payment Service development |
| Mobile build strategy (single vs per-restaurant) | White-label deployment | Before first restaurant onboarding |
| Google Play Store submission responsibility | App distribution | Before app release |
| Saudi postal system (SPL) API availability | Address management | Before address feature development |
| Email service provider final selection | Recommended AWS SES | Before Notification Service development |
| Virus scanning for file uploads | Security | Before file upload feature |
| ZATCA e-invoicing requirements | VAT compliance | Before receipt generation |
| Expected order volume at launch | Infrastructure sizing | Before production infrastructure provisioning |
| Number of initial restaurant deployments | Infrastructure and white-label planning | Before production environment setup |
| Stripe Connect vs individual Stripe accounts | Multi-restaurant payments | Before payment architecture finalization |
| Driver self-registration vs restaurant-provisioned only | Driver onboarding flow | Before User Service development |
| Saudi Arabia specific regulations (CITC, NCA, PDPL) | Compliance | Before production launch |

## Appendix B: Phase 2 Features (Out of Scope for Phase 1)

Per PROJECT_SCOPE.md, the following are deferred to Phase 2:

1. **Advanced Tiered Loyalty Program**: Multi-tier rewards (Bronze, Silver, Gold), tier-based perks, birthday rewards, referral bonuses
2. **AI-Driven Personalization**: Machine learning-based menu recommendations, personalized upsell prompts, customer behavior prediction
3. **iOS Mobile Apps**: Customer and Driver apps for iOS (Apple App Store)
4. **Apple Pay**: Payment method integration (requires iOS)
5. **In-App Driver Payments**: Driver earnings tracking, wallet, automatic payouts
6. **Kitchen Display System (KDS)**: Dedicated kitchen screen for order management
7. **Advanced Analytics**: Cohort analysis, funnel visualization, predictive analytics
8. **ZATCA E-Invoicing**: Full compliance with ZATCA electronic invoicing regulations
9. **Multi-Language Expansion**: Beyond Arabic/English (Urdu, Hindi for expat workers)
10. **Admin Super-Panel**: Central management console for white-label platform operator

---

*Document Version: 1.0*
*Created: March 2026*
*Based on: PROJECT_SCOPE.md v1.1*
*Last Updated: March 2026*
