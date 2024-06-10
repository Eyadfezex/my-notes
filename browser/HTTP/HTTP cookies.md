# HTTP cookies

its a small piece of data server sends it to user's web browser. the browser can store, create, modify cookies, and sent them back to server.

## What cookies are used for

The server will use the contents of HTTP cookies to determine whether different requests come from the same browser/user and then issue a personalized or generic response as appropriate.

**The following describes a very simple user sign-in system:**
![very simple user sign-in system](../../img/simple%20user%20sign-in%20system.png)
**Cookies are mainly used for three purposes:**

- **Session management:** User sign-in status, shopping cart contents, game scores, or any other user session-related details that the server needs to remember.
- **Personalization:** User preferences such as display language and UI theme.
- **Tracking:** Recording and analyzing user behavior.

Cookies used to be the only way to store data on client-side. Now, modern options like Web Storage (local & session) and IndexedDB are better.

These APIs are designed for storage, don't bloat requests, and hold more data than cookies. Cookies can slow down websites, especially with many cookies or slow connections.
