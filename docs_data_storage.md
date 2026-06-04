# Where spareke Stores Data Right Now

## Current Development Storage

Right now, spareke stores backend data locally using **SQLite through Prisma ORM**.

The database file is created here:

```text
spareke-marketplace/prisma/dev.db
```

The connection is configured in:

```text
spareke-marketplace/.env
```

Current local value:

```env
DATABASE_URL="file:./dev.db"
```

Because Prisma resolves this relative to `prisma/schema.prisma`, the actual local database file is inside the `prisma` folder.

## Database Schema

The data structure is defined here:

```text
spareke-marketplace/prisma/schema.prisma
```

## Main Data Tables

### User Data
Stored in:

```text
User
```

Includes:

- Name
- Email
- Phone
- Password hash
- Role
- Country
- Account status

### Vehicle Data
Stored in:

```text
VehiclePassport
```

Includes:

- Owner ID
- Make
- Model
- Year
- Trim
- Fuel type
- Transmission
- VIN hash
- Plate
- Mileage
- Health score
- Valuation
- AI summary
- Vehicle documents JSON

### Vehicle Service History
Stored in:

```text
ServiceRecord
```

Includes:

- Vehicle ID
- Provider/mechanic/garage ID
- Service title
- Notes
- Parts used
- Mileage at service
- Cost
- Currency
- Completion date

This is what powers the vehicle passport history and future valuation intelligence.

### Subscriber Data
Stored in:

```text
Subscription
```

Includes:

- User ID
- Plan
- Status
- Renewal date

Subscription payment automation updates this table when `/api/subscriptions/webhook` receives a paid event.

### Wallet Data
Stored in:

```text
Wallet
WalletTransaction
```

Includes:

- Wallet balance
- Currency
- Escrow payouts
- Payment/fund-release transaction history

### Escrow Data
Stored in:

```text
Escrow
Order
```

Includes:

- Order amount
- Escrow status
- Platform fee
- Provider payout
- Release schedule
- Release timestamp

### Product and Marketplace Data
Stored in:

```text
Product
```

Includes:

- Seller
- Name
- Category
- Brand
- OEM/part number
- Price
- Currency
- Stock
- Country/city
- Verification status
- Fitment JSON

### RFQ and Quote Data
Stored in:

```text
RFQ
RFQQuote
```

Includes:

- Buyer request
- Category
- Quantity
- Destination
- Supplier quotes
- Lead time
- Price

### Garage Booking Data
Stored in:

```text
GarageBooking
```

Includes:

- Vehicle owner
- Garage
- Technician
- Vehicle passport link
- Service title
- Status
- Estimated/final price
- Vehicle packet JSON sent to provider

### Admin Audit Trail
Stored in:

```text
AuditLog
```

Includes:

- Actor/admin/user
- Action
- Entity type
- Entity ID
- Metadata JSON
- Timestamp

## Production Storage Recommendation

For production, spareke should move from SQLite to **PostgreSQL**.

Recommended production setup:

```env
DATABASE_URL="postgresql://USER:PASSWORD@HOST:5432/spareke"
```

Recommended storage split:

- PostgreSQL: users, roles, products, vehicle passports, subscriptions, escrow, orders, RFQs
- S3-compatible object storage: product images, verification documents, vehicle documents
- Redis: sessions, queues, realtime counters, background jobs
- Search engine: OpenSearch/Elasticsearch for parts fitment and global marketplace search

## Current Seeded Data

Seed file:

```text
spareke-marketplace/prisma/seed.js
```

Seed creates:

- Demo users for every role
- Demo vehicle owner passport
- Demo fleet vehicle passports
- Demo service history
- Demo products
- Demo RFQ and quote
- Demo booking
- Demo escrow order
- Demo subscription
- Demo audit log
