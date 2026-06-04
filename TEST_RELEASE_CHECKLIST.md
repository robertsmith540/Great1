# spareke Test Release Checklist

## Before Sharing Demo

- [ ] `npm install` runs successfully
- [ ] `npm run demo:setup` runs successfully
- [ ] `npm run build` passes
- [ ] `/` loads welcome page
- [ ] `/login` works with demo accounts
- [ ] `/dashboard/admin` loads for admin
- [ ] `/marketplace` shows products
- [ ] `/documents/manage` rejects unsafe files
- [ ] `/intelligence` loads
- [ ] `/ml/activate` loads
- [ ] `/champions` shows awards

## Security Checks

- [ ] Do not commit `.env`
- [ ] Do not commit Firebase private key
- [ ] Rotate any key pasted into chat or shared documents
- [ ] Firebase rules reviewed
- [ ] Firebase Admin env variables only in secret manager
- [ ] Demo database contains no real user documents

## Deployment Checks

- [ ] PostgreSQL database created
- [ ] `DATABASE_URL` set in hosting provider
- [ ] `JWT_SECRET` set and strong
- [ ] Firebase client env variables set
- [ ] Firebase Admin server env variables set
- [ ] `firebase.database.rules.json` published
- [ ] Production upload storage plan selected

## Mobile/GPS Checks

- [ ] Test through HTTPS for phone GPS
- [ ] Browser location permission allowed
- [ ] `/locator` shows providers
- [ ] `/realtime` starts GPS publisher
- [ ] `/emergency/trips` hides exact GPS until assigned

