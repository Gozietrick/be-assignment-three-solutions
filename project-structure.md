//1) Analyze the project structure of the fs-books application:
Why is the code organized into separate directories (books/, common/, routes/)?
How does this structure support scalability and maintainability?
What are the benefits of having separate files for controllers, services, and schemas?

//Solutions

**Why is the code organized into separate directories (books/, common/, routes/)?**  
- The `books/` directory contains all files related to the "books" resource, such as its controller, service, and schema/model.
- The `common/` directory holds shared utilities, helpers, or error classes that can be reused throughout the application.
- The `routes/` directory defines the API endpoints and connects them to the appropriate controllers.

**How does this structure support scalability and maintainability?**  
- It groups related code together, making it easier to find, update, and manage.
- As the app grows, new features or resources can be added as new directories without cluttering the main folder.
- Shared logic in `common/` avoids code duplication and simplifies updates.

**Benefits of having separate files for controllers, services, and schemas:**  
- **Controllers** handle HTTP requests and responses, keeping route logic clean.
- **Services** contain business logic, making it reusable and testable, and keeping controllers focused.
- **Schemas/Models** define the data structure and validation, separating data concerns from logic and presentation.

This separation of concerns improves code readability, makes testing easier, and allows multiple developers to work on different parts of the application without conflicts.

//2) Explain the role of the utils.common.js file:
What utility functions are typically included?
How do these functions promote code reuse across the application?

//Solutions

**Role of the utils.common.js file:**  
This file contains utility functions that are commonly needed across different parts of the application. It acts as a shared toolbox for reusable logic that doesn't belong to a specific feature or resource.

**Typical utility functions included:**  
- Data validation helpers (e.g., checking if a value is empty or valid)
- Error formatting or response helpers
- Functions for generating unique IDs
- Date/time formatting utilities
- File read/write helpers
- Any generic function used in multiple modules

**How these functions promote code reuse:**  
- Centralizes common logic, so you write and maintain it in one place.
- Reduces code duplication, making the codebase cleaner and easier to update.
- Makes it easy to apply consistent logic or formatting throughout the app.
- Improves maintainability, since changes to a utility function automatically apply everywhere it's used.
