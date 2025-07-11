//1) Analyze the sendResponse utility function:
What is the purpose of standardizing API responses?
How does this pattern help frontend developers?
What information should be included in a successful API response?

//Solution

**Purpose of standardizing API responses:**  
Standardizing API responses ensures that every response from the server follows a consistent structure. This makes it easier for clients to parse, handle, and display data or errors, regardless of which endpoint they are calling.

**How does this pattern help frontend developers?**  
- Frontend developers can reliably expect the same fields (like `status`, `message`, `data`) in every response, reducing the need for custom parsing logic.
- It simplifies error handling and UI updates, since the response format is predictable.
- Makes debugging and integration faster, as developers know what to expect from the API.

**What information should be included in a successful API response?**  
A successful API response should typically include:
- `status`: Indicates success (e.g., "success" or HTTP status code).
- `message`: A human-readable message describing the result.
- `data`: The actual data payload returned by the API (can be an object, array, etc.).
- Optionally, `meta` information for pagination or additional context.

**Example:**
```json
{
  "status": "success",
  "message": "Book created successfully",
  "data": {
    "id": 1,
    "title": "Example Book"
  }
}
```

//2) Design a consistent error response format:
What fields should be included in error responses?
How can you make error messages helpful for debugging while being safe for production?

//Solutions

**Fields to include in error responses:**
- `status`: Indicates an error (e.g., "error" or "fail").
- `message`: A user-friendly description of the error.
- `errorCode` (optional): A custom code for identifying the error type.
- `details` (optional): Additional information for debugging (only in development).
- `stack` (optional): Stack trace for debugging (only in development).

**Making error messages helpful and safe:**
- In production, provide clear but generic messages to avoid exposing sensitive details.
- In development, include detailed error info and stack traces to help with debugging.
- Use environment checks to control what information is sent in the response.

**Example error response (production):**
```json
{
  "status": "error",
  "message": "Resource not found"
}
```

**Example error response (development):**
```json
{
  "status": "error",
  "message": "Resource not found",
  "errorCode": "NOT_FOUND",
  "details": "No book found with ID 123",
  "stack": "Error: ...stack trace..."
}
```