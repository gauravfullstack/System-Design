

# 🌐 What is a REST API?

### 1. Definition
A **REST API (Representational State Transfer)** is an architectural style for designing **web services** that allow systems to communicate over **HTTP** using standard operations like `GET`, `POST`, `PUT`, and `DELETE`.

It allows **clients (like browsers, mobile apps)** to talk to **servers** and exchange data in a **stateless**, scalable, and uniform way.

---

### 2. Real-World Analogy 🧠  
Think of a REST API like a **restaurant menu**:
- You (the client) order something using a menu (API endpoint).
- The waiter (HTTP request) sends your order to the kitchen (server).
- The kitchen prepares it and sends it back (response).

---

# ❓ Why REST API?

### 🔹 Key Benefits
| Benefit                  | Explanation |
|--------------------------|-------------|
| 🔁 **Stateless**          | Each request is independent (no session stored on server) |
| ♻️ **Cacheable**         | Responses can be cached for performance |
| 🔧 **Uniform Interface** | Standard HTTP methods make it easy to understand |
| 🌍 **Scalable**          | Statelessness helps with horizontal scaling |
| 🧩 **Platform Agnostic** | Can be used with any frontend (React, iOS, Android) |

---

# 🧱 Building Blocks of a REST API

---

## 1. 🔗 URL (Uniform Resource Locator)
- Identifies the **resource** on the server.
- Example:  
  `/api/users/123` → Refers to user with ID = 123.

✅ Always use **nouns**, not verbs, in REST URLs.

| Action        | URL Example            |
|---------------|------------------------|
| Get all users | `GET /api/users`       |
| Get one user  | `GET /api/users/123`   |
| Create user   | `POST /api/users`      |
| Update user   | `PUT /api/users/123`   |
| Delete user   | `DELETE /api/users/123`|

---

## 2. 📮 HTTP Methods (Verbs)
| Method  | Purpose                  | Idempotent? | Example                    |
|---------|--------------------------|-------------|----------------------------|
| `GET`   | Fetch data               | ✅ Yes      | Get list of users          |
| `POST`  | Create new data          | ❌ No       | Add new user               |
| `PUT`   | Update/replace data      | ✅ Yes      | Replace entire user info   |
| `PATCH` | Partially update data    | ❌ No       | Update user's name         |
| `DELETE`| Delete data              | ✅ Yes      | Remove a user              |

---

## 3. 📬 Headers
- Metadata sent with request/response.
- Common Headers:
  - `Content-Type`: Tells the format (e.g., `application/json`)
  - `Authorization`: Token for secure API calls
  - `Accept`: Format expected in response

```http
GET /api/users HTTP/1.1  
Host: example.com  
Authorization: Bearer <token>  
Accept: application/json  
```

---

## 4. 📨 Request
- Data sent **to** the server (in body or query).
- Example:
```json
POST /api/users  
Body:  
{
  "name": "Gaurav",
  "email": "gaurav@example.com"
}
```

---

## 5. 📤 Response
- Data sent **from** the server back to the client.
- Includes body + headers + status code.
```json
{
  "id": 123,
  "name": "Gaurav",
  "email": "gaurav@example.com"
}
```

---

## 6. 🧾 Status Codes
| Code | Meaning              | Description                        |
|------|----------------------|------------------------------------|
| 200  | OK                   | Successful GET/PUT/DELETE          |
| 201  | Created              | Successful POST                    |
| 204  | No Content           | Success but no data (e.g., DELETE) |
| 400  | Bad Request          | Client-side error (invalid data)   |
| 401  | Unauthorized         | Missing or invalid auth token      |
| 403  | Forbidden            | No permission                      |
| 404  | Not Found            | Resource doesn't exist             |
| 500  | Internal Server Error| Server crashed                     |

---
