# Client Management System

A Django REST API project for managing clients and their projects. This system allows you to register clients, manage projects, and assign users to different projects.

## Features

- User Authentication
- Client Management (CRUD operations)
- Project Management
- User Assignment to Projects
- REST API Endpoints
- Admin Interface

## Prerequisites

- Python 3.8+
- MySQL 5.7+
- pip (Python package manager)

## Installation

1. Clone the repository or create a new directory:
bash
mkdir client_management
cd client_management


2. Create and activate virtual environment:
bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate


3. Install required packages:
bash
pip install django djangorestframework mysqlclient


4. Create Django project and app:
bash
django-admin startproject client_management
cd client_management
python manage.py startapp clients


5. Database Setup:
sql
mysql -u root -p
CREATE DATABASE client_management_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;


6. Update database settings in client_management/settings.py:
python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'client_management_db',
        'USER': 'your_mysql_username',
        'PASSWORD': 'your_mysql_password',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}


7. Run migrations:
bash
python manage.py makemigrations
python manage.py migrate


8. Create superuser:
bash
python manage.py createsuperuser


## Project Structure


client_management/
│
├── client_management/      # Project directory
│   ├── __init__.py
│   ├── settings.py        # Project settings
│   ├── urls.py           # Main URL configuration
│   └── wsgi.py
│
├── clients/               # App directory
│   ├── __init__.py
│   ├── admin.py          # Admin interface configuration
│   ├── apps.py
│   ├── models.py         # Database models
│   ├── serializers.py    # API serializers
│   ├── views.py          # API views
│   └── tests.py
│
├── manage.py
├── requirements.txt
└── README.md


## API Endpoints

### Clients

- List all clients: GET /clients/
- Create new client: POST /clients/
- Retrieve client details: GET /clients/:id/
- Update client: PUT /clients/:id/
- Delete client: DELETE /clients/:id/
- Create project for client: POST /clients/:id/projects/

### Projects

- List user's projects: GET /projects/

## API Examples

### Create Client
bash
POST /clients/
{
    "client_name": "Company A"
}


### Create Project
bash
POST /clients/:id/projects/
{
    "project_name": "Project A",
    "users": [1, 2]  # User IDs
}


## Authentication

The API uses Django's session-based authentication. You can:
1. Log in through the admin interface (/admin/)
2. Use Basic Authentication for API requests
3. Include session cookie in API requests after logging in

## Admin Interface

Access the admin interface at /admin/ to:
- Manage users
- Create/edit clients
- Manage projects
- Assign users to projects

## Running the Development Server

bash
python manage.py runserver

The server will start at http://localhost:8000

## Testing the API

You can test the API using:
1. Browser (for GET requests)
2. Postman
3. curl commands

### Example curl commands:

List clients:
bash
curl -H "Authorization: Basic <base64-encoded-credentials>" http://localhost:8000/clients/


Create client:
bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Basic <base64-encoded-credentials>" \
  -d '{"client_name":"New Client"}' \
  http://localhost:8000/clients/


## Error Handling

Common issues and solutions:

1. Database connection errors:
   - Check MySQL service is running
   - Verify database credentials in settings.py
   - Ensure database exists

2. Migration errors:
   - Run python manage.py makemigrations
   - Run python manage.py migrate
