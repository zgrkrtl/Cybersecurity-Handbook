# IDOR (Insecure Direct Object Reference)

## What is IDOR?

IDOR stands for **Insecure Direct Object Reference**.

It is an access control vulnerability where:
- An application exposes internal object identifiers (IDs)
- The server does not properly verify user authorization
- An attacker manipulates the ID to access unauthorized data

IDOR is a type of Broken Access Control vulnerability.

---

# How It Works (Basic Example)

Example request:

GET /api/user/12345

If the application only checks:
- "Is the user logged in?"

But does NOT check:
- "Does this user own ID 12345?"

Then attacker can try:

GET /api/user/12346  
GET /api/user/12347  

And access other users’ data.

---

# Common Targets

- User profiles
- Invoices
- Orders
- Medical records
- Support tickets
- Private messages
- File downloads

---

# Where IDOR Appears

- REST APIs
- URL parameters
- Hidden form fields
- JSON requests
- File download endpoints

Example vulnerable pattern:

POST /api/order/view
{
  "order_id": 9876
}

If authorization is missing → IDOR.

---

# Impact

- Data exposure
- Privacy violation
- Account takeover (in some cases)
- Modification or deletion of other users’ data

Severity depends on:
- Sensitivity of exposed data
- Ability to modify vs just view

---

# Root Cause

Missing or improper authorization checks.

Common mistake:
Checking authentication (logged in)  
instead of authorization (allowed access).

---

# Detection Clues (Blue Team)

- Sequential ID access patterns
- Same user requesting many different object IDs
- Access to objects not owned by requester
- API requests with manipulated parameters

Example suspicious behavior:
User A accessing 100+ different account IDs in short time.

---

# Prevention

## 1. Enforce Proper Authorization
Always verify:
Does this user have permission to access this object?

## 2. Avoid Predictable IDs
Use UUIDs instead of sequential numbers (helps but does not replace auth checks).

## 3. Implement Access Control at Backend
Never rely on frontend checks.

## 4. Use Centralized Authorization Logic
Avoid scattered permission checks.

---

# IDOR vs Authentication Issues

Authentication problem:
User is not properly logged in.

Authorization problem (IDOR):
User is logged in but accesses data they should not.
