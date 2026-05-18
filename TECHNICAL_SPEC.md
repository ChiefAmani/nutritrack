# TECHNICAL_SPEC.md

## Project Overview
The AI Nutrition Engine is the core backend service for NutriTrack, providing personalized nutrition coaching features for busy professionals. It will leverage AI to generate meal plans, track user intake, create grocery lists, compile weekly nutrition reports, and facilitate email coaching nudges. The engine aims to automate and personalize nutrition guidance, reducing manual effort and promoting sustainable healthy habits.

## Tech Stack
- Python==3.11.9
- FastAPI==0.110.0
- Pydantic==2.6.1
- SQLAlchemy==2.0.29
- psycopg2-binary==2.9.9
- Uvicorn==0.29.0
- python-jose==3.3.0
- passlib==1.7.4
- python-multipart==0.0.9
- python-dotenv==1.0.1

## File Tree
```
.
|-- main.py
|-- app/
|   |-- __init__.py
|   |-- core/
|   |   |-- config.py
|   |   |-- security.py
|   |   `-- database.py
|   |-- crud/
|   |   |-- __init__.py
|   |   |-- user.py
|   |   |-- meal_plan.py
|   |   `-- food_log.py
|   |-- models/
|   |   |-- __init__.py
|   |   |-- user.py
|   |   |-- meal_plan.py
|   |   `-- food_log.py
|   |-- schemas/
|   |   |-- __init__.py
|   |   |-- user.py
|   |   |-- meal_plan.py
|   |   `-- food_log.py
|   |-- api/
|   |   |-- __init__.py
|   |   |-- v1/
|   |   |   |-- __init__.py
|   |   |   |-- endpoints/
|   |   |   |   |-- users.py
|   |   |   |   |-- auth.py
|   |   |   |   |-- meal_plans.py
|   |   |   |   |-- food_logs.py
|   |   |   |   `-- grocery_lists.py
|   |   |   `-- api.py
|   `-- services/
|       |-- __init__.py
|       |-- ai_nutrition.py
|       `-- report_generator.py
|-- tests/
|   |-- __init__.py
|   |-- api/
|   |   `-- v1/
|   |       |-- test_users.py
|   |       `-- test_auth.py
|   `-- conftest.py
|-- alembic/
|   |-- env.py
|   |-- script.py.mako
|   `-- versions/
|-- alembic.ini
|-- Dockerfile
|-- requirements.txt
`-- .env.example
```

## API Endpoints

### Authentication
- Method: POST
- Path: /api/v1/auth/register
- Request body: { "email": "string", "password": "string", "name": "string" }
- Response: { "access_token": "string", "token_type": "bearer" }
- Auth: None

- Method: POST
- Path: /api/v1/auth/login
- Request body: { "username": "string", "password": "string" } (form data)
- Response: { "access_token": "string", "token_type": "bearer" }
- Auth: None

### User Management
- Method: GET
- Path: /api/v1/users/me
- Request body: None
- Response: { "id": "integer", "email": "string", "name": "string", "dietary_preferences": "array", "goals": "array" }
- Auth: Bearer token required

- Method: PUT
- Path: /api/v1/users/me
- Request body: { "name": "string", "dietary_preferences": "array", "goals": "array" }
- Response: { "id": "integer", "email": "string", "name": "string", "dietary_preferences": "array", "goals": "array" }
- Auth: Bearer token required

### Meal Planning
- Method: POST
- Path: /api/v1/meal_plans/generate
- Request body: { "target_calories": "integer", "dietary_restrictions": "array", "preferences": "array" }
- Response: { "id": "integer", "user_id": "integer", "date": "string", "meals": "array" }
- Auth: Bearer token required

- Method: GET
- Path: /api/v1/meal_plans/current
- Request body: None
- Response: { "id": "integer", "user_id": "integer", "date": "string", "meals": "array" }
- Auth: Bearer token required

### Food Logging
- Method: POST
- Path: /api/v1/food_logs
- Request body: { "meal_type": "string", "food_item": "string", "calories": "integer", "protein": "float", "carbs": "float", "fat": "float", "quantity": "float", "unit": "string" }
- Response: { "id": "integer", "user_id": "integer", "timestamp": "string", "meal_type": "string", "food_item": "string", "calories": "integer", "protein": "float", "carbs": "float", "fat": "float", "quantity": "float", "unit": "string" }
- Auth: Bearer token required

- Method: GET
- Path: /api/v1/food_logs/today
- Request body: None
- Response: [ { "id": "integer", "user_id": "integer", "timestamp": "string", "meal_type": "string", "food_item": "string", "calories": "integer", "protein": "float", "carbs": "float", "fat": "float", "quantity": "float", "unit": "string" } ]
- Auth: Bearer token required

- Method: GET
- Path: /api/v1/food_logs/summary
- Request body: { "period": "string" } (e.g., "daily", "weekly")
- Response: { "total_calories": "integer", "total_protein": "float", "total_carbs": "float", "total_fat": "float", "logs": "array" }
- Auth: Bearer token required

### Grocery Lists
- Method: GET
- Path: /api/v1/grocery_lists/generate
- Request body: None
- Response: { "id": "integer", "user_id": "integer", "date": "string", "items": "array" }
- Auth: Bearer token required

### Nutrition Reports
- Method: GET
- Path: /api/v1/nutrition_reports/weekly
- Request body: None
- Response: { "id": "integer", "user_id": "integer", "start_date": "string", "end_date": "string", "summary": "string", "insights": "array" }
- Auth: Bearer token required

## Environment Variables
- `DATABASE_URL`: PostgreSQL connection string (e.g., `postgresql://user:password@host:port/dbname`)
- `SECRET_KEY`: Used for JWT token signing
- `ALGORITHM`: JWT algorithm (e.g., `HS256`)
- `ACCESS_TOKEN_EXPIRE_MINUTES`: JWT token expiration time in minutes

## Dependencies
```
fastapi==0.110.0
pydantic==2.6.1
SQLAlchemy==2.0.29
psycopg2-binary==2.9.9
uvicorn==0.29.0
python-jose==3.3.0
passlib==1.7.4
python-multipart==0.0.9
python-dotenv==1.0.1
alembic==1.13.1
```