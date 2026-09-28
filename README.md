# Welcome to your Expo app 👋

This is an [Expo](https://expo.dev) project created with [`create-expo-app`](https://www.npmjs.com/package/create-expo-app).

## Get started

1. Install dependencies

   ```bash
   npm install
   ```

2. Start the app

   ```bash
   npx expo start
   ```

In the output, you'll find options to open the app in a

- [development build](https://docs.expo.dev/develop/development-builds/introduction/)
- [Android emulator](https://docs.expo.dev/workflow/android-studio-emulator/)
- [iOS simulator](https://docs.expo.dev/workflow/ios-simulator/)
- [Expo Go](https://expo.dev/go), a limited sandbox for trying out app development with Expo

You can start developing by editing the files inside the **app** directory. This project uses [file-based routing](https://docs.expo.dev/router/introduction).

## Get a fresh project

When you're ready, run:

```bash
npm run reset-project
```

This command will move the starter code to the **app-example** directory and create a blank **app** directory where you can start developing.

### Other setup steps

- To set up ESLint for linting, run `npx expo lint`, or follow our guide on ["Using ESLint and Prettier"](https://docs.expo.dev/guides/using-eslint/)
- If you'd like to set up unit testing, follow our guide on ["Unit Testing with Jest"](https://docs.expo.dev/develop/unit-testing/)
- Learn more about the TypeScript setup in this template in our guide on ["Using TypeScript"](https://docs.expo.dev/guides/typescript/)

## Learn more

To learn more about developing your project with Expo, look at the following resources:

- [Expo documentation](https://docs.expo.dev/): Learn fundamentals, or go into advanced topics with our [guides](https://docs.expo.dev/guides).
- [Learn Expo tutorial](https://docs.expo.dev/tutorial/introduction/): Follow a step-by-step tutorial where you'll create a project that runs on Android, iOS, and the web.

## Join the community

Join our community of developers creating universal apps.

- [Expo on GitHub](https://github.com/expo/expo): View our open source platform and contribute.
- [Discord community](https://chat.expo.dev): Chat with Expo users and ask questions.













# 🌐 SZSDomains — Domain Selling Website

A full-stack domain marketplace where users can browse, buy, and transfer premium domains.
Domains are sourced from GoDaddy and sold directly to buyers via EPP (Auth) Code transfer.

---

## 📖 Table of Contents

1. [Project Overview](#-project-overview)
2. [Business Model](#-business-model)
3. [Tech Stack](#-tech-stack)
4. [Features](#-features)
5. [User Flow](#-user-flow)
6. [Site Map](#-site-map)
7. [Database Schema](#-database-schema)
8. [API Endpoints](#-api-endpoints)
9. [Folder Structure](#-folder-structure)
10. [Environment Variables](#-environment-variables)
11. [Setup & Installation](#-setup--installation)
12. [Deployment](#-deployment)
13. [Roadmap](#-roadmap)
14. [License](#-license)

---

## 🎯 Project Overview

**SZSDomains** is a domain reselling platform. We buy premium domains from GoDaddy and list them for sale on our own website. When a user purchases a domain:

1. Payment is processed via Escrow (or payment gateway).
2. We unlock the domain at GoDaddy.
3. We deliver the **EPP / Auth Code** to the buyer.
4. Buyer initiates transfer at their registrar.
5. Transfer completes in 5–7 days.

The core challenge is **trust** — since we are not a registrar, we must use escrow, clear communication, and transparency to convert buyers.

---

## 💼 Business Model

| Step | Action |
|------|--------|
| 1 | Buy domains in bulk from GoDaddy (auctions, closeouts, expired) |
| 2 | List them on SZSDomains with a markup |
| 3 | Buyer purchases via Escrow.com / Payment Gateway |
| 4 | We unlock the domain and deliver EPP Code |
| 5 | Buyer transfers the domain to their registrar |
| 6 | Escrow releases funds to us |

**Revenue:** Markup on domain price + optional escrow fee pass-through.

---

## 🛠 Tech Stack

### Frontend
- **Framework:** Next.js 14 (App Router) / React
- **Styling:** Tailwind CSS + shadcn/ui
- **State Management:** Zustand / React Query
- **Forms:** React Hook Form + Zod

### Backend
- **Runtime:** Node.js
- **Framework:** Express.js / Next.js API Routes
- **Auth:** NextAuth.js (JWT + OAuth)
- **Validation:** Zod

### Database
- **Primary DB:** PostgreSQL
- **ORM:** Prisma
- **Cache:** Redis (for sessions, rate limiting)

### Payments
- **Escrow:** Escrow.com API
- **Direct:** Stripe / Razorpay / PayPal

### Email
- **Provider:** Resend / SendGrid / Nodemailer
- **Templates:** React Email

### Storage
- **Files:** AWS S3 / Cloudinary (invoices, screenshots)

### DevOps
- **Hosting:** Vercel (frontend) + Railway/Render (backend)
- **CI/CD:** GitHub Actions
- **Monitoring:** Sentry + Vercel Analytics

---

## ✨ Features

### 👤 User (Buyer) Features

- 🔍 **Browse & Search Domains** — keyword, extension, category, price range
- 📋 **Filter & Sort** — by price, age, length, extension, popularity
- 🔎 **View Domain Details** — price, age, traffic stats, use-case suggestions
- 🛒 **Buy Now / Make Offer** — instant purchase or negotiate
- 💳 **Secure Checkout** — Escrow.com, Stripe, Razorpay, PayPal
- 📧 **EPP Code Delivery** — dashboard + email
- 📦 **Order Tracking** — real-time transfer status
- ⭐ **Leave Reviews** — rate purchased domains
- ❤️ **Wishlist** — save domains for later
- 💬 **Support Queries** — raise tickets, live chat, contact form
- 📜 **Terms of Service** — refund policy, transfer lock, disclaimer
- 🔔 **Email Alerts** — new domain notifications

### 🔧 Admin Features

- 📊 **Dashboard** — sales, users, orders, revenue overview
- 🌐 **Domain Management** — add/edit/delete, bulk upload, mark sold
- 👥 **User Management** — view, block, email users
- 💬 **Query Management** — reply, status update, priority
- 📦 **Order Management** — payment status, EPP delivery, refunds
- 📝 **Content Management** — homepage, FAQ, ToS, banners
- ⭐ **Review Management** — approve, reject, reply
- 📈 **Reports & Analytics** — sales, traffic, conversion
- ⚙️ **Settings** — payment gateways, email, security

---

## 🔄 User Flow

```
┌─────────────────────────────────────────────────────────────┐
│  1. User lands on homepage                                  │
│  2. Browses / searches domains                              │
│  3. Clicks on a domain → views details                      │
│  4. Clicks "Buy Now" or "Make Offer"                        │
│  5. Signs up / Logs in                                      │
│  6. Pays via Escrow / Payment Gateway                       │
│  7. Receives EPP Code + transfer instructions (email + UI)  │
│  8. Initiates transfer at their registrar                   │
│  9. Transfer completes in 5–7 days                          │
│ 10. Leaves review / rating                                  │
└─────────────────────────────────────────────────────────────┘
```

---

## 🗺 Site Map

```
WEBSITE
│
├── 🏠 Homepage
│   ├── Header / Navigation
│   ├── Search Bar (Hero)
│   ├── Trust Section
│   ├── How It Works
│   ├── Trending Domains
│   ├── Currently Available Domains
│   ├── Recently Sold
│   ├── Why Choose Us
│   ├── FAQ
│   └── Footer
│
├── 📋 Domain Listing Page (filters + sort)
│
├── 🔍 Domain Detail Page
│
├── 🛒 Checkout Page
│
├── 👤 User Dashboard
│   ├── My Orders / Transactions
│   ├── Wishlist
│   ├── My Queries
│   ├── Reviews
│   └── Profile Settings
│
├── 📞 Support Page
│
├── 📜 Terms of Service
│
├── 🔐 Auth Pages (Sign Up / Login / Forgot Password)
│
└── 🔧 ADMIN PANEL
    ├── Dashboard
    ├── Domain Management
    ├── User Management
    ├── Query Management
    ├── Order Management
    ├── Content Management
    ├── Review Management
    ├── Reports & Analytics
    └── Settings
```

---

## 🗄 Database Schema

### Entity Relationship Overview

```
User ───< Order >─── Domain
 │           │
 │           ├──< Transaction
 │           ├──< Review
 │           └──< Query
 │
 ├──< Wishlist >─── Domain
 │
 └──< Query
```

### Tables

#### 1. `users`

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| id | UUID | PK, default gen_random_uuid() | Unique user ID |
| name | VARCHAR(100) | NOT NULL | Full name |
| email | VARCHAR(255) | UNIQUE, NOT NULL | Email address |
| password_hash | TEXT | NULL | Hashed password (null if OAuth) |
| phone | VARCHAR(20) | NULL | Phone number |
| role | ENUM('user','admin') | DEFAULT 'user' | User role |
| is_verified | BOOLEAN | DEFAULT false | Email verified? |
| is_blocked | BOOLEAN | DEFAULT false | Admin block status |
| avatar_url | TEXT | NULL | Profile picture |
| created_at | TIMESTAMP | DEFAULT NOW() | Registration date |
| updated_at | TIMESTAMP | DEFAULT NOW() | Last update |

**Indexes:** `email`, `role`

---

#### 2. `domains`

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| id | UUID | PK | Unique domain ID |
| name | VARCHAR(255) | UNIQUE, NOT NULL | Full domain name (e.g., example.com) |
| extension | VARCHAR(20) | NOT NULL | TLD (.com, .in, .io) |
| category | VARCHAR(50) | NULL | Tech, Finance, Health, etc. |
| price | DECIMAL(12,2) | NOT NULL | Selling price (USD) |
| currency | VARCHAR(3) | DEFAULT 'USD' | Currency code |
| description | TEXT | NULL | Marketing description |
| use_case | TEXT | NULL | Suggested use cases |
| registration_date | DATE | NULL | Domain age (from WHOIS) |
| expiry_date | DATE | NULL | Domain expiry |
| registrar | VARCHAR(100) | DEFAULT 'GoDaddy' | Source registrar |
| traffic_stats | JSONB | NULL | Monthly visitors, sources |
| status | ENUM('available','sold','reserved') | DEFAULT 'available' | Current status |
| is_featured | BOOLEAN | DEFAULT false | Show on homepage |
| is_trending | BOOLEAN | DEFAULT false | Show in trending section |
| views_count | INTEGER | DEFAULT 0 | Page views |
| sold_price | DECIMAL(12,2) | NULL | Final sold price |
| sold_at | TIMESTAMP | NULL | Sold date |
| created_at | TIMESTAMP | DEFAULT NOW() | Listing date |
| updated_at | TIMESTAMP | DEFAULT NOW() | Last update |

**Indexes:** `name`, `status`, `category`, `extension`, `is_featured`, `is_trending`

---

#### 3. `orders`

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| id | UUID | PK | Order ID |
| order_number | VARCHAR(20) | UNIQUE, NOT NULL | Human-readable (e.g., ORD-2024-001) |
| user_id | UUID | FK → users.id | Buyer |
| domain_id | UUID | FK → domains.id | Purchased domain |
| amount | DECIMAL(12,2) | NOT NULL | Final amount |
| currency | VARCHAR(3) | DEFAULT 'USD' | Currency |
| payment_method | ENUM('escrow','stripe','razorpay','paypal') | NOT NULL | Payment gateway |
| payment_status | ENUM('pending','paid','failed','refunded') | DEFAULT 'pending' | Payment state |
| escrow_transaction_id | VARCHAR(100) | NULL | Escrow.com transaction ID |
| transfer_status | ENUM('pending','epp_sent','in_progress','completed','failed') | DEFAULT 'pending' | Transfer state |
| epp_code | TEXT | NULL | Encrypted EPP/Auth code |
| epp_sent_at | TIMESTAMP | NULL | When EPP was delivered |
| transfer_completed_at | TIMESTAMP | NULL | When transfer finished |
| notes | TEXT | NULL | Admin notes |
| created_at | TIMESTAMP | DEFAULT NOW() | Order date |
| updated_at | TIMESTAMP | DEFAULT NOW() | Last update |

**Indexes:** `user_id`, `domain_id`, `payment_status`, `transfer_status`

---

#### 4. `transactions`

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| id | UUID | PK | Transaction ID |
| order_id | UUID | FK → orders.id | Related order |
| gateway | VARCHAR(50) | NOT NULL | escrow / stripe / razorpay |
| gateway_txn_id | VARCHAR(150) | NULL | External transaction ID |
| amount | DECIMAL(12,2) | NOT NULL | Amount |
| currency | VARCHAR(3) | DEFAULT 'USD' | Currency |
| status | ENUM('initiated','success','failed','refunded') | DEFAULT 'initiated' | Status |
| raw_response | JSONB | NULL | Full gateway response |
| created_at | TIMESTAMP | DEFAULT NOW() | Timestamp |

**Indexes:** `order_id`, `status`

---

#### 5. `reviews`

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| id | UUID | PK | Review ID |
| user_id | UUID | FK → users.id | Reviewer |
| order_id | UUID | FK → orders.id | Related order |
| domain_id | UUID | FK → domains.id | Reviewed domain |
| rating | SMALLINT | CHECK (1–5) | Star rating |
| comment | TEXT | NULL | Review text |
| status | ENUM('pending','approved','rejected') | DEFAULT 'pending' | Moderation |
| is_featured | BOOLEAN | DEFAULT false | Show on homepage |
| admin_reply | TEXT | NULL | Admin response |
| created_at | TIMESTAMP | DEFAULT NOW() | Date |

**Indexes:** `user_id`, `domain_id`, `status`

---

#### 6. `queries` (Support Tickets)

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| id | UUID | PK | Query ID |
| user_id | UUID | FK → users.id, NULL | Logged-in user (null for guests) |
| name | VARCHAR(100) | NOT NULL | Contact name |
| email | VARCHAR(255) | NOT NULL | Contact email |
| subject | VARCHAR(255) | NOT NULL | Query subject |
| message | TEXT | NOT NULL | Query body |
| category | ENUM('general','order','transfer','payment','other') | DEFAULT 'general' | Type |
| priority | ENUM('low','medium','high') | DEFAULT 'medium' | Priority |
| status | ENUM('open','in_progress','closed') | DEFAULT 'open' | Status |
| admin_reply | TEXT | NULL | Admin response |
| replied_at | TIMESTAMP | NULL | Reply timestamp |
| created_at | TIMESTAMP | DEFAULT NOW() | Created |
| updated_at | TIMESTAMP | DEFAULT NOW() | Last update |

**Indexes:** `user_id`, `status`, `priority`

---

#### 7. `wishlists`

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| id | UUID | PK | Wishlist ID |
| user_id | UUID | FK → users.id | User |
| domain_id | UUID | FK → domains.id | Saved domain |
| created_at | TIMESTAMP | DEFAULT NOW() | Added date |

**Unique Constraint:** `(user_id, domain_id)`

---

#### 8. `content_blocks` (CMS)

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| id | UUID | PK | Block ID |
| key | VARCHAR(100) | UNIQUE, NOT NULL | e.g., 'homepage_hero' |
| title | VARCHAR(255) | NULL | Block title |
| body | JSONB | NOT NULL | Content (text, list, etc.) |
| updated_by | UUID | FK → users.id | Admin |
| updated_at | TIMESTAMP | DEFAULT NOW() | Last update |

**Examples of keys:** `homepage_hero`, `trust_section`, `how_it_works`, `faq`, `tos`, `footer`

---

#### 9. `faqs`

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| id | UUID | PK | FAQ ID |
| question | TEXT | NOT NULL | Question |
| answer | TEXT | NOT NULL | Answer |
| display_order | INTEGER | DEFAULT 0 | Sort order |
| is_active | BOOLEAN | DEFAULT true | Show/hide |
| created_at | TIMESTAMP | DEFAULT NOW() | Created |

---

#### 10. `email_logs`

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| id | UUID | PK | Log ID |
| user_id | UUID | FK → users.id, NULL | Recipient |
| to_email | VARCHAR(255) | NOT NULL | Recipient email |
| template | VARCHAR(100) | NOT NULL | Template name |
| subject | VARCHAR(255) | NOT NULL | Subject |
| status | ENUM('sent','failed','bounced') | DEFAULT 'sent' | Status |
| error | TEXT | NULL | Error message |
| sent_at | TIMESTAMP | DEFAULT NOW() | Sent time |

---

#### 11. `sessions` (if using DB sessions)

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| id | UUID | PK | Session ID |
| user_id | UUID | FK → users.id | User |
| token | TEXT | UNIQUE, NOT NULL | Session token |
| ip_address | VARCHAR(45) | NULL | Client IP |
| user_agent | TEXT | NULL | Browser info |
| expires_at | TIMESTAMP | NOT NULL | Expiry |
| created_at | TIMESTAMP | DEFAULT NOW() | Created |

---

#### 12. `audit_logs` (Admin actions)

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| id | UUID | PK | Log ID |
| admin_id | UUID | FK → users.id | Admin |
| action | VARCHAR(100) | NOT NULL | e.g., 'domain.create' |
| entity | VARCHAR(50) | NOT NULL | e.g., 'domain' |
| entity_id | UUID | NULL | Affected record |
| changes | JSONB | NULL | Before/after diff |
| ip_address | VARCHAR(45) | NULL | Admin IP |
| created_at | TIMESTAMP | DEFAULT NOW() | Timestamp |

**Indexes:** `admin_id`, `entity`, `created_at`

---

### Prisma Schema (Reference)

```prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id            String    @id @default(uuid())
  name          String
  email         String    @unique
  passwordHash  String?   @map("password_hash")
  phone         String?
  role          Role      @default(USER)
  isVerified    Boolean   @default(false) @map("is_verified")
  isBlocked     Boolean   @default(false) @map("is_blocked")
  avatarUrl     String?   @map("avatar_url")
  createdAt     DateTime  @default(now()) @map("created_at")
  updatedAt     DateTime  @updatedAt @map("updated_at")

  orders        Order[]
  reviews       Review[]
  queries       Query[]
  wishlists     Wishlist[]
  sessions      Session[]
  auditLogs     AuditLog[]

  @@index([email])
  @@index([role])
}

enum Role {
  USER
  ADMIN
}

model Domain {
  id               String       @id @default(uuid())
  name             String       @unique
  extension        String
  category         String?
  price            Decimal      @db.Decimal(12, 2)
  currency         String       @default("USD")
  description      String?
  useCase          String?      @map("use_case")
  registrationDate DateTime?    @map("registration_date") @db.Date
  expiryDate       DateTime?    @map("expiry_date") @db.Date
  registrar        String       @default("GoDaddy")
  trafficStats     Json?        @map("traffic_stats")
  status           DomainStatus @default(AVAILABLE)
  isFeatured       Boolean      @default(false) @map("is_featured")
  isTrending       Boolean      @default(false) @map("is_trending")
  viewsCount       Int          @default(0) @map("views_count")
  soldPrice        Decimal?     @map("sold_price") @db.Decimal(12, 2)
  soldAt           DateTime?    @map("sold_at")
  createdAt        DateTime     @default(now()) @map("created_at")
  updatedAt        DateTime     @updatedAt @map("updated_at")

  orders           Order[]
  reviews          Review[]
  wishlists        Wishlist[]

  @@index([name])
  @@index([status])
  @@index([category])
  @@index([extension])
  @@index([isFeatured])
  @@index([isTrending])
}

enum DomainStatus {
  AVAILABLE
  SOLD
  RESERVED
}

model Order {
  id                  String          @id @default(uuid())
  orderNumber         String          @unique @map("order_number")
  userId              String          @map("user_id")
  domainId            String          @map("domain_id")
  amount              Decimal         @db.Decimal(12, 2)
  currency            String          @default("USD")
  paymentMethod       PaymentMethod   @map("payment_method")
  paymentStatus       PaymentStatus   @default(PENDING) @map("payment_status")
  escrowTransactionId String?         @map("escrow_transaction_id")
  transferStatus      TransferStatus  @default(PENDING) @map("transfer_status")
  eppCode             String?         @map("epp_code")
  eppSentAt           DateTime?       @map("epp_sent_at")
  transferCompletedAt DateTime?       @map("transfer_completed_at")
  notes               String?
  createdAt           DateTime        @default(now()) @map("created_at")
  updatedAt           DateTime        @updatedAt @map("updated_at")

  user                User            @relation(fields: [userId], references: [id])
  domain              Domain          @relation(fields: [domainId], references: [id])
  transactions        Transaction[]
  reviews             Review[]

  @@index([userId])
  @@index([domainId])
  @@index([paymentStatus])
  @@index([transferStatus])
}

enum PaymentMethod {
  ESCROW
  STRIPE
  RAZORPAY
  PAYPAL
}

enum PaymentStatus {
  PENDING
  PAID
  FAILED
  REFUNDED
}

enum TransferStatus {
  PENDING
  EPP_SENT
  IN_PROGRESS
  COMPLETED
  FAILED
}

model Transaction {
  id           String            @id @default(uuid())
  orderId      String            @map("order_id")
  gateway      String
  gatewayTxnId String?           @map("gateway_txn_id")
  amount       Decimal           @db.Decimal(12, 2)
  currency     String            @default("USD")
  status       TransactionStatus @default(INITIATED)
  rawResponse  Json?             @map("raw_response")
  createdAt    DateTime          @default(now()) @map("created_at")

  order        Order             @relation(fields: [orderId], references: [id])

  @@index([orderId])
  @@index([status])
}

enum TransactionStatus {
  INITIATED
  SUCCESS
  FAILED
  REFUNDED
}

model Review {
  id         String       @id @default(uuid())
  userId     String       @map("user_id")
  orderId    String       @map("order_id")
  domainId   String       @map("domain_id")
  rating     Int
  comment    String?
  status     ReviewStatus @default(PENDING)
  isFeatured Boolean      @default(false) @map("is_featured")
  adminReply String?      @map("admin_reply")
  createdAt  DateTime     @default(now()) @map("created_at")

  user       User         @relation(fields: [userId], references: [id])
  order      Order        @relation(fields: [orderId], references: [id])
  domain     Domain       @relation(fields: [domainId], references: [id])

  @@index([userId])
  @@index([domainId])
  @@index([status])
}

enum ReviewStatus {
  PENDING
  APPROVED
  REJECTED
}

model Query {
  id         String        @id @default(uuid())
  userId     String?       @map("user_id")
  name       String
  email      String
  subject    String
  message    String
  category   QueryCategory @default(GENERAL)
  priority   Priority      @default(MEDIUM)
  status     QueryStatus   @default(OPEN)
  adminReply String?       @map("admin_reply")
  repliedAt  DateTime?     @map("replied_at")
  createdAt  DateTime      @default(now()) @map("created_at")
  updatedAt  DateTime      @updatedAt @map("updated_at")

  user       User?         @relation(fields: [userId], references: [id])

  @@index([userId])
  @@index([status])
  @@index([priority])
}

enum QueryCategory {
  GENERAL
  ORDER
  TRANSFER
  PAYMENT
  OTHER
}

enum Priority {
  LOW
  MEDIUM
  HIGH
}

enum QueryStatus {
  OPEN
  IN_PROGRESS
  CLOSED
}

model Wishlist {
  id        String   @id @default(uuid())
  userId    String   @map("user_id")
  domainId  String   @map("domain_id")
  createdAt DateTime @default(now()) @map("created_at")

  user      User     @relation(fields: [userId], references: [id])
  domain    Domain   @relation(fields: [domainId], references: [id])

  @@unique([userId, domainId])
}

model ContentBlock {
  id        String   @id @default(uuid())
  key       String   @unique
  title     String?
  body      Json
  updatedBy String?  @map("updated_by")
  updatedAt DateTime @updatedAt @map("updated_at")
}

model Faq {
  id           String   @id @default(uuid())
  question     String
  answer       String
  displayOrder Int      @default(0) @map("display_order")
  isActive     Boolean  @default(true) @map("is_active")
  createdAt    DateTime @default(now()) @map("created_at")
}

model EmailLog {
  id        String      @id @default(uuid())
  userId    String?     @map("user_id")
  toEmail   String      @map("to_email")
  template  String
  subject   String
  status    EmailStatus @default(SENT)
  error     String?
  sentAt    DateTime    @default(now()) @map("sent_at")

  @@index([userId])
}

enum EmailStatus {
  SENT
  FAILED
  BOUNCED
}

model Session {
  id        String   @id @default(uuid())
  userId    String   @map("user_id")
  token     String   @unique
  ipAddress String?  @map("ip_address")
  userAgent String?  @map("user_agent")
  expiresAt DateTime @map("expires_at")
  createdAt DateTime @default(now()) @map("created_at")

  user      User     @relation(fields: [userId], references: [id])

  @@index([userId])
}

model AuditLog {
  id        String   @id @default(uuid())
  adminId   String   @map("admin_id")
  action    String
  entity    String
  entityId  String?  @map("entity_id")
  changes   Json?
  ipAddress String?  @map("ip_address")
  createdAt DateTime @default(now()) @map("created_at")

  admin     User     @relation(fields: [adminId], references: [id])

  @@index([adminId])
  @@index([entity])
  @@index([createdAt])
}
```

---

## 🔌 API Endpoints

### Public Routes

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/domains` | List all available domains (with filters) |
| GET | `/api/domains/:id` | Get domain details |
| GET | `/api/domains/trending` | Get trending domains |
| GET | `/api/domains/recently-sold` | Get recently sold domains |
| GET | `/api/domains/search?q=` | Search domains |
| GET | `/api/faqs` | Get all FAQs |
| GET | `/api/content/:key` | Get content block (hero, trust, etc.) |
| POST | `/api/queries` | Submit a support query |
| POST | `/api/newsletter` | Subscribe to newsletter |

### Auth Routes

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Register new user |
| POST | `/api/auth/login` | Login |
| POST | `/api/auth/logout` | Logout |
| POST | `/api/auth/forgot-password` | Send reset link |
| POST | `/api/auth/reset-password` | Reset password |
| GET | `/api/auth/me` | Get current user |

### User Routes (Protected)

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/user/orders` | Get my orders |
| GET | `/api/user/orders/:id` | Get order details + EPP |
| POST | `/api/user/orders` | Create order (checkout) |
| GET | `/api/user/wishlist` | Get wishlist |
| POST | `/api/user/wishlist` | Add to wishlist |
| DELETE | `/api/user/wishlist/:domainId` | Remove from wishlist |
| GET | `/api/user/queries` | Get my queries |
| POST | `/api/user/reviews` | Submit review |
| GET | `/api/user/reviews` | Get my reviews |
| PATCH | `/api/user/profile` | Update profile |

### Payment Routes

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/payments/escrow/create` | Create Escrow transaction |
| POST | `/api/payments/escrow/webhook` | Escrow webhook |
| POST | `/api/payments/stripe/create` | Create Stripe session |
| POST | `/api/payments/stripe/webhook` | Stripe webhook |
| POST | `/api/payments/razorpay/create` | Create Razorpay order |
| POST | `/api/payments/razorpay/webhook` | Razorpay webhook |

### Admin Routes (Protected — role: admin)

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/admin/dashboard` | Dashboard stats |
| GET | `/api/admin/domains` | List all domains |
| POST | `/api/admin/domains` | Add domain |
| PATCH | `/api/admin/domains/:id` | Update domain |
| DELETE | `/api/admin/domains/:id` | Delete domain |
| POST | `/api/admin/domains/bulk` | Bulk upload (CSV) |
| PATCH | `/api/admin/domains/:id/sold` | Mark as sold |
| GET | `/api/admin/users` | List users |
| PATCH | `/api/admin/users/:id/block` | Block/unblock user |
| GET | `/api/admin/orders` | List all orders |
| PATCH | `/api/admin/orders/:id` | Update order (EPP, status) |
| GET | `/api/admin/queries` | List all queries |
| PATCH | `/api/admin/queries/:id` | Reply / update query |
| GET | `/api/admin/reviews` | List all reviews |
| PATCH | `/api/admin/reviews/:id` | Approve/reject review |
| GET | `/api/admin/content` | List content blocks |
| PATCH | `/api/admin/content/:key` | Update content block |
| GET | `/api/admin/faqs` | List FAQs |
| POST | `/api/admin/faqs` | Add FAQ |
| PATCH | `/api/admin/faqs/:id` | Update FAQ |
| DELETE | `/api/admin/faqs/:id` | Delete FAQ |
| GET | `/api/admin/reports/sales` | Sales report |
| GET | `/api/admin/reports/traffic` | Traffic report |
| GET | `/api/admin/audit-logs` | Audit logs |

---

## 📁 Folder Structure

```
szsdomains/
├── apps/
│   ├── web/                          # Next.js frontend
│   │   ├── app/
│   │   │   ├── (public)/
│   │   │   │   ├── page.tsx          # Homepage
│   │   │   │   ├── domains/
│   │   │   │   │   ├── page.tsx      # Listing
│   │   │   │   │   └── [id]/page.tsx # Detail
│   │   │   │   ├── how-it-works/page.tsx
│   │   │   │   ├── recently-sold/page.tsx
│   │   │   │   ├── support/page.tsx
│   │   │   │   └── terms/page.tsx
│   │   │   ├── (auth)/
│   │   │   │   ├── login/page.tsx
│   │   │   │   ├── register/page.tsx
│   │   │   │   └── forgot-password/page.tsx
│   │   │   ├── (user)/
│   │   │   │   └── dashboard/
│   │   │   │       ├── page.tsx
│   │   │   │       ├── orders/
│   │   │   │       ├── wishlist/
│   │   │   │       ├── queries/
│   │   │   │       ├── reviews/
│   │   │   │       └── profile/
│   │   │   ├── (admin)/
│   │   │   │   └── admin/
│   │   │   │       ├── page.tsx      # Dashboard
│   │   │   │       ├── domains/
│   │   │   │       ├── users/
│   │   │   │       ├── orders/
│   │   │   │       ├── queries/
│   │   │   │       ├── reviews/
│   │   │   │       ├── content/
│   │   │   │       ├── reports/
│   │   │   │       └── settings/
│   │   │   ├── api/                  # API routes (if using Next.js API)
│   │   │   └── layout.tsx
│   │   ├── components/
│   │   │   ├── ui/                   # shadcn components
│   │   │   ├── domain/
│   │   │   ├── layout/
│   │   │   └── forms/
│   │   ├── lib/
│   │   │   ├── api.ts
│   │   │   ├── auth.ts
│   │   │   ├── utils.ts
│   │   │   └── validators.ts
│   │   ├── hooks/
│   │   ├── styles/
│   │   ├── public/
│   │   ├── next.config.js
│   │   ├── tailwind.config.ts
│   │   └── package.json
│   │
│   └── api/                          # Express backend (if separate)
│       ├── src/
│       │   ├── routes/
│       │   ├── controllers/
│       │   ├── services/
│       │   ├── middleware/
│       │   ├── utils/
│       │   ├── jobs/                 # Cron jobs (transfer status check)
│       │   └── index.ts
│       └── package.json
│
├── packages/
│   ├── database/                     # Prisma
│   │   ├── prisma/
│   │   │   ├── schema.prisma
│   │   │   └── migrations/
│   │   └── index.ts
│   ├── shared/                       # Shared types, constants
│   │   ├── types/
│   │   └── constants/
│   └── emails/                       # React Email templates
│       └── templates/
│
├── .env.example
├── .gitignore
├── docker-compose.yml
├── package.json
├── pnpm-workspace.yaml
└── README.md
```

---

## 🔐 Environment Variables

```bash
# App
NEXT_PUBLIC_APP_URL=https://szsdomains.com
NODE_ENV=production

# Database
DATABASE_URL=postgresql://user:pass@localhost:5432/szsdomains

# Redis
REDIS_URL=redis://localhost:6379

# Auth
NEXTAUTH_SECRET=your-secret-key
NEXTAUTH_URL=https://szsdomains.com
JWT_SECRET=your-jwt-secret

# OAuth (optional)
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=

# Email
RESEND_API_KEY=
EMAIL_FROM=noreply@szsdomains.com

# Payments — Escrow.com
ESCROW_EMAIL=
ESCROW_API_KEY=
ESCROW_ENV=production

# Payments — Stripe
STRIPE_SECRET_KEY=
STRIPE_WEBHOOK_SECRET=
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=

# Payments — Razorpay
RAZORPAY_KEY_ID=
RAZORPAY_KEY_SECRET=

# Payments — PayPal
PAYPAL_CLIENT_ID=
PAYPAL_CLIENT_SECRET=

# Storage (S3 / Cloudinary)
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_BUCKET_NAME=
AWS_REGION=

# Encryption (for EPP codes)
EPP_ENCRYPTION_KEY=32-byte-hex-key

# Monitoring
SENTRY_DSN=

# Admin seed
ADMIN_EMAIL=admin@szsdomains.com
ADMIN_PASSWORD=change-me-immediately
```

---

## 🚀 Setup & Installation

### Prerequisites
- Node.js 18+
- PostgreSQL 14+
- Redis 6+
- pnpm (recommended)

### Steps

```bash
# 1. Clone the repo
git clone https://github.com/your-org/szsdomains.git
cd szsdomains

# 2. Install dependencies
pnpm install

# 3. Copy environment file
cp .env.example .env
# Fill in all required values

# 4. Setup database
pnpm --filter database prisma migrate dev
pnpm --filter database prisma db seed

# 5. Run development servers
pnpm dev
```

### Available Scripts

```bash
pnpm dev              # Start all apps in dev mode
pnpm build            # Build all apps
pnpm start            # Start production
pnpm lint             # Lint all code
pnpm test             # Run tests
pnpm db:migrate       # Run migrations
pnpm db:seed          # Seed database
pnpm db:studio        # Open Prisma Studio
```

---

## 🌍 Deployment

### Frontend (Vercel)
1. Connect GitHub repo to Vercel
2. Set environment variables
3. Deploy — auto-deploys on push to `main`

### Backend (Railway / Render)
1. Create new service from repo
2. Set build command: `pnpm --filter api build`
3. Set start command: `pnpm --filter api start`
4. Add environment variables
5. Add PostgreSQL + Redis add-ons

### Database
- Use **Neon** / **Supabase** / **Railway Postgres** for managed PostgreSQL
- Run migrations on deploy

### Domain & SSL
- Point domain to Vercel
- SSL auto-provisioned via Let's Encrypt

---

## 🗓 Roadmap

### Phase 1 — MVP
- [x] Project setup (Next.js + Prisma + Postgres)
- [ ] Auth (register, login, JWT)
- [ ] Domain listing + search + filters
- [ ] Domain detail page
- [ ] Checkout with Stripe/Escrow
- [ ] EPP code delivery (email + dashboard)
- [ ] Basic admin panel

### Phase 2 — Core Features
- [ ] User dashboard (orders, wishlist, queries, reviews)
- [ ] Support ticket system
- [ ] Review system
- [ ] Email notifications (order, EPP, transfer)
- [ ] Admin: domain/user/order/query management

### Phase 3 — Trust & Content
- [ ] Trust section
- [ ] How It Works
- [ ] Recently Sold
- [ ] Trending Domains
- [ ] FAQ
- [ ] Terms of Service
- [ ] Content Management System

### Phase 4 — Advanced
- [ ] Escrow.com full integration
- [ ] Auto transfer status check (cron)
- [ ] Analytics dashboard
- [ ] Reports (sales, traffic, conversion)
- [ ] Audit logs
- [ ] 2FA for admin

### Phase 5 — Scale
- [ ] Multi-currency support
- [ ] Bulk domain upload (CSV)
- [ ] API for partners
- [ ] Mobile app (React Native)
- [ ] AI-based domain pricing suggestions

---

## 🤝 Contributing

1. Fork the repo
2. Create a feature branch (`git checkout -b feature/amazing`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push (`git push origin feature/amazing`)
5. Open a Pull Request

---

## 📜 License

MIT License © 2024 SZSDomains

---

## 📞 Contact

- **Email:** support@szsdomains.com
- **Website:** https://szsdomains.com
- **Twitter/X:** @szsdomains

---

**⚠️ Important Legal Notes**

- ICANN's **60-Day Transfer Lock** applies after registration and after each transfer.
- Always use **Escrow** for high-value transactions.
- Never share EPP codes publicly — deliver only via secure channels.
- Comply with GoDaddy's terms of service regarding resale and transfers.