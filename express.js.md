## **EXPRESS.JS**

Express.js is an npm library. It’s the de facto server framework for Node.js.  
As a server framework, Express.js handles HTTP requests and responds accordingly.  
When we run Express, it gives us an object that has HTTP methods (GET, POST being the most commonly used), and request and response objects.  
When a request comes into the server, Express matches the request’s path and methods to the routes that we’ve defined in our code. It can interpret part of the path as parameters for the request.  
When we define our routes, we use an HTTP method on the Express object, and give it as arguments an endpoint (as a string) and a callback function to run when a request is matched to this route. In this case, the callback function is usually called a controller.  
The request object contains data: all the information about the request. If a body was attached to the request, we can access it like so: request.body. To access the request’s parameters, we use request.params, and so on.  
The response object is used by the controller to build a response, and to send it back to the client. The response can sometimes be informed by the request, or just be a status code to let the client know that the request was (un)successfully handled. 

Installing ```Express.js``` in our project’s directory from the command line:
```
============================  ~/workspace/express-app 
$ npm install express
```
Hit enter and the Express.js library will be installed in our project. Note that we need to be inside our project directory to run this command. We can check that the installation was successful by looking at the dependencies property of our package.json.

#### Creating a simple Express app ####

```javascript
//we require express to be able to use Express in this file:
const express = require('express') 
//running express() gives us an object whose properties (mostly methods) we can use to do server stuff:
const app = express() 
//we declare a variable holding the port on which our server will listen for requests:
const port = 3000 

//we use the get method, which takes a path (a string > '/') and a callback function
//when app is listening and a request come to the route './', the callback function is ran
app.get('/', (req, res) => res.send('Hello World!'))

//we use the listen method to tell app to start listening on the port previously defined 
//here, we also give it a callback function that prints a message to the console if the server was successfully started
app.listen(port, () => console.log(`Example app listening on port ${port}!`))
```

The code above is saved in an index.js file inside the express-app project.
When we run it in the terminal like so,
```
============================  ~/workspace/express-app 
$ node index.js
``` 
the app starts a server and listens on port 3000 for connections. 

We can now go to our browser and see the output by loading:
http://localhost:3000/  
The app responds with “Hello World!” to requests to the root URL (/) or route. For every other path, it will respond with a 404 Not Found.

Here it is! Say hello back to our express app! 

![Here it is! Say hello back to our express app!](./blog-image2.png)

 

#### Basic routing ####

Routing refers to the ways an application responds to a client request to a particular endpoint, which consists of a URI (or path) and a specific HTTP request method (GET, POST, and so on).
Each route can have one or more handler functions, which are executed when the route is matched.  

Structure of the route definition:

![](./blog-image3.png)

	

 
