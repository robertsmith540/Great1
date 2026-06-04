# spareke Current Progress

## Brand Update

The product name is now standardized as:

**spareke**

Positioning:

**Automotive Intelligence System**

A logo asset has been added based on the provided workwear reference image.

Logo files:

- `public/spareke-logo.svg` — full horizontal logo with tagline
- `public/spareke-mark.svg` — compact icon/mark for headers and favicon

The app metadata and header now use the spareke automotive intelligence identity.

## Backend + UI Connection Progress

The following frontend sections are now connected to real backend/database systems:

### Login

`/login`

- Real login form connected to `/api/auth/login`
- Demo account selector
- JWT session cookie is created after login
- User is redirected to the correct dashboard based on backend role

### Auth Session

- Header now shows login button when logged out
- Header shows signed-in user and dashboard link when logged in
- `/api/auth/me` returns the logged-in user, wallet, subscription and vehicle passport data

### Marketplace

`/marketplace`

- Now reads real products from Prisma database
- Products include seller details, stock, verification, country and fitment data

### Vehicle Owner Dashboard

`/dashboard/vehicle-owner`

- Now requires login
- Reads real vehicle passport data from Prisma
- Reads service history from Prisma
- Displays health score, mileage, valuation and AI summary from backend data

### Admin Dashboard

`/dashboard/admin`

- Now requires admin login
- Reads real backend counts from Prisma:
  - Users
  - Products
  - Vehicle passports
  - RFQs
  - Orders
  - Subscriptions
  - Escrow rows
  - Verification queue

### Other Dashboards

The mechanic, garage, vendor, wholesaler, manufacturer and fleet pages are now protected by backend authentication and role checks. Their next stage is to replace remaining static placeholder metrics with database-backed metrics and forms.

## Demo Login

All seeded users use password:

```text
SpareKe123!
```

Accounts:

- `owner@spareke.com`
- `mechanic@spareke.com`
- `garage@spareke.com`
- `vendor@spareke.com`
- `wholesaler@spareke.com`
- `manufacturer@spareke.com`
- `fleet@spareke.com`
- `admin@spareke.com`

## How to Run

```bash
cd spareke-marketplace
npm install
npm run backend:setup
npm run dev
```

Open:

```text
http://localhost:3000
```

## Next Recommended Build Stage

1. Connect every dashboard metric to Prisma data.
2. Add product create/edit forms for vendors, wholesalers and manufacturers.
3. Add vehicle passport create/edit UI.
4. Add garage booking UI connected to `/api/bookings`.
5. Add RFQ posting and quote submission UI.
6. Add admin verification action buttons.
7. Add wallet pages and escrow release buttons.
8. Add image/document upload support.
9. Add production PostgreSQL configuration.
10. Add payment gateway integrations.

## Latest Backend-Connected Dashboard Update

The remaining dashboards now have stronger backend connections and working forms.

### Vehicle Owner

- Backend vehicle passport display
- Backend service history display
- Garage booking form connected to `/api/bookings`
- RFQ posting form connected to `/api/rfqs`

### Mechanic

- Reads assigned requests from `GarageBooking`
- Reads available unassigned specialist requests
- Can claim/update booking status through `/api/bookings/:id`
- Can add service history to vehicle passport through `/api/vehicle-passports/:id/service-records`
- Reads wallet data

### Garage

- Reads live garage bookings
- Reads vehicle passport packets attached to bookings
- Can update booking status
- Can add service history to vehicle passports
- Reads orders and wallet data

### Vendor

- Reads product listings from database
- Reads orders, RFQs, wallet and subscription
- Product creation form connected to `/api/products`
- RFQ quote form connected to `/api/rfqs/:id/quotes`

### Wholesaler

- Reads bulk catalogue from database
- Calculates warehouse value from live product stock
- Reads bulk RFQs and orders
- Product creation form connected to `/api/products`
- Quote form connected to `/api/rfqs/:id/quotes`

### Manufacturer

- Reads factory catalogue from database
- Reads global RFQ demand signals
- Reads submitted quotes
- Product creation form connected to `/api/products`
- Quote form connected to `/api/rfqs/:id/quotes`

### Fleet

- Reads fleet-owned vehicle passports
- Reads fleet RFQs, bookings, orders and wallet
- RFQ form connected to `/api/rfqs`
- Fleet seed data now includes multiple vehicle passports

### Data Storage Documentation

A new document explains where vehicle data, subscriber data and vehicle history are stored:

```text
docs_data_storage.md
```
