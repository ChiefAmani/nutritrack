# TECHNICAL_SPEC.md

## Project Overview
This project defines the core backend API for NutriTrack, an AI nutrition coaching SaaS. It will provide endpoints for AI meal planning, calorie/macro tracking, grocery list generation, weekly nutrition reports, and email coaching nudges, enabling initial user testing and validation of MVP features.

## Tech Stack
- fastapi==0.110.0
- pydantic==2.6.1
- sqlalchemy==2.0.29
- psycopg2-binary==2.9.9
- python-dotenv==1.0.1
- uvicorn==0.29.0

## File Tree
```
backend/
  app/
    __init__.py
    main.py
    database.py
    models.py
    schemas.py
    crud.py
    routers/
      __init__.py
      meal_plans.py
      tracking.py
      grocery_lists.py
      reports.py
      nudges.py
  .env.example
  requirements.txt
```

## API Endpoints

### User Authentication (Placeholder - to be expanded)
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

### Meal Plans
- Method: POST
- Path: /api/v1/meal_plans/generate
- Request body: { "user_id": "int", "dietary_preferences": "list[str]", "calorie_target": "int", "macro_split": "dict" }
- Response: { "plan_id": "int", "meals": "list[dict]" }
- Auth: Bearer token required

- Method: GET
- Path: /api/v1/meal_plans/{plan_id}
- Response: { "plan_id": "int", "meals": "list[dict]" }
- Auth: Bearer token required

### Calorie/Macro Tracking
- Method: POST
- Path: /api/v1/tracking/log_food
- Request body: { "user_id": "int", "food_item": "string", "calories": "int", "protein": "float", "carbs": "float", "fat": "float", "meal_type": "string", "date": "date" }
- Response: { "log_id": "int", "message": "Food logged successfully" }
- Auth: Bearer token required

- Method: GET
- Path: /api/v1/tracking/summary/{user_id}
- Request query: { "date": "date" }
- Response: { "total_calories": "int", "total_protein": "float", "total_carbs": "float", "total_fat": "float", "logged_items": "list[dict]" }
- Auth: Bearer token required

### Grocery List Generation
- Method: POST
- Path: /api/v1/grocery_lists/generate
- Request body: { "user_id": "int", "meal_plan_id": "int" }
- Response: { "list_id": "int", "items": "list[dict]" }
- Auth: Bearer token required

- Method: GET
- Path: /api/v1/grocery_lists/{list_id}
- Response: { "list_id": "int", "items": "list[dict]" }
- Auth: Bearer token required

### Weekly Nutrition Reports
- Method: GET
- Path: /api/v1/reports/weekly/{user_id}
- Request query: { "start_date": "date", "end_date": "date" }
- Response: { "report_id": "int", "summary": "dict", "trends": "dict" }
- Auth: Bearer token required

### Email Coaching Nudges
- Method: POST
- Path: /api/v1/nudges/schedule
- Request body: { "user_id": "int", "message_template_id": "int", "scheduled_time": "datetime" }
- Response: { "nudge_id": "int", "message": "Nudge scheduled" }
- Auth: Bearer token required

## Environment Variables
- DATABASE_URL="postgresql://user:password@db:5432/nutritrack"
- SECRET_KEY="your-super-secret-key"
- ALGORITHM="HS256"
- ACCESS_TOKEN_EXPIRE_MINUTES=30

## Dependencies
```
fastapi==0.110.0
pydantic==2.6.1
sqlalchemy==2.0.29
psycopg2-binary==2.9.9
python-dotenv==1.0.1
uvicorn==0.29.0
```