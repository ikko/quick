Here is a **comprehensive Flask cheatsheet** summarizing the key elements of Flask, a lightweight and powerful Python web framework.

---

## **1. Installation**
```bash
# Install Flask
pip install Flask

# Verify installation
python -c "import flask; print(flask.__version__)"
```

---

## **2. Basic Flask App**
```python
from flask import Flask

app = Flask(__name__)  # Initialize the app

@app.route("/")        # Route for the root URL
def home():
    return "Hello, Flask!"

if __name__ == "__main__":
    app.run(debug=True)  # Start the server with debugging enabled
```

- **Run the app**:
    ```bash
    python app.py
    ```
- Access the app at `http://127.0.0.1:5000`.

---

## **3. Routing**
Define routes and HTTP methods:

```python
@app.route("/hello")
def hello():
    return "Hello, World!"

# Route with dynamic parameters
@app.route("/user/<username>")
def show_user_profile(username):
    return f"User: {username}"

# Route accepting multiple HTTP methods
@app.route("/post", methods=["GET", "POST"])
def handle_post():
    if request.method == "POST":
        return "Post Request!"
    return "Get Request!"
```

---

## **4. Request Object**
Access data sent to the server.

```python
from flask import request

@app.route("/data", methods=["POST"])
def data():
    # Get form data
    name = request.form.get("name")

    # Get JSON data
    json_data = request.get_json()

    # Query Parameters
    page = request.args.get("page", default=1, type=int)

    return f"Form: {name}, JSON: {json_data}, Query Page: {page}"
```

---

## **5. Response and Status Codes**
Customize HTTP responses:

```python
from flask import Response, jsonify

@app.route("/response")
def custom_response():
    return Response("Custom Response", status=202)

@app.route("/json")
def json_response():
    data = {"name": "Flask", "status": "success"}
    return jsonify(data), 200  # jsonify automatically sets Content-Type: application/json
```

---

## **6. Templates with Jinja2**
Flask uses Jinja2 for templating.

### **Folder Structure**
```
app.py
templates/
    index.html
```

### **Render Template**
```python
from flask import render_template

@app.route("/")
def index():
    return render_template("index.html", name="Flask")
```

### **Jinja2 Syntax**
```html
<!-- templates/index.html -->
<!DOCTYPE html>
<html>
<head><title>Flask App</title></head>
<body>
    <h1>Welcome, {{ name }}!</h1>  <!-- Variable -->
    {% if name == "Flask" %}       <!-- Conditional -->
        <p>This is a Flask App.</p>
    {% endif %}
</body>
</html>
```

---

## **7. Static Files**
Serve static files like CSS, JavaScript, and images.

### **Folder Structure**
```
static/
    style.css
```

### **Usage in Template**
```html
<link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
```

---

## **8. Sessions and Cookies**
Manage user sessions and cookies.

```python
from flask import session, redirect, url_for

app.secret_key = "supersecretkey"  # Required for session

@app.route("/login/<user>")
def login(user):
    session["username"] = user
    return redirect(url_for("profile"))

@app.route("/profile")
def profile():
    user = session.get("username", "Guest")
    return f"Welcome, {user}!"

@app.route("/logout")
def logout():
    session.pop("username", None)
    return "Logged out!"
```

---

## **9. Redirects and Errors**
### **Redirect**
```python
from flask import redirect, url_for

@app.route("/old-url")
def old_url():
    return redirect(url_for("new_url"))

@app.route("/new-url")
def new_url():
    return "You've been redirected!"
```

### **Error Handling**
```python
@app.errorhandler(404)
def page_not_found(error):
    return "This page doesn't exist!", 404
```

---

## **10. Flask CLI Commands**
```bash
# Run the Flask app
flask run

# Set environment variables
export FLASK_APP=app.py
export FLASK_ENV=development
```

---

## **11. Blueprints**
Organize the app into multiple modules.

### **Folder Structure**
```
project/
    app.py
    blueprints/
        __init__.py
        user.py
```

### **Blueprint Example**
**blueprints/user.py**
```python
from flask import Blueprint

user_bp = Blueprint("user", __name__)

@user_bp.route("/user/<name>")
def user_profile(name):
    return f"User: {name}"
```

**app.py**
```python
from flask import Flask
from blueprints.user import user_bp

app = Flask(__name__)
app.register_blueprint(user_bp)

if __name__ == "__main__":
    app.run(debug=True)
```

---

## **12. Database Integration (Flask-SQLAlchemy)**
### **Install**
```bash
pip install Flask-SQLAlchemy
```

### **Example**
```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config["SQLALCHEMY_DATABASE_URI"] = "sqlite:///site.db"
db = SQLAlchemy(app)

# Define a model
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(80), unique=True, nullable=False)

# Create the database
with app.app_context():
    db.create_all()

# Route to add a user
@app.route("/add/<username>")
def add_user(username):
    user = User(username=username)
    db.session.add(user)
    db.session.commit()
    return f"Added {username}"
```

---

## **13. Middleware and Hooks**
### **Before/After Request Hooks**
```python
@app.before_request
def before_request_func():
    print("This runs before every request!")

@app.after_request
def after_request_func(response):
    print("This runs after every request!")
    return response
```

---

## **14. Testing Flask Apps**
```python
import unittest
from app import app

class FlaskTestCase(unittest.TestCase):
    def setUp(self):
        self.app = app.test_client()

    def test_home(self):
        response = self.app.get("/")
        self.assertEqual(response.status_code, 200)
        self.assertIn(b"Hello", response.data)

if __name__ == "__main__":
    unittest.main()
```

---

## **15. Flask Extensions**
| **Extension**       | **Purpose**                         | **Install Command**         |
|----------------------|-------------------------------------|-----------------------------|
| Flask-SQLAlchemy     | Database ORM                       | `pip install Flask-SQLAlchemy` |
| Flask-Migrate        | Database migrations                | `pip install Flask-Migrate` |
| Flask-WTF            | Forms support                      | `pip install Flask-WTF`     |
| Flask-Login          | User authentication                | `pip install Flask-Login`   |
| Flask-RESTful        | Build REST APIs                    | `pip install Flask-RESTful` |
| Flask-Mail           | Send emails                        | `pip install Flask-Mail`    |

---

## **16. Debugging Tips**
- Enable Debug Mode: `app.run(debug=True)`
- Use Flask Debug Toolbar:
    ```bash
    pip install flask-debugtoolbar
    ```
    ```python
    from flask_debugtoolbar import DebugToolbarExtension
    app.debug = True
    toolbar = DebugToolbarExtension(app)
    ```

---

## **17. Deployment**
For production:
- Use a production-ready server like **Gunicorn**.
```bash
pip install gunicorn
gunicorn app:app
```

---

This cheatsheet provides a quick reference for Flask development.
