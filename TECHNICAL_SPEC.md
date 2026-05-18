# TECHNICAL_SPEC.md

## Project Overview
Integrate automated grocery list generation from AI meal plans with a grocery delivery service, initially Instacart. This feature will allow NutriTrack users to seamlessly order ingredients for their personalized meal plans, significantly enhancing convenience and supporting consistent healthy eating habits.

## Tech Stack
- python==3.10.12
- fastapi==0.110.0
- pydantic==2.6.1
- requests==2.31.0
- uvicorn==0.27.1

## File Tree
```
backend/
|-- app/
|   |-- main.py
|   |-- routers/
|   |   `-- grocery.py
|   |-- services/
|   |   |-- meal_planner.py  # Existing AI meal planning logic (assumed)
|   |   |-- grocery_generator.py
|   |   `-- instacart_api.py
|   `-- models/
|       `-- grocery.py
`-- tests/
    `-- test_grocery.py
```

## API Endpoints

### 1. Generate Grocery List
- Method: POST
- Path: /api/grocery/generate
- Description: Generates a grocery list based on a provided meal plan ID.
- Request body:
  ```json
  {
    "meal_plan_id": "string"
  }
  ```
- Response:
  ```json
  {
    "grocery_list_id": "string",
    "items": [
      {
        "name": "string",
        "quantity": "number",
        "unit": "string"
      }
    ]
  }
  ```
- Auth: Bearer token required

### 2. Initiate Grocery Delivery (Instacart)
- Method: POST
- Path: /api/grocery/delivery/instacart
- Description: Initiates a grocery delivery order via Instacart using a generated grocery list.
- Request body:
  ```json
  {
    "grocery_list_id": "string",
    "user_address": "string",
    "delivery_time_slot": "string"
  }
  ```
- Response:
  ```json
  {
    "delivery_order_id": "string",
    "instacart_checkout_url": "string"
  }
  ```
- Auth: Bearer token required

## Environment Variables
- INSTACART_API_KEY
- INSTACART_CLIENT_ID
- INSTACART_CLIENT_SECRET
- INSTACART_REDIRECT_URI

## Dependencies
```
fastapi==0.110.0
pydantic==2.6.1
requests==2.31.0
uvicorn==0.27.1
```
