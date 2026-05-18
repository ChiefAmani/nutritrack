# TECHNICAL_SPEC.md

## Project Overview
This document specifies the API endpoints for the NutriTrack AI Nutrition Coaching SaaS. It outlines the core functionalities including AI meal planning, calorie/macro tracking, grocery list generation, weekly nutrition reports, and email coaching nudges, enabling frontend development and integration for initial user testing and validation.

## Tech Stack
- FastAPI==0.110.0
- Pydantic==2.6.1
- Uvicorn==0.29.0

## File Tree
- .
- app/
- app/api/
- app/api/endpoints/
- app/api/endpoints/__init__.py
- app/api/endpoints/meal_plans.py
- app/api/endpoints/tracking.py
- app/api/endpoints/grocery_lists.py
- app/api/endpoints/reports.py
- app/api/endpoints/nudges.py
- app/api/endpoints/me.py (placeholder for user-related endpoints)
- app/api/__init__.py
- app/__init__.py
- app/main.py
- TECHNICAL_SPEC.md
- requirements.txt
- .env

## API Endpoints

### Root Endpoint
- Method: GET
- Path: /
- Description: Basic health check or welcome message.
- Request body: None
- Response: message: string (e.g., "Welcome to NutriTrack API!")
- Auth: None

### Meal Plans
- Method: POST
- Path: /api/meal_plans/generate
- Description: Generates a personalized meal plan based on user preferences.
- Request body:
  user_id: string
  dietary_preferences: list of strings
  calorie_target: integer
  macro_split: object (protein: integer, carbs: integer, fat: integer)
- Response:
  meal_plan_id: string
  plan_details: list of objects (meal_type: string, recipe_name: string, ingredients: list of strings, calories: integer, macros: object (protein: integer, carbs: integer, fat: integer))
- Auth: Bearer token required

- Method: GET
- Path: /api/meal_plans/{meal_plan_id}
- Description: Retrieves a specific meal plan.
- Request body: None
- Response: (Same as POST response for plan_details)
- Auth: Bearer token required

### Tracking
- Method: POST
- Path: /api/tracking/log_meal
- Description: Logs a consumed meal for calorie and macro tracking.
- Request body:
  user_id: string
  meal_name: string
  consumed_at: datetime
  calories: integer
  macros: object (protein: integer, carbs: integer, fat: integer)
- Response:
  tracking_id: string
  status: string (e.g., "success")
- Auth: Bearer token required

- Method: GET
- Path: /api/tracking/summary/{user_id}
- Description: Retrieves daily or weekly tracking summary for a user.
- Request body: None
- Response:
  user_id: string
  date_range: string
  total_calories: integer
  total_macros: object (protein: integer, carbs: integer, fat: integer)
  meals_logged: integer
- Auth: Bearer token required

### Grocery Lists
- Method: POST
- Path: /api/grocery_lists/generate
- Description: Generates a grocery list based on a meal plan.
- Request body:
  user_id: string
  meal_plan_id: string
- Response:
  grocery_list_id: string
  items: list of objects (item_name: string, quantity: string, unit: string)
- Auth: Bearer token required

- Method: GET
- Path: /api/grocery_lists/{grocery_list_id}
- Description: Retrieves a specific grocery list.
- Request body: None
- Response: (Same as POST response for items)
- Auth: Bearer token required

### Reports
- Method: GET
- Path: /api/reports/weekly_nutrition/{user_id}
- Description: Generates a weekly nutrition report for a user.
- Request body: None
- Response:
  report_id: string
  user_id: string
  start_date: date
  end_date: date
  average_calories_per_day: integer
  macro_breakdown: object (protein_percentage: integer, carbs_percentage: integer, fat_percentage: integer)
  insights: list of strings
- Auth: Bearer token required

### Nudges
- Method: POST
- Path: /api/nudges/send
- Description: Triggers an email coaching nudge for a user.
- Request body:
  user_id: string
  nudge_type: string
  message_content: string
- Response:
  nudge_id: string
  status: string (e.g., "sent")
- Auth: Bearer token required

## Environment Variables
- DATABASE_URL: Connection string for the database.
- SECRET_KEY: Secret key for JWT authentication.
- EMAIL_API_KEY: API key for email sending service.

## Dependencies
fastapi==0.110.0
pydantic==2.6.1
uvicorn==0.29.0
python-dotenv==1.0.1
# Add other database drivers, AI model dependencies, etc. as needed
