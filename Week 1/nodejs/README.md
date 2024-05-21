# NodeJS
### What is Node.js?
* Node.js is an open source server environment
* Node.js runs on various platforms (Windows, Linux, Unix, Mac OS X, etc.)
* Node.js uses JavaScript on the server

### What Can Node.js Do?
* Node.js can generate dynamic page content
* Node.js can create, open, read, write, delete, and close files on the server
* Node.js can collect form data
* Node.js can add, delete, modify data in your database

### What is a Node.js File?
* Node.js files contain tasks that will be executed on certain events
* A typical event is someone trying to access a port on the server
* Node.js files must be initiated on the server before having any effect
* Node.js files have extension ".js"

### Top 6 Node JS frameworks:
* 1.Express.js

Express.js, also called "Express," is a minimalist, fast Node.js backend framework. The software is open-source and is released under the MIT license.
* 2.Meteor.js

Meteor is a Node backend framework that is well-defined for JavaScript. It functions as an open-source database that is integrated into a framework and is sufficient to automate client modifications without the involvement of developers.
* 3.Koa.js

Koa.js is another open-source Node.js backend framework. The creators of Koa.js are the same ones who created Express.js. Koa is also very popular, as the framework has about 1 million downloads per week and around 90 companies use it for their website.
* 4.Sails.js
  
Sails.js is a Model-View-Controller (MVC) framework of Node.js adhering to the principle of "convention rather than configuration." This backend Node.js framework, inspired by Ruby on Rails, is used for backend development to quickly create REST APIs, real-time applications, or single-page applications.
* 5.Nest.js

The Node.js web framework called Nest.JS is designed to be combined with TypeScript. This feature allows the developer to create scalable and efficient server-side applications.
* 6.Hapi.js

Hapi.js is an open-source Node.js framework for backend suitable for developing high-performance and scalable web applications.

### Install Node.js
* Download: https://nodejs.org/en/download

Using windows: Install file .msi\
Using Linux: sudo apt install nodejs (install package manager: sudo apt install npm)

### Set up and test a Node.js with Express development environment
Create a file hello.js as follows:

```javascript
//Load HTTP module
const http = require("http");
const hostname = "127.0.0.1";
const port = 3000;

//Create HTTP server and listen on port 3000 for requests
const server = http.createServer((req, res) => {
  //Set the response HTTP header with HTTP status and Content type
  res.statusCode = 200;
  res.setHeader("Content-Type", "text/plain");
  res.end("Hello Hola\n");
});

//Listen for request on port 3000, and as a callback function have the port listened on logged
server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

Start the server by run file hello.js

<img src="https://github.com/pentest-khoa-02/TheMinh/blob/settingnodejs/image/Untitled3.png" width="456px" align="center">

Navigate to the URL http://127.0.0.1:3000 \
Complete!

<img src="https://github.com/pentest-khoa-02/TheMinh/blob/settingnodejs/image/Untitled4.png" width="456px" align="center">
