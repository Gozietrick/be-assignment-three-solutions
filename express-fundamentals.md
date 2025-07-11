//1) What is Express.js and how does it simplify Node.js web application development?

//Solutions
From what i understand, Express.js is a flexible web application framework built on top of Node.js. It simplifies Node.js web development by providing a structured set of features for building server side apps and API servers, such as routing, middleware support, HTTPs request/responses and easy integration with templates and databases.
Express.js simplifies Node.js development by: 
- Simplified routing: it makes easy to define routes for different HTTP methods and URLs. Without Express, one would be writing more raw node.Js code to handle routes manually
- Supporting middleware: Express allows us to add middleware functions to handle things like logging, authentication, body parsing and so on
- Setting up faster: it gives boiler tools to setup servers quickly with just a few lines of codes
- Handling Request/ response handling: Built-in methods for sending responses include: (res.send(),res.json()) and parsing request (req.body,req.params)
- Building a Robust API: It is an ideal space for creating RESTful APIs with clear route definitions and middle ware chaining 
- the adoption and plenty of plugins/middleware support 
example: const express= require('express');
const app= express();
app.get('/',(req,res)=> {
    res.send('Hello world)
})

//2) Explain the difference between middleware and route handlers in Express.js

Solutions
In Express.js both middleware and route handlers are functions used to handle HTTPs requests but they serve different purpose: 
- Middleware: are functions that have access to the request (req),response (res) objects and the next() function in the request-response cycle. They can modify the request or response, end the request, or pass control to the next middleware. Its use case include:  logging, authentication, parsing Json or form data, error handling and others.
- Route handlers routes: These functions that respond to a specific HTTP request method (GET,POST,DELETE,e.tc) at a specific URl path. They are the final destination of the request where a response is sent. USe case include: returning a webpage or data, processing form submissions, sending API responses.

Example:
```js
const express = require('express');
const app = express();

// Middleware example
app.use((req, res, next) => {
  console.log('Request received');
  next(); // Pass control to the next middleware or route handler
});

// Route handler example
app.get('/hello', (req, res) => {
  res.send('Hello from route handler!');
});
```
In all:  
- Middleware can run for every request or specific routes and can modify requests/responses or perform actions before reaching the route handler.  
- Route handlers send the final response to the client for a specific


//3) How does Express.js handle HTTP requests and responses differently from vanilla Node.js?

//Solutions
Already established above, Express.js provides a higher-level, easier-to-use API for handling HTTP requests and responses compared to vanilla Node.js. It simplifies HTTP handling by abstracting and automating what we would have to manually build vanilla Node.js

- In vanilla Node.js:
=You must manually create an HTTP server using the `http` module.
= Routing (handling different URLs and HTTP methods) must be implemented manually.
= Parsing request bodies (like JSON or form data) requires extra code or third-party modules.
= Sending responses requires setting headers and status codes manually.

- In Express.js:
= Routing is built-in and easy to define with methods like `app.get()`, `app.post()`, etc.
= Middleware makes it simple to parse request bodies, handle cookies, and more.
= Sending responses is easier with methods like `res.send()`, `res.json()`, and `res.status()`.
=Error handling and organizing code is more straightforward.

Example:

*Vanilla Node.js:*
```js
const http = require('http');
const server = http.createServer((req, res) => {
  if (req.url === '/hello' && req.method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello from Node.js!');
  }
});
server.listen(3000);
```

*Express.js:*
```js
const express = require('express');
const app = express();

app.get('/hello', (req, res) => {
  res.send('Hello from Express!');
});

app.listen(3000);
```
