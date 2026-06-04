# How spareke Becomes a Full Machine-Learning System

Yes, it is doable.

The correct approach is not to jump directly into black-box AI. spareke should evolve in phases:

## Phase 1: Baseline Intelligence — Done

The system now has functional baseline models:

- Demand forecast baseline
- Labour estimate baseline
- OBD diagnostic baseline
- Part recognition foundation
- Supplier risk scoring
- Insurance risk scoring
- Fleet route wear prediction
- RFQ advisor

These are not deep-learning models yet, but they are functional and integrated.

## Phase 2: Data Collection — Active

The system now stores model-related data:

- OBDReading
- PartRecognitionRequest
- SupplierRiskScore
- FleetRouteWearSignal
- LabourBenchmark
- MLPrediction
- MLModel

Every prediction can be logged and compared with real outcomes later.

## Phase 3: Real ML Training

Use Python-based ML stack:

- pandas
- scikit-learn
- XGBoost/LightGBM
- PyTorch/TensorFlow for computer vision
- FastAPI for model serving
- MLflow or simple model registry

## Phase 4: Model Service

Recommended architecture:

```text
Next.js spareke app → Internal ML API → Python model service → PostgreSQL/feature store
```

The Next.js app keeps business logic and security. The Python ML service performs heavy model predictions.

## Phase 5: Production ML Ops

Add:

- Feature store
- Training pipelines
- Model versioning
- Prediction monitoring
- Drift detection
- Retraining schedules
- Human override workflows

## What Was Activated Now

New route:

```text
/ml/activate
```

New APIs:

```text
GET  /api/ml/status
POST /api/ml/sync
POST /api/ml/predict
```

New model registry:

```text
MLModel
```

New prediction log:

```text
MLPrediction
```

New advanced intelligence APIs:

```text
POST /api/intelligence/obd
POST /api/intelligence/part-recognition
POST /api/intelligence/supplier-risk
POST /api/intelligence/insurance-risk
POST /api/intelligence/fleet-wear
GET  /api/intelligence/rfq-advisor?rfqId=...
```

## Current Status

spareke is now ML-ready and baseline-functional.

Full ML becomes accurate after collecting enough real data:

- 500+ labour jobs per region/task
- 5,000+ RFQs and accepted quotes
- 10,000+ product searches and purchase outcomes
- 1,000+ vehicle service histories
- 1,000+ OBD readings and resolved faults
- verified image datasets for parts recognition
