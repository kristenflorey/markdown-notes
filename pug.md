# Pug
- Pug fully integrates with Express, a popular Node.js web framework, as a supported view engine.

#### Installation
- Pug is available via npm:
`npm install pug`


#### Rendering Proccess of Pug

#### `pug.compile(source, options)`
- will compile the Pug source code into a JavaScript function that takes a data object (called “locals”) as an argument.
- Call that resultant function with your data, and voilà!, it will return a string of HTML rendered with your data.
- The compiled function can be re-used, and called with different sets of data.
  - **source**: `string`
    - The source Pug template to compile
  - **options**: `?options`
    - An options object
  - **returns**: `function`
    - A function generate the HTML form an object containing locals
    ```js
    var pug = require('pug');

    // Compile a function
    var fn = pug.compile('string of pug', options);

    // Render the function
    var html = fn(locals);
    // => '<string>of pug</string>'
    ```

#### `pug.render(source, options, callback)`
- combines compiling and rendering into one step
- the template function will be re-compiled every time `render` is called, which may impact performance.
  - **source**: `string`
    - The source Pug template to render
  - **options**: `?options`
    - An options object, also used as the locals object
  - **callback**: `function`
    - Node.js-style callback receiving the rendered results. This callback is called synchronously.
  - **returns**: `string`
    - The resulting HTML string
    ```js
    var pug = require('pug');

    var html = pug.render('string of pug', options);
    // => '<string>of pug</string>'
    ```

#### Options
- All API methods accept the following set of options:

| Option                   | Accepts         | Action                                                                                                                                                                                                                                                       |
|--------------------------|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `filename`               | `string`        | The name of the file being compiled. Used in exceptions, and required for relative `include` \s and `extend`\s. Defaults to `Pug`.                                                                                                                           |
| `basedir`                | `string`        | The root directory of all absolute inclusion.                                                                                                                                                                                                                |
| `doctype`                | `string`        | If the `doctype` is not specified as part of the template, you can specify it here. It is sometimes useful to get self-closing tags and remove mirroring of boolean attributes.                                                                              |
| `filters`                | `object`        | Hash table of custom filters. Defaults to `undefined`.                                                                                                                                                                                                       |
| `self`                   | `boolean`       | Use a `self` namespace to hold the locals. It will speed up the compilation, but instead of writing `variable` you will have to write `self.variable` to access a property of the locals object. Defaults to `false`.                                        |
| `debug`                  | `boolean`       | If set to `true`, the tokens and function body are logged to stdout.                                                                                                                                                                                         |
| `compileDebug`           | `boolean`       | If set to `true`, the function source will be included in the compiled template for better error messages (sometimes useful in development). It is enabled by default, unless used with Express in production mode.                                          |
| `globals`                | `Array<string>` | Add a list of global names to make accessible in templates.                                                                                                                                                                                                  |
| `cache`                  | `boolean`       | If set to `true`, compiled functions are cached. `filename` must be set as the cache key. Only applies to `render` functions. Defaults to `false`.                                                                                                           |
| `inlineRuntimeFunctions` | `boolean`       | Inline runtime functions instead of `require`-ing them from a shared version. For `compileClient` functions, the default is `true` (so that one does not have to include the runtime). For all other compilation or rendering types, the default is `false`. |
| `name`                   | `string`        | The name of the template function. Only applies to `compileClient` functions. Defaults to `'template'`.                                                                                                                                                      |


#### Iteration
- Pug supports two primary methods of iteration: `each` and `while`.
   #### `each`
  Iterate over arrays and objects in a template:
  ```pug
  ul
    each val in [1, 2, 3, 4, 5]
      li= val
  ```
  Capture index as you iterate:
  ```pug
  ul
    each val, index in ['zero', 'one', 'two']
      li= index + ': ' + val
  ```
  Iterate over the keys in an object:
  ```pug
  ul
    each val, key in {1: 'one', 2: 'two', 3: 'three'}
      li= key + ': ' + val
  ```
  Add an `else` block in the case that the array or object are empty
  ```pug
  - var values = [];
  ul
    each val in values
      li= val
    else
      li There are no values
  ```
  #### `while`
  - Create a loop with `while` keyword:
  ```pug
  - var n = 0;
  ul
    while n < 4
      li= n++
  ```    
---
