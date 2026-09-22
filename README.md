# Adaptiv Health

A comprehensive cardiac-rehabilitation health monitoring platform with a **FastAPI backend**, **React clinician dashboard**, and **Flutter patient mobile app**.

------------------------------------

## Overview

Adaptiv Health is a clinical-grade health monitoring system designed for:
- **Patients** — Track heart rate, blood pressure, nutrition, rehab progress, and recovery via the mobile app
- **Clinicians** — Monitor patients, assess risk, manage alerts, and message patients via the web dashboard
- **Backend** — Secure data management with ML-powered risk prediction, anomaly detection, and AI coaching

------------------------------------
## ----------Quick Start------------

```bash
#Dashboard for doc
Dashboard available at dashboard-adaptivhealthuowd.xyz

      LoginCredentials
      admin 
      #username: admin@test.com
      #password: password123
      Doctor
      #username: doctor@test 
      #password: password123

***********************************
# mobile app for patient
cd\mobile-app

flutter pub get

flutter run -d chrome --dart-define=API_BASE_URL=https://api.back-adaptivhealthuowd.xyz/api/v1

      LoginCredntials
      Patient
      #username: patient1@test.com
      #password: password123

#start mock simulator in profile screen
**********************************

```


Mobile app-- release build apk availble at mobile-app\build\outputs\flutter-apk

### To run LOCAL
### Prerequisites
- Python 3.9+
- Node.js 16+
- Flutter 3.13+
- PostgreSQL 12+




### 1. Configure Environment
```bash
cp .env.example .env        # Edit with your database URL, secret key, etc.
cp web-dashboard/.env.example web-dashboard/.env
```


### 2. Start the Backend
```bash
pip install -r requirements.txt
python start_server.py
```
Backend runs on `http://localhost:8080`. API docs at `/docs`.





### 3. Start the Web Dashboard
```bash
for web,
dashboard-adaptivhealthuowd.xyz

for local,
cd web-dashboard
npm install
npm start
```
Dashboard runs on `http://localhost:3000`.


test login for dashbaord,
username: doctor@test.com
password: password123



### 4. Start the Mobile App
```bash
for web,
flutter run -d chrome --dart-define=API_BASE_URL=https://api.back-adaptivhealthuowd.xyz/api/v1

for local,
cd mobile-app
flutter pub get
flutter run -d chrome --dart-define=USE_LOCAL=true

```

test login for mobile-app,
username: patient1@test.com
password: password123

------------------------------------




## Features

### Patient Mobile App (Flutter) — 16 Screens
- Real-time heart rate monitoring with animated ring display
- Vital signs tracking (SpO2, blood pressure, HRV)
- AI-powered health recommendations and coaching
- Guided workout sessions with HR zone management
- Recovery scoring and breathing exercises
- Nutrition tracking and recipe library
- Rehab programme management
- Device pairing (BLE) and health platform integrations (Fitbit, Apple Health, Google Fit)
- Doctor messaging with read receipts
- Dark mode support
- Onboarding flow and notifications

### Clinician Web Dashboard (React) — 8 Pages
- Patient roster with search and filtering
- Individual patient vitals, history, and medical profile
- Risk assessment with ML prediction explainability
- Advanced ML panel (anomaly detection, trend forecasting)
- Alert management and clinical recommendations
- Patient-clinician messaging
- Admin panel (user management)
- Professional medical UI (WCAG 2.1 AA compliant)

### Backend API (FastAPI) — 16 Route Modules
- JWT authentication with token refresh and blocklist
- Vital signs recording and retrieval
- ML risk prediction with explainability
- Anomaly detection and trend forecasting
- Natural language AI coaching endpoints
- Nutrition tracking and food analysis
- Rehab programme management
- Patient-clinician messaging
- Activity tracking and alerts
- Medical history and consent management
- Medication reminders
- Rate limiting and CORS

-----------------------------------

## Architecture

```text
┌───────────────────────────────┐        ┌───────────────────────────────┐
│     Patient Mobile App        │        │   Clinician Web Dashboard     │
│      Flutter / Dart           │        │   React / TypeScript          │
│ - Vitals, rehab, nutrition    │        │ - Rosters, alerts, messages   │
│ - BLE + health platform sync  │        │ - Risk review + admin tools   │
│ - Edge AI risk checks         │        │ - ML explainability views     │
└──────────────┬────────────────┘        └──────────────┬────────────────┘
           │ HTTPS + JWT                          │ HTTPS + JWT
           └──────────────┬───────────────────────┘
                  │
           ┌──────────▼──────────┐
           │   FastAPI Backend   │
           │ - Auth + RBAC       │
           │ - Vitals + alerts   │
           │ - Rehab + nutrition  │
           │ - Messaging + NLP    │
           │ - ML prediction API  │
           └───────┬───────┬──────┘
               │       │
         ┌─────────────▼┐   ┌──▼─────────────────┐
         │ PostgreSQL   │   │ ML + Integrations   │
         │ SQLAlchemy   │   │ scikit-learn/TFLite │
         │ migrations   │   │ Gemini, SMTP, APIs  │
         └──────────────┘   └─────────────────────┘
```

The mobile app handles patient data capture and edge-side checks, while the dashboard is the clinician workflow layer. Both clients communicate with the backend over authenticated HTTPS, and the backend centralizes persistence, business rules, ML scoring, messaging, and external service calls.

---

## Project Structure

```
AdaptivHealth/
├── app/                          # Backend (FastAPI)
│   ├── main.py                   # Application entry point
│   ├── config.py                 # Environment configuration
│   ├── database.py               # SQLAlchemy database setup
│   ├── rate_limiter.py           # Request rate limiting
│   ├── api/                      # Route handlers (16 modules)
│   ├── models/                   # SQLAlchemy models (14 files)
│   ├── schemas/                  # Pydantic schemas (14 files)
│   └── services/                 # Business logic & ML (16 files)
│
├── web-dashboard/                # React Clinician Dashboard
│   └── src/
│       ├── pages/                # 8 pages + tests
│       ├── components/           # Reusable UI components
│       ├── services/             # API client (Axios)
│       ├── theme/                # Colours, typography, MUI theme
│       └── types/                # TypeScript interfaces
│
├── mobile-app/                   # Flutter Patient App
│   └── lib/
│       ├── screens/              # 16 screens + home sub-widgets
│       ├── providers/            # State management (Provider)
│       ├── services/             # API, BLE, health, notifications
│       ├── widgets/              # Shared reusable widgets
│       └── theme/                # Design tokens
│
├── ml_models/                    # Trained ML model + training scripts
├── tests/                        # Backend test suite (34 test files, pytest)
├── migrations/                   # SQL migration scripts (14 files)
├── scripts/                      # DB setup, migration, deploy utilities
├── docs/                         # Technical documentation
│
├── .env.example                  # Environment variable template
├── requirements.txt              # Python dependencies
├── Dockerfile                    # Container build
├── start_server.py               # Server launcher
└── start.bat                     # Windows quick start
```

-------------------------------------

## API Endpoints

Representative endpoints:

- `POST /auth/register`
- `POST /auth/login`
- `POST /auth/refresh`
- `GET /vitals/latest`
- `GET /vitals/history`
- `POST /vitals/submit`
- `POST /predictions/risk`
- `GET /messages/`
- `POST /messages/`

For complete route coverage, use local API docs at `http://localhost:8080/docs`.

-----------------------------------

## Security

- JWT authentication with refresh tokens and blocklist
- Password hashing with `pbkdf2_sha256` (600k iterations)
- Optional AES-256-GCM encryption for PHI fields
- SQLAlchemy ORM protections against injection risks
- CORS controls and request rate limiting
- Secure token storage on mobile (`flutter_secure_storage`)

-----------------------------------

## Technology Stack

| Layer | Technology |
|-------|-----------|
| **Mobile App** | Flutter, Dart, Provider, Dio |
| **Web Dashboard** | React 18, TypeScript, MUI, Axios |
| **Backend** | FastAPI, Python, Pydantic |
| **Database** | PostgreSQL, SQLAlchemy |
| **ML** | scikit-learn, TensorFlow Lite |
| **Auth** | JWT (HS256), pbkdf2_sha256 |
| **Deployment** | Nginx, AWS RDS |

------------------------------------

## Testing

```bash
# Backend tests
pytest

# Web dashboard tests
cd web-dashboard && npm test

# Flutter tests
cd mobile-app && flutter test
```

------------------------------------

## Deployment

### SSH to EC2
ssh -i "adaptiv-key.pem" ec2-user@--public ip--

### RDS login

psql "host=adaptivhealth-db.c34gaqco4qk4.ap-south-1.rds.amazonaws.com \
      port=5432 dbname=postgres user=postgres password=password"

### Backend
```bash
pip install -r requirements.txt
python start_server.py
```

### Web Dashboard
```bash
cd web-dashboard
npm run build
```

Serve the generated `build/` directory with your preferred static hosting.

### Mobile App
```bash
cd mobile-app
flutter build apk --release           # Android
flutter build appbundle --release     # Google Play
flutter build ios --release           # iOS
```

-----------------------------------

## Environment Variables

See [.env.example](.env.example) for all required and optional variables including:
- `DATABASE_URL` — PostgreSQL connection string
- `SECRET_KEY` — JWT signing secret
- `GEMINI_API_KEY` — Google Gemini for AI features
- `SMTP_*` — Email configuration for password resets
- `PHI_ENCRYPTION_KEY` — Optional field-level encryption

-----------------------------------
-----------------------------------


