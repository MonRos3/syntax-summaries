# Flask and Python Commands Reference Guide

## Table of Contents

- [Environment Setup](#environment-setup)
- [Flask Installation](#flask-installation)
- [Basic Flask Application](#basic-flask-application)
- [Flask CLI Commands](#flask-cli-commands)
- [Route Definitions](#route-definitions)
- [Request Handling](#request-handling)
- [Templates and Static Files](#templates-and-static-files)
- [Database Operations](#database-operations)
- [Error Handling](#error-handling)
- [Testing Commands](#testing-commands)
- [Deployment Commands](#deployment-commands)

## Environment Setup

### Virtual Environment Commands

```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment (Windows)
venv\Scripts\activate

# Activate virtual environment (macOS/Linux)
source venv/bin/activate

# Deactivate virtual environment
deactivate

# List installed packages
pip list

# Generate requirements file
pip freeze > requirements.txt

# Install from requirements file
pip install -r requirements.txt
```

## Flask Installation

```bash
# Install Flask
pip install flask

# Install Flask with additional dependencies
pip install flask[async]

# Install Flask development tools
pip install flask python-dotenv

# Install Flask extensions
pip install flask-sqlalchemy flask-migrate flask-wtf flask-login
```

## Basic Flask Application

### Minimal Flask App (`app.py`)

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run(debug=True)
```

### Application Factory Pattern

```python
from flask import Flask

def create_app():
    app = Flask(__name__)
    app.config['SECRET_KEY'] = 'your-secret-key'

    # Register blueprints
    from .routes import main
    app.register_blueprint(main)

    return app
```

## Flask CLI Commands

### Running the Application

```bash
# Run Flask development server
flask run

# Run with specific host and port
flask run --host=0.0.0.0 --port=5000

# Run in debug mode
flask --debug run

# Set Flask app environment variable
export FLASK_APP=app.py  # Linux/macOS
set FLASK_APP=app.py     # Windows

# Set environment to development
export FLASK_ENV=development
```

### Custom CLI Commands

```python
import click
from flask.cli import with_appcontext

@click.command()
@with_appcontext
def init_db():
    """Initialize the database."""
    # Database initialization code here
    click.echo('Initialized the database.')

# Register command
app.cli.add_command(init_db)
```

## Route Definitions

### Basic Routes

```python
from flask import Flask, request, jsonify, render_template

@app.route('/')
def index():
    return 'Home Page'

@app.route('/about')
def about():
    return 'About Page'

# Route with variable
@app.route('/user/<username>')
def user_profile(username):
    return f'User: {username}'

# Route with multiple HTTP methods
@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        # Handle login logic
        return 'Login successful'
    return 'Login form'

# Route with type conversion
@app.route('/post/<int:post_id>')
def show_post(post_id):
    return f'Post ID: {post_id}'
```

### URL Building

```python
from flask import url_for, redirect

@app.route('/redirect-example')
def redirect_example():
    return redirect(url_for('index'))
```

## Request Handling

### Accessing Request Data

```python
from flask import request, jsonify

@app.route('/data', methods=['POST'])
def handle_data():
    # Form data
    username = request.form.get('username')

    # JSON data
    json_data = request.get_json()

    # Query parameters
    page = request.args.get('page', 1, type=int)

    # Files
    uploaded_file = request.files.get('file')

    # Headers
    user_agent = request.headers.get('User-Agent')

    return jsonify({
        'username': username,
        'json_data': json_data,
        'page': page
    })
```

### Response Handling

```python
from flask import make_response, jsonify

@app.route('/custom-response')
def custom_response():
    response = make_response('Custom response')
    response.headers['Custom-Header'] = 'Value'
    response.status_code = 201
    return response

@app.route('/json-response')
def json_response():
    return jsonify({'message': 'Success', 'data': [1, 2, 3]})
```

## Templates and Static Files

### Rendering Templates

```python
from flask import render_template

@app.route('/template')
def template_example():
    users = ['Alice', 'Bob', 'Charlie']
    return render_template('index.html', users=users)

@app.route('/user/<name>')
def user_template(name):
    return render_template('user.html', name=name)
```

### Template Structure (`templates/base.html`)

```html
<!DOCTYPE html>
<html>
  <head>
    <title>{% block title %}{% endblock %}</title>
    <link
      rel="stylesheet"
      href="{{ url_for('static', filename='css/style.css') }}"
    />
  </head>
  <body>
    {% block content %}{% endblock %}
    <script src="{{ url_for('static', filename='js/script.js') }}"></script>
  </body>
</html>
```

## Database Operations

### SQLAlchemy Setup

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///app.db'
db = SQLAlchemy(app)

# Model definition
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(80), unique=True, nullable=False)
    email = db.Column(db.String(120), unique=True, nullable=False)

    def __repr__(self):
        return f'<User {self.username}>'
```

### Database Commands

```bash
# Flask-Migrate commands
flask db init      # Initialize migration repository
flask db migrate   # Generate migration
flask db upgrade   # Apply migrations
flask db downgrade # Rollback migrations
```

### Database Operations in Python

```python
# Create tables
with app.app_context():
    db.create_all()

# Insert data
@app.route('/add-user')
def add_user():
    user = User(username='john', email='john@example.com')
    db.session.add(user)
    db.session.commit()
    return 'User added'

# Query data
@app.route('/users')
def get_users():
    users = User.query.all()
    return jsonify([{'id': u.id, 'username': u.username} for u in users])
```

## Error Handling

### Custom Error Pages

```python
@app.errorhandler(404)
def not_found_error(error):
    return render_template('404.html'), 404

@app.errorhandler(500)
def internal_error(error):
    db.session.rollback()
    return render_template('500.html'), 500

# Custom exception handling
class ValidationError(Exception):
    pass

@app.errorhandler(ValidationError)
def handle_validation_error(e):
    return jsonify({'error': str(e)}), 400
```

## Testing Commands

### Test Setup

```python
import pytest
from app import create_app, db

@pytest.fixture
def app():
    app = create_app({'TESTING': True})
    with app.app_context():
        db.create_all()
        yield app
        db.drop_all()

@pytest.fixture
def client(app):
    return app.test_client()

def test_index(client):
    response = client.get('/')
    assert response.status_code == 200
```

### Running Tests

```bash
# Install pytest
pip install pytest

# Run tests
pytest

# Run tests with coverage
pip install pytest-cov
pytest --cov=app

# Run specific test file
pytest tests/test_routes.py

# Run with verbose output
pytest -v
```

## Deployment Commands

### Production Server Setup

```bash
# Install production server
pip install gunicorn

# Run with Gunicorn
gunicorn -w 4 -b 0.0.0.0:5000 app:app

# Run with specific configuration
gunicorn --config gunicorn.conf.py app:app
```

### Docker Commands

```dockerfile
# Dockerfile
FROM python:3.9-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .
EXPOSE 5000

CMD ["gunicorn", "--bind", "0.0.0.0:5000", "app:app"]
```

```bash
# Build Docker image
docker build -t flask-app .

# Run Docker container
docker run -p 5000:5000 flask-app

# Docker Compose
docker-compose up -d
```

### Environment Configuration

```python
# config.py
import os

class Config:
    SECRET_KEY = os.environ.get('SECRET_KEY') or 'dev-secret-key'
    SQLALCHEMY_DATABASE_URI = os.environ.get('DATABASE_URL') or 'sqlite:///app.db'
    SQLALCHEMY_TRACK_MODIFICATIONS = False

class DevelopmentConfig(Config):
    DEBUG = True

class ProductionConfig(Config):
    DEBUG = False
```

### Using Environment Variables

```bash
# .env file
FLASK_APP=app.py
FLASK_ENV=development
SECRET_KEY=your-secret-key-here
DATABASE_URL=postgresql://user:pass@localhost/dbname

# Load environment variables
pip install python-dotenv
```

```python
from dotenv import load_dotenv
load_dotenv()
```

## Useful Flask Extensions

```bash
# Authentication
pip install flask-login flask-jwt-extended

# Forms
pip install flask-wtf wtforms

# API development
pip install flask-restful flask-marshmallow

# Caching
pip install flask-caching

# CORS
pip install flask-cors

# Mail
pip install flask-mail
```

## Quick Reference Commands

```bash
# Project initialization
mkdir flask-project && cd flask-project
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install flask
echo "from flask import Flask\napp = Flask(__name__)\n@app.route('/')\ndef home():\n    return 'Hello Flask!'" > app.py
flask run

# Development workflow
flask --debug run          # Start development server
flask db migrate          # Create migration
flask db upgrade          # Apply migration
pytest                    # Run tests
pip freeze > requirements.txt  # Update dependencies
```
