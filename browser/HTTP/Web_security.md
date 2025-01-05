# Web security

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

---

# HTTPS

**Hypertext Transfer Protocol Secure (HTTPS)** is the secure version of HTTP, the primary protocol used to transmit data between a web browser and a website. HTTPS encrypts data to enhance security during transfer, which is especially crucial when users send sensitive information, such as login credentials or financial details. :contentReference[oaicite:0]{index=0}

## How Does HTTPS Work?

HTTPS employs the **Transport Layer Security (TLS)** protocol (formerly known as Secure Sockets Layer, or SSL) to encrypt communications. This involves an **asymmetric public key infrastructure**, utilizing two keys:

- **Private Key**: Controlled by the website owner, this key remains confidential on the web server and decrypts information encrypted by the public key.

- **Public Key**: Available to anyone interacting with the server securely; it encrypts information that only the private key can decrypt.

This mechanism ensures that data exchanged between the browser and the server remains confidential and protected from interception. :contentReference[oaicite:1]{index=1}

## Importance of HTTPS

- **Data Protection**: HTTPS encrypts data, preventing unauthorized parties from eavesdropping on communications. Without HTTPS, information sent over HTTP is in plaintext, making it vulnerable to interception and attacks.

- **Authentication**: HTTPS verifies that users are communicating with the intended website, safeguarding against impersonation by malicious actors.

- **Trust and Credibility**: Modern browsers, like Google Chrome, label non-HTTPS websites as "not secure," which can deter users. A secure HTTPS connection is often indicated by a padlock icon in the URL bar, enhancing user trust.

- **SEO Benefits**: Search engines may rank HTTPS-enabled websites higher, as they are considered more secure and trustworthy.

## Obtaining HTTPS for a Website

To implement HTTPS, a website must acquire an **SSL/TLS certificate** from a trusted Certificate Authority (CA). This certificate authenticates the website's identity and enables encryption. Many hosting providers offer SSL/TLS certificates, and some services, like Cloudflare, provide free SSL/TLS encryption to facilitate secure connections. :contentReference[oaicite:2]{index=2}

## Conclusion

Implementing HTTPS is essential for protecting user data, ensuring website authenticity, and maintaining user trust. It is a fundamental practice for any website, particularly those handling sensitive information.

For more detailed information, refer to Cloudflare's article on [What is HTTPS?](https://www.cloudflare.com/learning/ssl/what-is-https/)
