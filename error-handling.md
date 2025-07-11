//1) Explain the catchAsync wrapper pattern:
How does it simplify error handling in async route handlers?
What happens if an error is thrown inside a catchAsync wrapped function?
Why is this pattern important for production applications?

//solutions

**catchAsync wrapper pattern:**  
The `catchAsync` pattern is a higher-order function that wraps asynchronous route handlers in Express.js. It automatically catches errors thrown in async functions and passes them to Express's error-handling middleware, so you don't need to write repetitive try-catch blocks in every async handler.

**How does it simplify error handling in async route handlers?**  
It removes the need for manual try-catch in each async route. Instead, you wrap your handler with `catchAsync`, and any error is automatically forwarded to the error middleware.

**What happens if an error is thrown inside a catchAsync wrapped function?**  
The error is caught and passed to the next middleware (usually the error handler) using `next(error)`. This ensures consistent error handling throughout your app.

**Why is this pattern important for production applications?**  
It prevents unhandled promise rejections, keeps code clean and DRY, and ensures all errors are handled in a centralized way, improving reliability and maintainability.

**Example:**
```js
const catchAsync = fn => (req, res, next) => {
  Promise.resolve(fn(req, res, next)).catch(next);
};

// Usage:
app.get('/route', catchAsync(async (req, res) => {
  // async code that might throw
}));
```

//2) How do you handle different types of errors in a REST API?
What HTTP status codes would you use for different error scenarios?
How do you provide meaningful error messages to API consumers?

//Solutions

**Handling different types of errors:**
- Use centralized error-handling middleware in Express to catch and respond to errors.
- Define custom error classes for different error types (e.g., NotFoundError, ValidationError).
- Catch errors in async code using patterns like `catchAsync`.

**Common HTTP status codes for error scenarios:**
- `400 Bad Request`: The client sent invalid data (e.g., validation errors).
- `401 Unauthorized`: Authentication is required or failed.
- `403 Forbidden`: The user is authenticated but not allowed to access the resource.
- `404 Not Found`: The requested resource does not exist.
- `409 Conflict`: There is a conflict with the current state (e.g., duplicate data).
- `500 Internal Server Error`: A generic server error occurred.

**Providing meaningful error messages:**
- Return a JSON response with a clear `message` property describing the error.
- Optionally include an `error` code or details for debugging (avoid exposing sensitive info in production).
- Example error response:
  ```json
  {
    "status": "error",
    "message": "User not found"
  }
  ```
- Always use consistent error response formats so API consumers can handle errors reliably.

**Example Express error handler:**
```js
app.use((err, req, res, next) => {
  res.status(err.statusCode || 500).json({
    status: 'error',
    message: err.message || 'Internal Server Error'
  });
});
```

