# Netlify Deployment Fix for spareke

The previous Netlify build failed because Prisma Client was not generated during Netlify CI.

Netlify error:

```text
Prisma has detected that this project was built on Netlify CI, which caches dependencies.
This leads to an outdated Prisma Client because Prisma's auto-generation isn't triggered.
To fix this, make sure to run the prisma generate command during the build process.
```

## Fix Added

### 1. `netlify.toml`

The project now includes:

```toml
[build]
  command = "npm run netlify:build"
  publish = ".next"

[build.environment]
  NODE_VERSION = "20"
  NPM_FLAGS = "--include=dev"

[[plugins]]
  package = "@netlify/plugin-nextjs"
```

### 2. `package.json` scripts

The project now includes:

```json
{
  "scripts": {
    "postinstall": "prisma generate",
    "netlify:build": "prisma generate --schema prisma/schema.postgres.prisma && next build"
  }
}
```

### 3. Netlify Next.js Plugin

The package is installed:

```bash
@netlify/plugin-nextjs
```

## Required Netlify Environment Variables

Go to:

```text
Netlify → Project → Site configuration → Environment variables
```

Add:

```env
DATABASE_URL="postgresql://USER:PASSWORD@HOST:5432/spareke?sslmode=require"
JWT_SECRET="a-long-random-secret"
NEXT_PUBLIC_APP_URL="https://your-netlify-site.netlify.app"
```

Firebase client variables:

```env
NEXT_PUBLIC_FIREBASE_API_KEY="your_firebase_api_key"
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN="spareke-f7f08.firebaseapp.com"
NEXT_PUBLIC_FIREBASE_DATABASE_URL="https://spareke-f7f08-default-rtdb.firebaseio.com"
NEXT_PUBLIC_FIREBASE_PROJECT_ID="spareke-f7f08"
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET="spareke-f7f08.firebasestorage.app"
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID="965821859280"
NEXT_PUBLIC_FIREBASE_APP_ID="1:965821859280:web:e3ebb8245b4e1417d6a5d5"
```

Firebase Admin variables, only after rotating the exposed key:

```env
FIREBASE_PROJECT_ID="spareke-f7f08"
FIREBASE_CLIENT_EMAIL="your-new-service-account-email"
FIREBASE_PRIVATE_KEY="your-new-private-key-with-escaped-newlines"
```

## Production Database Requirement

Netlify deployment should use PostgreSQL, not local SQLite.

Recommended providers:

- Neon PostgreSQL
- Supabase PostgreSQL
- Railway PostgreSQL
- Render PostgreSQL

After creating PostgreSQL and setting `DATABASE_URL`, run schema push once:

```bash
npx prisma db push --schema prisma/schema.postgres.prisma
```

Optional demo seed:

```bash
node prisma/seed.js
```

Be careful: seeding production creates demo users.

## Netlify Build Command

If Netlify UI asks for a build command, use:

```bash
npm run netlify:build
```

Publish directory:

```text
.next
```

## Why this zip should work better

This package includes:

- `netlify.toml`
- Updated `package.json`
- Updated `package-lock.json`
- `@netlify/plugin-nextjs`
- `prisma/schema.postgres.prisma`
- Prisma generation during install/build
- Deployment and environment variable documentation
