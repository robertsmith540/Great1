# Firebase Admin Secret Setup for spareke

## Critical warning

A Firebase service account private key is a server-side secret. Never commit it to GitHub, never place it in public code, and never expose it to the browser.

If a private key was pasted into chat, email, screenshots, or any shared tool, treat it as compromised and rotate it in Firebase Console.

## Rotate the exposed key

1. Open Firebase Console / Google Cloud Console.
2. Go to IAM & Admin → Service Accounts.
3. Select the Firebase Admin SDK service account.
4. Go to Keys.
5. Delete the exposed key.
6. Generate a new key.
7. Store the new key only in environment variables / secret manager.

## Required environment variables

Use the raw values from the new service account JSON:

```env
FIREBASE_PROJECT_ID="spareke-f7f08"
FIREBASE_CLIENT_EMAIL="firebase-adminsdk-xxxxx@spareke-f7f08.iam.gserviceaccount.com"
FIREBASE_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n"
```

Important:

- `FIREBASE_CLIENT_EMAIL` must be plain email only.
- Do not include markdown like `[...](mailto:...)`.
- `FIREBASE_PRIVATE_KEY` should keep escaped newlines as `\n` if stored in a single-line env variable.

## Local development

Create `.env.local` locally. This file is ignored by `.gitignore`.

```env
FIREBASE_PROJECT_ID="spareke-f7f08"
FIREBASE_CLIENT_EMAIL="firebase-adminsdk-xxxxx@spareke-f7f08.iam.gserviceaccount.com"
FIREBASE_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n"
```

Then restart:

```bash
npm run dev
```

## Vercel production

Add the same three variables in:

```text
Vercel Project → Settings → Environment Variables
```

Do not put private keys in `NEXT_PUBLIC_*` variables.

## Validate locally

After setting env vars, run:

```bash
npm run security:check-firebase-admin
```

## Why this matters

The Firebase Admin key can mint custom Firebase tokens. If stolen, attackers could potentially impersonate server-side authority. It must be rotated and stored only in trusted secret storage.
