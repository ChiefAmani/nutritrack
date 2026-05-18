# NutriTrack Backend Technical Specification

## 1. Project Overview
NutriTrack is an AI nutrition coaching SaaS platform for busy professionals. This document outlines the technical specifications for the core backend MVP, focusing on user authentication and meal logging functionalities.

## 2. Technology Stack
- **Language:** Python 3.9+
- **Framework:** FastAPI
- **Database:** PostgreSQL (via SQLAlchemy ORM)
- **Authentication:** JWT (JSON Web Tokens)
- **Dependency Management:** Poetry

## 3. File Tree
- main.py
- database.py
- models.py
- schemas.py
- crud.py
- auth.py
- dependencies.py
- requirements.txt
- .env.example

## 4. API Endpoints

### 4.1. User Authentication

#### `POST /register`
- **Description:** Registers a new user.
- **Request Body:**
  ```json
  {
    "email": "user@example.com",
    "password": "securepassword123"
  }
  ```
- **Response:**
  - **201 Created:**
    ```json
    {
      "message": "User registered successfully",
      "user_id": "uuid_of_user"
    }
    ```
  - **400 Bad Request:** If email already exists or invalid input.

#### `POST /token`
- **Description:** Authenticates a user and returns an access token.
- **Request Body (form-data):**
  - `username`: user's email
  - `password`: user's password
- **Response:**
  - **200 OK:**
    ```json
    {
      "access_token": "jwt_token_string",
      "token_type": "bearer"
    }
    ```
  - **401 Unauthorized:** Invalid credentials.

### 4.2. Meal Logging

#### `POST /meals`
- **Description:** Logs a new meal for the authenticated user.
- **Authentication:** Requires valid JWT in `Authorization: Bearer <token>` header.
- **Request Body:**
  ```json
  {
    "name": "Chicken Salad",
    "calories": 450,
    "protein": 30,
    "carbs": 20,
    "fat": 25,
    "meal_time": "2026-05-17T12:30:00Z"
  }
  ```
- **Response:**
  - **201 Created:**
    ```json
    {
      "message": "Meal logged successfully",
      "meal_id": "uuid_of_meal"
    }
    ```
  - **401 Unauthorized:** If no valid token.
  - **400 Bad Request:** Invalid input.

#### `GET /meals`
- **Description:** Retrieves all meals for the authenticated user.
- **Authentication:** Requires valid JWT in `Authorization: Bearer <token>` header.
- **Query Parameters:**
  - `start_date` (optional): Filter meals from this date (YYYY-MM-DD).
  - `end_date` (optional): Filter meals up to this date (YYYY-MM-DD).
- **Response:**
  - **200 OK:**
    ```json
    [
      {
        "id": "uuid_of_meal_1",
        "name": "Chicken Salad",
        "calories": 450,
        "protein": 30,
        "carbs": 20,
        "fat": 25,
        "meal_time": "2026-05-17T12:30:00Z"
      },
      {
        "id": "uuid_of_meal_2",
        "name": "Oatmeal",
        "calories": 200,
        "protein": 5,
        "carbs": 30,
        "fat": 5,
        "meal_time": "2026-05-17T08:00:00Z"
      }
    ]
    ```
  - **401 Unauthorized:** If no valid token.

## 5. Environment Variables
- `DATABASE_URL`: PostgreSQL connection string (e.g., `postgresql://user:password@host:port/dbname`)
- `SECRET_KEY`: A strong, random string for JWT signing.
- `ALGORITHM`: JWT algorithm (e.g., `HS256`)
- `ACCESS_TOKEN_EXPIRE_MINUTES`: Token expiration time in minutes (e.g., `30`)

## 6. Dependencies (requirements.txt)
```
fastapi==0.110.0
uvicorn==0.28.0
sqlalchemy==2.0.27
pydantic==2.6.1
python-jose[cryptography]==3.3.0
passlib[bcrypt]==1.7.4
psycopg2-binary==2.9.9
python-dotenv==1.0.1
```
