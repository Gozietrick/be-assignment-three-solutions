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



REST API DESIGN
//1) What are the core principles of REST architecture and how do they apply to API design?

//Solutions
REST (Representational State Transfer) is an architectural style for designing networked applications. Its core principles are:

- **Statelessness:** Each request from a client to a server must contain all the information needed to understand and process the request. The server does not store any client context between requests.
- **Client-Server Architecture:** The client and server are separate entities. The client handles the user interface, while the server manages data and logic. This separation allows each to evolve independently.
- **Uniform Interface:** REST APIs have a consistent, standardized way of interacting with resources, typically using HTTP methods (GET, POST, PUT, DELETE) and clear URIs.
- **Resource-Based:** Everything is treated as a resource, identified by URIs. Resources can be manipulated using standard HTTP methods.
- **Stateless Communication:** Each request is independent; no session or context is stored on the server between requests.
- **Cacheability:** Responses must define themselves as cacheable or not to improve performance on the client side.
- **Layered System:** The architecture can be composed of hierarchical layers, with each layer only interacting with the adjacent one.

**Application to API Design:**
- Design endpoints around resources (e.g., `/users`, `/products`).
- Use standard HTTP methods for actions (GET for retrieve, POST for create, PUT/PATCH for update, DELETE for remove).
- Make APIs stateless—do not rely on server-side sessions.
- Use clear, consistent URIs and responses.
- Support caching where appropriate to improve efficiency.

**Example:**
A RESTful API for users might have:
- `GET /users` – Get all users
- `POST /users` – Create a new user
- `GET /users/123` – Get user with ID 123
- `PUT /users/123` – Update user 123
- `DELETE /users/123` – Delete user

//2) Explain the difference between GET, POST, PUT, and DELETE HTTP methods. When would you use each?

//Solutions
- **GET:**  
  Used to retrieve data from the server. It does not modify any data.  
  *Example:* Fetching a list of users with `GET /users`.

- **POST:**  
  Used to send data to the server to create a new resource.  
  *Example:* Creating a new user with `POST /users`.

- **PUT:**  
  Used to update an existing resource or create it if it does not exist. Usually replaces the entire resource.  
  *Example:* Updating user information with `PUT /users/123`.

- **DELETE:**  
  Used to remove a resource from the server.  
  *Example:* Deleting a user with `DELETE /users/123`.

//3) How do you structure RESTful endpoints for a resource like "books" or "todos"?

//Solutions
RESTful endpoints are structured around resources using clear and consistent URIs and HTTP methods. Just it said in class, for a resource like "books" or "todos", you typically use the following patterns:

**For "books":**
- `GET /books` – Get a list of all books
- `POST /books` – Create a new book
- `GET /books/:id` – Get a single book by its ID
- `PUT /books/:id` – Update a book by its ID (replace the whole book)
- `PATCH /books/:id` – Update part of a book by its ID (partial update)
- `DELETE /books/:id` – Delete a book by its ID

**For "todos":**
- `GET /todos` – Get all todos
- `POST /todos` – Create a new todo
- `GET /todos/:id` – Get a specific todo by ID
- `PUT /todos/:id` – Update a todo by ID
- `DELETE /todos/:id` – Delete a todo by ID

- Plural nouns is used for resource names (e.g., `/books`, `/todos`).
- Path parameters (e.g., `:id`) is used to identify specific resources.
- The appropriate use of HTTP method for action like (GET, POST, PUT, PATCH, DELETE).
- Keep URIs intuitive and hierarchical, reflecting the resource structure.