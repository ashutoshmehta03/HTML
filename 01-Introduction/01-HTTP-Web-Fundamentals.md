# HTTP & Web Fundamentals

## 1. What is HTTP?

HTTP stands for Hypertext Transfer Protocol — it’s a set of rules used to transfer data between the client (browser) and server on the web.

It allows communication between frontend (browser) and backend (server) in a request-response model.

It’s the foundation of all web communication — every website you open (like YouTube, Google, or api.hitesh.ai) runs on HTTP or HTTPS.

## 2. Why is HTTP Important?

HTTP defines how browsers request data and how servers respond.

Example:

- You open https://youtube.com
- Browser sends an HTTP Request
- Server sends back an HTTP Response with HTML, images, text, etc.
- Browser renders that page visually.

## 3. HTTP is Stateless

HTTP does not remember anything from previous requests.
Each new request is independent — that’s why it’s called a stateless protocol.

Example:

- You open YouTube home (HTTP request #1).
- Then you open a new video (HTTP request #2).
- Both are treated as new, fresh requests — no memory of what happened earlier.
- That’s why cookies or sessions are used to maintain state.

## 4. Request–Response Model

Every interaction on the web happens in this pattern:

Client (browser) sends a request → Server (backend) replies with a response.

Example:

- GET https://api.hitesh.ai/courses

Server responds with:

- 200 OK
- Content-Type: application/json

## 5. Common HTTP Methods (Verbs)

- GET: Used to retrieve data (e.g., Get list of users).

- POST: Used to send data (e.g., Submit a form or login).

- PUT: Used to update existing data (e.g., Update user info).

- DELETE: Used to remove data (e.g., Delete a record).

Example:

- GET /users - fetch data
- POST /users - create a new user
- DELETE /users/1 - delete user 1

## 6. Common Response Status Codes

- 200 OK: Request successful.

- 201 Created: New resource created successfully.

- 400 Bad Request: Invalid input or missing data.

- 401 Unauthorized: Login or token required.

- 404 Not Found: The resource does not exist.

- 500 Internal Server Error: Something went wrong on the server.

## 7. HTTP Headers

Headers carry extra information about a request or response.

They help define the content type, browser info, authentication tokens, cache behavior, and cookies.

Example Request Headers:

- GET /dashboard
- User-Agent: Chrome/123.0
- Accept: text/html
- Cookie: session_id=xyz123

Example Response Headers:

- Content-Type: text/html
- Set-Cookie: session_id=xyz123; - Secure; HttpOnly
- Cache-Control: max-age=3600

## 8. What Happens When You Open a Website (Step-by-Step)

When you visit a site like https://api.hitesh.ai/course?id=1234, here’s what happens behind the scenes:

1. DNS Lookup:-
   Browser asks DNS (Domain Name System) for the IP address of api.hitesh.ai.

2. TCP Connection:-
   Browser connects to that IP using TCP (Transmission Control Protocol) — ensures reliable data transfer.

3. TLS Handshake (for HTTPS):-
   Browser and server exchange certificates for encrypted communication.

4. Send HTTP Request:-
   Browser sends something like:

- GET /course?id=1234
- Host: api.hitesh.ai

5. Server Processes Request:-
   Backend (like Node.js) handles the logic and prepares a response.

6. Server Sends Response:-

- 200 OK
- Content-Type: text/html

  Body - HTML, image, JSON, etc.

7. Browser Renders the Page:-
   Browser converts that raw data into a visual web page.

8. TCP Connection Closes:-
   HTTP is stateless, so the connection ends after the response.

## 9. HTTPS — The Secure HTTP

HTTPS = HTTP + Encryption (TLS/SSL).
It ensures your data is safe from hackers.
Most secure websites use it.

- Port 443 → HTTPS (default secure port).

- Port 80 → HTTP (insecure).

Example:

- https://youtube.com is secure.
- If you open http://youtube.com, it automatically redirects to HTTPS.

In AWS or internal company systems, plain HTTP may be used internally (not public).

## 10. HTTP/1.1 vs HTTP/2

HTTP/1.1: Sends one request at a time → slower.

HTTP/2: Uses multiplexing → many files at once, faster.

Compression: Supported in HTTP/2.

Encryption: Common in both, especially with HTTPS.

Real Example:

- When you open a big website with many images and scripts, HTTP/2 loads them all simultaneously — that’s why modern sites load faster.

## 11. Cookies

Cookies are small pieces of data stored in your browser to remember things between requests.
They solve the stateless nature of HTTP by maintaining user information.

Example:

- You log in to YouTube - a cookie is saved → you stay logged in even after closing the tab.

How Cookies Work

1. You log in → server sends:

- Set-Cookie: session_id=abc123; HttpOnly; Secure

2. Browser stores it.

3. On next visit, browser sends:

- Cookie: session_id=abc123

4. Server reads this cookie and keeps you logged in.

Cookie Attributes

- Name=Value: The data stored (e.g. user=ashu)

- Expires / Max-Age: Expiry time

- Domain: Which site can access the cookie

- Path: URL path restriction

- Secure: Sent only over HTTPS

- HttpOnly: Hidden from JavaScript

- SameSite: Controls cross-site sending

Example:

- Set-Cookie: token=xyz456; Secure; HttpOnly; SameSite=Strict; Max-Age=86400

Types of Cookies

- Session Cookies: Deleted after browser closes

- Persistent Cookies: Stay even after browser closes

- Third-Party Cookies: Set by external sites (like ads)

- Secure Cookies: Only via HTTPS

- HttpOnly Cookies: Secure, not accessible via JavaScript

Real-World Example (Login Flow)

Request:

- POST /login
  Content-Type: application/json
  {
  "email": "ashu@gmail.com",
  "password": "123456"
  }

Response:

- Set-Cookie: session_token=xyz123; Secure; HttpOnly; Max-Age=86400

Next request automatically sends:

- Cookie: session_token=xyz123

- You remain logged in.

## 12. Cache (Browser Memory)

Cache stores website data temporarily to make pages load faster without re-fetching everything from the server.

Example:

- When you revisit https://api.hitesh.ai/home, your browser loads images and CSS from the cache — super fast.

Types of Cache

- Browser Cache: Stored on user’s local system.

- CDN Cache: Stored on global edge servers.

- Proxy Cache: Shared between client and server for multiple users.

Cache-Control Header

Servers define caching rules using this header.

Examples:

- Cache-Control: max-age=3600
- Cache-Control: no-cache
- Cache-Control: no-store
- Cache-Control: public
- Cache-Control: private

If you set max-age=3600, the browser reuses data for one hour.

Real Example

- When visiting YouTube:

- Logo and thumbnails are fetched once.

- Next time, they load from cache instead of server → page loads instantly.

## 13. URL — Uniform Resource Locator

A URL defines how and where a web resource lives.

Example:

- https://api.hitesh.ai/course?id=1234

- Protocol: https

- Host (Domain): api.hitesh.ai

- Port: 443 (default for HTTPS)

- Path: /course

- Query Params: ?id=1234

## 14. Developer Tools (Network Tab)

Browser DevTools → Network Tab helps debug requests.

You can see:

- Requests and responses

- Headers

- Status codes (200, 404, etc.)

- Payloads and timing

- Cookies and cache

This tool is essential for every web developer.

## 15. Summary — The Eye Model of the Web

You can think of the web as an eye — each part plays a role:

- User: Browser (Client)
- DNS: Finds IP address
- TCP: Creates reliable connection
- TLS: Encrypts communication
- HTTP: Sends and receives requests
- Cookies & Cache: Store and remember data
- Response: Browser renders the page

That’s how the entire web cycle works — simple, stateless, and efficient.

In Short:

> HTTP is the language of the web — connecting your browser and the server through requests, responses, headers, cookies, and caching.
