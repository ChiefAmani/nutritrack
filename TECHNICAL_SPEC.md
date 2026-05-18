# NutriTrack API Technical Specification

## Introduction
This document outlines the technical specifications for the NutriTrack AI Nutrition Coaching API. It serves as a contract for frontend development and integration, detailing the core endpoints for user management, meal planning, tracking, grocery lists, reports, and nudges.

## Base URL
`https://api.nutritrack.com`

## Authentication
All API endpoints require authentication. A valid API key or JWT token must be included in the `Authorization` header for all requests.

## Endpoints

### 1. User Management (Me)
*   **GET /api/me**
    *   **Description:** Retrieve the authenticated user's profile information.
    *   **Response:**
        ```
        {
          "id": "user123",
          "name": "John Doe",
          "email": "john.doe@example.com",
          "preferences": {
            "dietary_restrictions": ["vegetarian"],
            "calorie_target": 2000
          }
        }
        ```

### 2. Meal Plans
*   **GET /api/meal_plans/current**
    *   **Description:** Retrieve the user's current meal plan.
    *   **Response:**
        ```
        {
          "date": "2026-05-18",
          "meals": [
            {
              "type": "breakfast",
              "name": "Oatmeal with Berries",
              "calories": 350,
              "macros": {"protein": 15, "carbs": 50, "fat": 10}
            },
            {
              "type": "lunch",
              "name": "Chicken Salad",
              "calories": 450,
              "macros": {"protein": 40, "carbs": 20, "fat": 25}
            }
          ]
        }
        ```
*   **POST /api/meal_plans/generate**
    *   **Description:** Generate a new meal plan based on user preferences.
    *   **Request:**
        ```
        {
          "dietary_restrictions": ["vegetarian"],
          "calorie_target": 2000,
          "meal_count": 3
        }
        ```
    *   **Response:** (Same as GET /api/meal_plans/current)

### 3. Tracking
*   **POST /api/tracking/log_meal**
    *   **Description:** Log a consumed meal.
    *   **Request:**
        ```
        {
          "meal_name": "Oatmeal with Berries",
          "calories": 350,
          "macros": {"protein": 15, "carbs": 50, "fat": 10},
          "timestamp": "2026-05-18T08:30:00Z"
        }
        ```
    *   **Response:**
        ```
        {"message": "Meal logged successfully."}
        ```
*   **GET /api/tracking/summary**
    *   **Description:** Get a summary of daily nutrition intake.
    *   **Response:**
        ```
        {
          "date": "2026-05-18",
          "total_calories": 800,
          "total_macros": {"protein": 55, "carbs": 70, "fat": 35},
          "meals_logged": 2
        }
        ```

### 4. Grocery Lists
*   **GET /api/grocery_lists/current**
    *   **Description:** Retrieve the user's current grocery list based on meal plans.
    *   **Response:**
        ```
        {
          "date": "2026-05-18",
          "items": [
            {"name": "Oats", "quantity": "1 cup"},
            {"name": "Mixed Berries", "quantity": "1/2 cup"},
            {"name": "Chicken Breast", "quantity": "200g"},
            {"name": "Lettuce", "quantity": "1 head"}
          ]
        }
        ```
*   **POST /api/grocery_lists/generate**
    *   **Description:** Generate a new grocery list.
    *   **Request:**
        ```
        {
          "meal_plan_id": "plan123",
          "start_date": "2026-05-18",
          "end_date": "2026-05-24"
        }
        ```
    *   **Response:** (Same as GET /api/grocery_lists/current)

### 5. Reports
*   **GET /api/reports/weekly**
    *   **Description:** Generate a weekly nutrition report.
    *   **Response:**
        ```
        {
          "start_date": "2026-05-11",
          "end_date": "2026-05-17",
          "average_daily_calories": 1950,
          "average_daily_macros": {"protein": 80, "carbs": 200, "fat": 70},
          "trends": "Consistent calorie intake, slightly low on protein."
        }
        ```

### 6. Nudges
*   **GET /api/nudges/current**
    *   **Description:** Retrieve current coaching nudges for the user.
    *   **Response:**
        ```
        [
          {
            "id": "nudge001",
            "type": "email",
            "message": "Remember to drink enough water today!",
            "action": "Hydration reminder"
          },
          {
            "id": "nudge002",
            "type": "app_notification",
            "message": "You're doing great! Keep tracking your meals.",
            "action": "Encouragement"
          }
        ]
        ```
*   **POST /api/nudges/send**
    *   **Description:** Manually trigger a coaching nudge (for admin/testing).
    *   **Request:**
        ```
        {
          "user_id": "user123",
          "type": "email",
          "message": "Time for your afternoon snack!",
          "action": "Snack reminder"
        }
        ```
    *   **Response:**
        ```
        {"message": "Nudge sent successfully."}
        ```
