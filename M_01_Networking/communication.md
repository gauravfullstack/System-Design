

# 🖥️ How the Web Works

### 1. Overview
The web is a system where **clients** (like browsers) and **servers** communicate over a **network** (like the Internet) to exchange data, mainly using protocols like **HTTP**.

At a high level:
- You type a URL → Browser sends a **request** → Server processes it → Server sends back a **response** → Browser displays the webpage.

---

### 2. Step-by-Step Process
1. **You enter a URL** (e.g., `www.google.com`) in your browser.
2. **DNS (Domain Name System)** translates the domain name into an **IP address**.
3. **Browser initiates a TCP connection** to the server's IP address.
4. **HTTP/HTTPS Request** is sent from your browser to the server.
5. **Server processes** the request (e.g., fetch data, render HTML).
6. **Server sends a Response** (HTML, CSS, JS, JSON, etc.).
7. **Browser renders the page** using the received data.
8. **Subsequent requests** for assets (images, CSS, JS) are made as needed.

---

### 3. Important Components
| Component            | Role                                          |
|----------------------|-----------------------------------------------|
| Browser              | Acts as client, sends HTTP requests           |
| Server               | Processes requests and sends responses       |
| DNS Server           | Resolves domain names to IP addresses         |
| TCP/IP               | Protocols that ensure data is sent reliably   |
| HTTP/HTTPS           | Defines rules for communication               |

---

# 🌐 Types of Protocols

---

## 1. HTTP (HyperText Transfer Protocol)
- A **stateless** protocol for **request-response** communication.
- Used mainly for loading web pages.
- Works over **TCP**.
- Example:  
  `GET /index.html` → Returns a webpage.

---

## 2. HTTP/3
- Next-generation HTTP built on **QUIC protocol** instead of TCP.
- **Faster connection setup** and **better handling of network changes** (e.g., switching from Wi-Fi to mobile data).
- Solves problems like **head-of-line blocking** in TCP.
- Example use: Modern browsers like Chrome use HTTP/3 with some websites.

---

## 3. HTTPS (HTTP Secure)
- HTTP + **TLS/SSL Encryption** = Secure Communication.
- Data is **encrypted** (confidentiality) and **integrity-verified**.
- Widely used for websites handling sensitive information (e.g., banking, shopping).
- Example: `https://www.amazon.com`

---

## 4. WebSocket
- **Full-duplex** communication — server and client can send messages **anytime**.
- Persistent open connection.
- Used for real-time apps: **chat apps**, **gaming**, **stock trading apps**.
- Example: WhatsApp Web uses WebSockets for live messaging.

---

## 5. TCP (Transmission Control Protocol)
- Reliable, **connection-oriented** communication.
- Ensures **data is received correctly and in order**.
- Used by HTTP, HTTPS, FTP, etc.
- Example: Downloading a file without corruption.

---

## 6. UDP (User Datagram Protocol)
- **Connectionless** communication.
- **Faster**, but **no guarantee** of delivery or order.
- Used for real-time apps where speed matters more than reliability (e.g., video calls, gaming).
- Example: Zoom call packets.

---

## 7. SMTP (Simple Mail Transfer Protocol)
- Used for **sending emails**.
- Push protocol — sends emails from client to email server.
- Example: Sending a message from Gmail.

---

## 8. FTP (File Transfer Protocol)
- Protocol to **transfer files** between client and server.
- Can use authentication (username, password).
- Not secure by default (use SFTP for secure transfer).
- Example: Uploading a website's files to a web server.

---

# ⚡ Summary (1-Liners)
- **Web** = Browser ↔ Server Communication via Internet.
- **HTTP** = Stateless protocol to fetch web content.
- **HTTP/3** = Faster HTTP using QUIC.
- **HTTPS** = Secure, encrypted HTTP.
- **WebSocket** = Real-time, two-way communication.
- **TCP** = Reliable, ordered delivery.
- **UDP** = Fast, unordered delivery.
- **SMTP** = Send emails.
- **FTP** = Transfer files.

---
