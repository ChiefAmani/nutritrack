# TECHNICAL_SPEC.md

## Project Overview
This project defines the core MVP backend for NutriTrack, an AI nutrition coaching SaaS. It will provide essential functionalities including user authentication, AI-driven meal planning, calorie/macro tracking, grocery list generation, and weekly nutrition reports. The backend will serve as the foundation for initial user testing and validation, enabling busy professionals to manage their nutrition efficiently.

## Tech Stack
- fastapi==0.0.1
- pydantic==2.6.1
- uvicorn==0.27.1
- sqlalchemy==2.0.25
- python-dotenv==1.0.1
- passlib==1.7.4
- python-jose[cryptography]==3.3.0

## File Tree
```
.
|-- backend/
|   |-- main.py
|   |-- database.py
|   |-- models.py
|   |-- schemas.py
|   |-- crud.py
|   |-- auth.py
|   `-- requirements.txt
`-- .env
```

## API Endpoints

### 1. User Registration
- Method: POST
- Path: /register
- Request body:
  ```json
  {
    "email": "string",
    "password": "string"
  }
  ```
- Response:
  ```json
  {
    "id": "integer",
    "email": "string"
  }
  ```
- Auth: None

### 2. User Login (OAuth2 Token)
- Method: POST
- Path: /token
- Request body: (form-data)
  - `username`: "string" (user's email)
  - `password`: "string"
- Response:
  ```json
  {
    "access_token": "string",
    "token_type": "bearer"
  }
  ```
- Auth: None

### 3. Generate Meal Plan
- Method: POST
- Path: /meal-plans
- Request body:
  ```json
  {
    "user_id": "integer",
    "dietary_preferences": "array of strings",
    "calorie_target": "integer",
    "duration_days": "integer"
  }
  ```
- Response:
  ```json
  {
    "id": "integer",
    "user_id": "integer",
    "plan_details": "json_object",
    "created_at": "datetime"
  }
  ```
- Auth: Bearer token required

### 4. Log Food Item
- Method: POST
- Path: /food-logs
- Request body:
  ```json
  {
    "user_id": "integer",
    "food_name": "string",
    "calories": "integer",
    "protein_g": "float",
    "carbs_g": "float",
    "fat_g": "float",
    "log_date": "date"
  }
  ```
- Response:
  ```json
  {
    "id": "integer",
    "user_id": "integer",
    "food_name": "string",
    "calories": "integer",
    "protein_g": "float",
    "carbs_g": "float",
    "fat_g": "float",
    "log_date": "date",
    "created_at": "datetime"
  }
  ```
- Auth: Bearer token required

### 5. Get Food Logs
- Method: GET
- Path: /food-logs
- Query parameters:
  - `user_id`: "integer"
  - `start_date`: "date" (optional)
  - `end_date`: "date" (optional)
- Response:
  ```json
  [
    {
      "id": "integer",
      "user_id": "integer",
      "food_name": "string",
      "calories": "integer",
      "protein_g": "float",
      "carbs_g": "float",
      "fat_g": "float",
      "log_date": "date",
      "created_at": "datetime"
    }
  ]
  ```
- Auth: Bearer token required

### 6. Generate Grocery List
- Method: GET
- Path: /grocery-lists
- Query parameters:
  - `user_id`: "integer"
  - `meal_plan_id`: "integer" (optional, if not provided, use active plan)
- Response:
  ```json
  {
    "id": "integer",
    "user_id": "integer",
    "meal_plan_id": "integer",
    "items": "array of strings",
    "generated_at": "datetime"
  }
  ```
- Auth: Bearer token required

### 7. Get Weekly Nutrition Report
- Method: GET
- Path: /nutrition-reports/weekly
- Query parameters:
  - `user_id`: "integer"
  - `end_date`: "date" (defaults to current week if not provided)
- Response:
  ```json
  {
    "user_id": "integer",
    "start_date": "date",
    "end_date": "date",
    "total_calories": "integer",
    "avg_macros": {
      "protein_g": "float",
      "carbs_g": "float",
      "fat_g": "float"
    },
    "insights": "string",
    "recommendations": "string"
  }
  ```
- Auth: Bearer token required

## Environment Variables
- `DATABASE_URL`: "sqlite:///./sql_app.db" (for MVP, can be PostgreSQL in production)
- `SECRET_KEY`: "your-super-secret-key" (for JWT token encoding)
- `ALGORITHM`: "HS256" (for JWT token encoding)
- `ACCESS_TOKEN_EXPIRE_MINUTES`: "30" (for JWT token expiration)

## Dependencies
```
fastapi==0.0.1
pydantic==2.6.1
uvicorn==0.27.1
sqlalchemy==2.0.25
python-dotenv==1.0.1
passlib==1.7.4
python-jose[cryptography]==3.3.0
```