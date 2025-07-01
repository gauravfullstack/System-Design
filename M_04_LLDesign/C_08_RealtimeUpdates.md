# 🔄 LLD Chapter: **Real-Time Updates (Polling vs WebSockets)**

> Learn how to keep your UI **synced** with backend changes in real time — using **Polling** and **WebSockets**, including when and how to choose each.

---

## ✅ Functional Requirements

| Requirement                 | Example Use Case                           |
| --------------------------- | ------------------------------------------ |
| Live data sync              | Chat, Stock Prices, Notifications          |
| Auto-update without refresh | New comment, likes, reactions in real time |
| Handle user inactivity      | Pause updates if tab is inactive           |
| Network resilience          | Reconnect or fall back if WebSocket fails  |

---

## 1️⃣ Short Polling

### 🔧 Concept

> Client sends an HTTP request at a **fixed interval** to check for updates.

### 🛠 Implementation

```ts
// Poll every 5 seconds
useEffect(() => {
  const interval = setInterval(() => {
    fetch("/api/notifications").then(res => res.json()).then(setData);
  }, 5000);

  return () => clearInterval(interval);
}, []);
```

### ✅ Pros

* Simple to implement
* Works over HTTPS (firewall friendly)
* Easy fallback option

### ❌ Cons

* Not real-time (5s delay = 5s lag)
* Wasted requests if no data changes
* Harder on backend and network

---

## 2️⃣ Long Polling

### 🔧 Concept

> Client sends a request and the **server holds it open** until new data is available.

### 🛠 Implementation (Conceptual)

```ts
const getUpdates = async () => {
  const res = await fetch("/api/long-poll");
  const data = await res.json();
  setData(data);
  getUpdates(); // Keep polling
};

useEffect(() => {
  getUpdates();
}, []);
```

### ✅ Pros

* More real-time than short polling
* Better resource usage (no polling when no changes)

### ❌ Cons

* Still not as fast or efficient as sockets
* Complex backend logic needed

---

## 3️⃣ WebSockets (Preferred for True Real-Time)

### 🔧 Concept

> Full-duplex connection between client and server (persistent open channel).

### 🛠 Client Setup

```ts
useEffect(() => {
  const socket = new WebSocket("wss://your-server.com");

  socket.onmessage = (event) => {
    const message = JSON.parse(event.data);
    setData(message);
  };

  return () => socket.close();
}, []);
```

### ✅ Pros

* **True real-time** (instant)
* Lower bandwidth usage
* Ideal for chat, live dashboards, multiplayer games

### ❌ Cons

* Requires WS support on backend
* Can break with proxies/firewalls
* Reconnect logic needs to be handled

---

## 🔁 Fallback Strategy: Hybrid Model

```ts
if ("WebSocket" in window) {
  useWebSocket();
} else {
  useLongPolling(); // fallback
}
```

---

## 📦 Folder Structure

```
/components/realtime
  usePolling.ts
  useWebSocket.ts
  RealtimeFeed.tsx
```

---

## 📊 Comparison Table

| Feature         | Short Polling | Long Polling | WebSocket  |
| --------------- | ------------- | ------------ | ---------- |
| Real-time       | ❌             | ⚠️           | ✅          |
| Complexity      | 🟢 Low        | 🟡 Medium    | 🔴 High    |
| Network Usage   | 🔴 High       | 🟡 Medium    | 🟢 Low     |
| Mobile Friendly | ✅             | ✅            | ⚠️ Depends |
| SEO             | ❌             | ❌            | ❌          |

---

## 🧠 Interview Discussion Points

* How would you build a real-time stock feed?
* What happens if the socket fails?
* How do you ensure socket connection is not spammed on tab changes?
* Where would you persist socket state? (e.g., React Context, global service, Zustand)

---

## 🧪 Best Practices

* ✅ Debounce UI updates if server sends too frequently
* ✅ Use `navigator.onLine` to pause/resume updates
* ✅ Add exponential backoff on retries
* ✅ Avoid memory leaks by closing sockets on unmount

---
