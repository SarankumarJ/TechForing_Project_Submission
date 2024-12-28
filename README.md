# Project Management API

This is a project management API built using Django and Django REST Framework (DRF). It allows teams to manage users, projects, tasks, and comments. The API includes authentication and authorization via JWT tokens.

## Features:
- User registration and authentication using JWT tokens
- CRUD operations for managing projects, tasks, comments, and users
- User roles in projects (Admin, Member)
- Task management with statuses (To Do, In Progress, Done) and priorities (Low, Medium, High)
- Swagger UI documentation for easy API interaction

## Requirements:
- Python 3.x
- Django 4.x
- Django REST Framework
- djangorestframework-simplejwt
- drf-yasg (for Swagger UI)

## Installation

1. Clone the repository:

```bash
git clone https://github.com/SarankumarJ/TechForing_Project_Submission.git
cd TechForing_Project
```

2. Set up the database:
Make sure you have a working database (PostgreSQL, SQLite, etc.)
Update the DATABASES configuration in settings.py as per your database setup.

3. Run migrations to create the necessary database tables:
```bash
python manage.py migrate
```

## Running the Project Locally

1. Create a superuser to access the admin panel and test the API:
```bash
python manage.py createsuperuser
```

2. Start the development server:
```bash
python manage.py runserver
```
3. Access the Swagger documentation at http://localhost:8000/swagger/.

## API Endpoints
### Users:

POST /api/users/register/ - Register a new user

POST /api/users/login/ - Login a user and get JWT tokens

GET /api/users/{id}/ - Retrieve user details

PUT/PATCH /api/users/{id}/ - Update user details

DELETE /api/users/{id}/ - Delete a user account

### Projects:

GET /api/projects/ - List all projects

POST /api/projects/ - Create a new project

GET /api/projects/{id}/ - Retrieve project details

PUT/PATCH /api/projects/{id}/ - Update project details

DELETE /api/projects/{id}/ - Delete a project

### Tasks:

GET /api/projects/{project_id}/tasks/ - List tasks in a project

POST /api/projects/{project_id}/tasks/ - Create a new task in a project

GET /api/tasks/{id}/ - Retrieve task details

PUT/PATCH /api/tasks/{id}/ - Update task details

DELETE /api/tasks/{id}/ - Delete a task

### Comments:

GET /api/tasks/{task_id}/comments/ - List comments on a task

POST /api/tasks/{task_id}/comments/ - Create a new comment on a task

GET /api/comments/{id}/ - Retrieve comment details

PUT/PATCH /api/comments/{id}/ - Update comment details

DELETE /api/comments/{id}/ - Delete a comment


## Authentication
This API uses JWT for authentication. To login, send a POST request to /api/users/login/ with the user's credentials. You will receive an access token and a refresh token.

For subsequent requests, include the JWT access token in the Authorization header like so:

```bash
Authorization: Bearer <your_jwt_token>
```
## Testing the API
You can test the API using Postman or Swagger UI. Make sure to include your JWT token in the header for authenticated endpoints.
