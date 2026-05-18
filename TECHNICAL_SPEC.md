# TECHNICAL_SPEC.md

## Project Overview
This project focuses on developing the core MVP backend features for NutriTrack, an AI nutrition coaching SaaS. The features include AI meal planning, calorie/macro tracking, grocery list generation, weekly nutrition reports, and email coaching nudges. The goal is to provide a robust and scalable foundation for initial user testing and launch, directly supporting the target of 500 paying users in 90 days.

## Tech Stack
- Python==3.10.12
- FastAPI==0.110.0
- Pydantic==2.6.1
- SQLAlchemy==2.0.27
- psycopg2-binary==2.9.9 (for PostgreSQL database)
- python-dotenv==1.0.1
- uvicorn==0.27.1

## File Tree
```
.
|-- main.py
|-- requirements.txt
|-- .env.example
|-- app/
|   |-- __init__.py
|   |-- core/
|   |   |-- __init__.py
|   |   |-- config.py
|   |   `-- database.py
|   |-- api/
|   |   |-- __init__.py
|   |   |-- endpoints/
|   |   |   |-- __init__.py
|   |   |   |-- meal_plans.py
|   |   |   |-- tracking.py
|   |   |   |-- grocery_lists.py
|   |   |   |-- reports.py
|   |   |   `-- nudges.py
|   |-- crud/
|   |   |-- __init__.py
|   |   |-- meal_plan_crud.py
|   |   |-- tracking_crud.py
|   |   |-- grocery_list_crud.py
|   |   |-- report_crud.py
|   |   `-- nudge_crud.py
|   |-- schemas/
|   |   |-- __init__.py
|   |   |-- meal_plan_schema.py
|   |   |-- tracking_schema.py
|   |   |-- grocery_list_schema.py
|   |   |-- report_schema.py
|   |   `-- nudge_schema.py
|   `-- models/
|       |-- __init__.py
|       |-- user_model.py
|       |-- meal_plan_model.py
|       |-- food_item_model.py
|       |-- tracked_item_model.py
|       |-- grocery_list_model.py
|       |-- report_model.py
|       `-- nudge_model.py
```

## API Endpoints

### Meal Planning
- Method: POST
- Path: /api/meal_plans/generate
- Request body: { "user_id": "str", "dietary_preferences": "list[str]", "calorie_target": "int", "macro_split": "dict" }
- Response: { "meal_plan_id": "str", "meals": "list[dict]" }
- Auth: Bearer token required

- Method: GET
- Path: /api/meal_plans/{meal_plan_id}
- Request body: None
- Response: { "meal_plan_id": "str", "meals": "list[dict]", "created_at": "datetime" }
- Auth: Bearer token required

### Calorie/Macro Tracking
- Method: POST
- Path: /api/tracking/log
- Request body: { "user_id": "str", "food_item": "str", "quantity": "float", "unit": "str", "meal_type": "str", "logged_at": "datetime" }
- Response: { "tracking_id": "str", "message": "str" }
- Auth: Bearer token required

- Method: GET
- Path: /api/tracking/{user_id}/daily_summary
- Request body: { "date": "date" }
- Response: { "user_id": "str", "date": "date", "total_calories": "int", "total_macros": "dict", "tracked_items": "list[dict]" }
- Auth: Bearer token required

### Grocery List Generation
- Method: POST
- Path: /api/grocery_lists/generate
- Request body: { "user_id": "str", "meal_plan_id": "str" }
- Response: { "grocery_list_id": "str", "items": "list[dict]" }
- Auth: Bearer token required

- Method: GET
- Path: /api/grocery_lists/{grocery_list_id}
- Request body: None
- Response: { "grocery_list_id": "str", "items": "list[dict]", "generated_at": "datetime" }
- Auth: Bearer token required

### Weekly Nutrition Reports
- Method: GET
- Path: /api/reports/{user_id}/weekly
- Request body: { "start_date": "date", "end_date": "date" }
- Response: { "report_id": "str", "user_id": "str", "period": "str", "summary": "dict", "insights": "list[str]" }
- Auth: Bearer token required

### Email Coaching Nudges
- Method: POST
- Path: /api/nudges/send
- Request body: { "user_id": "str", "nudge_type": "str", "content": "str" }
- Response: { "nudge_id": "str", "message": "str" }
- Auth: Bearer token required

## Environment Variables
- DATABASE_URL="postgresql+psycopg2://user:password@host:port/database"
- SECRET_KEY="your_super_secret_key"
- EMAIL_HOST="smtp.example.com"
- EMAIL_PORT="587"
- EMAIL_USERNAME="your_email@example.com"
- EMAIL_PASSWORD="your_email_password"

## Dependencies
```
fastapi==0.110.0
pydantic==2.6.1
sqlalchemy==2.0.27
psycopg2-binary==2.9.9
python-dotenv==1.0.1
uvicorn==0.27.1
```