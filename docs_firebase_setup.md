# Firebase Realtime Setup for spareke

Firebase live feeds will only become true push realtime after Firebase project credentials are added.

## Why live feed may not show yet

The code is already scaffolded, but the app cannot connect to Firebase until these environment values are filled:

```env
NEXT_PUBLIC_FIREBASE_API_KEY=""
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=""
NEXT_PUBLIC_FIREBASE_DATABASE_URL=""
NEXT_PUBLIC_FIREBASE_PROJECT_ID=""
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=""
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=""
NEXT_PUBLIC_FIREBASE_APP_ID=""
```

Until then, `/realtime` uses a backend polling fallback from `/api/providers/nearby` every 5 seconds.

## Firebase Database Path

Live provider locations are written to:

```text
spareke/regions/{REGION}/providers/{USER_ID}/location
```

Example:

```text
spareke/regions/KE/providers/user_123/location
```

## Suggested Realtime Database Security Rules for Development

Use strict rules before production. For first internal testing:

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

Production should restrict writes to authenticated providers only.

## What happens now

- Provider clicks **Start live GPS** on `/realtime`.
- Browser asks for location permission.
- Location is saved to spareke backend through `/api/providers/location`.
- If Firebase is configured, location is also pushed to Firebase Realtime Database.
- Client viewer listens to Firebase; otherwise it polls backend every 5 seconds.

## Firebase config received

The Firebase web config has been added to `.env` for local development.

Important: the pasted Firebase config did not include `databaseURL`. For Realtime Database, spareke added the standard default URL pattern:

```text
https://spareke-f7f08-default-rtdb.firebaseio.com
```

If your Firebase Console shows a different Realtime Database URL, replace `NEXT_PUBLIC_FIREBASE_DATABASE_URL` in `.env`.

## If live feed still does not work

Check these in Firebase Console:

1. Realtime Database is created/enabled.
2. The database URL matches `.env`.
3. Database rules allow the current test write path.
4. Browser location permission is allowed.
5. Restart `npm run dev` after changing `.env`.

Path used by spareke:

```text
spareke/regions/{REGION}/providers/{USER_ID}/location
```
