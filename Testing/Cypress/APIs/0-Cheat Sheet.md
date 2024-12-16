# Cypress APIs

## **Navigation**

### **cy.visit()**

- Navigates to a given URL.
- **Example:**

  ```js
  cy.visit("https://example.com");
  ```

## **Element Selection**

### **cy.get()**

- Selects elements on the page that match a given selector.
- Accepts CSS selectors, XPath selectors, or text content.
- **Examples:**

  ```js
  cy.get(".my-button");
  cy.get("xpath=/html/body/div/button");
  cy.get('button[data-testid="my-button"]');
  cy.get("button").contains("Submit");
  ```

### **cy.contains()**

- Finds an element containing specific text.
- Can be used standalone or with `cy.get()`/`cy.find()`.
- **Examples:**

  ```js
  cy.contains("Submit");
  cy.get("button").contains("Submit");
  ```

### **cy.find()**

- Searches for elements within a parent element using a selector.
- Useful for scoped queries.
- **Example:**

  ```js
  cy.get(".parent-element").find(".child-element");
  ```

## **Actions**

### **cy.type()**

- Types text into an input field.
- **Example:**

  ```js
  cy.get('input[name="username"]').type("myusername");
  ```

### **cy.click()**

- Clicks on an element.
- **Example:**

  ```js
  cy.get('button[data-testid="my-button"]').click();
  ```

### **cy.submit()**

- Submits a form.
- **Example:**

  ```js
  cy.get("form").submit();
  ```

## **Assertions**

### **cy.should()**

- Asserts that an element meets a specific condition.
- **Examples:**

  ```js
  cy.get('button[data-testid="my-button"]').should("be.visible");
  cy.get('button[data-testid="my-button"]').should("have.text", "Submit");
  ```

### **cy.assert()**

- Asserts that a condition is true.
- Can be used with non-Cypress objects.
- **Example:**

  ```js
  cy.assert(1 + 1 === 2);
  ```

## **Network**

### **cy.intercept()**

- Intercepts HTTP requests and responses.
- Can mock responses, verify requests, and more.
- **Example:**

  ```js
  cy.intercept("GET", "/api/data", { fixture: "my-fixture.json" });
  ```

### **cy.wait()**

- Waits for a specific amount of time or for a condition to be met.
- **Examples:**

  ```js
  cy.wait(1000); // Waits for 1 second.
  cy.wait("@my-request"); // Waits for a specific request.
  ```

## **Control Flow**

### **cy.then()**

- Executes a callback function after a Cypress command is completed.
- **Example:**

  ```js
  cy.get("button")
    .click()
    .then(() => {
      cy.get(".success-message").should("be.visible");
    });
  ```

### **cy.wrap()**

- Wraps a non-Cypress object, allowing you to chain Cypress commands.
- **Example:**

  ```js
  const user = { name: "John" };
  cy.wrap(user).its("name").should("equal", "John");
  ```
