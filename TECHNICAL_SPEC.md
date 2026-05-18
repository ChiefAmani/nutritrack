# TECHNICAL_SPEC.md

## Project Overview
Develop the core backend API for NutriTrack's MVP, enabling AI meal planning, calorie/macro tracking, and user management for busy professionals. This backend will support initial user testing and launch, validating core features and facilitating user acquisition.

## Tech Stack
- Python==3.10.12
- fastapi==0.110.0
- pydantic==2.6.1
- uvicorn==0.27.1
- sqlalchemy==2.0.25
- psycopg2-binary==2.9.9
- python-dotenv==1.0.1

## File Tree
.
|-- backend/
|   |-- main.py
|   |-- database.py
|   |-- models.py
|   |-- schemas.py
|   |-- crud.py
|   \-- requirements.txt
\-- .env

## API Endpoints

### User Management
- Method: POST
- Path: /api/users/register
- Request body: { "email": "string", "password": "string", "name": "string", "age": "integer", "weight_kg": "float", "height_cm": "float", "activity_level": "string" }
- Response: { "id": "integer", "email": "string", "name": "string" }
- Auth: None

- Method: POST
- Path: /api/users/login
- Request body: { "email": "string", "password": "string" }
- Response: { "access_token": "string", "token_type": "bearer" }
- Auth: None

### Meal Planning
- Method: POST
- Path: /api/meal_plans/generate
- Request body: { "user_id": "integer", "dietary_preferences": "list[string]", "calorie_target": "integer", "macro_split": { "protein": "float", "carbs": "float", "fat": "float" } }
- Response: { "plan_id": "integer", "meals": "list[object]" } (object contains meal details like name, ingredients, calories, macros)
- Auth: Bearer token required

- Method: GET
- Path: /api/meal_plans/{plan_id}
- Response: { "plan_id": "integer", "meals": "list[object]" }
- Auth: Bearer token required

### Calorie/Macro Tracking
- Method: POST
- Path: /api/track_entries
- Request body: { "user_id": "integer", "meal_id": "integer", "consumed_at": "datetime", "calories": "integer", "protein": "float", "carbs": "float", "fat": "float" }
- Response: { "entry_id": "integer", "user_id": "integer", "meal_id": "integer", "consumed_at": "datetime" }
- Auth: Bearer token required

- Method: GET
- Path: /api/track_entries/user/{user_id}
- Response: "list[object]" (each object contains tracking entry details)
- Auth: Bearer token required

## Environment Variables
- DATABASE_URL="postgresql://user:password@host:port/database"
- SECRET_KEY="your_super_secret_key"
- ALGORITHM="HS256"
- ACCESS_TOKEN_EXPIRE_MINUTES="30"

## Dependencies
fastapi==0.110.0
pydantic==2.6.1
uvicorn==0.27.1
sqlalchemy==2.0.25
psycopg2-binary==2.9.9
python-dotenv==1.0.1
python-jose[cryptography]==3.3.0
passlib[bcrypt]==1.7.4