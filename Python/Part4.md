# Python for Backend (Web Development)# 1. Flask (Lightweight Web Framework)

**Definition:** Flask is a lightweight Python web framework for building web apps and APIs.

## Features
- Minimalist → easy to start  
- Supports routing, templates, REST APIs  
- Extendable with libraries (Flask-RESTful, SQLAlchemy)  

## Installation
```bash
pip install Flask
```
## Basic Flask App

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello, Flask!"

if __name__ == "__main__":
    app.run(debug=True)
```
## Explanation

- `Flask(__name__)` → Create Flask application  
- `@app.route("/")` → Define route for URL `/`  
- `app.run(debug=True)` → Run server with debug mode enabled


# 2. Routes & HTTP Methods

**Routes:** URL endpoints users can access  

**HTTP Methods:** Actions on routes  
- **GET** → Fetch data  
- **POST** → Create data  
- **PUT** → Update data  
- **DELETE** → Delete data  

**Example:**

```python
from flask import request, jsonify

@app.route("/users", methods=["GET", "POST"])
def users():
    if request.method == "GET":
        return jsonify({"users": ["Alice", "Bob"]})
    elif request.method == "POST":
        data = request.get_json()
        return jsonify({"message": f"User {data['name']} created"})
```

# 3. Templates (Jinja2)

**Definition:** Jinja2 allows dynamic HTML rendering  

**Steps:**  
1. Create `templates/` folder  
2. Add HTML files with placeholders  

**Example (`templates/home.html`):**  
```html
<h1>Hello, {{ name }}!</h1>
```

## Render Template in Flask

```python
from flask import render_template

@app.route("/welcome/<name>")
def welcome(name):
    return render_template("home.html", name=name)
```

## Template Features (Jinja2)

- **Variables:** `{{ variable }}`  
- **Control statements:** `{% if %}`, `{% for %}`  

**Example:**
```html
{% for user in users %}
    <p>{{ user }}</p>
{% endfor %}
```

## 4. REST APIs

**Definition**: REST → Representational State Transfer

### Principles
- Stateless  
- Use HTTP methods  
- Resources are identified via URLs  

### Flask REST API Example

```python
from flask import Flask, jsonify, request

app = Flask(__name__)
users = []

@app.route("/api/users", methods=["GET"])
def get_users():
    return jsonify(users)

@app.route("/api/users", methods=["POST"])
def add_user():
    data = request.get_json()
    users.append(data)
    return jsonify({"message": "User added"}), 201
```

## 5. Middleware

**Definition**: Functions that run before or after requests for logging, authentication, or modification.

### Example
```python
@app.before_request
def before_request_func():
    print(f"Request to {request.path}")

@app.after_request
def after_request_func(response):
    print("Request completed")
    return response
```

## Use Cases

- Logging requests  
- Checking authentication tokens  
- Modifying response headers  

---

## Why Important

- **Flask**: Quick backend prototype, lightweight APIs  
- **Routes & HTTP Methods**: Handle web requests efficiently  
- **Templates (Jinja2)**: Dynamically render web pages  
- **REST APIs**: Enable frontend-backend communication  
- **Middleware**: Pre/post processing → logging, security, performance  

---

## ✅ Practice Examples

- Create a Flask app with routes `/home`, `/about`  
- Build a REST API for students (`GET`, `POST`, `PUT`, `DELETE`)  
- Render a template showing a list of users using Jinja2  
- Add a middleware to log all requests with method and URL  
- Combine Flask + REST API + template rendering in one project  
