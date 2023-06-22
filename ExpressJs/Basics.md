## Introduction
Express.js is a popular web application framework for Node.js (a JavaScript runtime environment). It provides a simple and flexible way to builder web applications and APIs. Express.js is known for its minimalistic approach and focuses on providing a robust set of features for creating server-side applications. It is widely used for developing both small and large-scale web apps.

##### Key features
1. Routing: Express.js allows you to define routes to handle different HTTP methods and URLs. You can specify callback functions (middleware) to be executed when a particular route is accessed.
2. Middleware: Middleware functions in Express.js are functions that have access to the request and response objects and can modify them. Middleware functions can perform tasks like parsing request bodies, handling authentication, logging, error handling and more.
3. Templating Engines: Express.js supports various templating engines like EJS, Puh, Handlebars, etc, which enable you to dynamically render HTML templates.
4. Error handling: Express.js provides mechanisms for handling errors and defining error-handling middleware. This allows you to centralize error handling and provides a consistent way to handle and respond to errors.
5. Middleware and Route Modularization: Express.js allows you to break your application's code into modular components using middleware and routers. This helps in organizing code and improving maintainability.

#### Examples and explanation
###### Basic server
```
const express = require('express');
const app = express();

app.get('/', (req, res) => {
    res.send('Hello, World!');
});

app.listen(3000, () => {
    console.log('Server started on port 3000');
});
```
This first example code sets up a basic Express server. It starts by importing the Express module and creating an Express application (`app`). The `app.get()` method defines a route for the root URL ("/") using the HTTP GET method. When a GET request is made to the root URL, the callback function is executed, which sends the response "Hello, World!" back to the client. Finally, the server starts listening on port 3000, and a message is logged to the console.

###### API Endpoint
```
app.get('/api/users', (req, res) => {
    // Logic to fetch users from database or external API
    const users = [{ name: 'John', age: 25}, {name: 'Jane', age: 30 }];
    res.json(users);
});
```
Here an API endpoint is defined for the URL "/api/users" using the HTTP GET method. When a GET request is made to this URL, the callback function is executed. Typically you would have logic inside this callback to fetch users from a database or an external API. In this example, we have a static array of users, and the `res.json()` methos sends the users back to the client as a JSON response.

###### Middleware
```
const logger = (req, res, next) => {
    console.log('${req.method} ${req.url}');
    next();
};

app.use(logger);

app.get('/', (req, res) =>{
    res.send('Hello, World!');
});
```
In this code a custom middleware function called `logger` is defined. Middleware functions have access to the request (`req`) and response (`res`) objects, as well as a `next` parameter that represents the next middleware function in the chain. In this case, the `logger` functions logs the HTTP method (`req.method`) and URL (`req.url`) to the console and then calls `next()` to pass control to the next middleware or route handler. The `app.use()` method is used to register the `logger` middleware. When the server receives a request, the `logger` middleware is executed before the route handles, allowing you to perform tasks like logging, authentication, etc.

###### Static Files
```
app.user(express.static('public'));
```
This code sets up the serving of static files from a directory named "public". The `express.static()` middleware is used to server static files such as images, CSS files, and client-side JavaScript files. In this example, any file requested by the client will be looked for in the "public" directory.
For instance, if there is a file named "logo.png" inside the "public/images" folder, it can be accessed via the URL "http://localhost:3000/images/logo.png".
