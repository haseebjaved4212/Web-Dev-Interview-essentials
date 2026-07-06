<div align="center">

# ⚡ FastAPI Interview Essentials

![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Level](https://img.shields.io/badge/Level-Beginner%20to%20Intermediate-brightgreen?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Interview%20Ready-blue?style=for-the-badge)

**A simple, beginner-friendly guide to crack FastAPI interviews with confidence**

</div>

---

## 📖 Table of Contents

1. [What is FastAPI](#-what-is-fastapi)
2. [FastAPI vs Flask vs Django](#-fastapi-vs-flask-vs-django)
3. [Installing and First App](#-installing-and-first-app)
4. [Path and Query Parameters](#-path-and-query-parameters)
5. [Request Body with Pydantic](#-request-body-with-pydantic)
6. [Response Models](#-response-models)
7. [Data Validation](#-data-validation)
8. [Async and Sync Endpoints](#-async-and-sync-endpoints)
9. [Dependency Injection](#-dependency-injection)
10. [Path Operations and HTTP Methods](#-path-operations-and-http-methods)
11. [Automatic Docs (Swagger and ReDoc)](#-automatic-docs-swagger-and-redoc)
12. [Project Structure](#-project-structure)
13. [Routers (like Blueprints)](#-routers-like-blueprints)
14. [Database Integration (SQLAlchemy)](#-database-integration-sqlalchemy)
15. [Authentication (OAuth2 and JWT)](#-authentication-oauth2-and-jwt)
16. [Middleware](#-middleware)
17. [Error Handling](#-error-handling)
18. [Background Tasks](#-background-tasks)
19. [CORS](#-cors)
20. [Testing in FastAPI](#-testing-in-fastapi)
21. [Deployment](#-deployment)
22. [Security Basics](#-security-basics)
23. [Common Interview Questions](#-common-interview-questions-spoken-style-answers)
24. [Quick Cheat Sheet](#-quick-cheat-sheet)

---

## 🚀 What is FastAPI

FastAPI is a modern Python web framework built for creating APIs quickly and with high performance. It is built on top of Starlette for the web parts and Pydantic for data validation. It supports async out of the box, which means it can handle a lot of concurrent requests efficiently.

**Spoken answer:** I would describe FastAPI as a modern, high performance framework made specifically for building APIs. What makes it stand out is that it uses Python type hints to validate data automatically, generates interactive documentation for free, and supports async natively so it scales really well under load.

---

## ⚖️ FastAPI vs Flask vs Django

| Feature | FastAPI | Flask | Django |
|---|---|---|---|
| Async support | Native | Limited | Improving |
| Data validation | Built-in (Pydantic) | Manual or extension | Manual or extension |
| Auto docs | Yes (Swagger, ReDoc) | No | No |
| Performance | Very high | Moderate | Moderate |
| Learning curve | Medium | Easy | Medium |
| Best for | High performance APIs | Small to medium apps | Large full-stack apps |

**Spoken answer:** In my experience, Flask gives simplicity and flexibility, Django gives a complete batteries included package, and FastAPI gives speed along with strong type safety. If I am building an API that needs to handle heavy traffic or needs strict input validation, FastAPI is usually my first choice.

---

## 🏁 Installing and First App

```bash
pip install fastapi uvicorn
```

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def home():
    return {"message": "Hello, FastAPI!"}
```

Run it with:

```bash
uvicorn main:app --reload
```

**Spoken answer:** To get started, I create a FastAPI instance and define endpoints using decorators like `@app.get`. Since FastAPI does not come with its own server, I run it using Uvicorn, which is an ASGI server. The `--reload` flag is handy during development because it restarts the server automatically when I save changes.

---

## 🛣️ Path and Query Parameters

```python
@app.get("/users/{user_id}")
def get_user(user_id: int):
    return {"user_id": user_id}

@app.get("/items")
def list_items(skip: int = 0, limit: int = 10):
    return {"skip": skip, "limit": limit}
```

**Spoken answer:** Path parameters come directly from the URL, like the user id in the example above, and query parameters come after the question mark in the URL. The nice part is that just by adding a type hint like `int`, FastAPI validates the input and converts it automatically. If someone sends text instead of a number, it returns a clear validation error on its own.

---

## 📦 Request Body with Pydantic

```python
from pydantic import BaseModel

class User(BaseModel):
    name: str
    age: int
    email: str

@app.post("/users")
def create_user(user: User):
    return {"name": user.name, "age": user.age}
```

**Spoken answer:** For request bodies, I define a Pydantic model that describes the expected shape of the data. FastAPI reads that model, validates the incoming JSON against it, and gives me a proper Python object to work with. If the data does not match, it automatically returns a 422 error with details about what went wrong.

---

## 🎯 Response Models

```python
class UserOut(BaseModel):
    name: str
    age: int

@app.post("/users", response_model=UserOut)
def create_user(user: User):
    return user
```

**Spoken answer:** A response model lets me control exactly what gets sent back to the client, even if the internal object has more fields, like a password hash. It also helps keep the auto generated documentation accurate, since the response schema is clearly defined.

---

## ✅ Data Validation

```python
from pydantic import BaseModel, Field, EmailStr

class User(BaseModel):
    name: str = Field(..., min_length=2)
    age: int = Field(..., gt=0, lt=120)
    email: EmailStr
```

**Spoken answer:** Validation in FastAPI comes almost for free through Pydantic. I can set constraints like minimum length, value ranges, or even use special types like `EmailStr` to validate an email format, without writing any manual if-else checks myself.

---

## ⏱️ Async and Sync Endpoints

```python
@app.get("/sync-endpoint")
def sync_route():
    return {"type": "sync"}

@app.get("/async-endpoint")
async def async_route():
    return {"type": "async"}
```

**Spoken answer:** FastAPI supports both regular and async functions for endpoints. I use `async def` when I am doing I/O bound work, like calling an external API or querying a database asynchronously, because it lets the server handle other requests while waiting instead of blocking. For simple CPU-bound logic, a normal function works fine too.

---

## 🧩 Dependency Injection

```python
from fastapi import Depends

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

@app.get("/items")
def read_items(db=Depends(get_db)):
    return db.query(Item).all()
```

**Spoken answer:** Dependency injection in FastAPI is done through the `Depends` function. I write a function that provides something, like a database session or the current user, and FastAPI automatically calls it and passes the result into my endpoint. This keeps my code clean and makes things like authentication checks reusable across many routes.

---

## 📮 Path Operations and HTTP Methods

```python
@app.get("/items")
def read_items(): ...

@app.post("/items")
def create_item(): ...

@app.put("/items/{id}")
def update_item(id: int): ...

@app.delete("/items/{id}")
def delete_item(id: int): ...
```

**Spoken answer:** FastAPI gives a dedicated decorator for each HTTP method, so GET, POST, PUT, and DELETE all have their own clear syntax. This makes the code more readable compared to checking `request.method` manually.

---

## 📚 Automatic Docs (Swagger and ReDoc)

Once the app is running, visit:

- `http://localhost:8000/docs` for Swagger UI
- `http://localhost:8000/redoc` for ReDoc

**Spoken answer:** One of my favorite things about FastAPI is that it generates interactive API documentation automatically, based on the type hints and Pydantic models I already wrote. I do not have to maintain separate documentation, and I can even test endpoints directly from the Swagger page.

---

## 🏗️ Project Structure

```
myapp/
├── app/
│   ├── main.py
│   ├── routers/
│   │   └── users.py
│   ├── models.py
│   ├── schemas.py
│   ├── database.py
│   └── dependencies.py
├── requirements.txt
└── .env
```

**Spoken answer:** For a real project, I separate things into routers for endpoints, schemas for Pydantic models, models for database tables, and a dependencies file for shared logic like authentication. This keeps `main.py` clean and just responsible for creating the app and including routers.

---

## 🧭 Routers (like Blueprints)

```python
from fastapi import APIRouter

router = APIRouter(prefix="/users", tags=["users"])

@router.get("/")
def list_users():
    return []

# In main.py
app.include_router(router)
```

**Spoken answer:** Routers in FastAPI work similarly to Blueprints in Flask. Instead of putting every endpoint in one file, I group related routes into their own router with a common prefix and tag, then include that router in the main app. This makes large projects much easier to navigate.

---

## 🗄️ Database Integration (SQLAlchemy)

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker, declarative_base

engine = create_engine("sqlite:///./app.db")
SessionLocal = sessionmaker(bind=engine)
Base = declarative_base()

class User(Base):
    __tablename__ = "users"
    id = Column(Integer, primary_key=True)
    name = Column(String)
```

**Spoken answer:** FastAPI does not include its own ORM, so I usually pair it with SQLAlchemy. I define models as Python classes that map to database tables, then use a dependency to provide a database session to each request, and close it once the request finishes.

---

## 🔐 Authentication (OAuth2 and JWT)

```python
from fastapi.security import OAuth2PasswordBearer
from jose import jwt

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

@app.get("/profile")
def profile(token: str = Depends(oauth2_scheme)):
    payload = jwt.decode(token, "secret", algorithms=["HS256"])
    return {"user": payload.get("sub")}
```

**Spoken answer:** FastAPI has built-in support for OAuth2 security schemes. A common pattern is to issue a JWT token after login, and then protect routes using a dependency that decodes and verifies the token on every request. This keeps authentication logic in one place instead of repeating it in every endpoint.

---

## 🪝 Middleware

```python
@app.middleware("http")
async def add_process_time(request, call_next):
    response = await call_next(request)
    response.headers["X-Process-Time"] = "fast"
    return response
```

**Spoken answer:** Middleware runs code before and after every request passes through the app. I use it for things like logging request timing, adding custom headers, or handling cross-cutting concerns that should apply to the whole API rather than one specific route.

---

## 🚨 Error Handling

```python
from fastapi import HTTPException

@app.get("/items/{id}")
def get_item(id: int):
    if id not in items:
        raise HTTPException(status_code=404, detail="Item not found")
    return items[id]
```

**Spoken answer:** For expected errors, I raise `HTTPException` with the right status code and a clear message. FastAPI also lets me register custom exception handlers using `@app.exception_handler` if I want a consistent error response format across the whole app.

---

## 🕒 Background Tasks

```python
from fastapi import BackgroundTasks

def send_email(email: str):
    print(f"Sending email to {email}")

@app.post("/signup")
def signup(email: str, background_tasks: BackgroundTasks):
    background_tasks.add_task(send_email, email)
    return {"message": "Signed up"}
```

**Spoken answer:** Background tasks let me run something after sending the response back to the client, like sending a confirmation email. This keeps the API response fast, since the client does not have to wait for that extra work to finish.

---

## 🌍 CORS

```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["https://myfrontend.com"],
    allow_methods=["*"],
    allow_headers=["*"],
)
```

**Spoken answer:** CORS handling in FastAPI is done through a built-in middleware. I specify exactly which origins, methods, and headers are allowed, so a frontend hosted on a different domain can safely call my API.

---

## 🧪 Testing in FastAPI

```python
from fastapi.testclient import TestClient

client = TestClient(app)

def test_home():
    response = client.get("/")
    assert response.status_code == 200
```

**Spoken answer:** FastAPI provides a `TestClient` built on top of the requests library, so I can write tests with pytest that hit my endpoints directly without needing a live server running, which makes the test suite fast and reliable.

---

## 🚀 Deployment

**Spoken answer:** In production, I run FastAPI with Uvicorn, often managed by Gunicorn using Uvicorn workers for better process management, and place it behind Nginx as a reverse proxy. I also make sure debug settings and detailed error messages are turned off before going live.

```bash
gunicorn -k uvicorn.workers.UvicornWorker main:app
```

---

## 🛡️ Security Basics

- Always validate input using Pydantic models, do not trust raw data
- Use OAuth2 with JWT for stateless authentication
- Keep secret keys in environment variables, never hardcode them
- Restrict CORS to trusted origins only
- Use HTTPS in production
- Hash passwords with libraries like `passlib` before storing them

**Spoken answer:** Security in FastAPI mostly comes from using its built-in tools properly. Pydantic handles input validation, OAuth2 utilities handle authentication, and I make sure secrets and origins are configured carefully so the API is not left open to abuse.

---

## 💬 Common Interview Questions (Spoken-Style Answers)

**Q: Why is FastAPI considered fast?**
It's built on Starlette and uses ASGI instead of WSGI, which allows it to handle requests asynchronously. This means the server does not block while waiting for I/O operations like database calls or external API requests, so it can serve more requests at the same time.

**Q: What is the difference between WSGI and ASGI?**
WSGI is synchronous and handles one request at a time per worker, while ASGI supports asynchronous communication, which allows handling many concurrent connections efficiently, including things like WebSockets.

**Q: How does FastAPI validate data automatically?**
It relies on Pydantic models combined with Python type hints. When a request comes in, FastAPI parses the data against the model, and if anything does not match the expected types or constraints, it returns a 422 response with a detailed error message, without me writing any manual validation code.

**Q: What is dependency injection in FastAPI and why is it useful?**
It's a way to share reusable logic, like getting a database session or checking the current user, across multiple endpoints using the `Depends` function. It keeps endpoint functions clean and makes testing easier since dependencies can be overridden.

**Q: Can FastAPI work with Flask style synchronous code?**
Yes, FastAPI supports regular synchronous functions too. Internally it runs them in a thread pool so they do not block the async event loop, which gives flexibility when working with libraries that do not support async.

**Q: How is FastAPI different from Flask in terms of documentation?**
FastAPI generates Swagger and ReDoc documentation automatically from the code itself, based on type hints and Pydantic models, while in Flask I would need an extension and manual work to get something similar.

---

## ⚡ Quick Cheat Sheet

| Concept | Code Snippet |
|---|---|
| Create app | `app = FastAPI()` |
| GET route | `@app.get("/path")` |
| POST route | `@app.post("/path")` |
| Path param | `def route(id: int):` |
| Query param | `def route(skip: int = 0):` |
| Request body | `def route(user: UserModel):` |
| Response model | `@app.post("/", response_model=Out)` |
| Dependency | `Depends(get_db)` |
| Raise error | `raise HTTPException(404, "Not found")` |
| Background task | `background_tasks.add_task(func)` |
| Router | `APIRouter(prefix="/users")` |
| Run server | `uvicorn main:app --reload` |

---

<div align="center">

**Made for interview prep by Haseeb Javed**
Good luck with your FastAPI interviews! 🚀

</div>