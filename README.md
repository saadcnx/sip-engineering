# 🔌 api-support-troubleshooting

> Practical notes and examples for debugging REST APIs, HTTP status codes, authentication issues, curl requests, and OpenAPI specifications built for developer support and API troubleshooting roles.

![Status](https://img.shields.io/badge/status-actively%20maintained-brightgreen)
![Type](https://img.shields.io/badge/type-api%20support%20lab-orange)
![Focus](https://img.shields.io/badge/focus-REST%20%7C%20HTTP%20%7C%20OpenAPI-blue)

---

## 📌 What This Repo Is

This repo is a structured reference and practice lab for API support work.

Each section contains:
- 📖 **Notes** — clear explanations of the concept
- 🧪 **Examples** — real `curl` commands, request/response pairs, and error samples
- 🔍 **Debugging tips** — what to check when something goes wrong
- ✅ **Fixes** — how to resolve the most common issues

---

## 🗂️ Repository Structure

```text
api-support-troubleshooting/
│
├── http-basics/
│   ├── http-methods.md          ← GET, POST, PUT, PATCH, DELETE
│   ├── request-response.md      ← anatomy of a request and response
│   └── headers.md               ← common headers and what they do
│
├── status-codes/
│   ├── 2xx-success.md           ← 200, 201, 204
│   ├── 3xx-redirects.md         ← 301, 302, 304
│   ├── 4xx-client-errors.md     ← 400, 401, 403, 404, 422, 429
│   ├── 5xx-server-errors.md     ← 500, 502, 503, 504
│   └── debugging-by-code.md     ← what to check for each error range
│
├── authentication-errors/
│   ├── api-keys.md              ← how API keys work, common mistakes
│   ├── bearer-tokens.md         ← JWT and OAuth bearer tokens
│   ├── oauth-basics.md          ← OAuth 2.0 flow explained simply
│   └── common-auth-errors.md    ← 401 vs 403, token expiry, wrong header
│
├── curl-examples/
│   ├── basic-requests.md        ← GET, POST, PUT, DELETE with curl
│   ├── with-headers.md          ← passing auth headers, content-type
│   ├── with-body.md             ← sending JSON body in curl
│   └── debugging-curl.md        ← -v flag, reading curl output
│
├── postman-notes/
│   ├── setup.md                 ← collections, environments, variables
│   ├── testing-endpoints.md     ← sending requests, reading responses
│   └── common-postman-issues.md ← SSL errors, env variables not loading
│
├── openapi-basics/
│   ├── what-is-openapi.md       ← spec overview, YAML vs JSON
│   ├── reading-a-spec.md        ← paths, parameters, schemas, responses
│   ├── common-spec-errors.md    ← validation failures, missing fields
│   └── tools.md                 ← Swagger UI, Redoc, Stoplight
│
└── README.md
```

---

## 🧪 Lab Sections

### 🌐 http-basics
Core concepts behind every API request — before debugging anything, these fundamentals need to be solid.

| Topic | What's Covered |
|---|---|
| HTTP Methods | When to use GET vs POST vs PUT vs PATCH vs DELETE |
| Request Structure | URL, headers, body, query params |
| Response Structure | Status line, headers, body |
| Common Headers | `Content-Type`, `Authorization`, `Accept`, `User-Agent` |

---

### 📊 status-codes
The most important signal in any API response — knowing what a status code means and what to check next.

| Range | Meaning | Common Codes |
|---|---|---|
| `2xx` | Success | 200 OK, 201 Created, 204 No Content |
| `3xx` | Redirect | 301 Moved, 304 Not Modified |
| `4xx` | Client Error | 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found, 422 Unprocessable, 429 Rate Limited |
| `5xx` | Server Error | 500 Internal Error, 502 Bad Gateway, 503 Unavailable, 504 Timeout |

---

### 🔐 authentication-errors
Auth issues are the most common API support problem. This section covers how each auth method works and why it breaks.

| Error | Likely Cause |
|---|---|
| `401 Unauthorized` | Missing, expired, or malformed token |
| `403 Forbidden` | Token is valid but lacks permission for this resource |
| `Invalid API key` | Key passed in wrong header or has extra whitespace |
| `Token expired` | JWT exp claim has passed — need to refresh |
| `invalid_client` | OAuth client ID or secret is wrong |

---

### ⚡ curl-examples
Practical `curl` commands for testing APIs directly from the terminal — no GUI needed.

```bash
# Basic GET request
curl https://api.example.com/users

# GET with auth header
curl https://api.example.com/users \
  -H "Authorization: Bearer YOUR_TOKEN"

# POST with JSON body
curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d '{"name": "Ali", "email": "ali@example.com"}'

# Verbose output for debugging
curl -v https://api.example.com/users \
  -H "Authorization: Bearer YOUR_TOKEN"
```

---

### 📬 postman-notes
Using Postman effectively for API testing and debugging — including environment setup and common gotchas.

| Topic | What's Covered |
|---|---|
| Collections | Organizing requests by API or feature |
| Environments | Switching between dev, staging, production |
| Variables | `{{base_url}}`, `{{token}}` — avoid hardcoding |
| Common Issues | SSL errors, env variable not loading, auth not persisting |

---

### 📄 openapi-basics
Reading and working with OpenAPI specs — a core skill for understanding any well-documented API.

| Topic | What's Covered |
|---|---|
| What is OpenAPI | YAML/JSON spec format, versions (3.0, 3.1) |
| Reading a Spec | `paths`, `parameters`, `requestBody`, `responses`, `schemas` |
| Common Errors | Missing required fields, wrong `$ref`, invalid schema types |
| Tools | Swagger UI, Redoc, Stoplight, Scalar |

---

## 🔍 Debugging Approach for API Issues

| Step | Action |
|---|---|
| 1️⃣ | **Read the status code** — what range is it? |
| 2️⃣ | **Read the response body** — is there an error message or code? |
| 3️⃣ | **Check the request** — correct method, URL, headers, body? |
| 4️⃣ | **Check authentication** — is the token valid, not expired, correct format? |
| 5️⃣ | **Reproduce with curl** — eliminate the client and test raw |
| 6️⃣ | **Check the API docs or OpenAPI spec** — are you calling it correctly? |
| 7️⃣ | **Document what you found** — status code, cause, fix |

---

## 🎯 Goal

Build the practical API knowledge to debug real developer issues fast — read an error response, identify the cause, and explain the fix clearly in a support context.

---

## 📈 Status

Actively maintained. New examples, curl commands, and debugging notes added as I work through real API scenarios.
