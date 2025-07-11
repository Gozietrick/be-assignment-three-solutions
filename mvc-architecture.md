//1) What is the MVC (Model-View-Controller) pattern and how does it help organize code?

//Solutions
The MVC (Model-View-Controller) pattern is a software architectural pattern that separates an application into three main components:

- **Model:** Lets see this as the Kitchen where food/data is prepared. It manages the data and business logic of the application. It represents the application's state and handles data storage, retrieval, and validation.
- **View:** Lets see this as the dining area. It handles the presentation layer. It displays data from the model to the user and sends user commands to the controller.
- **Controller:** Lets see this as tyhe waiter(takes ordesrs, deliver food, handles request). It acts as an intermediary between the model and the view. It receives user input from the view, processes it (often updating the model), and returns the output display to the view.

**How it helps organize code:**
- Separates concerns, making code easier to manage and maintain.
- Allows developers to work on different parts (data, UI, logic) independently.
- Improves scalability and testability by keeping business logic, user interface, and and testability by keeping business logic, user interface, and input handling separate.
It is used in frameworks like Express.js, Django, Ruby on rails and so on. They support the MVC pattern. 

//2) Explain the responsibilities of each component in the MVC pattern:
Controller: What does it handle?
Service: What business logic does it contain?
Schema/Model: What data structure does it define?

//Solutions

**Controller:**  
This handles incoming HTTP requests, processes user input, calls the appropriate service or model methods, and returns responses to the client. It acts as the bridge between the view and the business logic. We can think of it as the "front desk" that receives and routes requests

**Service:**  
This contains the core business logic of the application. Services perform operations such as calculations, data processing, and coordination between models. They implement the rules and workflows of the application, keeping controllers thin. Its can be seen like the "engine room" where the real work happens. 

**Schema/Model:**  
It defines the data structure and schema for the application's data. Models represent and manage the data, handle validation, and interact with the database or data source. It can be seen "Blueprint" and interfaceb to the database. it handles databse CRUD opeartions (using Sequelize, Mongoose and others)



