# spareke Realtime, Regional Adaptation and Insurance Layer

## 1. Regional Adaptation

spareke now has a regional adaptation foundation.

Model:

```text
RegionConfig
```

Stores:

- Country code
- Country name
- Local spareke brand name
- Currency
- Distance unit: km or mi
- Language
- Payment rails
- Tax rules JSON
- Insurance rules JSON
- Emergency number
- Regional support contact

Seeded regions:

- Kenya: KES, km, M-Pesa/card/bank transfer
- United States: USD, miles, card/ACH/wallet
- United Kingdom: GBP, miles, card/bank/wallet
- China: CNY, km, Alipay/WeChat Pay/bank transfer

Helper:

```text
src/lib/regional.ts
```

This allows dashboards and pages to dynamically tailor themselves by region and user.

## 2. Firebase Realtime Integration

spareke now has a Firebase Realtime Database scaffold.

Files:

```text
src/lib/firebase.ts
src/components/realtime/LiveLocationPublisher.tsx
src/components/realtime/LiveLocationViewer.tsx
src/app/realtime/page.tsx
```

Route:

```text
/realtime
```

What it does:

- Provider can publish browser GPS location
- Location is saved to spareke backend through `/api/providers/location`
- If Firebase env keys are configured, location is also written to Firebase Realtime Database
- Client viewer listens to Firebase for live provider movement

Firebase realtime path pattern:

```text
spareke/regions/{REGION}/providers/{USER_ID}/location
```

Example:

```text
spareke/regions/KE/providers/user_123/location
```

## 3. Firebase Environment Variables

Add these to `.env` or production hosting environment:

```env
NEXT_PUBLIC_FIREBASE_API_KEY=""
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=""
NEXT_PUBLIC_FIREBASE_DATABASE_URL=""
NEXT_PUBLIC_FIREBASE_PROJECT_ID=""
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=""
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=""
NEXT_PUBLIC_FIREBASE_APP_ID=""
```

Without these values, the realtime page still saves location to the spareke backend, but Firebase live movement is disabled.

## 4. GPS Provider Location

Model:

```text
ProviderLocation
```

Stores:

- User/provider ID
- Provider type: mechanic, garage, towing, specialist
- Latitude
- Longitude
- Availability
- Service radius
- Response minutes
- Specialties
- Region/country

APIs:

```text
GET  /api/providers/nearby?lat=-1.2921&lng=36.8219&type=TOWING
POST /api/providers/location
```

Pages:

```text
/locator
/realtime
```

## 5. Insurance Layer

spareke now includes a vehicle insurance foundation.

Models:

```text
InsuranceProvider
InsurancePolicy
InsuranceQuote
```

Pages:

```text
/insurance/manage
```

APIs:

```text
GET  /api/insurance/providers?country=KE
POST /api/insurance/quote
GET  /api/insurance/policies
POST /api/insurance/policies
```

Insurance features started:

- Regional insurer providers
- Vehicle insurance quotes
- Policy access/viewing
- Renewal tracking
- Policy status
- Region-specific currency and rules

Future production additions:

- Actual insurer API integrations
- Policy document upload
- Renewal payment gateway
- Claims intake
- Inspection linkage
- Fleet insurance policy management

## 6. Recommended Production Architecture

For a global spareke system:

```text
PostgreSQL + Prisma = source of truth
Firebase Realtime Database = live GPS movement and realtime provider availability
Firebase Cloud Messaging = push notifications
S3-compatible storage = documents/images
Redis/background jobs = escrow auto-release, insurance renewals, subscription retries
OpenSearch = global parts and vehicle fitment search
```
