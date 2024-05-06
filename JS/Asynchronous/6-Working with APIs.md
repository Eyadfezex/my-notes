# Working with APIs

When working with remote APIs, you need a way to interact with those APIs. Modern JavaScript provides two native ways to send HTTP requests to remote servers, `XMLHttpRequest` and `Fetch`.

---

## `XMLHttpRequest`

`XMLHttpRequest` (XHR) is an API in web development that enables client-side scripts to communicate with servers. It's a fundamental part of making asynchronous HTTP requests from a web page. XMLHttpRequest allows the browser to send HTTP requests to a server and handle the server's response without having to reload the page.

```js
// Create a new XMLHttpRequest object
var xhr = new XMLHttpRequest();

// Configure the request: GET method, URL to fetch data from
xhr.open("GET", "https://api.example.com/data", true);

// Set up a function to handle the response when it's received
xhr.onreadystatechange = function () {
  // Check if the request is complete and the response is ready
  if (xhr.readyState === 4) {
    // Check if the request was successful (status code 200)
    if (xhr.status === 200) {
      // Parse the JSON response
      var responseData = JSON.parse(xhr.responseText);
      // Update the webpage with the received data
      console.log("Data:", responseData.data);
    } else {
      // If the request was not successful, display an error message
      console.error("Error: Unable to fetch data");
    }
  }
};

// Send the request
xhr.send();
```

---

## Fetch

The `fetch` function allows you to send HTTP requests to a server and handle responses. It returns a Promise that resolves to the Response object representing the response to the request.

```js
// Fetching data from the API endpoint
fetch("https://api.example.com/data")
  .then((response) => {
    // Check if the response is successful
    if (!response.ok) {
      throw new Error("Network response was not ok");
    }
    // Parse the JSON data in the response
    return response.json();
  })
  .then((data) => {
    // Do something with the JSON data
    console.log(data);
  })
  .catch((error) => {
    // Handle any errors that occurred during the fetch
    console.error("There was a problem with the fetch operation:", error);
  });
```
