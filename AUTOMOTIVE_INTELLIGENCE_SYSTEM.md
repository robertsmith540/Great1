# spareke: Automotive Intelligence System

The motto is not cosmetic. The platform now has a defined intelligence layer that supports every major user group.

## Intelligence Already Present

### 1. Vehicle Passport Intelligence

Data sources:

- VehiclePassport
- ServiceRecord
- FleetAlert
- GarageBooking

Capabilities:

- Vehicle health score
- Service history memory
- AI summary
- Valuation support
- Mechanic request packet
- Service-due and brake-health signals

### 2. Vendor Demand Intelligence

Data sources:

- Product stock
- RFQs
- Marketplace demand
- Orders
- Garage bookings

Capabilities:

- Demand signals by category
- Stockout risk
- Suggested restock focus
- Product visibility opportunities

### 3. Wholesaler Global Demand Intelligence

Data sources:

- RFQ quantities
- Demand by region
- Product stock cover
- Bulk sourcing activity

Capabilities:

- Import priority
- FCL/LCL suggestions
- Emerging-market opportunities
- Regional stock cover estimates

### 4. Manufacturer Production Intelligence

Data sources:

- Global RFQs
- Demand signals
- Shortage categories
- Regional market demand

Capabilities:

- Recommended production quantities
- Overproduction risk
- Target market suggestions
- Product family demand confidence

### 5. Fleet Predictive Maintenance Intelligence

Data sources:

- Fleet vehicle passports
- Service history
- Brake health
- Service due distance
- Fleet alerts

Capabilities:

- Service due in km/miles
- Brake system alerts
- Health board
- Fleet spend tracking
- Preventive maintenance signals

### 6. Emergency/GPS Intelligence

Data sources:

- ProviderLocation
- AssistanceTrip
- Firebase Realtime Database

Capabilities:

- Nearby provider ETA
- Towing/mechanic/garage availability
- Public approximate location
- Private assigned-trip exact location
- Trip privacy rules

### 7. Insurance Intelligence

Data sources:

- InsuranceProvider
- InsurancePolicy
- InsuranceQuote
- RegionConfig
- Vehicle passport health

Capabilities:

- Regional policy quotes
- Renewal tracking
- Policy switching support
- Region-specific insurance rules

### 8. Trust and Recognition Intelligence

Data sources:

- RecognitionAward
- Reviews/ratings foundation
- Orders/bookings/completion stats

Capabilities:

- Mechanic of the Month
- Garage of the Month
- Vendor of the Month
- Wholesaler of the Month
- Manufacturer Excellence
- Client of the Month
- Wall of Champions

## New Intelligence Hub

Route:

```text
/intelligence
```

API:

```text
GET /api/intelligence/overview?region=KE
```

Backend functions:

```text
src/lib/intelligence.ts
```

## More Intelligence We Can Add

### Real AI/ML modules later

1. OBD-II live diagnostic ingestion
2. Computer vision part recognition
3. Demand forecast model from RFQs/searches/bookings
4. Counterfeit/fraud detection model
5. Insurance risk scoring from vehicle health
6. Fleet route wear prediction
7. Supplier quality scoring
8. Dynamic labour pricing by region/task/urgency
9. AI negotiation assistant for RFQs
10. Predictive warranty claim detection

## Vision Fit

The attached HTML concepts map very well to the spareke vision:

- vendor demand dashboard → vendor demand intelligence
- global intelligence landing page → `/intelligence`
- AI diagnostic engine mobile dashboard → vehicle passport diagnostics and future mobile app
- manufacturer production trends → manufacturer production intelligence
- wholesaler global demand intelligence → bulk sourcing and wholesaler dashboard

The current implementation turns these concepts into a unified intelligence layer rather than isolated pages.
