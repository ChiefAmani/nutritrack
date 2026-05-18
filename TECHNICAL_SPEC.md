# TECHNICAL_SPEC.md

## Project Overview
This document specifies the core backend MVP for NutriTrack, an AI nutrition coaching SaaS. It will provide API endpoints for user authentication, meal plan creation, retrieval, updates, and deletion, supporting the initial user testing and launch.

## Tech Stack
- fastapi==0.110.0
- uvicorn==0.29.0
- sqlalchemy==2.0.29
- pydantic==2.7.1
- python-jose[cryptography]==3.3.0
- passlib[bcrypt]==1.7.4
- python-multipart==0.0.9
- psycopg2-binary==2.9.9 (for PostgreSQL, if used; otherwise, sqlite3 is default for SQLAlchemy)

## File Tree
.
- main.py
- database.py
- models.py
- schemas.py
- crud.py
- auth.py
- dependencies.py
- .env

## API Endpoints

### User Management
- Method: POST
  Path: /api/v1/users/register
  Request body: { "email": "string", "password": "string" }
  Response: { "id": "integer", "email": "string" }
  Auth: None

- Method: POST
  Path: /api/v1/users/login
  Request body: { "username": "string", "password": "string" }
  Response: { "access_token": "string", "token_type": "bearer" }
  Auth: None

- Method: GET
  Path: /api/v1/users/me
  Request body: None
  Response: { "id": "integer", "email": "string" }
  Auth: Bearer token required

### Meal Plan Management
- Method: POST
  Path: /api/v1/meal_plans/
  Request body: { "dietary_preferences": "string", "calorie_target": "integer", "meal_count": "integer" }
  Response: { "id": "integer", "dietary_preferences": "string", "calorie_target": "integer", "meal_count": "integer", "user_id": "integer" }
  Auth: Bearer token required

- Method: GET
  Path: /api/v1/meal_plans/{meal_plan_id}
  Request body: None
  Response: { "id": "integer", "dietary_preferences": "string", "calorie_target": "integer", "meal_count": "integer", "user_id": "integer" }
  Auth: Bearer token required

- Method: GET
  Path: /api/v1/meal_plans/
  Request body: None
  Response: [ { "id": "integer", "dietary_preferences": "string", "calorie_target": "integer", "meal_count": "integer", "user_id": "integer" } ]
  Auth: Bearer token required

- Method: PUT
  Path: /api/v1/meal_plans/{meal_plan_id}
  Request body: { "dietary_preferences": "string", "calorie_target": "integer", "meal_count": "integer" } (all fields optional for update)
  Response: { "id": "integer", "dietary_preferences": "string", "calorie_target": "integer", "meal_count": "integer", "user_id": "integer" }
  Auth: Bearer token required

- Method: DELETE
  Path: /api/v1/meal_plans/{meal_plan_id}
  Request body: None
  Response: { "message": "Meal plan deleted successfully" }
  Auth: Bearer token required

## Environment Variables
- DATABASE_URL="sqlite:///./sql_app.db" (or PostgreSQL connection string)
- SECRET_KEY="your-super-secret-key"
- ALGORITHM="HS256"
- ACCESS_TOKEN_EXPIRE_MINUTES="30"

## Dependencies
fastapi==0.110.0
uvicorn==0.29.0
sqlalchemy==2.0.29
pydantic==2.7.1
python-jose[cryptography]==3.3.0
passlib[bcrypt]==1.7.4
python-multipart==0.0.9
psycopg2-binary==2.9.9