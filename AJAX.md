# Ajax
  - Ajax is a group of different technologies that work together to allow a website to communicate with a server in the background without requiring the website to reload in order to display new changes.
    - when a change happens, the server is no longer responsible for updating the HTML and then sending the entire HTML document back
    - Instead, the server would send back data about the change, either in an XML or JSON format, and the website could then process that data and update the DOM accordingly

#### JavaScript is the engine behind AJAX
  - When the data comes back from the server, JavaScript can also then be used to make the necessary updates to the DOM.

### XML
  - The XML portion of this acronym is outdated. In the early days of AJAX, after successfully updating the book's status to "Want To Read", the server would send back data in XML format, like so:

  ```js
    <?xml version="1.0" encoding="UTF-8"?>
    <book>
        <id>29633913</id>
        <status>Want To Read</status>
    </book>
  ```
  - Nowadays, XML has been largely replaced by JSON, and you will almost always be dealing with a JSON response from a server that might look like this:
```js
    {
      "book": {
        "id": 29633913,
        "status": "Want to Read"
      }
    }
```

### Fetch
- API
- At a high level, **Fetch is used to make HTTP requests.**
- It uses **Promises** to handle the asynchronous nature of HTTP requests and responses.

  #### GET Request
  - **Default request**
  - GET requests are used to retrieve information from the server
  - Here's what a GET request might look like using the Fetch API:
    ```js
      fetch("https://jservice.xyz/api/games")
        .then(function(res) {
          console.log("response: ", res);
          return res.json();
        })
        .then(function(data) {
          console.log("data:", data);
        });
    ```

    ##### Arguments:
    - `fetch`'s first argument is the URL that you want to make a request to (the path to the resource you want to fetch)
    - The second argument is an optional `options` object

    ##### Invoking `fetch`:
    - Invoking `fetch` returns a Promise that resolves with a Fetch Response object.
      - This Response object represents the entire HTTP response, and it holds crucial information like `status` and `url`.

    ##### Callbacks:
    - In the first callback, the body of the response is a **ReadableStream** (represents a readable stream of byte data).
      - the `.json()` method takes that stream and returns a promise that resolves with the result of parsing the body text as JSON
      - The `.json()` method is the equivalent of using `JSON.parse()` except that it works on a ReadableStream instead of just a string.
    - In the second callback, you can now access the data found in the body of the response

  #### POST Request
  - POST requests are used to create data on the server.


  ```js
    // with promises/catch
    const handleClick = () -> {
      fetch("/name")
        .then(res => {
          if (!res.ok) {
            throw res;
          }
        })
        .then(data => {
          document.querySelector('h1').innerHTML = data.name;
        })
        .catch(err => {
          err.json().then(errorJSON => {
            document.querySelector('div').innerHTML = errorJSON.message
          });
        });
    };

    // with async/await
    const handleClick = () => {
      const res = await fetch('/name');
      // localhost: 3000/name
      const json = await res.json();
      debugger
      if (!res.ok) {
        document.querySelector('h1').innerHTML = json.error;  
      } else {
        document.querySelector('div').innerHTML = json.name  
      }
    }

    document.querySelector('button').addEventListener('click', handleClick)
  ```

img src="https://assets.aaonline.io/Module-Web/ajax/ajax.svg" height="500"/>

  - In this file, you'll be setting up event listeners and implementing AJAX requests using the Fetch API.

  - launch the server by running npm start, and then go to your browser and navigate to localhost:3000.
