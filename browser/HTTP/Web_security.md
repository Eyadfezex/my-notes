# Web_security

**CORS (Cross-Origin Resource Sharing):**

- CORS is an HTTP-header based mechanism that allows a server to indicate which origins (domain, scheme, or port) other than its own are permitted to load resources.
- It is essential for enabling web applications to interact securely with resources from different origins.
- The Origin consists of the scheme (e.g., http://), domain (e.g., example.com), and port (e.g., :443) of a web page.

**SOP (Same-Origin Policy):**

- SOP is a web browser security mechanism designed to prevent websites from attacking each other.
- It restricts scripts on a web page from making requests to a different origin (scheme, domain, or port) than the one from which the script was loaded.
- SOP helps to mitigate various types of attacks, including cross-site scripting (XSS) and cross-site request forgery (CSRF).

**Common CORS Exceptions:**

- **Simple Requests**: Certain types of HTTP requests, known as "simple requests," are subject to less strict CORS checks. These requests include only safe methods (GET, HEAD, OPTIONS), don't include custom headers, and don't use certain types of request entity bodies. Simple requests are automatically allowed by the browser without the need for explicit server-side CORS headers.

**Cross-site Request Forgery (CSRF):**

- CSRF is an attack that tricks the victim into submitting a malicious request. It occurs when a user is tricked into clicking a link or submitting a form on a trusted website while authenticated.
- This attack can result in unauthorized actions being performed on the victim's behalf on another site where the victim is authenticated.

These notes provide an overview of CORS, SOP, and common exceptions to CORS checks, as well as an introduction to CSRF attacks.
