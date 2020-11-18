# Express.js

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

#### Requests
##### Configure The Routing For Your Application
- **Routing** refers to determining how an application should respond to a client request
  - Each route can have one or more handler functions, which are executed when the route is matched.
- Route definition takes the following structure:
` app.METHOD(PATH, HANDLER)`
  - `app` is an instance of express.
  - `METHOD` is an HTTP request method, in lowercase.
      - `get()` - to handle GET requests
        ```js
        app.get('root/path/', (req, res) => {
          // To send a plain text response to the client, call the res.send() method passing in the desired content
          res.send('Hello from Express!');
        });
        ```
      - `post()` - to handle POST requests
        ```js
        app.post('/', function (req, res) {
          res.send('Got a POST request')
        })
        ```
      - `put()` - to handle PUT requests
        ```js
        app.put('/user', function (req, res) {
          res.send('Got a PUT request at /user')
        })
        ```
      - `delete()` - to handle DELETE requests
        ```js
        app.delete('/user', function (req, res) {
          res.send('Got a DELETE request at /user')
        })
        ```
    - `GET` and `POST` are two of the most commonly used HTTP methods, followed by `PUT` and `DELETE`.
  - `PATH` is a path on the server.
  - `HANDLER` is the function executed when the route is matched.




#### Listening for HTTP Connections
- To start the server listening for HTTP connections from clients, call the `app.listen()` method passing:
  - The desired port to use
  - An *optional* callback function
  ```js
  const port = 8081;

  app.listen(port, () => console.log(`Listening on port ${port}...`));
  ```
---
### Express Methods

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

### Express Properties
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
