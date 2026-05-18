# TECHNICAL_SPEC.md

## Project Overview
This project aims to develop the core MVP backend features for NutriTrack, an AI nutrition coaching SaaS. The initial focus is on user authentication, AI meal planning, and basic calorie/macro tracking to enable initial user testing and achieve early paying users.

## Tech Stack
- fastapi==0.110.0
- uvicorn==0.29.0
- pydantic==2.6.1
- pydantic-settings==2.2.1
- sqlalchemy==2.0.29
- psycopg2-binary==2.9.9
- python-jose[cryptography]==3.3.0
- passlib[bcrypt]==1.7.4
- email-validator==2.1.1

## File Tree
.
main.py
requirements.txt
database.py
models.py
schemas.py
crud.py
auth.py
routers/
    users.py
    meals.py

## API Endpoints

### User Registration
- Method: POST
- Path: /api/v1/users/register
- Request body:
    {
      "email": "string",
      "password": "string"
    }
- Response:
    {
      "id": "integer",
      "email": "string",
      "is_active": "boolean"
    }
- Auth: None

### User Login
- Method: POST
- Path: /api/v1/users/login
- Request body:
    {
      "username": "string",
      "password": "string"
    }
- Response:
    {
      "access_token": "string",
      "token_type": "bearer"
    }
- Auth: None

### Generate Meal Plan
- Method: POST
- Path: /api/v1/meals/plan
- Request body:
    {
      "dietary_preferences": "string",
      "calorie_target": "integer",
      "meal_count": "integer"
    }
- Response:
    {
      "plan_id": "integer",
      "user_id": "integer",
      "meals": [
        {
          "meal_name": "string",
          "description": "string",
          "calories": "integer",
          "macros": {
            "protein": "integer",
            "carbs": "integer",
            "fat": "integer"
          }
        }
      ]
    }
- Auth: Bearer token required

### Log Food Intake
- Method: POST
- Path: /api/v1/tracking/food
- Request body:
    {
      "food_item": "string",
      "calories": "integer",
      "protein": "integer",
      "carbs": "integer",
      "fat": "integer",
      "meal_type": "string"
    }
- Response:
    {
      "tracking_id": "integer",
      "user_id": "integer",
      "food_item": "string",
      "calories": "integer",
      "protein": "integer",
      "carbs": "integer",
      "fat": "integer",
      "meal_type": "string",
      "timestamp": "datetime"
    }
- Auth: Bearer token required

## Environment Variables
- DATABASE_URL: PostgreSQL connection string (e.g., `postgresql://user:password@host:port/database`)
- SECRET_KEY: A strong, random string for JWT token encryption
- ALGORITHM: JWT algorithm (e.g., `HS256`)
- ACCESS_TOKEN_EXPIRE_MINUTES: Token expiration time in minutes (e.g., `30`)

## Dependencies
(See requirements.txt)
