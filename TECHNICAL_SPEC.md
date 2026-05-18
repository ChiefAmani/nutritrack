# TECHNICAL_SPEC.md

## Project Overview
This project is the backend MVP for NutriTrack, an AI nutrition coaching SaaS. It will provide core functionalities including user management, AI meal planning, and basic food tracking, tailored for busy professionals seeking personalized nutrition guidance.

## Tech Stack
- Python==3.10.12
- FastAPI==0.110.0
- Uvicorn==0.29.0
- SQLAlchemy==2.0.29
- Pydantic==2.7.1
- Psycopg2-binary==2.9.9
- python-jose[cryptography]==3.3.0
- passlib[bcrypt]==1.7.4

## File Tree
.env
main.py
requirements.txt
app/
|-- __init__.py
|-- database.py
|-- models.py
|-- schemas.py
|-- crud.py
|-- auth.py
|-- routers/
    |-- __init__.py
    |-- users.py
    |-- meal_plans.py

## API Endpoints

### User Authentication
- Method: POST
- Path: /api/v1/auth/register
- Request body: { "email": "string", "password": "string" }
- Response: { "message": "string" }
- Auth: None

- Method: POST
- Path: /api/v1/auth/login
- Request body: { "email": "string", "password": "string" }
- Response: { "access_token": "string", "token_type": "bearer" }
- Auth: None

### User Management
- Method: GET
- Path: /api/v1/users/me
- Request body: None
- Response: { "id": "integer", "email": "string" }
- Auth: Bearer token required

### Meal Planning
- Method: POST
- Path: /api/v1/meal_plans/
- Request body: { "user_id": "integer", "dietary_preferences": "string", "calorie_target": "integer", "meal_count": "integer" }
- Response: { "id": "integer", "user_id": "integer", "plan_details": "string", "created_at": "datetime" }
- Auth: Bearer token required

- Method: GET
- Path: /api/v1/meal_plans/{meal_plan_id}
- Request body: None
- Response: { "id": "integer", "user_id": "integer", "plan_details": "string", "created_at": "datetime" }
- Auth: Bearer token required

## Environment Variables
- DATABASE_URL=postgresql://user:password@host:port/dbname
- SECRET_KEY=your_super_secret_key_for_jwt
- ALGORITHM=HS256
- ACCESS_TOKEN_EXPIRE_MINUTES=30

## Dependencies
fastapi==0.110.0
uvicorn==0.29.0
sqlalchemy==2.0.29
pydantic==2.7.1
psycopg2-binary==2.9.9
python-jose[cryptography]==3.3.0
passlib[bcrypt]==1.7.4
