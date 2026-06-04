# Netlify Drop Deploy Instructions

Use the ZIP named:

```text
spareke-netlify-root-package.zip
```

This ZIP has `package.json`, `netlify.toml`, `src`, `prisma`, and all project files at the ZIP root.

Do NOT upload a ZIP that contains a single `spareke-marketplace/` folder inside it, because Netlify may not find `netlify.toml`.

## Required environment variables before deploy

Set these in Netlify:

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

## Build settings

Build command:

```bash
npm run netlify:build
```

Publish directory:

```text
.next
```
