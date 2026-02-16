# Backend & REST APIs (Interview Q&A)

## Q1. What is an API?
### ✅ Answer:
An API is a **contract** that allows two applications to communicate by sending requests and receiving responses.

**One-liner:**
> "An API defines how a client can request data or services from a server and how the server responds."

---
## Q2. What is a REST API?

### ✅ Answer:
REST is an **architectural style** for designing APIs using standard HTTP methods and **stateless communication**.
### Key points:
- Resource-based URLs
- Uses HTTP methods
- Stateless

**One-liner:**
> "REST APIs expose resources using standard HTTP methods in a stateless way."

---
## Q3. Why is REST stateless?
### ✅ Answer:
REST is stateless to improve **scalability, reliability, and simplicity**. Each request contains all the information needed to process it, so the server does not store client state.

**One-liner:**
> "Statelessness allows horizontal scaling and simplifies backend systems."

---
## Q4. What are HTTP methods and their use?

|Method|Use|
|---|---|
|GET|Read data|
|POST|Create resource / trigger action|
|PUT|Replace entire resource|
|PATCH|Update part of resource|
|DELETE|Remove resource|

**One-liner:**

> "HTTP methods define the type of operation performed on a resource."

---

## Q5. Difference between PUT and PATCH?

### ✅ Answer:
- **PUT** replaces the entire resource
- **PATCH** updates only specific fields

**One-liner:**

> "PUT replaces the resource, PATCH modifies part of it."

---
## Q6. Can a GET request have a body?
### ✅ Answer:
Technically possible, but **not recommended**. GET request bodies are not standardized or reliably supported.

**One-liner:**
> "GET bodies are technically allowed but practically unsupported and should be avoided."

---
## Q7. Can a POST request be sent without a body?
### ✅ Answer:
Yes. POST without a body is valid when the request **triggers an action** and does not require additional input data.

**One-liner:**
> "POST without body is acceptable for action-based endpoints."

Example: Logout endpoint

---
## Q8. Why should login not be done via GET?

### ✅ Answer:
Login should not use GET because credentials in URLs can be **logged, cached, and exposed**, and GET violates REST semantics by changing server state.

**One-liner:**
> "GET exposes credentials in URLs and is cacheable, making it insecure for login."

---
## Q9. What are HTTP status codes and why are they important?

### Common codes:
- 200 OK
- 201 Created
- 400 Bad Request
- 401 Unauthorized
- 403 Forbidden
- 404 Not Found
- 500 Internal Server Error

### ✅ Answer:

Status codes inform the client about the **result of a request**.

**One-liner:**

> "Status codes communicate success or failure of API requests."

---

## Q10. Explain the request–response lifecycle.

### ✅ Answer:
1. Client sends request
2. Server routes request
3. Business logic executes
4. Database access (if required)
5. Response returned with status and data

**One-liner:**
> "A request flows through routing, business logic, data access, and returns a response."
---
## Q11. What is JSON and why is it used?

### ✅ Answer:

JSON is a lightweight data format used to exchange structured data between client and server.

**One-liner:**
> "JSON is language-independent, readable, and easy to parse."
---
## Q12. How does authentication work in stateless APIs? (High level)
### ✅ Answer:
In stateless APIs, the client authenticates once to obtain a **token**, then sends that token with every request. The server validates the token without storing session state.

**One-liner:**
> "Stateless authentication uses tokens sent with every request."
---
## Q13. What is the role of headers in REST APIs?
### ✅ Answer:
Headers carry **metadata** such as authentication tokens, content type, and caching rules.

**One-liner:**
> "Headers pass metadata like auth tokens and content types."
---
## Q14. How do backend frameworks help (Flask / FastAPI / Django)?

### ✅ Answer:
Backend frameworks handle routing, request parsing, validation, and response formatting, allowing developers to focus on business logic.
**One-liner:**
> "Frameworks simplify backend development by handling common infrastructure tasks."

---
## Q15. SQL vs NoSQL — when to use which?
### ✅ Answer:
- **SQL** for structured data and relationships
- **NoSQL** for flexible schemas and high-scale workloads
**One-liner:**
> "SQL fits relational data; NoSQL fits flexible or high-scale data."
---
## Q16. What is indexing and why is it used?
### ✅ Answer:
Indexing improves **query performance** by allowing faster data lookup.

**One-liner:**
> "Indexes speed up data retrieval at the cost of extra storage."
---
## Q17. What is the cloud and why is it used?
### ✅ Answer:
Cloud platforms provide on-demand compute, storage, and services, enabling scalable and cost-effective deployments.

**One-liner:**
> "Cloud enables scalable infrastructure without managing physical servers."

---
## Q18. What are EC2 and S3?
### ✅ Answer:
- **EC2**: Virtual compute instances
- **S3**: Object storage service

**One-liner:**
> "EC2 provides compute, S3 provides storage."
---
## Q19. How can GenAI be integrated into backend systems?

### ✅ Answer:
GenAI is integrated by calling **LLM APIs** from backend services to perform tasks like summarization, chat, or classification.
**One-liner:**
> "GenAI integration is typically done via API calls to LLM services."

---
## ✅ Day 2 Quick Revision Checklist
- REST principles and statelessness
- HTTP methods and status codes
- GET vs POST semantics
- Stateless authentication (token-based)
- Backend frameworks (conceptual)
- Databases, cloud basics, GenAI usage