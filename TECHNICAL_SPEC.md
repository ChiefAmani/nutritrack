# TECHNICAL_SPEC.md

## Project Overview
This project aims to develop the core MVP backend features for NutriTrack, an AI nutrition coaching SaaS. The backend will support AI meal planning, calorie/macro tracking, grocery list generation, weekly nutrition reports, and email coaching nudges. This is critical for acquiring initial paying users and validating core features to achieve 500 paying users in 90 days.

## Tech Stack
- Python==3.10.12
- FastAPI==0.110.0
- Pydantic==2.6.1
- SQLAlchemy==2.0.28
- Psycopg2-binary==2.9.9 (for PostgreSQL connectivity)
- Uvicorn==0.29.0 (ASGI server)
- python-dotenv==1.0.1 (for environment variables)
- scikit-learn==1.4.1.post1 (for AI/ML components)
- pandas==2.2.1 (for data handling in AI/ML)
- numpy==1.26.4 (for numerical operations in AI/ML)

## File Tree
```
.
|-- main.py
|-- requirements.txt
|-- .env.example
|-- database/
|   |-- __init__.py
|   |-- connection.py
|   `-- models.py
|-- crud/
|   |-- __init__.py
|   |-- users.py
|   |-- meals.py
|   `-- tracking.py
|-- schemas/
|   |-- __init__.py
|   |-- user.py
|   |-- meal.py
|   `-- tracking.py
|-- services/
|   |-- __init__.py
|   |-- ai_meal_planner.py
|   |-- report_generator.py
|   `-- email_nudges.py
`-- tests/
    |-- test_main.py
    |-- test_users.py
    `-- test_meals.py
```

## API Endpoints

### User Management
- Method: POST
- Path: /api/users/register
- Request body: { "email": "string", "password": "string", "name": "string", "age": "integer", "weight_kg": "float", "height_cm": "float", "goal": "string" }
- Response: { "id": "integer", "email": "string", "name": "string" }
- Auth: None

- Method: POST
- Path: /api/users/login
- Request body: { "email": "string", "password": "string" }
- Response: { "access_token": "string", "token_type": "bearer" }
- Auth: None

- Method: GET
- Path: /api/users/me
- Request body: None
- Response: { "id": "integer", "email": "string", "name": "string", "age": "integer", "weight_kg": "float", "height_cm": "float", "goal": "string" }
- Auth: Bearer token required

### Meal Planning
- Method: POST
- Path: /api/meals/plan
- Request body: { "user_id": "integer", "dietary_preferences": "list[string]", "calorie_target": "integer", "meal_count": "integer" }
- Response: { "plan_id": "integer", "meals": "list[object]" } (each object contains meal details)
- Auth: Bearer token required

- Method: GET
- Path: /api/meals/plan/{plan_id}
- Request body: None
- Response: { "plan_id": "integer", "meals": "list[object]" }
- Auth: Bearer token required

### Calorie/Macro Tracking
- Method: POST
- Path: /api/tracking/log
- Request body: { "user_id": "integer", "meal_id": "integer", "food_item": "string", "calories": "integer", "protein_g": "float", "fat_g": "float", "carbs_g": "float", "log_date": "string (YYYY-MM-DD)" }
- Response: { "log_id": "integer", "message": "Tracking entry created" }
- Auth: Bearer token required

- Method: GET
- Path: /api/tracking/user/{user_id}/daily/{date}
- Request body: None
- Response: { "date": "string (YYYY-MM-DD)", "total_calories": "integer", "total_protein_g": "float", "total_fat_g": "float", "total_carbs_g": "float", "entries": "list[object]" }
- Auth: Bearer token required

### Grocery List Generation
- Method: GET
- Path: /api/grocery-list/user/{user_id}/plan/{plan_id}
- Request body: None
- Response: { "list_id": "integer", "items": "list[string]" }
- Auth: Bearer token required

### Weekly Nutrition Reports
- Method: GET
- Path: /api/reports/user/{user_id}/weekly/{start_date}
- Request body: None
- Response: { "report_id": "integer", "summary": "string", "average_calories": "float", "average_macros": "object" }
- Auth: Bearer token required

### Email Coaching Nudges
- Method: POST
- Path: /api/nudges/send
- Request body: { "user_id": "integer", "message": "string", "scheduled_date": "string (YYYY-MM-DD)" }
- Response: { "nudge_id": "integer", "status": "string" }
- Auth: Bearer token required

## Environment Variables
- DATABASE_URL="postgresql://user:password@host:port/dbname"
- SECRET_KEY="your_super_secret_key"
- ALGORITHM="HS256"
- ACCESS_TOKEN_EXPIRE_MINUTES="30"
- EMAIL_HOST="smtp.example.com"
- EMAIL_PORT="587"
- EMAIL_USERNAME="your_email@example.com"
- EMAIL_PASSWORD="your_email_password"

## Dependencies
```
fastapi==0.110.0
pydantic==2.6.1
SQLAlchemy==2.0.28
psycopg2-binary==2.9.9
uvicorn==0.29.0
python-dotenv==1.0.1
scikit-learn==1.4.1.post1
pandas==2.2.1
numpy==1.26.4
passlib[bcrypt]==1.7.4
python-jose[cryptography]==3.3.0
```