# TECHNICAL_SPEC.md

## Project Overview
NutriTrack AI nutrition coaching SaaS backend for busy professionals. It will provide AI-driven meal planning, calorie/macro tracking, grocery list generation, weekly nutrition reports, and email coaching nudges to help users maintain healthy habits and achieve their fitness goals.

## Tech Stack
- fastapi==0.110.0
- pydantic==2.6.1
- sqlalchemy==2.0.29
- psycopg2-binary==2.9.9
- python-dotenv==1.0.1
- uvicorn==0.29.0
- celery==5.3.6
- redis==5.0.1
- passlib[bcrypt]==1.7.4
- python-jose[cryptography]==3.3.0
- email-validator==2.1.1

## File Tree
.
|-- backend/
|   |-- app/
|   |   |-- __init__.py
|   |   |-- main.py
|   |   |-- api/
|   |   |   |-- __init__.py
|   |   |   |-- v1/
|   |   |   |   |-- __init__.py
|   |   |   |   |-- endpoints/
|   |   |   |   |   |-- __init__.py
|   |   |   |   |   |-- users.py
|   |   |   |   |   |-- meals.py
|   |   |   |   |   |-- tracking.py
|   |   |   |   |   |-- groceries.py
|   |   |   |   |   |-- reports.py
|   |   |   |   |   |-- auth.py
|   |   |   |-- schemas/
|   |   |   |   |-- __init__.py
|   |   |   |   |-- user.py
|   |   |   |   |-- meal.py
|   |   |   |   |-- tracking.py
|   |   |   |   |-- grocery.py
|   |   |   |   |-- report.py
|   |   |   |   |-- auth.py
|   |   |-- core/
|   |   |   |-- __init__.py
|   |   |   |-- config.py
|   |   |   |-- database.py
|   |   |   |-- security.py
|   |   |   |-- tasks.py
|   |   |-- crud/
|   |   |   |-- __init__.py
|   |   |   |-- user.py
|   |   |   |-- meal.py
|   |   |   |-- tracking.py
|   |   |   |-- grocery.py
|   |   |   |-- report.py
|   |   |-- models/
|   |   |   |-- __init__.py
|   |   |   |-- user.py
|   |   |   |-- meal.py
|   |   |   |-- tracking.py
|   |   |   |-- grocery.py
|   |   |   |-- report.py
|   |-- tests/
|   |   |-- __init__.py
|   |   |-- test_users.py
|   |   |-- test_meals.py
|   |   |-- test_tracking.py
|   |   |-- test_groceries.py
|   |   |-- test_reports.py
|   |   |-- test_auth.py
|   |-- Dockerfile
|   |-- requirements.txt
|   |-- .env.example
|   |-- README.md

## API Endpoints

### Auth
- Method: POST
  Path: /api/v1/auth/register
  Request body: { email: str, password: str, name: str }
  Response: { access_token: str, token_type: str }
  Auth: None
- Method: POST
  Path: /api/v1/auth/login
  Request body: { email: str, password: str }
  Response: { access_token: str, token_type: str }
  Auth: None
- Method: GET
  Path: /api/v1/auth/me
  Request body: None
  Response: { id: int, email: str, name: str }
  Auth: Bearer token required

### Users
- Method: GET
  Path: /api/v1/users/me
  Request body: None
  Response: { id: int, email: str, name: str, preferences: dict }
  Auth: Bearer token required
- Method: PUT
  Path: /api/v1/users/me
  Request body: { name: str | None, preferences: dict | None }
  Response: { id: int, email: str, name: str, preferences: dict }
  Auth: Bearer token required

### Meal Planning
- Method: POST
  Path: /api/v1/meals/plan
  Request body: { dietary_preferences: dict, calorie_target: int, macro_split: dict }
  Response: { meal_plan: list[dict] }
  Auth: Bearer token required
- Method: GET
  Path: /api/v1/meals/plan/current
  Request body: None
  Response: { meal_plan: list[dict] }
  Auth: Bearer token required
- Method: GET
  Path: /api/v1/meals/{meal_id}
  Request body: None
  Response: { id: int, name: str, ingredients: list[str], nutritional_info: dict }
  Auth: Bearer token required

### Calorie/Macro Tracking
- Method: POST
  Path: /api/v1/tracking/log
  Request body: { meal_id: int | None, custom_food_name: str | None, calories: int, protein: float, carbs: float, fat: float, date: str }
  Response: { id: int, user_id: int, meal_id: int | None, custom_food_name: str | None, calories: int, protein: float, carbs: float, fat: float, date: str }
  Auth: Bearer token required
- Method: GET
  Path: /api/v1/tracking/summary
  Request body: { start_date: str, end_date: str }
  Response: { daily_summaries: list[dict] }
  Auth: Bearer token required

### Grocery List Generation
- Method: POST
  Path: /api/v1/groceries/generate
  Request body: { meal_plan_id: int | None, start_date: str, end_date: str }
  Response: { grocery_list: list[str] }
  Auth: Bearer token required
- Method: GET
  Path: /api/v1/groceries/current
  Request body: None
  Response: { grocery_list: list[str] }
  Auth: Bearer token required

### Weekly Nutrition Reports
- Method: GET
  Path: /api/v1/reports/weekly
  Request body: { start_date: str, end_date: str }
  Response: { report_data: dict }
  Auth: Bearer token required
- Method: POST
  Path: /api/v1/reports/schedule_email
  Request body: { frequency: str, recipient_email: str }
  Response: { message: str }
  Auth: Bearer token required

## Environment Variables
- DATABASE_URL
- SECRET_KEY
- ALGORITHM
- ACCESS_TOKEN_EXPIRE_MINUTES
- CELERY_BROKER_URL
- CELERY_RESULT_BACKEND
- SMTP_SERVER
- SMTP_PORT
- SMTP_USERNAME
- SMTP_PASSWORD
- SENDER_EMAIL

## Dependencies
fastapi==0.110.0
pydantic==2.6.1
sqlalchemy==2.0.29
psycopg2-binary==2.9.9
python-dotenv==1.0.1
uvicorn==0.29.0
celery==5.3.6
redis==5.0.1
passlib[bcrypt]==1.7.4
python-jose[cryptography]==3.3.0
email-validator==2.1.1
