# 📰 News Aggregator API with Spring Boot

A secure, extensible, and asynchronous **RESTful API** built using **Spring Boot**, that enables users to register, log in, manage their news preferences, and fetch news from external APIs like **NewsAPI.org**. This application supports JWT-based authentication, caching, keyword search, and marking articles as read/favorite.

---

## 📌 Features

### ✅ Core Functionality
- 🔐 **JWT Authentication** with Spring Security
- 🧾 **User Registration & Login**
- ⚙️ **User-specific News Preferences** (language, region, category)
- 🗞️ **News Fetching** from external news APIs using `WebClient`
- 🛡️ **Robust Exception Handling & Input Validation**
- 🧪 **Tested via Postman and cURL**

### 🚀 Optional Extensions Implemented
- ⚡ **Caching** of news responses using **Caffeine Cache**
- ⭐ Mark news articles as **Read** or **Favorite**
- 🔍 **Search** news by keyword
- ⏱️ **Scheduled Background Cache Refreshing** using Spring Scheduler

---

## 📁 Technologies Used

| Layer        | Tech Stack                             |
|--------------|----------------------------------------|
| Backend      | Spring Boot, Spring Web, Spring Security |
| Auth         | JWT (JSON Web Token)                   |
| Database     | H2 (In-memory)                         |
| HTTP Client  | WebClient (Reactive)                   |
| Caching      | Caffeine Cache                         |
| Build Tool   | Maven                                  |

---

## 🔐 Authentication Flow

1. Register a user via `/api/register`
2. Login using `/api/login` → Get JWT token
3. Use this token as a Bearer token in the `Authorization` header for all secured endpoints.

---

## 📨 API Endpoints

### 🔑 Authentication
| Method | Endpoint         | Description                |
|--------|------------------|----------------------------|
| POST   | `/api/register`  | Register a new user        |
| POST   | `/api/login`     | Login and receive JWT token|

---

### ⚙️ User Preferences
| Method | Endpoint            | Description                      |
|--------|---------------------|----------------------------------|
| GET    | `/api/preferences`  | Get user’s news preferences      |
| PUT    | `/api/preferences`  | Update user’s news preferences   |

---

### 🗞️ News
| Method | Endpoint                  | Description                           |
|--------|---------------------------|---------------------------------------|
| GET    | `/api/news`               | Get news based on preferences         |
| GET    | `/api/news/search/{kw}`   | Search for news by keyword            |

---

### ⭐ Favorites & Read Articles
| Method | Endpoint                       | Description                     |
|--------|--------------------------------|---------------------------------|
| POST   | `/api/news/{id}/read`          | Mark article as read            |
| POST   | `/api/news/{id}/favorite`      | Mark article as favorite        |
| GET    | `/api/news/read`               | Get all read articles           |
| GET    | `/api/news/favorites`          | Get all favorite articles       |

---

## 🔁 Background Scheduler
- A Spring scheduler updates the cached articles **periodically** (configurable via `@Scheduled`) to keep news fresh while minimizing API calls.

---

## 🔐 Security & Validation
- Passwords are encrypted using `BCrypt`
- JWT tokens are required for accessing secure routes
- Request bodies are validated using:
    - `@NotNull`
    - `@Email`
    - `@Size`

---

## ⚙️ Configuration

### `application.properties`
```properties
# JWT Config
jwt.secret=your_secret_key
jwt.expiration=3600000

# NewsAPI Key
newsapi.key=a836c8875eeb48d597ff649a874a249c
