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

For more detailed information, refer to Cloudflare's article on [What is HTTPS?](https://www.cloudflare.com/learning/ssl/what-is-https/)

---

# Content Security Policy (CSP)

Content Security Policy (CSP) is a powerful security feature designed to mitigate cross-site scripting (XSS) and other code injection attacks by allowing web developers to define a list of trusted content sources. By enforcing this policy, CSP ensures that only resources from approved origins are executed or rendered, effectively reducing the risk of executing malicious scripts.

## **Key Components of CSP**

1. **Source Allowlists:**
   - These are the trusted domains, protocols, or paths from which content can be loaded. Sources can be categorized based on content type (e.g., scripts, styles, images).
2. **Directives:**

   - Directives are instructions that specify which content types can be loaded, and from which sources. For example, `script-src` defines allowed sources for JavaScript files, while `style-src` defines permitted sources for CSS.

3. **Keywords:**

   - Keywords like `'self'`, `'none'`, and `'unsafe-inline'` provide predefined values to control content sources and their level of trust.
     - `'self'`: Allows content from the same origin (i.e., the current domain).
     - `'none'`: Disallows all sources.
     - `'unsafe-inline'`: Allows inline scripts, though this should be avoided due to security risks.

4. **Inline Code and `eval()` Restrictions:**

   - CSP provides a way to restrict inline scripts and dynamic code evaluation (e.g., `eval()`), which are common attack vectors for XSS. You can enforce strict policies that disable inline code execution and the use of `eval()`.
     - Example: Disallow inline scripts by using `'unsafe-inline'`.

5. **Reporting:**
   - CSP includes a reporting mechanism that allows you to receive notifications when a policy violation occurs. The browser sends violation reports to a designated endpoint, helping you identify and resolve potential security issues.
     - Example: Setting up a reporting URI like `report-uri /csp-violation-report-endpoint`.

---

## **Common CSP Directives**

- `default-src`: The fallback policy for loading all content types if no specific policy is provided.
- `script-src`: Specifies allowed sources for JavaScript files. Common sources include `'self'` (same origin), `'https://apis.example.com'`, and `'unsafe-eval'` (though the latter is discouraged).
- `style-src`: Defines permitted sources for CSS. Typically, you’ll restrict this to trusted CDNs or your own domain.
- `img-src`: Specifies allowed image sources. For example, you can permit images only from your own domain and trusted CDNs.
- `connect-src`: Limits the allowed origins for network requests such as AJAX, WebSockets, and fetch requests.
- `font-src`: Specifies allowed sources for web fonts.
- `frame-src`: Defines the allowed origins for embedding frames, such as `iframe` or `object`.

---

## **Example CSP Header**

To allow scripts from the same origin and from a trusted external source like Google APIs, you would set the following HTTP header:

```http
Content-Security-Policy: script-src 'self' https://apis.google.com; object-src 'none'; connect-src 'self' https://api.example.com; report-uri /csp-violation-report-endpoint
```

This policy does the following:

- Permits JavaScript from the current domain (`'self'`) and from `https://apis.google.com`.
- Disallows the use of `<object>`, `<embed>`, and `<applet>` elements (`object-src 'none'`).
- Restricts AJAX and WebSocket connections to `https://api.example.com` and the same origin (`'self'`).
- Configures a violation report endpoint at `/csp-violation-report-endpoint`.

---

## **Additional Considerations for Implementing CSP**

1. **Use of Hashes or Nonces for Inline Scripts:**

   - To allow inline scripts securely, CSP allows you to specify hashes or nonces that match the content of the inline script. This allows you to whitelist specific inline scripts while blocking others.
     - Example: `script-src 'self' 'nonce-<random-value>'`.

2. **Avoid `'unsafe-inline'` and `'unsafe-eval'`:**

   - It's highly recommended to avoid `'unsafe-inline'` for scripts and styles, as well as `'unsafe-eval'` for JavaScript. These features significantly reduce the security of your application and open it up to attacks like XSS.

3. **Content Security Reporting:**

   - Set up the `report-uri` or `report-to` directive to capture CSP violations. This helps you proactively monitor any malicious attempts to inject content.

4. **Testing and Iteration:**
   - Implementing CSP can break functionality, especially when using third-party libraries or scripts. Start by using the `Content-Security-Policy-Report-Only` header to test your policy without enforcing it. This helps identify any violations before applying them in production.

---

For a deeper dive into the nuances of CSP and its implementation, check out the comprehensive guide on [Content Security Policy on web.dev](https://web.dev/articles/csp).
