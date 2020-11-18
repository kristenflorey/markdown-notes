# Express.js

#### Jump to...
  - [Routing](#routing)
    - [Methods](#routingmethods)
    - [Paths](#paths)
    - [Parameters](#parameters)
    - [Handlers](#handlers)
  - [Middleware](#middleware)
  - [Express Properties](#properties)
  - [Express Methods](#methods)
#### Installing Express
- Open terminal window in your project folder and initialize npm
`npm init -y`
- This should install  `package.json` and  `package-lock.json` in the root of your project.
- Install Express 4.0
`npm install express@^4.0.0`
- The `package.json` file will now list Express as a dependency:
```json
{
 "name": "my-project-folder-name",
 "version": "1.0.0",
 "description": "",
 "main": "index.js",
 "scripts": {
   "test": "echo \"Error: no test specified\" && exit 1"
 },
 "keywords": [],
 "author": "",
 "license": "ISC",
 "dependencies": {
   "express": "^4.17.1"
 }
}
```

#### Creating an Express Application
- Add a file named `app.js` and open in your code editor
- Use the `require` directive to import the `express` model and assign it to a variable named `express`.
```js
const express = require('express');
```
- Assign the return value from the `express` function call to a variable named `app`:
```js
const app = express();
```
- The `app` variable holds a reference to an Express Application (`app`) object. You'll call methods on the `app` object as you build out your web application.

### Routing <a id="routing"></a>
- **Routing** refers to determining how an application should respond to a client request
  - Each route can have one or more handler functions, which are executed when the route is matched.
- Route definition takes the following structure:
` app.METHOD(PATH, HANDLER)`
  - `app` is an instance of express.
  - `METHOD` is an HTTP request method, in lowercase.
  - `PATH` is a path on the server.
  - `HANDLER` is the function executed when the route is matched.
#### Route Methods <a id="routingmethods"></a>
- A route method is derived from one of the HTTP methods, and is attached to an instance of the express class.
  - `GET` and `POST` are two of the most commonly used HTTP methods, followed by `PUT` and `DELETE`.

- #### `get()`
  - to handle GET requests
  ```js
  app.get('/', function (req, res) => {
    res.send('Hello from Express!');
  });
  ```
- #### `post()`
  - to handle POST requests
  ```js
  app.post('/', function (req, res) {
    res.send('Got a POST request')
  })
  ```
- #### `put()`
  - to handle PUT requests
  ```js
  app.put('/user', function (req, res) {
    res.send('Got a PUT request at /user')
  })
  ```
- #### `delete()`
  - to handle DELETE requests
  ```js
  app.delete('/user', function (req, res) {
    res.send('Got a DELETE request at /user')
  })
  ```
#### Route Paths <a id="paths"></a>
- Route paths, in combination with a request method, define the endpoints at which requests can be made.
  - Route paths can be strings, string patterns, or regular expressions.
  - Route paths can be based on regular expressions by surrounding search string with `/`s
[List of root paths](https://expressjs.com/en/guide/routing.html)

#### Route Parameters <a id="parameters"></a>
- Route parameters are named URL segments that are used to capture the values specified at their position in the URL.
  - The captured values are populated in the `req.params` object, with the name of the route parameter specified in the path as their respective keys.
    ```
    Route path: /users/:userId/books/:bookId
    Request URL: http://localhost:3000/users/34/books/8989
    req.params: { "userId": "34", "bookId": "8989" }
    ```
  - To define routes with route parameters, simply specify the route parameters in the path of the route as shown below.
    ```js
    app.get('/users/:userId/books/:bookId', function (req, res) {
      res.send(req.params)
    })
    ```

#### Route Handlers <a id="handlers"></a>
- You can provide multiple callback functions that behave like [middleware](#middleware) to handle a request.
- Route handlers can be in the form of a function, an array of functions, or combinations of both.
  - You can create chainable route handlers for a route path by using **`app.route()`**
  ```js
  app.route('/book')
  .get(function (req, res) {
    res.send('Get a random book')
  })
  .post(function (req, res) {
    res.send('Add a book')
  })
  .put(function (req, res) {
    res.send('Update the book')
  })
  ```
  - Use the `express.Router` class to create modular, mountable route handlers.
    - A `Router` instance is a complete middleware and routing system; for this reason, it is often referred to as a “mini-app”.

### Middleware <a id="middleware"></a>
- **Express is a routing and middleware web framework** that has minimal functionality of its own: An Express application is essentially a series of middleware function calls.
- Middleware functions are functions that have access to the request object (`req`), the response object (`res`), and the `next` function in the application’s request-response cycle.
  - The `next` function is a function in the Express router which, when invoked, executes the middleware succeeding the current middleware.
- Middleware functions can perform the following tasks:
  - Execute any code.
  - Make changes to the request and the response objects.
  - End the request-response cycle.
  - Call the next middleware in the stack.
- If the current middleware function does not end the request-response cycle, it must call `next()` to pass control to the next middleware function. Otherwise, the request will be left hanging.
```js
const express = require('express');
const app = express();

app.get('/', function(req, res, next) {
  next();
});

app.listen(3000)
```
- `.get()`: HTTP method for which the middleware function applies
- `'/'`: Path (route) for which the middleware function applies
- `function`: The middleware function
- `req`: HTTP request argument to the middleware function
- `res`: HTTP response argument to the middleware function
- **`next`**: Callback argument to the middleware function

#### Listening for HTTP Connections
- To start the server listening for HTTP connections from clients, call the `app.listen()` method passing:
  - The desired port to use
  - An *optional* callback function
  ```js
  const port = 8081;

  app.listen(port, () => console.log(`Listening on port ${port}...`));
  ```

#### Configurable Middleware
- If you need your middleware to be configurable, export a function which accepts an options object or other parameters, which, then returns the middleware implementation based on the input parameters.

```js
module.exports = function (options) {
  return function (req, res, next) {
    // Implement the middleware function based on the options object
    next()
  }
}
```  

The middleware can now be used as shown below.
```js
var mw = require('./my-middleware.js')

app.use(mw({ option1: '1', option2: '2' }))
```
An Express Application can use the following types of middleware:
  - ##### Application-level middleware
    - Bind application-level middleware to an instance of the `app` object by using the `app.use()` and `app.METHOD()` functions, where `METHOD` is the HTTP method of the request that the middleware function handles (such as `GET`, `PUT`, or `POST`) in lowercase.
  - ##### Router-level middleware
    - Router-level middleware works in the same way as application-level middleware, except it is bound to an instance of `express.Router()`.
    - Load router-level middleware by using the `router.use()` and `router.METHOD()` functions.
  - ##### Error-handling
    - Define [error-handling](https://expressjs.com/en/guide/error-handling.html) middleware functions in the same way as other middleware functions, except with four arguments instead of three, specifically with the signature (`err`, `req`, `res`, `next`)):
      ```js
      app.use(function (err, req, res, next) {
        console.error(err.stack)
        res.status(500).send('Something broke!')
      })
      ```
  - ##### Built-in middleware
  | Function                          | Action                                                      | Arguments                                                                        |
|-----------------------------------|-------------------------------------------------------------|----------------------------------------------------------------------------------|
| `express.static(root, [options])` | serves status assets such as HTML files, images, and so on. | `root`: specifies the root directory `options`: [options object](https://expressjs.com/en/4x/api.html#express.static) |
| `express.json([options])`         | parses incoming requests with JSON payloads                 | `options`: [options object](https://expressjs.com/en/4x/api.html#express.json)                                      |
| `express.urlencoded([options])`   | parses incoming requests with URL-encoded payloads          | `options`: [options object](https://expressjs.com/en/4x/api.html#express.urlencoded)                                      |
  - ##### Third-party middleware
    - Use third-party middleware to add functionality to Express apps.
    - Install the Node.js module for the required functionality, then load it in your app at the application level or at the router level.
    `$ npm install cookie-parser`
    - The following example illustrates installing and loading the cookie-parsing middleware function cookie-parser.
      ```js
      const express = require('express')
      const app = express()
      const cookieParser = require('cookie-parser')

      // load the cookie-parsing middleware
      app.use(cookieParser())
      ```

### Express Methods <a id="methods"></a>

- #### `express.json([options])`
- This is a built-in middleware function in Express. It parses incoming requests with JSON payloads and is based on body-parser.


| Request                  | Application    | Response            | Router            | Middleware         |
|--------------------------|----------------|---------------------|-------------------|--------------------|
| `req.accepts()`          | `app.delete()`     | `res.`append()` ()`     | `router.all()`    | `bodyParser()`     |
| `req.acceptsCharsets()`  | `app.disable()`    | `res.attachment()`  | `router.METHOD()` | `compress()`       |
| `req.acceptsEncodings()` | `app.enable()`     | `res.cookie()`      | `router.param()`  | `cookieParser()`   |
| `req.acceptsLanguages()` | `app.engine()`     | `res.clearCookie()` | `router.route()`  | `cookieSession()`  |
| `req.get()`              | `app.get()`        | `res.download()`    | `router.use()`    | `csrf()`           |
| `req.is()`               | `app.listen()`     | `res.end()`         |                   | `errorHandler()`   |
| `req.param()`            | `app.method()`     | `res.format()`      |                   | `methodOverride()` |
| `req.range()`            | `app.param()`  | `res.get()`         |                   | `morgan()`         |
|                          | `app.path()`   | `res.json()`        |                   | `responseTime()`   |
|                          | `app.post()`   | `res.links()`       |                   | `favicon()`        |
|                          | `app.put()`    | `res.location()`    |                   | `directory()`      |
|                          | `app.render()` | `res.redirect()`    |                   | `serveStatic()`    |
|                          | `app.route()`  | `res.render()`      |                   | `timeout()`        |
|                          | `app.set()`    | `res.send()`        |                   | `vhost()`          |
|                          | `app.use()`    | `res.sendFile()`    |                   | `session()`        |
|                          |                | `res.sendStatus()`  |                   |                    |
|                          |                | `res.set()`         |                   |                    |
|                          |                | `res.status()`      |                   |                    |
|                          |                | `res.type()`        |                   |                    |
|                          |                | `res.vary()`        |                   |                    |




### Express Properties <a id="properties"></a>
| Request             | Response          | Application     |
|---------------------|-------------------|-----------------|
| `req.app`           | `res.app`         | `app.locals`    |
| `req.baseUrl`       | `res.headersSent` | `app.mountpath` |
| `req.body`          | `res.locals`      |                 |
| `req.cookies`       |                   |                 |
| `req.fresh`         |                   |                 |
| `req.hostname`      |                   |                 |
| `req.ip`            |                   |                 |
| `req.ips`           |                   |                 |
| `req.method`        |                   |                 |
| `req.originalUrl`   |                   |                 |
| `req.params`        |                   |                 |
| `req.path`          |                   |                 |
| `req.protocol`      |                   |                 |
| `req.query`         |                   |                 |
| `req.route`         |                   |                 |
| `req.secure`        |                   |                 |
| `req.signedCookies` |                   |                 |
| `req.stale`         |                   |                 |
| `req.subdomains`    |                   |                 |
| `req.xhr`           |                   |                 |

###
