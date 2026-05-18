# TECHNICAL_SPEC.md

## Project Overview
Implement core growth mechanics and user tracking for NutriTrack's AI nutrition coaching SaaS. This project focuses on setting up event tracking for user onboarding and feature engagement, and a basic referral system to drive initial user acquisition and validate core MVP features.

## Tech Stack
- Python==3.10.12
- fastapi==0.110.0
- pydantic==2.6.1
- uvicorn==0.27.1
- sqlalchemy==2.0.25
- psycopg2-binary==2.9.9
- python-dotenv==1.0.1

## File Tree
```
.
- main.py
- requirements.txt
- .env.example
- app/
  - __init__.py
  - core/
    - __init__.py
    - config.py
  - db/
    - __init__.py
    - database.py
    - models.py
  - api/
    - __init__.py
    - endpoints/
      - __init__.py
      - tracking.py
      - referral.py
    - schemas.py
  - services/
    - __init__.py
    - tracking_service.py
    - referral_service.py
```

## API Endpoints

### 1. Track User Event
- Method: POST
- Path: /api/v1/track/event
- Request body:
  ```json
  {
    "user_id": "string",
    "event_name": "string",
    "event_data": "object"
  }
  ```
- Response:
  ```json
  {
    "message": "Event tracked successfully"
  }
  ```
- Auth: Bearer token required (for authenticated users) or API key (for public events like sign-up initiation).

### 2. Generate Referral Link
- Method: POST
- Path: /api/v1/referral/generate
- Request body:
  ```json
  {
    "referrer_user_id": "string"
  }
  ```
- Response:
  ```json
  {
    "referral_code": "string",
    "referral_link": "string"
  }
  ```
- Auth: Bearer token required.

### 3. Get Referral Status
- Method: GET
- Path: /api/v1/referral/status/{referral_code}
- Request parameters:
  - `referral_code`: string (path parameter)
- Response:
  ```json
  {
    "referral_code": "string",
    "referrer_user_id": "string",
    "referred_users_count": "integer",
    "status": "string"
  }
  ```
- Auth: No auth required for public check, but internal calls might use auth.

## Environment Variables
- `DATABASE_URL`: PostgreSQL connection string (e.g., `postgresql+psycopg2://user:password@host:port/dbname`)
- `SECRET_KEY`: Used for token encoding/decoding (e.g., JWT secret)
- `ANALYTICS_API_KEY`: Optional, if integrating with an external analytics service.

## Dependencies
```
fastapi==0.110.0
pydantic==2.6.1
uvicorn==0.27.1
sqlalchemy==2.0.25
psycopg2-binary==2.9.9
python-dotenv==1.0.1
```