<img src="https://hackernoon.com/hn-images/1*PmL3-GUNxYP26qTSlVrmzw.png" width="400"/>

#### Jump to...
- [Syntax](#syntax)
- [Rendering](#render)
- [Method options](#options)
- [Inheritance](#inheritance)
- [Interpolation](#interpolation)
- [Iteration](#iteration)
# Pug
- Pug (formerly known as Jade) is a preprocessor which simplifies the task of writing HTML. It also adds a ton of functionality, such as Javascript objects, conditionals, loops, mixins and templates.
- Pug fully integrates with Express, a popular Node.js web framework, as a supported view engine.

#### Installation
- Pug is available via npm:
`npm install - g pug-cli`

#### Pug Syntax <a id="syntax"></a>
- **whitespace sensitive**: Pug uses indentation to work out with tags are nested inside each other.
  ```pug
  div.remark
    p Pug rocks!!
  ```
   The code above produces this:
  ```pug
  <div class="remark">
    <p>Pug rocks!!</p>
  </div>
  ```
  - It doesn't matter what level of indentation you use, as long as the **level of indentation remains consistent**
- **Pug doesn't have any closing tags**
  - If no tag is specified, Pug will assume a `<div>` element.

#### Classes, IDs and Attributes
- **Classes** are expressed as `.className`
- **IDs** are expressed as `#IDname`
- **Attributes** are added using brackets

#### Plain Text and Text Blocks
- Pug provides various methods for adding plain text directly into the rendered HTML.
  - Add plain text inline:
  `h1.navbar-header We can write anything we want here …`
  - Prefix a line with a pipe `|` character:
    ```
    p
      | You are logged in as
      | user@example.com
    ```  
  - When dealing with large blocks of text, you can just add a dot right after the tag name, or after the closing parenthesis, if the tag has attributes:
    ```
    p.
      HTML TEXT.....
    ```  
#### Comments
  - Comments in Pug can be escaped similar to Javascript with `//`
    ```
    //- Invisible comment.
    //Visible comment.
    ```

#### Rendering Proccess of Pug <a id="render"></a>

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

#### Options <a id="options"></a>
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


#### Template Inheritance <a id="inheritance"></a>
- Pug supports template inheritance. Template inheritance works via the `block` and `extends` keywords.
   #### `block`
   - in a template, a `block` is simply a "block" of Pug that a child template may replace.
      - This process is recursive
  - Pug blocks can optionally provide default content.    
  ```pug
  //- layout.pug
  html
    head
      title My Site - #{title}
      block scripts
        script(src='/jquery.js')
    body
      block content
      block foot
        #footer
          p some footer content
  ```
  - Pug allows you to `replace` (default), `prepend`, or `append` blocks.
    - When using` block append` or `block prepend`, the word “`block`” is optional:
    ```pug
    //- page.pug
    extends layout

    append head
      script(src='/vendor/three.js')
      script(src='/game.js')
    ```

  #### `extends`
  - extend block layout with a path to the parent template
  - define one of more blocks to override the parent block content
  - also possible to override a block to provide additional blocks
  ```pug
  //- page-a.pug
  extends layout.pug

  block scripts
    script(src='/jquery.js')
    script(src='/pets.js')

  block content
    h1= title
    - var pets = ['cat', 'dog']
    each petName in pets
      include pet.pug
  ```

#### Buffered vs Unbuffered Code
- **Unbuffered code** starts with a minus (`-`). It doesn’t directly add anything to the output, but its values may be used from within Pug.
- **Buffered code**, on the other hand, starts with an equals (`=`). It evaluates a JavaScript expression and outputs the result.  

#### Interpolation <a id="interpolation"></a>
- String interpolation is the process of replacing one or more placeholders in a template with a corresponding value.
  - buffered input offers one method of doing this.
- Another is using `#{}`. Here, Pug will evaluate any code between the curly brackets, escape it, and render it into the template

  | Syntax                        | Action                                                                                                                                            |
  |-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
  | `res.render(path, variables)` | Searches for a pug file to render at path "path", and passes "variables" to it                                                                    |
  | `#{variable}`                 | Interpolates "variable" inline with the surrounding Jade code, after evaluating "variable"                                                        |
  | `!{variable}`                 | Interpolates "variable" inline with the surrounding Jade code, without evaluating "variable".                                                     |
  | `#[element]`                  | Interpolates "element" inside of an existing Pug HTML element. Syntax of interpolated HTML elements is identical to that of normal HTML elements. |


  | Parameter | Details                                                                                                                                                           |
  |-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
  | path      | Used in `res.render`. This is the path of the Pug file that we are going to render. The path is taken from the root of the folder set on your Express app:` app.set("views", "templates/views")`. For example, `res.render("index")` will search for a Pug file at `templates/views/index.pug`. Subdirectories can be specified too; `res.render("admin/index")` looks for a Pug file at `templates/views/admin/index.pug`. |
  | variables | Used in `res.render`. A JavaScript object of variables to be made accessible to the Pug file defined by `path` (above). Within the Pug file, the keys of the above JavaScript object become available as variables. If `variables = {title: "Hello", color: "red"}`, we could use the `title` and `color` variable. Subproperties of nested objects are also available.                                                   |
  | variable  | Used in bracket syntax `#{}` or `!{}`. The value of `variable` will be output in the context of its surrounding Pug code. If a pound symbol is prepended to the opening curly bracket, `variable` will be evaluated before being output. If an exclamation point is prepended to the opening curly brace, `variable` **will not** be evaluated.                                                                               |
  | element   | Used in square bracket syntax `#[]`. The HTML element (in Pug syntax, not normal HTML syntax) will be evaluated and output inline with the surrounding Pug code.                                                                                                                                                                                                                                                   |


#### Iteration <a id="iteration"></a>
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

---
