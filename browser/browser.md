# Browser

1. **Browser Life Cycle**:

   - The browser life cycle runs through 7 base components:
     1. User interface.
     2. Browser engine.
     3. Rendering engine.
     4. Networking.
     5. JavaScript interpreter.
     6. UI backend.
     7. Data like cookies.

2. **Browser Working Steps**:
   - **Resource Gathering**:
     - The web browser uses networking modules to gather all the different resources on the Internet.
   - **Parse HTML & Create DOM Tree**:
     - The browser parses HTML code and creates a DOM tree, which is a hierarchical representation of all HTML elements in the page.
   - **Error Checking**:
     - The browser checks the HTML code for any errors.
   - **Create Render Tree from DOM Tree**:
     - The browser constructs a render tree from the DOM tree. In this step, CSS styles are applied to the HTML elements.
   - **Layout**:
     - Once the render tree is constructed, the browser performs layout or "reflow" to determine the position and size of each render object on the screen.
   - **Painting**:
     - The final step is to paint the content onto the screen. This involves rendering pixels based on the layout information and the visual styles of each rendered object.

These steps illustrate the process by which a web browser fetches and renders web pages, ultimately displaying them to the user.

---

## Differences: Web Page, Website, Web Server, and Search Engine

To understand these differences, consider a library analogy:

1. **Web Page**:

   - A web page is like an individual book in the library, each page having specific content and location. It’s a single document on a website.

2. **Website**:

   - A website is analogous to a section in the library (like Science or History), containing multiple related web pages (like different books).

3. **Web Server**:

   - The web server is comparable to the entire library building, hosting multiple sections (websites) and ensuring access to the correct content.

4. **Search Engine**:
   - A search engine functions like the library’s search index, helping users find specific books (web pages) by cataloging their locations and content.

This analogy helps clarify the roles and interactions between these internet components.
