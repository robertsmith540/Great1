# Firebase GPS Security + Assigned Trip Privacy

This document describes the secure GPS model for spareke emergency mechanics, garages and towing.

## Core Privacy Rule

Public users should **not** see exact provider GPS.

spareke separates location into two layers:

## 1. Public Approximate Availability

Path:

```text
spareke/regions/{region}/publicProviders/{providerId}/approx
```

Purpose:

- Show provider is available
- Show approximate distance/ETA
- Show provider type: mechanic, towing, garage
- Do not expose exact private coordinates publicly

## 2. Assigned Trip Exact Tracking

Path:

```text
spareke/regions/{region}/trips/{tripId}/clientLocation
spareke/regions/{region}/trips/{tripId}/providerLocation
spareke/regions/{region}/trips/{tripId}/meta
```

Exact location is only visible to:

- The client who created the trip
- The assigned provider
- Admin

Exact tracking activates only when the trip is accepted/assigned.

Exact tracking is disabled after:

- Completion
- Cancellation
- Dispute close

## Backend Model

Prisma model:

```text
AssistanceTrip
```

Important fields:

- clientId
- providerId
- vehicleId
- requestType
- status
- pickupLat/pickupLng
- firebaseTripPath
- exactLocationEnabled
- vehiclePacketJson

## APIs

Create trip:

```http
POST /api/emergency/trips
```

List trips:

```http
GET /api/emergency/trips
```

Assign provider:

```http
POST /api/emergency/trips/:id/assign
```

Complete trip:

```http
POST /api/emergency/trips/:id/complete
```

Cancel trip:

```http
POST /api/emergency/trips/:id/cancel
```

Mint Firebase custom token:

```http
GET /api/firebase/token
```

## Firebase Custom Auth

The app now supports Firebase custom auth tokens through Firebase Admin.

Server env variables needed:

```env
FIREBASE_PROJECT_ID="spareke-f7f08"
FIREBASE_CLIENT_EMAIL="firebase-adminsdk-xxxxx@spareke-f7f08.iam.gserviceaccount.com"
FIREBASE_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n"
```

Client logs into Firebase using:

```text
/api/firebase/token
```

Custom token claims:

- role
- region
- sparekeUserId

## Firebase Rules

Rules file:

```text
firebase.database.rules.json
```

These rules enforce:

- Providers can only write their own public approximate location
- Client/provider/admin can read exact trip locations
- Client can write only their own clientLocation
- Provider can write only their own providerLocation
- Completed/cancelled trips cannot continue writing location

## Pages

Privacy explanation:

```text
/emergency/privacy
```

Private trip manager:

```text
/emergency/trips
```

General locator:

```text
/locator
```

Realtime testing:

```text
/realtime
```

## Production Notes

Before launch:

1. Upload `firebase.database.rules.json` to Firebase Console.
2. Add Firebase Admin service account env variables to hosting.
3. Ensure provider exact locations are not stored permanently unless legally required.
4. Add TTL cleanup for trip realtime paths after completion.
5. Add consent text for client/provider location sharing.
6. Show public users approximate provider dots only.
