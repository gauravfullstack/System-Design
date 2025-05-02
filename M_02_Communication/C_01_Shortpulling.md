# 🔁 1. **Short Polling** – Beginner Friendly, Practical & Interview-Ready

---

## 🧠 What is Short Polling?

> **Short Polling** is when the client (usually your React app) repeatedly sends a request to the server **at fixed intervals** to check if there’s any new data.

### Example:
```js
setInterval(() => {
  fetch('/api/notifications')
    .then(res => res.json())
    .then(data => console.log(data));
}, 5000); // every 5 seconds
```

---

## 🧪 Real-world Use Case

- A chat app checking for new messages every 5 seconds  
- A stock price tracker pulling updates periodically  
- Checking for OTP status or payment completion  

---

## 🛠️ How It Works

```
Client (React App)
   |
   |--> fetch() every 5 seconds
   |
   |<-- Server responds immediately (with or without new data)
   |
   |--> repeats again after 5s
```

- Request is sent every X seconds, **even if no data has changed**
- Server replies quickly with current data

---

## ❌ Problems With Short Polling

| Issue               | Why It Matters                         |
|---------------------|----------------------------------------|
| Wastes bandwidth    | Makes a request even when no updates   |
| Increases server load | Unnecessary repeated hits            |
| Delayed real-time feel | Updates only come in 5s chunks      |

---

## ✅ When to Use It

| ✅ Good For                              | ❌ Not Ideal For                     |
|-----------------------------------------|-------------------------------------|
| Low-frequency data checks (e.g. alerts) | Real-time apps (e.g. chat, games)   |
| Simple implementation                   | Efficient communication             |

---

## 🧾 Summary – What to Say in an Interview

> “Short polling is a client-side technique where the frontend repeatedly sends requests to the server at fixed intervals to check for updates. It’s easy to implement but not optimal for real-time use cases because it causes extra load even when there’s no new data.”

---
