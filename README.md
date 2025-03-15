# Django REST Framework E-commerce API

A simple Django REST Framework API that provides e-commerce functionality with items and orders management, including user authentication and a contact form. This project demonstrates best practices in building RESTful APIs with Django.

## Features

- Token-based authentication system
- Items listing and retrieval
- Order management with stock validation
- Contact form submission
- Comprehensive test coverage
- Dockerized application for easy deployment

## Project Structure

```
django-rest-framework/
├── backend/
│   ├── core/                # Contact form functionality
│   ├── docker/              # Docker configuration files
│   ├── DRF/                 # Main Django project settings
│   ├── ecommerce/           # E-commerce functionality
│   ├── utils/               # Utility modules and abstract models
│   └── requirements.txt     # All dependicies
├── steps/                   # Project documentation
├── .env                     # Environment variables
├── docker-compose.yml       # Docker compose configuration
└── server.py                # Server configuration
```

## Requirements

- Python 3.8+
- Django 3.2+
- Django REST Framework 3.12+
- Docker and Docker Compose (for containerized setup)

## Installation

### Method 1: Standard Git Clone

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/django-rest-framework.git
   cd django-rest-framework
   ```

2. Create and activate a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: .\venv\Scripts\activate
   ```

3. Install dependencies:
   ```bash
   cd backend
   pip install -r requirements.txt
   ```

4. Set up environment variables:
   ```bash
   cp ../env.template ../.env
   # Edit the .env file with your settings
   ```

5. Apply migrations:
   ```bash
   python manage.py migrate
   ```

6. Create a superuser:
   ```bash
   python manage.py createsuperuser
   ```

7. Run the development server:
   ```bash
   python manage.py runserver
   ```

### Method 2: Using Docker

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/django-rest-framework.git
   cd django-rest-framework
   ```

2. Set up environment variables:
   ```bash
   cp env.template .env
   # Edit the .env file with your settings
   ```

3. Build and start the Docker containers:
   ```bash
   docker-compose up -d --build
   ```

4. Create a superuser:
   ```bash
   docker-compose exec web python manage.py createsuperuser
   ```

5. Access the application at `http://localhost:8000`

## API Usage

### Authentication

The API uses token-based authentication. You need to obtain a token before making authenticated requests.

#### Getting a Token

Using curl:
```bash
curl -X POST http://localhost:8000/api-token-auth/ -H "Content-Type: application/json" -d '{"username": "your_username", "password": "your_password"}'
```

Using Postman:
1. Create a POST request to `http://localhost:8000/api-token-auth/`
2. Set the Content-Type header to `application/json`
3. Add a request body with your credentials:
   ```json
   {
       "username": "your_username",
       "password": "your_password"
   }
   ```
4. Send the request and save the token from the response

### Items API

#### List all items

```bash
# Using curl
curl -X GET http://localhost:8000/item/ -H "Authorization: Token your_token_here"

# Using Postman
GET http://localhost:8000/item/
Headers: Authorization: Token your_token_here
```

#### Get a specific item

```bash
# Using curl
curl -X GET http://localhost:8000/item/1/ -H "Authorization: Token your_token_here"

# Using Postman
GET http://localhost:8000/item/1/
Headers: Authorization: Token your_token_here
```

### Orders API

#### List all orders (for the authenticated user)

```bash
# Using curl
curl -X GET http://localhost:8000/order/ -H "Authorization: Token your_token_here"

# Using Postman
GET http://localhost:8000/order/
Headers: Authorization: Token your_token_here
```

#### Create a new order

```bash
# Using curl
curl -X POST http://localhost:8000/order/ -H "Content-Type: application/json" -H "Authorization: Token your_token_here" -d '{"item": "1", "quantity": "3"}'

# Using Postman
POST http://localhost:8000/order/
Headers: 
  - Content-Type: application/json
  - Authorization: Token your_token_here
Body:
{
    "item": "1",
    "quantity": "3"
}
```

#### Get a specific order

```bash
# Using curl
curl -X GET http://localhost:8000/order/1/ -H "Authorization: Token your_token_here"

# Using Postman
GET http://localhost:8000/order/1/
Headers: Authorization: Token your_token_here
```

### Contact API

#### Submit a contact form

```bash
# Using curl
curl -X POST http://localhost:8000/contact/ -H "Content-Type: application/json" -d '{"name": "Shaurya Bisht", "email": "shaurya@example.com", "message": "Hello, I have a question about your products."}'

# Using Postman
POST http://localhost:8000/contact/
Headers: Content-Type: application/json
Body:
{
    "name": "Shaurya Bisht",
    "email": "shaurya@example.com",
    "message": "Hello, I have a question about your products."
}
```

## Testing

Run the tests with:

```bash
# Standard method
python manage.py test

# Using Docker
docker-compose exec web python manage.py test
```

## Admin Interface

Access the admin interface at `http://localhost:8000/admin/` using your superuser credentials.


## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes (`git commit -m 'Add some feature'`)
4. Push to the branch (`git push origin feature/your-feature`)
5. Open a Pull Request
