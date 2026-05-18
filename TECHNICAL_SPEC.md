# TECHNICAL_SPEC.md

## Project Overview
This document outlines the Minimum Viable Product (MVP) for NutriTrack, an AI nutrition coaching SaaS. The MVP focuses on core functionalities: AI-driven meal planning, calorie/macro tracking, and grocery list generation. It aims to validate the core value proposition for busy professionals by providing personalized, efficient nutrition guidance.

## Tech Stack
- python==3.10.12
- fastapi==0.110.0
- uvicorn==0.27.1
- pydantic==2.6.1
- sqlalchemy==2.0.25
- psycopg2-binary==2.9.9
- python-dotenv==1.0.1
- openai==1.12.0 (for AI meal planning integration)

## File Tree
```
.
|-- main.py
|-- requirements.txt
|-- .env.example
|-- app/
|   |-- __init__.py
|   |-- api/
|   |   |-- __init__.py
|   |   |-- endpoints/
|   |   |   |-- __init__.py
|   |   |   |-- auth.py
|   |   |   |-- users.py
|   |   |   |-- meal_plans.py
|   |   |   `-- tracking.py
|   |-- core/
|   |   |-- __init__.py
|   |   |-- config.py
|   |   `-- security.py
|   |-- crud/
|   |   |-- __init__.py
|   |   |-- user.py
|   |   |-- meal_plan.py
|   |   `-- food_log.py
|   |-- db/
|   |   |-- __init__.py
|   |   |-- base.py
|   |   `-- session.py
|   |-- models/
|   |   |-- __init__.py
|   |   |-- user.py
|   |   |-- meal_plan.py
|   |   `-- food_log.py
|   `-- schemas/
|       |-- __init__.py
|       |-- user.py
|       |-- meal_plan.py
|       `-- food_log.py
```

## API Endpoints

### User Authentication
- Method: POST
- Path: /api/v1/auth/register
- Request body: { "email": "string", "password": "string" }
- Response: { "message": "User registered successfully" }
- Auth: None

- Method: POST
- Path: /api/v1/auth/login
- Request body: { "email": "string", "password": "string" }
- Response: { "access_token": "string", "token_type": "bearer" }
- Auth: None

### User Profile
- Method: GET
- Path: /api/v1/users/me
- Request body: None
- Response: { "id": "int", "email": "string", "dietary_preferences": "string", "goals": "string" }
- Auth: Bearer token required

- Method: PUT
- Path: /api/v1/users/me
- Request body: { "dietary_preferences": "string", "goals": "string" }
- Response: { "id": "int", "email": "string", "dietary_preferences": "string", "goals": "string" }
- Auth: Bearer token required

### AI Meal Planning
- Method: POST
- Path: /api/v1/meal_plans/generate
- Request body: { "preferences": "string", "goals": "string", "num_days": "int" }
- Response: { "meal_plan_id": "int", "plan_details": "string" } (plan_details will be a JSON string or similar structure)
- Auth: Bearer token required

- Method: GET
- Path: /api/v1/meal_plans/{meal_plan_id}
- Request body: None
- Response: { "meal_plan_id": "int", "user_id": "int", "plan_details": "string", "generated_date": "datetime" }
- Auth: Bearer token required

- Method: GET
- Path: /api/v1/meal_plans/grocery_list/{meal_plan_id}
- Request body: None
- Response: { "grocery_list": ["string"] }
- Auth: Bearer token required

### Calorie/Macro Tracking
- Method: POST
- Path: /api/v1/tracking/log_food
- Request body: { "food_item": "string", "quantity": "float", "unit": "string", "calories": "int", "protein": "float", "carbs": "float", "fat": "float", "log_date": "date" }
- Response: { "log_id": "int", "message": "Food logged successfully" }
- Auth: Bearer token required

- Method: GET
- Path: /api/v1/tracking/summary
- Request body: { "start_date": "date", "end_date": "date" }
- Response: { "total_calories": "int", "total_protein": "float", "total_carbs": "float", "total_fat": "float", "daily_summaries": [{ "date": "date", "calories": "int", "protein": "float", "carbs": "float", "fat": "float" }] }
- Auth: Bearer token required

## Environment Variables
- DATABASE_URL="postgresql+psycopg2://user:password@host:port/database_name"
- SECRET_KEY="your_super_secret_key"
- ALGORITHM="HS256"
- ACCESS_TOKEN_EXPIRE_MINUTES="30"
- OPENAI_API_KEY="your_openai_api_key"

## Dependencies
```
fastapi==0.110.0
uvicorn==0.27.1
pydantic==2.6.1
sqlalchemy==2.0.25
psycopg2-binary==2.9.9
python-dotenv==1.0.1
passlib[bcrypt]==1.7.4
python-jose[cryptography]==3.3.0
openai==1.12.0
```