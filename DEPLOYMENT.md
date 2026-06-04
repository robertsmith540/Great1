# spareke Deployment Guide

This project currently runs locally with SQLite for fast development. For a real online demo, deploy with **Vercel + PostgreSQL + Firebase Realtime Database**.

## Recommended Stack

- Vercel: Next.js hosting
- Neon or Supabase: PostgreSQL database
- Firebase Realtime Database: live GPS for mechanics/garages/towing
- Firebase Storage or S3: future image/document uploads

## 1. Create PostgreSQL

Use Neon/Supabase/Railway and copy the connection string:

```env
DATABASE_URL="postgresql://USER:PASSWORD@HOST:5432/spareke?sslmode=require"
```

## 2. Set Vercel Environment Variables

Add all values from:

```text
.env.production.example
```

Important variables:

```env
DATABASE_URL=
JWT_SECRET=
NEXT_PUBLIC_FIREBASE_DATABASE_URL=
NEXT_PUBLIC_FIREBASE_API_KEY=
```

## 3. Push Production Database Schema

From your local machine or a CI shell:

```bash
npx prisma db push --schema prisma/schema.postgres.prisma
```

Optional seed:

```bash
node prisma/seed.js
```

For production, replace demo seed data with real onboarding.

## 4. Deploy to Vercel

Vercel will use:

```text
vercel.json
```

Build command:

```bash
prisma generate --schema prisma/schema.postgres.prisma && next build
```

## 5. Firebase Realtime Database Rules for Internal Testing

```json
{
  "rules": {
    "spareke": {
      "regions": {
        "$region": {
          "providers": {
            "$uid": {
              "location": {
                ".read": true,
                ".write": true
              }
            }
          }
        }
      }
    }
  }
}
```

Lock these down before public launch.

## 6. Test After Deploy

Open:

```text
/login
/realtime
/locator
/marketplace
/dashboard/vehicle-owner
/dashboard/vendor
/insurance/manage
```

Demo password if seeded:

```text
SpareKe123!
```
