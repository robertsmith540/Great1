# spareke Security Hardening Status

spareke handles sensitive data: vehicle passports, GPS locations, insurance policies, business verification, payments and escrow. This document tracks the security hardening layer now added and what remains before public launch.

## Added Now

### 1. Security Headers

Implemented in:

```text
middleware.ts
```

Headers added:

- Content-Security-Policy
- X-Frame-Options: DENY
- X-Content-Type-Options: nosniff
- Referrer-Policy
- Permissions-Policy
- Cross-Origin-Opener-Policy
- Cross-Origin-Resource-Policy

### 2. API Rate Limiting

Implemented in:

```text
middleware.ts
```

Current in-memory limits:

- Login route: stricter limit
- General API routes: broader limit

For production, replace with Redis/Upstash/Vercel KV so limits work across all serverless instances.

### 3. Same-Origin Write Guard

Implemented in:

```text
middleware.ts
```

Mutating API requests from other browser origins are blocked, except allowlisted webhooks.

This reduces CSRF risk.

### 4. Login Brute-Force Lockout

Implemented in:

```text
src/app/api/auth/login/route.ts
```

After repeated failed attempts, login is temporarily locked for that IP/email combination.

### 5. Stronger Password Rules

Implemented in:

```text
src/app/api/auth/register/route.ts
```

Passwords must include:

- Minimum 10 characters
- Uppercase letter
- Lowercase letter
- Number

### 6. Audit Logs

Added audit logs for:

- Successful login
- Account registration
- Existing escrow/admin/product actions

Audit model:

```text
AuditLog
```

### 7. Upload Security Metadata Validation

Implemented:

```text
src/lib/uploadSecurity.ts
src/app/api/uploads/validate/route.ts
```

Allowed file types:

- JPG
- PNG
- WEBP
- PDF

Blocked:

- Executables
- Scripts
- Shell files
- APK/JAR/MSI/DMG etc.

Max file size:

```text
8MB
```

Production must still scan actual file bytes before publishing.

### 8. CSRF Token Endpoint

Implemented:

```text
GET /api/security/csrf
```

File:

```text
src/app/api/security/csrf/route.ts
```

Current primary CSRF protection is same-origin checking. The token endpoint is ready for deeper form integration later.

## Firebase GPS Security Rules Needed

Do not use fully public read/write rules in production.

Recommended direction:

- Providers can only write their own location.
- Clients can only see assigned provider exact location.
- Public locator should show approximate provider availability, not exact private coordinates.
- Location history should expire.

## Payment Security Still Needed Before Real Money

Before real escrow/payments:

- Verify payment webhook signatures.
- Add idempotency keys.
- Use immutable ledger entries.
- Add manual review thresholds.
- Add refund/dispute workflow with evidence storage.

## Upload/Malware Security Still Needed Before Documents

Before real user documents:

- Private storage bucket.
- Signed upload URLs.
- Virus/malware scanning.
- MIME sniffing from actual bytes.
- Document access policies.
- Audit every document view/download.

## Production Must Replace In-Memory Security State

The current rate limiter and login lockout use memory maps for MVP/local/demo use.

Production should use:

- Upstash Redis
- Vercel KV
- Cloudflare Turnstile/Bot protection
- WAF such as Cloudflare

## Current Security Position

The system is now safer for a controlled demo, but not yet ready for public real-money production without:

1. PostgreSQL production database
2. Redis-backed rate limiting
3. Secured Firebase rules
4. Secure file storage and malware scanning
5. Payment webhook signature verification
6. Admin MFA
7. Real monitoring/alerting
