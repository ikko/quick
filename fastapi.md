Here's a **comprehensive FastAPI and FastAPI-Utils cheatsheet** for building APIs quickly and efficiently with FastAPI, including its common features, tools, and integrations with `fastapi-utils`.

---

# 🚀 **FastAPI & FastAPI-Utils Cheatsheet**

## **1. Setup and Installation**

### Install FastAPI and Uvicorn (ASGI server)
```bash
pip install fastapi uvicorn
```

### Install FastAPI-Utils (Utility Library)
```bash
pip install fastapi-utils
```

---

## **2. Quick Start: Hello World**

### Basic FastAPI Application
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"Hello": "World"}
```

### Run the App
```bash
uvicorn main:app --reload
```
- **`main`**: Python filename without `.py`
- **`app`**: FastAPI instance
- **`--reload`**: Enables auto-reloading in development

---

## **3. Path Parameters and Query Parameters**

### Path Parameters
```python
@app.get("/items/{item_id}")
def read_item(item_id: int, q: str = None):
    return {"item_id": item_id, "query": q}
```

### Query Parameters
```python
@app.get("/items/")
def read_items(skip: int = 0, limit: int = 10):
    return {"skip": skip, "limit": limit}
```

---

## **4. Request Body**

### Using Pydantic Models
```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    description: str = None
    price: float
    tax: float = None

@app.post("/items/")
def create_item(item: Item):
    return {"item": item}
```

### Update Operations
```python
@app.put("/items/{item_id}")
def update_item(item_id: int, item: Item):
    return {"item_id": item_id, "updated_item": item}
```

---

## **5. Response Models**

### Define Response Schema
```python
from typing import List

@app.get("/items/", response_model=List[Item])
def read_items():
    return [{"name": "Item 1", "price": 10.0}]
```

---

## **6. Request Validation**

### Query Parameter Validation
```python
@app.get("/items/")
def read_items(q: str = None, limit: int = 10):
    return {"q": q, "limit": limit}
```

### Field Validation with Pydantic
```python
from pydantic import BaseModel, Field

class Item(BaseModel):
    name: str = Field(..., min_length=2)
    price: float = Field(..., gt=0, description="Price must be greater than zero")

@app.post("/items/")
def create_item(item: Item):
    return {"item": item}
```

---

## **7. Dependency Injection**

### Basic Dependencies
```python
from fastapi import Depends

def common_parameters(q: str = None):
    return {"q": q}

@app.get("/items/")
def read_items(commons: dict = Depends(common_parameters)):
    return commons
```

---

## **8. Middleware**

### Adding Custom Middleware
```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],  # Allow all origins
    allow_credentials=True,
    allow_methods=["*"],  # Allow all methods
    allow_headers=["*"],  # Allow all headers
)
```

---

## **9. Background Tasks**

### Running Tasks in the Background
```python
from fastapi import BackgroundTasks

def write_log(message: str):
    with open("log.txt", "a") as f:
        f.write(message)

@app.post("/send-notification/")
def send_notification(message: str, background_tasks: BackgroundTasks):
    background_tasks.add_task(write_log, f"Message: {message}\n")
    return {"message": "Notification sent"}
```

---

## **10. FastAPI Utils**

### **`asynchronous_tasks`** - Background Tasks with FastAPI-Utils
```python
from fastapi_utils.tasks import repeat_every

@app.on_event("startup")
@repeat_every(seconds=10)  # Repeat every 10 seconds
def periodic_task():
    print("This task runs every 10 seconds!")
```

---

### **`CRUDRouter`** - Automatic CRUD Routers

Install required dependencies:
```bash
pip install fastapi-utils SQLAlchemy
```

**Example: Generate CRUD endpoints for a database model**
```python
from fastapi import FastAPI
from fastapi_utils.cbv import cbv
from fastapi_utils.inferring_router import InferringRouter
from pydantic import BaseModel
from typing import List

app = FastAPI()
router = InferringRouter()

# Fake Database
fake_db = []

class Item(BaseModel):
    id: int
    name: str
    price: float

@cbv(router)
class ItemAPI:
    @router.get("/", response_model=List[Item])
    def get_items(self):
        return fake_db

    @router.post("/", response_model=Item)
    def create_item(self, item: Item):
        fake_db.append(item)
        return item

app.include_router(router, prefix="/items")
```

---

### **`repeat_every`** - Periodic Background Tasks
```python
from fastapi_utils.tasks import repeat_every

@app.on_event("startup")
@repeat_every(seconds=60)  # Task runs every 60 seconds
def scheduled_task():
    print("Running scheduled task!")
```

---

## **11. Error Handling**

### Custom Exception Handling
```python
from fastapi import HTTPException

@app.get("/items/{item_id}")
def read_item(item_id: int):
    if item_id == 0:
        raise HTTPException(status_code=404, detail="Item not found")
    return {"item_id": item_id}
```

### Custom Exception Class
```python
from fastapi.responses import JSONResponse

class ItemException(Exception):
    def __init__(self, message: str):
        self.message = message

@app.exception_handler(ItemException)
def custom_exception_handler(request, exc: ItemException):
    return JSONResponse(status_code=400, content={"detail": exc.message})

@app.get("/items/")
def raise_exception():
    raise ItemException("This is a custom exception")
```

---

## **12. Authentication**

### OAuth2 with Password Flow
```python
from fastapi.security import OAuth2PasswordBearer

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

@app.get("/items/")
def read_items(token: str = Depends(oauth2_scheme)):
    return {"token": token}
```

---

## **13. Testing with FastAPI**

### Using `TestClient` for Testing
```python
from fastapi.testclient import TestClient

client = TestClient(app)

def test_read_root():
    response = client.get("/")
    assert response.status_code == 200
    assert response.json() == {"Hello": "World"}
```

---

## **14. Static Files**

### Serve Static Files
```python
from fastapi.staticfiles import StaticFiles

app.mount("/static", StaticFiles(directory="static"), name="static")
```

Place files in a `static` folder and access them at `/static/filename`.

---

## **15. Templates (Jinja2 Integration)**

### Setup Templates
```python
from fastapi.templating import Jinja2Templates
from fastapi import Request

templates = Jinja2Templates(directory="templates")

@app.get("/")
def home(request: Request):
    return templates.TemplateResponse("index.html", {"request": request, "name": "FastAPI"})
```

---

## **16. Final Notes**

- **FastAPI** is ideal for modern, fast, and type-safe API development.
- **FastAPI-Utils** simplifies background tasks, CRUD generation, and scheduled tasks.
- Use **`uvicorn`** with `--reload` for development and production-ready servers like `gunicorn` or `hypercorn`.

### 📚 Resources:
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [FastAPI-Utils GitHub](https://github.com/dmontagu/fastapi-utils)

---

This cheatsheet provides a **complete reference** for building and scaling APIs with FastAPI and using FastAPI-Utils for utility tasks like background jobs, scheduling, and automatic CRUD creation. 🚀