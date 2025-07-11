//1) What is middleware in Express.js and how does it work in the request-response cycle?

//Solutions
Middleware in Express.js is a function that has access to the request (req) and response (res) objects, as well as the next() function in the application's request-response cycle. Middleware can execute code, modify the request or response, end the request-response cycle, or pass control to the next middleware.

In the request-response cycle, middleware functions are executed in the order they are defined. Each middleware can perform tasks like logging, authentication, parsing request bodies, or handling errors before passing control to the next middleware or route handler.

**Example:**
```js
app.use((req, res, next) => {
  console.log('Middleware executed');
  next(); // Passes control to the next middleware or route handler
});
```

//2) Explain the purpose of each middleware used in the projects:
cors(): What problem does it solve?
helmet(): What security features does it provide?
compression(): How does it improve performance?
express.json(): Why is this necessary?


**cors():**  
Enables Cross-Origin Resource Sharing (CORS), allowing your API to be accessed from web pages hosted on different domains. It solves the problem of browsers blocking requests from different origins for security reasons.

**helmet():**  
Provides various security headers to help protect your app from common web vulnerabilities like cross-site scripting (XSS), clickjacking, and others by setting appropriate HTTP headers.

**compression():**  
Compresses HTTP responses using gzip or similar algorithms, reducing the size of data sent to clients. This improves performance by making responses faster to download.

**express.json():**  
Parses incoming requests with JSON payloads and makes the data available on `req.body`. It is necessary for handling JSON data sent in POST or PUT requests.

//3) How does middleware order affect the application's behavior?

//Solutions
Middleware order is important because Express.js executes middleware functions in the order they are defined in the code. Each middleware can modify the request or response, or even end the request-response cycle. If a middleware does not call `next()`, the request will not move to the next middleware or route handler.

- Middleware that needs to run for every request (like logging, CORS, or body parsing) should be defined early.
- Route-specific middleware should be placed before the routes they affect.
- Error-handling middleware should be defined after all other app routes and middleware.

**Incorrect order can cause:**
- Some middleware not to run.
- Requests being blocked or not reaching the intended route.
- Security or parsing middleware being skipped.

**Example:**
```js
app.use(cors());        // Should be first to handle CORS for all requests
app.use(express.json()); // Should be before routes to parse JSON bodies

app.use('/api', apiRoutes); // Routes

app.use(errorHandler);  // Error handler should be last
```
