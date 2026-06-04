# spareke — Automotive Intelligence System

spareke is a regional-aware automotive marketplace and intelligence platform for:

- Vehicle owners
- Mechanics
- Garages
- Vendors
- Wholesalers
- Manufacturers
- Fleet operators
- Insurers
- Towing providers
- Admin operators

It includes marketplace, vehicle passports, RFQs, garage bookings, escrow foundations, insurance, GPS, secure uploads, recognition awards, and ML-ready intelligence modules.

## Quick Start

```bash
cd spareke-marketplace
npm install
npm run demo:setup
npm run dev
```

Open:

```text
http://localhost:3000
```

## Demo Accounts

Password for all demo accounts:

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
| Towing Provider | tow@spareke.com |

## Main Pages

- `/` — Welcome landing page
- `/signup` — Signup before dashboard
- `/login` — Login
- `/marketplace` — Parts marketplace
- `/intelligence` — Automotive intelligence hub
- `/intelligence/advanced` — Advanced AI modules
- `/ml/activate` — ML activation/registry
- `/locator` — GPS locator
- `/realtime` — Firebase realtime GPS
- `/emergency/trips` — Private emergency trips
- `/documents/manage` — Secure uploads
- `/insurance/manage` — Insurance quotes/policies
- `/champions` — Wall of Champions
- `/dashboard/admin` — Admin control

See full route map:

```text
ROUTE_MAP.md
```

## Testing Guide

```text
DEMO_TEST_GUIDE.md
```

## Security Notes

```text
SECURITY_HARDENING.md
SECURE_UPLOAD_PIPELINE.md
FIREBASE_GPS_PRIVACY.md
FIREBASE_ADMIN_SECRET_SETUP.md
```

## ML/AI Notes

```text
AUTOMOTIVE_INTELLIGENCE_SYSTEM.md
FULL_MACHINE_LEARNING_ACTIVATION.md
```

## Create Shareable Demo Archive

```bash
npm run demo:archive
```

This creates a zip outside the project folder and excludes secrets, node_modules, local DB and private uploads.

## Production Recommendation

For live deployment:

- Vercel for Next.js
- PostgreSQL via Neon/Supabase/Railway
- Firebase Realtime Database for live GPS
- S3/Firebase Storage for documents
- Redis/Upstash for production rate limiting
- Real payment gateway for escrow

See:

```text
DEPLOYMENT.md
```
