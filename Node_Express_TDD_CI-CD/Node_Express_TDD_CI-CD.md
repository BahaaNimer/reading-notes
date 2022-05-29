# Node.js

    It is open-source,cross-platform runtime environment, you can use it to create all kinds of server-side tools and applications in JavaScript.

- And the runtime it's for use outside of a browser context.

> In other meanning you can runtime directly on a computer or server OS.

- Code is written in _"plain old JavaScript"_, which means that less time is spent dealing with "context shift" between languages when you're writing both client-side and server-side code.

- Node was designed to optimize throughput and scalability in web applications and is a good solution for many common web-development problems.

- JavaScript is a relatively new programming language and benefits from improvements in language design when compared to other traditional web-server languages.

- It is available on Microsoft Windows, macOS, Linux, Solaris, FreeBSD, OpenBSD, WebOS, and NonStop OS.

- It is well-supported by many web hosting providers, that often provide specific infrastructure and documentation for hosting Node sites.

- It has a very active third party ecosystem and developer community.

### You can use Node.js to create a simple web server using the Node HTTP package.

```js
// Load HTTP module
const http = require('http');

const hostname = '127.0.0.1';
const port = 8000;

// Create HTTP server
const server = http.createServer(function (req, res) {
  // Set the response HTTP header with HTTP status and Content type
  res.writeHead(200, { 'Content-Type': 'text/plain' });

  // Send the response body "Hello World"
  res.end('Hello World\n');
});

// Prints a log once the server starts listening
server.listen(port, hostname, function () {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

You can run the server :

```js
node hello.js
```

And you can use these methods :

```js
GET, POST, DELETE, PUT;
```

# Express

    it's the most popular Node web framework.

- Write handlers for requests with different HTTP verbs at different URL paths (routes).

- Integrate with "view" rendering engines in order to generate responses by inserting data into templates.

- Set common web application settings like the port to use for connecting, and the location of templates that are used for rendering the response.

- Add additional request processing "middleware" at any point within the request handling pipeline.

      Express is unopinionated.

To use Express :

```js
const express = require('express');
const app = express();
const port = 3000;

app.get('/', function (req, res) {
  res.send('Hello World!');
});

app.listen(port, function () {
  console.log(`Example app listening on port ${port}!`);
});
```

Importing modules :

```js
const module-name = require('module-name');
const app = module-name();
```

Exporting a methods form object :

```js
exports.method-name = function();
exports.method-name2 = function();
```

Export a complete object :

```js
module.exports = {
method-name: function(),
method-name2: function();
}
```

> Node is a single-threaded event-driven execution environment.

## Express methods :

```js
checkout(), copy(), delete(), get(), head(), lock(), merge(), mkactivity(), mkcol(), move(), m-search(), notify(), options(), patch(), post(), purge(), put(), report(), search(), subscribe(), trace(), unlock(), unsubscribe().
```

> There is a special routing method, "app.all()", which will be called in response to any HTTP method.

You can use express router :

```js
// wiki.js - Wiki route module

const express = require('express');
const router = express.Router();

// Home page route
router.get('/', function(req, res) {
res.send('Wiki home page');
});

// About page route
router.get('/about', function(req, res) {
res.send('About this wiki');
});

module.exports = router;

and you can access it:
const wiki = require('./wiki.js');
// ...
app.use('/wiki', wiki);
```

Middleware :

    is a functions typically perform some operation on the request or response and then call the next function in the "stack".

> The only difference between a middleware function and a route handler callback is that middleware functions have a third argument next.

```js
const express = require('express');
const app = express();

// An example middleware function
let a_middleware_function = function (req, res, next) {
  // ... perform some operations
  next(); // Call next() so Express will call the next middleware function in the chain.
};

// Function added with use() for all routes and verbs
app.use(a_middleware_function);

// Function added with use() for a specific route
app.use('/someroute', a_middleware_function);

// A middleware function added for a specific HTTP verb and route
app.get('/', a_middleware_function);

app.listen(3000);
```

    You can use the express.static middleware to serve static files, including your images, CSS and JavaScript (static() is the only middleware function that is actually part of Express).

```js
app.use(express.static('directory-name'));
```

You can call it :

```js
http://localhost:3000/images/dog.jpg
http://localhost:3000/css/style.css
http://localhost:3000/js/app.js
http://localhost:3000/about.html
```

You can call static() multiple times to serve multiple directories.

```js
app.use(express.static('directory-name'));
app.use(express.static('directory-name2'));
```

You can also create a virtual prefix for your static URLs.

```js
app.use('/media', express.static('directory-name'));
```

you can call it:

```js
http://localhost:3000/media/images/dog.jpg
http://localhost:3000/media/video/cat.mp4
http://localhost:3000/media/cry.mp3
```

## Handling errors :

```js
app.use(function (err, req, res, next) {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});
```

> But must be called after all other app.use() and routes calls so that they are the last middleware in the request handling process!

## Using databases :

first:

```js
npm install mongodb
```

Example :

```js
//for mongodb version 3.0 and up
const MongoClient = require('mongodb').MongoClient;
MongoClient.connect(
  'mongodb://localhost:27017/animals',
  function (err, client) {
    if (err) throw err;

    let db = client.db('animals');
    db.collection('mammals')
      .find()
      .toArray(function (err, result) {
        if (err) throw err;
        console.log(result);
        client.close();
      });
  }
);
```

# NPM

    npm is the world's largest software registry. Open source developers from every continent use npm to share and borrow packages, and many organizations use npm to manage private development as well.

npm consists of three distinct components:

- the website
- the Command Line Interface (CLI)
- the registry

## Use npm to . . .

- Adapt packages of code for your apps, or incorporate packages as they are.

- Download standalone tools you can use right away.

- Run packages without downloading using **npx**.

- Share code with any npm user, anywhere.

- Restrict code to specific developers.

- Create organizations to coordinate package maintenance, coding, and developers.

- Form virtual teams by using organizations.

- Manage multiple versions of code and code dependencies.

- Update applications easily when underlying code is updated.

- Discover multiple ways to solve the same puzzle.

- Find other developers who are working on similar problems and projects.

# TDD

    “Test-driven development” refers to a style of programming in which three activities are tightly interwoven: coding, testing (in the form of writing unit tests) and design (in the form of refactoring).

## It can be succinctly described by the following set of rules :

write a “single” unit test describing an aspect of the program.

run the test, which should fail because the program lacks that feature.

write “just enough” code, the simplest possible, to make the test pass.

“refactor” the code until it conforms to the simplicity criteria.

repeat, “accumulating” unit tests over time.

## Common Pitfalls :

> Typical individual mistakes include :

- forgetting to run tests frequently

- writing too many tests at once

- writing tests that are too large or coarse-grained

- writing overly trivial tests, for instance omitting assertions

- writing tests for trivial code, for instance accessors

> Typical team pitfalls include :

- partial adoption – only a few developers on the team use TDD

- poor maintenance of the test suite – most commonly leading to a test suite with a prohibitively long running time

- abandoned test suite (i.e. seldom or never run) – sometimes as a result of poor

- maintenance, sometimes as a result of team turnover

# CI/CD

## CI :

Continuous Integration

- rnsure everyone's changes integrate
- catch bugs
- reduce merge conflicts

## CD :

Continuous Delivery

- develop to release at any time

Continuous Deployment

- deploy new features immediately
