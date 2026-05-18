# NutriTrack Backend MVP Technical Specification

## 1. Introduction
This document outlines the technical specifications for the NutriTrack Minimum Viable Product (MVP) backend. The primary goal is to develop core features for initial user testing and launch, focusing on AI-driven personalization for busy professionals.

## 2. Core Features

### 2.1 User Authentication & Management
- **Description**: Secure user registration, login, and profile management.
- **Endpoints**:
    - `POST /auth/register`: User registration with email, password, name.
    - `POST /auth/login`: User login, returning JWT token.
    - `GET /users/me`: Retrieve authenticated user profile.
    - `PUT /users/me`: Update authenticated user profile (e.g., dietary preferences, fitness goals).
- **Data Model**: User (id, email, password_hash, name, dietary_preferences, fitness_goals)
- **Security**: JWT-based authentication for all protected endpoints.

### 2.2 AI Meal Planning
- **Description**: Generate personalized meal plans based on user preferences, dietary restrictions, and fitness goals.
- **Endpoints**:
    - `POST /meal-plans/generate`: Generate a new meal plan for a specified duration (e.g., 7 days).
        - **Request Body**: `{"duration_days": 7, "dietary_preferences": "vegetarian", "fitness_goals": "weight loss"}`
    - `GET /meal-plans/{plan_id}`: Retrieve a specific meal plan.
    - `GET /meal-plans`: Retrieve all meal plans for the authenticated user.
- **Data Model**: MealPlan (id, user_id, start_date, end_date, meals: [Meal]), Meal (day, type, recipe_id, calories, macros)

### 2.3 Calorie & Macro Tracking
- **Description**: Allow users to log food intake and track daily calories and macronutrients against their goals.
- **Endpoints**:
    - `POST /food-logs`: Log a food item for a specific date.
        - **Request Body**: `{"date": "2026-05-17", "meal_type": "lunch", "food_item": "chicken salad", "calories": 350, "protein": 30, "carbs": 20, "fat": 15}`
    - `GET /food-logs/{date}`: Retrieve food logs for a specific date.
    - `GET /food-logs/summary/{date}`: Get daily calorie/macro summary.
- **Data Model**: FoodLog (id, user_id, date, meal_type, food_item, calories, protein, carbs, fat)

### 2.4 Grocery List Generation
- **Description**: Generate a grocery list based on the user's meal plan.
- **Endpoints**:
    - `GET /grocery-lists/generate/{meal_plan_id}`: Generate a grocery list from a meal plan.
- **Data Model**: GroceryList (id, user_id, meal_plan_id, items: [GroceryItem]), GroceryItem (name, quantity, unit)

### 2.5 Weekly Nutrition Reports
- **Description**: Generate weekly summaries of calorie/macro intake, progress towards goals, and insights.
- **Endpoints**:
    - `GET /reports/weekly/{start_date}`: Generate a weekly nutrition report.
- **Data Model**: NutritionReport (id, user_id, start_date, end_date, summary_text, avg_calories, avg_macros, insights)

## 3. Technology Stack
- **Backend Framework**: FastAPI (Python)
- **Database**: PostgreSQL
- **ORM**: SQLAlchemy
- **Authentication**: JWT
- **Deployment**: Docker, AWS/GCP (future)

## 4. API Design Principles
- RESTful architecture
- JSON for request/response bodies
- Clear error messages with appropriate HTTP status codes
- Versioning (e.g., `/api/v1/`)

## 5. Future Considerations (Beyond MVP)
- Integration with wearable devices
- AI-driven recipe recommendations
- Community features
- Payment gateway integration
