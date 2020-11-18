# Promises
- a `Promise` in JavaScript is a commitment that sometime in the future, your code will get a **value** from some operation (like reading a file or getting JSON from a Web site) or your code will get **an error** from that operation (like the file doesn't exist or the Web site is down).
- Creating `Promise` objects with the `Promise` constructor:
  - Accepts a function that has two parameters that are each functions themselves:
    - `resolve()` transitions the `Promise` object to the fulfilled state
    - `reject()` transitions the `Promise` object to the rejected state
```js
new Promise((resolve, reject) => {				
  // do some async stuff						
  // call resolve(value) to make the Promise succeed
  // call reject(reason) to make the Promise fail	 
});											
```

- `Promise`s can exist in three states:
  - **Pending**: The `Promise` object has not resolved. Once it does, the state of the `Promise` object may transition to either the fulfilled or rejected state.
  - **Fulfilled**: Whatever operation the `Promise` represented succeeded and your success handler will get called. Now that it's fulfilled, the `Promise`:
    - must not transition to any other state.
    - must have a value, which must not change.
    - fulfilled Promise objects can be created by using:
			`Promise.resolve(value)`
  - **Rejected**: Whatever operation the Promise represented failed and your error handler will get called. Now that it's rejected, the Promise:
    - must not transition to any other state.
    - must have a reason, which must not change.
    - If a `Promise` object transitions to the rejected state and no error handler exists for the `then`, then that `then` is skipped altogether.
- `Promise` objects have the following methods available on them so that you can handle the state change from pending to either fulfilled or rejected.
  - `then(successHandler, errorHandler)` is a way to handle a `Promise` when it leaves the pending state.
catch(errorHandler)
- The handlers mentioned in the previous list are:
  - **`Success Handler`** is a function that has one parameter, the value that a fulfilled `Promise` has.
  - **`Error Handler`** is a function that has one parameter, the reason that the `Promise` failed.

#### `then()`
- handles what will happen when the `Promise` comes out of the **pending** state.
- each returns another `Promise` that transitions out of it's pending state when the `then` that created it completes
- You can pass a second argument into the then method as the `error handler` (essentially saying, if this then does not resolve, then this error handler will do something.)
#### Chaining `then()`
- In the case of an error, the chain of `then`s will evaluate as:
  1. First `then`: I do not have an error handler. I will pass the error on and not run the success handler.
  2. Second `then`: I do not have an error handler. I will pass the error on and not run the success handler.
  3. Third `then`: I have an error handler and will run it.
- The success handler is called with the value of the operation of the `Promise` when the `Promise` object transitions to the fulfilled state. If an error condition occurs, them the error handler of the then is called.
- If a `Promise` object transitions to the rejected state and no error handler exists for the `then`, then that `then` is skipped altogether.
- If an error handler is called and does not raise an exception, then the next `Promise` object transitions to the fulfilled state and the next success handler is called.
#### `catch()`
- Rather than using a `then` with a success and error handler, you can use the similar `catch` method that takes just an error handler.

```js
promiseFunction("print")							
  .then(res => res)								
  .then(res => res)								
  .then(() => console.log(“anonymous function text”))
  .catch(reason => console.err("Badness happened", 		reason));										
```

- If the `catch` doesn't throw an exception, then it returns a `Promise` in a fulfilled state with whatever the return value is, just like the `error handler` of a `then`.
#### `Promise.all()`
- accepts an array of values and returns a new `Promise` object in the pending state colloquially called a "**super promise**".
- converts all non-`Promise` values into `Promise` objects that are immediately in the **fulfilled** state.
- If any one of the `Promise`s in the array transitions to the rejected state, then the "super promise" transitions to the rejected state with the same reason that the inner `Promise` object failed.
- If all of the inner `Promise` objects in the array transition to the **fulfilled** state, then the "super promise" transitions to the **fulfilled** state with a value of an array populated with all of the resolved values of the original array.

#### `async`
- Declaring a function with `async` will make it implicitly return a `Promise` if it doesn’t
- will return immediately resolved value of resolve

#### `await`
- when a `Promise` is `await`ed, execution of the containing `async` function will pause until the promise is fulfilled
- once fulfilled, the `await` expression will evaluate to the resolved value of the `Promise`
- using `await` outside of an `async` function will result in a `SyntaxError`
- use `try…catch` pattern to handle errors when the `Promise` is rejected

##### Refactoring a Promise chain from .then to await

```js
function wrapper() {				
  promise1						
    .then(res1 => {				
      console.log(res1);			
      return promise2;			
    })							
    .then(res2 => {				
      console.log(res2);			
      return promise3;			
    })							
    .then(res3 => {				
      console.log(res3);			
    });							
}
```

with async/await…
```js
async function wrapper() {		
  console.log(await promise1);
  console.log(await promise2);
  console.log(await promise3);
  console.log(await promise4);
}								
```

#### `fetch`

- Use the `fetch` API to make `Promise`-based API calls
- `fetch` takes 2 parameters:
  - url
  - an object with options for the request
- returns a `Promise`

```js
const fetch = require('node-fetch');

const MOVIE_API_KEY = "some-api-key";

const url = `https://omdbapi.com/?apikey=${MOVE_API_KEY}&t=fight+club`

fetch(url)
    .then(res => res.json())
    .then(json => console.log(json.Actors))
    .catch(reason => console.log('rejected because', reason))
```
