# spareke Demo Test Guide

This guide helps you or a technical tester run the spareke demo locally.

## 1. Requirements

Install these first:

- Node.js 20+
- npm
- A modern browser: Chrome, Edge, Safari or Firefox

For GPS testing, use:

- `localhost`, or
- an HTTPS deployment/tunnel

Do not open files directly with `file:///...`.

## 2. Start From Fresh Clone/Folder

```bash
cd spareke-marketplace
npm install
npm run demo:setup
npm run dev
```

Then open:

```text
http://localhost:3000
```

## 3. Demo Login Accounts

All demo users use:

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

## 4. Recommended Test Flow

### A. Public First Impression

Open:

```text
/
```

Check:

- Welcome page
- Search bar
- Shop/Mechanic/List Business cards
- How spareke works
- Community spotlight awards
- Verified experts

### B. Signup

Open:

```text
/signup
```

Try creating:

- Vehicle owner
- Vendor
- Garage
- Fleet admin

### C. Login

Open:

```text
/login
```

Login as:

```text
owner@spareke.com
```

Then test:

```text
/dashboard/vehicle-owner
/vehicle-passports/manage
/bookings/manage
/rfqs/manage
/insurance/manage
```

### D. Vendor / Wholesaler / Manufacturer

Login as:

```text
vendor@spareke.com
wholesaler@spareke.com
manufacturer@spareke.com
```

Test:

```text
/dashboard/vendor
/dashboard/wholesaler
/dashboard/manufacturer
/products/manage
/requests/open
/bulk-sourcing
/intelligence
```

### E. Mechanic / Garage / Towing GPS

Login as:

```text
mechanic@spareke.com
```

Test:

```text
/locator
/realtime
/emergency/privacy
/emergency/trips
/dashboard/mechanic
```

### F. Admin

Login as:

```text
admin@spareke.com
```

Test:

```text
/dashboard/admin
/admin/verifications
/champions
/documents/manage
/escrow/manage
/ml/activate
```

## 5. GPS Testing

Open:

```text
/realtime
```

Click:

```text
Start live GPS
```

Allow browser location.

If Firebase Admin credentials are not configured, backend fallback still works, but exact secure Firebase custom-token tracking requires:

```env
FIREBASE_PROJECT_ID
FIREBASE_CLIENT_EMAIL
FIREBASE_PRIVATE_KEY
```

## 6. Secure Upload Test

Open:

```text
/documents/manage
```

Try uploading:

- PNG
- JPG
- WEBP
- PDF

Blocked/rejected:

- EXE
- JS
- SH
- APK
- PDF with JavaScript/OpenAction
- Files over 8MB

## 7. ML/AI Test

Open:

```text
/intelligence
/intelligence/advanced
/ml/activate
```

Try:

- OBD diagnostic form
- Part recognition form
- Insurance risk form
- Fleet route wear form

## 8. Reset Demo Data

If data becomes messy:

```bash
npm run demo:reset
npm run dev
```

## 9. Common Problems

### `next: not found`

Run:

```bash
npm install
```

### Database errors

Run:

```bash
npm run demo:reset
```

### GPS not working

Use:

```text
http://localhost:3000
```

or HTTPS. Browser GPS usually will not work by opening files directly.

### Firebase realtime not working

Check:

- Realtime Database is enabled
- Database URL is correct
- Firebase rules are published
- Firebase Admin env variables are configured for custom tokens

