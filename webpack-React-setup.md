## **WEBPACK - REACT SET UP**
A few months ago, I built a Node.js app to scrape job websites and return a list of jobs that match a defined set of keywords.  

This app was run in Node.js with no frontend, simply returning an HTML string. 
I could have used create-react-app to bootstrap a React frontend. However, I wanted to take this opportunity to learn more about Webpack, and how to configure it. 

STEP 1:  
The app was run by running ```node index.js``` in Node.js. This would invoke several ‘scraping’ functions, save new results to the database and format them into an HTML table. 
However, ```index.js``` is what we conventionally name the file holding the server bits, so we moved the scraping functions into a ```scrape.js``` file. We then added a ‘scrape’ script in ```package.json```.  
The processes that were run with ```node index.js``` can now be run with ```npm run scrape```.

STEP 2:  
For the frontend to be able to talk to our backend, we need a server. We used Express.js. 
- Install Express.js in the project by running ```npm install express``` in the terminal. Express can now be found in the ```package.json``` file, that lists the project’s dependencies. 
- Require Express in our now-empty ```index.js``` file (line 1).
- Create an ```app``` variable by running ```express()``` (line 4)
- Create an endpoint (line 6) with a ```get``` HTTP method and a root (```‘/’```) path. When a request hits this endpoint, a ```file``` variable is created (line 7) and sent as a response (line 8). 

/index.js
```javascript
const express = require('express');
const fs = require('fs')

const app = express();

app.get('/', async (req, res) => {
  const file = fs.readFileSync('index.html').toString();
  res.send(file);
});

app.listen(4000, () => {
  console.log('listening on port 4000');
});
``` 
STEP 3:  
The Node.js file system module allows you to work with the file system on your computer. It is a native Node.js module (i.e.: no need to install it, just require it where you need it). 
We require ```fs``` on line 2 and use it with the ```readFileSync``` method on line 7. The method takes the name of the file to be read, as a string, and return the content of the file. We also use the ```toString()``` method as the response needs to be sent as a string. 
We now have an endpoint that serves the content of an ```index.html``` file. 

STEP 4:  
Next, we need to create this ```index.html``` file. At first it only contains a simple Hello World. After starting the server, we can go to <http://localhost:4000/> and see Hello World displayed on the page. Our server and endpoint are working!

STEP 5:  
So far we’re only sending HTML (that the browser can easily deal with) back to the client. However we want to use React for our frontend; that’s going to take a bit of compiling since React is written in jsx, that the browser can not read. 
First let’s install React and react-dom, and create a React component. 

/app.jsx
```javascript  
import React from 'react';
import ReactDom from 'react-dom';

const App = () => {
  return(
    <div>Hello Woooorld!</div> 
  )
}

ReactDom.render(
  <App />,
  document.getElementById('root')
);
```

We import React and ReactDom in our file (line 1 and 2). We then create a simple function component named ```App``` that returns a ```<div>``` tag containing some text (Hello Woooorld!). React-dom is used (line 10) as an interface between React and the DOM, effectively rendering our content in the browser.  
```ReactDom.render``` takes a component (```App```) and renders it (along with all its children, if any) in the element passed as an argument to the ```getElementById()``` method (here, ```‘root’```). 

STEP 6:  
We now need to go back to our ```index.html``` file and actually give it some HTML! 
We create a ```<div>``` with a ‘root’ id so that React-dom knows where to render our jsx. We also need a ```<script>``` tag. It points to the external script file ```assets/bundle.js``` and define the client-side script. 

/index.html
```html  
<html>
  <head>
    <title>Job Search App</title>
  </head>
  <body>
    <div id="root"></div>
    <script src="/assets/bundle.js"></script>
  </body>
</html>
``` 

What’s happening now when our ```‘/’``` endpoint gets hit is:
- Node’s file system reads our ```index.html``` file.
- ```index.html``` has a script tag that point to ```assets/bundle.js```
Except it's is still empty so nothing’s happening.

STEP 7:  
Bundling!  
For our React/jsx code to be used inside the HTML, it needs to be compiled/bundled. We’re using Webpack to do so. 
We first need to install it on our project, along with a bunch of Babel packages. We also install webpack-cli (=Command Line Interface) as, apparently, we need it to use webpack from the command line. 
We create a ```webpack.config.js``` file and at this point I just copy and paste the config from a previous project. 

/webpack.config.js
```javascript
const path = require('path');

module.exports = {
  mode: 'development',
  devtool: 'source-map',
  entry: ['@babel/polyfill', './ui/app.jsx'],
  output: {
    path: path.resolve(__dirname, 'assets'),
    filename: 'bundle.js',
  },
  module: {
    rules: [
      {
        test: /\.js[x]?$/,
        exclude: '/node_modules/',
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env','@babel/preset-react'],
          },
        },
      },
    ],
  },
};
```

I don’t exactly know what everything does here but we can work some of it out:
- mode: development 
- entry: second element is where our React code is (= input for the bundling).
- output: the compiled code will be stored as ```bundle.js``` in the ```assets``` folder.  

The rest is more config, including files to be ignored (such as node_modules).  
We also add a new script to our ```package.json``` file:
```javascript
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "scrape": "node scrape.js",
    "build-assets": "webpack", // webpack script 
    "start": "node index.js"
  },
```
We can now run ```npm run build-assets``` to bundle our React code with webpack. It will be saved as ```bundle.js``` in the ```assets``` folder.

STEP 8:  
We’re adding a line to our ```index.js``` file:
``` javascript
const fs = require('fs')
const express = require('express');

const app = express();

app.get('/', async (req, res) => {
  const file = fs.readFileSync('index.html').toString();
  res.send(file);
});

app.use('/assets', express.static('assets')); // line added here

app.listen(4000, () => {
  console.log('listening on port 4000');
});
```

This is used to serve static files from the ```assets``` folder, where our bundled code now lives.

That’s it! After bundling the code (```npm run build-assets```), we can start the server (```npm start```) and go to <http://localhost:4000/> to see our React component rendered in the browser!
  
![](./blog-image1.png)

