# How Web Applications Work

## What is a Web Application?

A web application is software that runs on a server  
and is accessed through a web browser over the internet.

Examples:
- Online banking
- E-commerce websites
- Social media platforms
- SaaS dashboards

---

# Basic Components

## 1. Client (Frontend)

Runs in the user’s browser.

Technologies:
- HTML (structure)
- CSS (style)
- JavaScript (logic)

Responsibilities:
- Display UI
- Send requests to server
- Render responses

---

## 2. Server (Backend)

Processes requests and returns responses.

Common backend technologies:
- Node.js
- Python (Django, Flask)
- PHP
- Java (Spring)
- .NET

Responsibilities:
- Business logic
- Authentication
- Database access
- Authorization

---

## 3. Database

Stores application data.

Examples:
- MySQL
- PostgreSQL
- MongoDB

Stores:
- User accounts
- Password hashes
- Orders
- Logs
- Content

---

# How a Request Works (Step-by-Step)

Example: User logs into a website.

1. User enters credentials in browser.
2. Browser sends HTTP request to server.
3. Server validates credentials.
4. Server queries database.
5. Server returns response.
6. Browser displays result.

---

# HTTP Basics

HTTP = HyperText Transfer Protocol

Main request methods:
- GET → Retrieve data
- POST → Send data
- PUT → Update data
- DELETE → Remove data

HTTP contains:
- Headers
- Body
- Status code (200, 404, 500, etc.)

---

# What Happens When You Type a URL?

Example: https://example.com

1. DNS resolves domain to IP address.
2. Browser establishes TCP connection.
3. TLS handshake (if HTTPS).
4. HTTP request is sent.
5. Server responds with HTML.
6. Browser loads additional resources (CSS, JS, images).

---

# Sessions & Authentication

After login:

- Server creates session
- Session ID stored in cookie
- Cookie sent automatically with each request

Alternative:
- JWT (JSON Web Token)

Purpose:
- Maintain user identity between requests

---

# APIs

Modern web apps use APIs.

API:
- Allows frontend and backend to communicate
- Often uses JSON format
- May be REST-based

Example:
Frontend sends:
POST /api/login

Server responds:
{
  "token": "abc123"
}

---

# Common Architecture

## 1. Monolithic
Frontend + backend tightly integrated.

## 2. Microservices
Application split into multiple services.

## 3. Three-Tier Architecture
- Presentation layer
- Application layer
- Data layer

---

# Security Considerations

Attack surface includes:
- User input fields
- Authentication system
- API endpoints
- File uploads
- Third-party integrations

Common risks:
- Injection
- Broken access control
- XSS
- Misconfiguration

---

# Key Takeaway

Web applications work by:

Browser → HTTP request → Server → Database → Response → Browser

Understanding this flow is essential for:
- Web security
- AppSec
- Blue team investigations
- Secure coding