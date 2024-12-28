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


## API Documentation with Swagger
Swagger is a great tool to automatically generate documentation for your API based on your views and serializers. Django REST Framework (DRF) has integration with Swagger via the drf-yasg package.

1.1 Install drf-yasg for Swagger UI
First, install drf-yasg to generate the Swagger UI for your project.
```bash
pip install drf-yasg
```
1.2 Update urls.py to include Swagger Documentation
In your Django project, update your urls.py to include the Swagger view:
```py
from django.urls import path, include
from rest_framework.routers import DefaultRouter
from drf_yasg.views import get_schema_view
from drf_yasg import openapi
from .views import UserProfileViewSet, ProjectViewSet, ProjectMemberViewSet, TaskViewSet, CommentViewSet

# Setting up Swagger Documentation
schema_view = get_schema_view(
   openapi.Info(
      title="Project Management API",
      default_version='v1',
      description="API for managing users, projects, tasks, and comments",
      terms_of_service="https://www.google.com/policies/terms/",
      contact=openapi.Contact(email="contact@projectmanagement.local"),
      license=openapi.License(name="BSD License"),
   ),
   public=True,
)

# Default router for API endpoints
router = DefaultRouter()
router.register(r'users', UserProfileViewSet)
router.register(r'projects', ProjectViewSet)
router.register(r'project_members', ProjectMemberViewSet)
router.register(r'tasks', TaskViewSet)
router.register(r'comments', CommentViewSet)

urlpatterns = [
    path('api/', include(router.urls)),
    path('swagger/', schema_view.with_ui('swagger', cache_timeout=0), name='schema-swagger-ui'),  # Swagger UI endpoint
]
```
This will provide a Swagger UI at the endpoint http://localhost:8000/swagger/ where users can interact with your API and view the documentation.

1.3 Example Swagger UI Output
Once you run the server and visit http://localhost:8000/swagger/, you’ll see a beautifully generated, interactive documentation interface. The API consumers can see all available endpoints, send test requests, and view the responses.
