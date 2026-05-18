# NutriTrack Backend MVP

## Project Overview
The NutriTrack Backend MVP provides core API services for AI nutrition coaching. It enables user management, AI-driven meal planning, calorie/macro tracking, grocery list generation, and weekly nutrition report generation. This backend serves as the foundation for initial user testing and launch, supporting busy professionals in maintaining healthy habits.

## Setup Instructions

### Prerequisites
Ensure you have Python 3.10.12 installed.

### Installation
1.  **Clone the repository:**
    ```bash
    git clone https://github.com/ChiefAmani/nutritrack.git
    cd nutritrack
    ```
2.  **Create a virtual environment (recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```
3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
    The `requirements.txt` file should contain:
    ```
    fastapi==0.110.0
    pydantic==2.6.1
    sqlalchemy==2.0.29
    psycopg2-binary==2.9.9
    uvicorn==0.29.0
    python-dotenv==1.0.1
    ```
4.  **Environment Variables:**
    Create a `.env` file in the root directory based on `.env.example`. This file will contain your database connection string and other sensitive configurations.

### Running the Application
To start the FastAPI application using Uvicorn:
```bash
uvicorn main:app --reload
```
The API will be accessible at `http://127.0.0.1:8000`.

## API Endpoints

### User Registration
-   **Path:** `/api/v1/users/register`
-   **Method:** `POST`
-   **Description:** Registers a new user with the system.
-   **Request Body Example:**
    ```json
    {
      "email": "user@example.com",
      "password": "securepassword123",
      "name": "John Doe"
    }
    ```
-   **Response Body Example (Success):**
    ```json
    {
      "id": 1,
      "email": "user@example.com",
      "name": "John Doe"
    }
    ```

### Other Endpoints
Further API endpoints for meal planning, calorie/macro tracking, grocery list generation, and weekly nutrition reports will be documented here as they are developed.
