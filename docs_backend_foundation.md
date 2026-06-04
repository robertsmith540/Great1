# SpareKe Backend Foundation

This document explains the backend foundation now added to the SpareKe prototype.

## 1. What Has Been Added

The project now includes a real backend foundation using:

- **Next.js API routes**
- **Prisma ORM**
- **SQLite local database for development**
- **JWT cookie authentication**
- **bcrypt password hashing**
- **Role-based permissions**
- **Seed/demo data**
- **Escrow and subscription automation endpoints**

The local database is designed so the system can run immediately on a laptop or preview environment. For production, the Prisma datasource can be changed from SQLite to PostgreSQL.

## 2. Setup Commands

From inside the project folder:

```bash
cd spareke-marketplace
npm install
npm run backend:setup
npm run dev
```

Then open:

```text
http://localhost:3000
```

## 3. Demo Accounts

All seeded accounts use the password:

```text
SpareKe123!
```

| Role | Email |
|---|---|
| Admin | admin@spareke.com |
| Vehicle Owner | owner@spareke.com |
| Mechanic | mechanic@spareke.com |
| Garage Owner | garage@spareke.com |
| Vendor | vendor@spareke.com |
| Wholesaler | wholesaler@spareke.com |
| Manufacturer | manufacturer@spareke.com |
| Fleet Admin | fleet@spareke.com |

## 4. Main API Endpoints

### Health

```http
GET /api/health
```

### Authentication

```http
POST /api/auth/register
POST /api/auth/login
POST /api/auth/logout
GET  /api/auth/me
```

Login example:

```json
{
  "email": "vendor@spareke.com",
  "password": "SpareKe123!"
}
```

### Products / Marketplace

```http
GET  /api/products
POST /api/products
GET  /api/products/:id
PATCH /api/products/:id
GET  /api/marketplace/parts?country=KE
```

### Vehicle Passport

```http
GET  /api/vehicle-passports
POST /api/vehicle-passports
GET  /api/vehicle-passports/:id
POST /api/vehicle-passports/:id/service-records
```

### RFQs and Quotes

```http
GET  /api/rfqs
POST /api/rfqs
POST /api/rfqs/:id/quotes
```

### Garage Bookings

```http
GET  /api/bookings
POST /api/bookings
```

### Orders and Escrow

```http
GET  /api/orders
POST /api/orders
POST /api/escrow/:id/complete
POST /api/escrow/release
```

### Subscription Automation

```http
GET  /api/subscriptions/webhook
POST /api/subscriptions/webhook
```

### Admin

```http
GET  /api/admin/overview
GET  /api/admin/users
POST /api/admin/verify
```

## 5. Database Models Added

The Prisma schema includes:

- User
- BusinessProfile
- VerificationDocument
- VehiclePassport
- ServiceRecord
- Product
- RFQ
- RFQQuote
- GarageBooking
- Order
- Escrow
- Subscription
- Wallet
- WalletTransaction
- AuditLog

## 6. Automation Logic Added

### Subscription Payment Automation

When a payment webhook is received:

1. Payment status is checked.
2. Subscription is created or updated.
3. Renewal date is extended.
4. Premium features can be unlocked.
5. Audit log is recorded.

### Escrow Release Automation

When work/order completion is submitted:

1. System checks dispute/fraud holds.
2. System checks provider completion.
3. System checks customer confirmation.
4. If customer has not confirmed, auto-release is scheduled.
5. If customer confirms, platform fee is deducted.
6. Provider wallet is credited.
7. Wallet transaction and audit log are created.

## 7. Production Upgrade Path

To move toward production:

1. Switch Prisma datasource from SQLite to PostgreSQL.
2. Add real payment gateways such as Stripe, Flutterwave, Paystack or M-Pesa.
3. Add file storage for verification documents and product images.
4. Add real-time messaging using WebSockets or managed realtime services.
5. Add background jobs for escrow auto-release and subscription retries.
6. Add admin UI forms connected to the backend endpoints.
7. Add full role-based middleware protection on dashboard pages.
8. Add production-grade logging, monitoring and audit trails.
