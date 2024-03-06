Here's a breakdown of the provided notes on HTTP and how the web works:

1. **HTTP Characteristics:**
   - HTTP is **connectionless**: After making the request, the client disconnects from the server, and the server re-establishes the connection to deliver the response.
   - HTTP can deliver any sort of data, as long as the two computers can read it.
   - HTTP is **stateless**: The client and server know about each other only during the current request. If they want to connect again, they need to provide information anew, and the connection is handled as the very first one.

2. **Request & Response Cycle:**
   - The Request & Response cycle involves the user typing a URL, the client sending the request through the Internet, the server processing the request, preparing the response, re-establishing the connection to send back the response, and then the two computers completely disconnect.

3. **HTTP Request Message:**
   - HTTP request messages consist of a start line, headers, and a body. The information in these sections varies depending on whether it's a request or a response.
   - The method is a command that tells the server what to do.
   - URI (Uniform Resource Identifier) identifies and accesses resources on the internet.

4. **HTTP Response Message:**
   - Status code informs the client if the request succeeded or failed.
   - Headers contain name & value pairs like content length.

5. **Request Mode:**
   - The mode determines how the request behaves. Modes include `cors`, `no-cors`, `same-origin`, and `WebSocket`.
   - `cors`: Allows requests to be made to domains other than the one serving the current page.
   - `no-cors`: Allows requests to other origins without accessing the response or response headers.
   - `same-origin`: Ensures that a request is always being made to your origin.
   - The default setting for the "mode" parameter is `cors`.

These notes provide a comprehensive overview of HTTP, its request and response cycle, and the modes for making requests.