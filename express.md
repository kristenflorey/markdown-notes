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
- determining how an application should respond to a client request

- The Express Application (`app`) object contains a collection of methods for defining an application's routes:
  - `get()` - to handle GET requests
  - `post()` - to handle POST requests
  - `put()` - to handle PUT requests
  - `delete()` - to handle DELETE requests
- `GET` and `POST` are two of the most commonly used HTTP methods, followed by `PUT` and `DELETE`.

##### Application
| Methods          | Properties      |
|-----------------|-----------------|
| `app.delete()`  | `app.locals`    |
| `app.disable()` | `app.mountpath` |
| `app.enable()`  |                 |
| `app.engine()`  |                 |
| `app.get()`     |                 |
| `app.listen()`  |                 |
| `app.METHOD()`  |                 |
| `app.param()`   |                 |
| `app.path()`    |                 |
| `app.post()`    |                 |
| `app.put()`     |                 |
| `app.render()`  |                 |
| `app.route()`   |                 |
| `app.set()`     |                 |
| `app.use()`     |                 |



- To define a route to handle requests, call the app.get() method passing:
  - the route path
  - a route handler function
  ```js
  app.get('root/path/', (req, res) => {
    // To send a plain text response to the client, call the res.send() method passing in the desired content
    res.send('Hello from Express!');
  });
  ```
#### Requests
| Properties          | Methods                  |
|---------------------|--------------------------|
| `req.app`           | `req.accepts()`          |
| `req.baseURL`       | `req.acceptsCharsets()`  |
| `req.body`          | `req.acceptsEncodings()` |
| `req.cookies`       | `req.acceptsLanguages()` |
| `req.fresh`         | `req.get()`              |
| `req.hostname`      | `req.is()`               |
| `req.ip`            | `req.param()`            |
| `req.ips`           | `req.range()`            |
| `rep.method`        |                          |
| `req.originalUrl`   |                          |
| `req.params`        |                          |
| `req.path`          |                          |
| `req.protocol`      |                          |
| `req.query`         |                          |
| `req.route`         |                          |
| `req.secure`        |                          |
| `req.signedCookies` |                          |
| `req.stale`         |                          |
| `req.subdomains`    |                          |
| `req.xhr`           |                          |

#### Responses

| Methods         | Properties        |
|-----------------|-------------------|
| `res.append()`      | `res.app`         |
| `res.attachment()`  | `res.headersSent` |
| `res.cookie()`      | `res.locals`      |
| `res.clearCookie()` |                   |
| `res.download()`    |                   |
| `res.end()`         |                   |
| `res.format()`      |                   |
| `res.get()`         |                   |
| `res.json()`        |                   |
| `res.jsonp()`       |                   |
| `res.links()`       |                   |
| `res.location()`    |                   |
| `res.redirect()`    |                   |
| `res.render()`      |                   |
| `res.send()`        |                   |
| `res.sendFile()`    |                   |
| `res.sendStatus()`  |                   |
| `res.set()`         |                   |
| `res.status()`      |                   |
| `res.type()`        |                   |
| `res.vary()`        |                   |

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
-
---
-
---
-
---
-
---
-
---
-
---
-
---
-
---
