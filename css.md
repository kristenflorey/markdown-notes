# CSS

What is a CSS rule?
  - A CSS rule is a grouping of CSS properties that are applied to HTML elements

How to link a stylesheet into an HTML page
  - css into css : with use of the `@import` tag!
    - css into html : by using the `link` HTML element.
      - The link element has to have the `rel` and `href` attributes configured like so:
        ```html
        <link rel="stylesheet" href="file.css">
        ```

#### CSS Specificity

- `IDs` are unique, thus are considered highly specific since they always target one element.
-  Calculating the `score specificity` of selectors, and the one with the highest score is the most specific.
- `in-line styling > id > pseudo-class selectors > class > tag namw`
