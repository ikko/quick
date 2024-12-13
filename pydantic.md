Here’s a **comprehensive Pydantic cheat sheet** to help you navigate its core functionalities for data validation and parsing in Python.

---

# **Pydantic Cheat Sheet**

Pydantic is a **data validation** and **settings management** library that uses Python type hints to validate and parse data efficiently.

---

## **1. Installation**

```bash
pip install pydantic
```

---

## **2. Core Concepts**

### **Data Model Definition**
Pydantic models are created by inheriting from `BaseModel`.

```python
from pydantic import BaseModel

# Define a simple data model
class User(BaseModel):
    id: int
    name: str
    age: int
    email: str

# Instantiate and validate data
user = User(id=1, name="John Doe", age=30, email="john@example.com")
print(user)
```

---

## **3. Validation and Parsing**

### **Automatic Validation**
Pydantic validates input types automatically:

```python
user = User(id="1", name="John Doe", age="30", email="john@example.com")
print(user)  # Automatically converts to correct types
```

### **Validation Error Handling**
Invalid inputs raise `ValidationError`:

```python
from pydantic import ValidationError

try:
    user = User(id="abc", name="John", age="30", email="invalid-email")
except ValidationError as e:
    print(e.json())
```

---

## **4. Default Values and Optional Fields**

### **Default Values**
Set default values for fields:

```python
class User(BaseModel):
    id: int
    name: str
    age: int = 25  # Default value

user = User(id=1, name="Alice")
print(user.age)  # 25
```

### **Optional Fields**
Use `Optional` from `typing` to allow `None`:

```python
from typing import Optional

class User(BaseModel):
    id: int
    name: str
    nickname: Optional[str] = None

user = User(id=1, name="Alice")
print(user.nickname)  # None
```

---

## **5. Field Validation with `Field`**

Use `Field` to add constraints such as min/max values, regex, or descriptions.

```python
from pydantic import BaseModel, Field

class Product(BaseModel):
    name: str
    price: float = Field(..., gt=0, description="Price must be greater than zero")
    description: str = Field(..., max_length=100)

product = Product(name="Book", price=15.99, description="A very nice book")
print(product)
```

**Constraints**:
- `gt`, `ge` → Greater than / Greater than or equal to  
- `lt`, `le` → Less than / Less than or equal to  
- `max_length`, `min_length` → String constraints  
- `regex` → Regex validation  

---

## **6. Custom Validators**

Add custom validation logic using the `@validator` decorator.

```python
from pydantic import BaseModel, validator

class User(BaseModel):
    id: int
    name: str
    email: str

    @validator("email")
    def validate_email(cls, v):
        if "@" not in v:
            raise ValueError("Invalid email format")
        return v

user = User(id=1, name="John", email="john@example.com")
print(user)
```

---

## **7. Nested Models**

Models can include other models as fields.

```python
class Address(BaseModel):
    street: str
    city: str

class User(BaseModel):
    id: int
    name: str
    address: Address

user = User(id=1, name="Alice", address={"street": "123 Main St", "city": "Wonderland"})
print(user)
```

---

## **8. Data Conversion**

### **Model to Dictionary/JSON**
Convert models into dictionaries or JSON:

```python
user_dict = user.dict()
user_json = user.json()

print(user_dict)
print(user_json)
```

### **Parsing Raw Data**
Parse data from JSON or dictionaries:

```python
data = '{"id": 1, "name": "Alice"}'
user = User.parse_raw(data)
print(user)

user_from_dict = User.parse_obj({"id": 2, "name": "Bob"})
print(user_from_dict)
```

---

## **9. Aliases and Export Configuration**

### **Field Aliases**
Map input fields to different names using `alias`.

```python
class User(BaseModel):
    user_id: int = Field(..., alias="id")

data = {"id": 123}
user = User(**data)
print(user)
```

### **Exclude/Include Fields in Export**
Control fields included in `.dict()` or `.json()`:

```python
class User(BaseModel):
    id: int
    name: str
    password: str

user = User(id=1, name="John", password="secret")
print(user.dict(exclude={"password"}))  # Excludes password field
```

---

## **10. Configuring Pydantic Models**

Pydantic models can be customized using the `Config` class.

```python
class User(BaseModel):
    id: int
    name: str

    class Config:
        orm_mode = True  # Enables compatibility with ORMs
        allow_population_by_field_name = True
```

---

## **11. Enums and Custom Types**

### **Using Enums**
Enums ensure a field contains specific values:

```python
from enum import Enum

class Role(str, Enum):
    admin = "admin"
    user = "user"

class User(BaseModel):
    id: int
    role: Role

user = User(id=1, role="admin")
print(user)
```

### **Custom Data Types**
Create custom data types for specific needs:

```python
from pydantic import BaseModel
from typing import NewType

PositiveInt = NewType("PositiveInt", int)

class Product(BaseModel):
    price: PositiveInt
```

---

## **12. Pydantic Settings for Configuration**

Pydantic can manage application settings using environment variables.

```python
from pydantic import BaseSettings

class Settings(BaseSettings):
    app_name: str
    debug: bool = False

    class Config:
        env_file = ".env"  # Reads environment variables from .env file

settings = Settings()
print(settings.app_name)
```

---

## **13. Advanced: Custom Root Types**

Create models with a single root field.

```python
class CustomModel(BaseModel):
    __root__: list[int]

data = CustomModel(__root__=[1, 2, 3])
print(data.__root__)
```

---

## **14. Error Handling**

Pydantic provides rich validation errors in JSON format.

```python
try:
    user = User(id="abc", role="unknown")
except ValidationError as e:
    print(e.errors())
```

---

## **15. Performance: `pydantic` v2 Optimizations**

Pydantic v2 offers significant speedups through stricter validation and better serialization options.

### Key Changes in v2:
- **Strict Types**: Enforce exact types.  
- **Custom JSON Encoders** for performance.  

```python
class User(BaseModel):
    id: int
    name: str

    model_config = {"strict": True}  # Enables strict validation
```

---

This **Pydantic cheat sheet** covers core functionality, validation strategies, model nesting, and common use cases.
