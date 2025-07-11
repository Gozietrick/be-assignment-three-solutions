//1) Compare and contrast in-memory storage vs. file-based storage:
What are the advantages and disadvantages of each?
When would you choose one over the other?
How does data persistence affect application restart behavior?

**In-memory storage:**
- **Advantages:**
  - Very fast read/write operations since data is stored in RAM.
  - Simple to implement for temporary or small-scale data.
- **Disadvantages:**
  - Data is lost when the application stops or restarts (not persistent).
  - Limited by available system memory.
  - Not suitable for large datasets or long-term storage.

**File-based storage:**
- **Advantages:**
  - Data is persistent—remains available after application restarts or crashes.
  - Can handle larger datasets than memory (limited by disk space).
  - Simple to implement for basic persistence needs.
- **Disadvantages:**
  - Slower read/write operations compared to memory.
  - Can become complex to manage as data grows (e.g., concurrency, corruption).
  - Not as scalable or performant as database solutions for large applications.

**When to choose each:**
- Use **in-memory storage** for caching, temporary data, or when speed is critical and persistence is not required.
- Use **file-based storage** when you need data to persist across restarts, for logging, or for simple applications that do not require a full database.

**Effect on application restart behavior:**
- With **in-memory storage**, all data is lost when the application restarts.
- With **file-based storage**, data is retained and can be reloaded when the application

//2) Explain the file-based database implementation:
How does the readFromFileDb() function work?
What happens when the JSON file doesn't exist?
How do you handle concurrent access to the same file?

//Solutions

**How does the readFromFileDb() function work?**  
The `readFromFileDb()` function typically reads data from a JSON file on disk, parses the file content, and returns it as a JavaScript object or array. It usually uses Node.js's `fs.readFileSync` or `fs.promises.readFile` to read the file, then `JSON.parse()` to convert the file content from a string to a usable object.

**What happens when the JSON file doesn't exist?**  
If the JSON file does not exist, the function should handle the error ( for "file not found") and return a default value (like an empty array or object). This prevents the application from crashing and allows it to start with an empty dataset.

**How do you handle concurrent access to the same file?**  
Concurrent access can cause data corruption if multiple processes read/write at the same time. To handle this:
- Use file locks or a queue to ensure only one write happens at a time.
- Use atomic write operations (write to a temp file, then rename).
- For simple apps, keep all file operations synchronous or use a single-threaded event loop.
- For more complex needs, consider using a database designed for concurrency.

**Example (basic read):**
```js
const fs = require('fs');
function readFromFileDb(path) {
  try {
    const data = fs.readFileSync(path, 'utf-8');
    return JSON.parse(data);
  } catch (err) {
    if (err.code === 'ENOENT') {
      return []; // File doesn't exist, return empty array
    }
    throw err;
  }
}
```

