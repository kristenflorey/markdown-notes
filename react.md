<img src="https://miro.medium.com/max/700/1*dLaDL-lSN0iprzmOpmM7zQ.png"/>

- **React.js** is a declarative, efficient, and flexible JavaScript library for building user interfaces. It lets you compose complex UIs from small and isolated pieces of code called **components**.
  - React manages **the creation and updating of DOM nodes in your Web page**

## Components
- React applications are built as a combination of parent and child components. As the names suggest, each child component has a parent and a parent component will have one or more child components.
- A **component** is a reusable piece of code, which defines how certain features should look and behave on the UI
  - #### Functional Component
    - A functional component in React consumes arbitrary data that you pass to it using props object. It returns an object which describes what UI React should render.
    - Functional components are also known as **Stateless components**.
  - #### Class-based Component
    - The class-based component has an additional property `state`, which you can use to hold a component’s private data.
    - Since these components have a state, these are also known as **Stateful components**.
      - We extend `React.Component` class of React library to make class-based components in React.
      - The `render()` method must be present in your class as React looks for this method in order to know what UI it should render on screen.
  <img src="https://cdn-media-1.freecodecamp.org/images/1*rPUhERO1Bnr5XdyzEwNOwg.png" />
    - #### `React.Component` subclasses
      - A component takes in parameters, called `props` (short for “properties”), and returns a hierarchy of views to display via the `render` method.
        - The `render` method returns a *description* of what you want to see on the screen. React takes the description and displays the result.
        
    ```js
    class ShoppingList extends React.Component {
      render() {
        return (
          <div className="shopping-list">
            <h1>Shopping List for {this.props.name}</h1>
            <ul>
              <li>Instagram</li>
              <li>WhatsApp</li>
              <li>Oculus</li>
            </ul>
          </div>
        );
      }
    }

    // Example usage: <ShoppingList name="Mark" />
    ```
    - Here, `ShoppingList` is a **React component class**, or **React component type**.
    - The `<div />` syntax is transformed at build time to `React.createElement('div')`.
    - Example above is equivalent to:
    ```js
    return React.createElement('div', {className: 'shopping-list'},
      React.createElement('h1', /* ... h1 children ... */),
      React.createElement('ul', /* ... ul children ... */)
    );
    ```
    - #### `React.PureComponent` subclasses
      - `React.PureComponent` is similar to `React.Component`. The difference between them is that `React.Component` doesn’t implement `shouldComponentUpdate()`, but `React.PureComponent` implements it with a shallow prop and state comparison.

### Props
- Components receive data via an argument traditionally named `props`.
- Parent components can decide the data that its children should show by passing only a subset of what it has to its children. Data is never passed up from the child to the parent.

## JSX
- JSX is a short form of *JavaScript Extended* and it is a way to write React components. Using JSX, you get the full power of JavaScript inside XML like tags.
- You put JavaScript expressions inside `{}`.
  - The way it works is you write JSX to describe what your UI should look like. A **transpiler** like `Babel` converts that code into a bunch of `React.createElement()` calls.
  - The React library then uses those `React.createElement()` calls to construct a tree-like structure of DOM elements (in case of React for Web) or Native views (in case of React Native) and keeps it in the memory.
<img src="https://cdn-media-1.freecodecamp.org/images/1*ighKXxBnnSdDlaOr5-ZOPg.png" />


## Creating React Elements
- Each JSX element is just syntactic sugar for calling `React.createElement()`

  ### `createElement()`
  ```js
  React.createElement(
    type,
    [props],
    [...children]
  )
  ```
  - Create and return a new **React element** of the given type.
    - The type argument can be either a tag name string (such as `div` or `span`), a **React component** type (a class or a function), or a **React fragment type**.
  ### `createFactory()`
  ```js
  React.createFactory(type)
  ```
  - Return a function that produces React elements of a given type.
    - Like `React.createElement()`, the type argument can be either a tag name string (such as `div` or `span`), a React component type (a class or a function), or a React fragment type.
## Transforming Elements
  ### `cloneElement()`
  ```js
  React.cloneElement(
    element,
    [props],
    [...children]
  )
  ```
  - Clone and return a new React `element` using element as the starting point.
    - The resulting element will have the original element’s props with the new props merged in shallowly.
    - New children will replace existing children. `key` and `ref` from the original element will be preserved.
  ### `isValidElement()`
  ```js
  React.isValidElement(object)
  ```
  - Verifies the object is a React element. Returns `true` or `false`.
  ### `React.Children`
  ```js
  React.Children.map(children, function[(thisArg)])
  ```
  - `React.Children` provides utilities for dealing with the `this.props.children` opaque data structure
    - Invokes a function on every immediate child contained within `children` with this set to `thisArg`
  [Additional `children` functions](https://reactjs.org/docs/react-api.html#reactchildren)


## Fragements
- React also provides a component for rendering multiple elements without a wrapper.
  ### `React.Fragment`
  - The `React.Fragment` component lets you return multiple elements in a `render()` method without creating an additional DOM element:
  ```js
  render() {
    return (
      <React.Fragment>
        Some text.
        <h2>A heading</h2>
      </React.Fragment>
    );
  }
  ```
## Updating the DOM
- When calling `ReactDOM.render`, React would compare the new element tree with the old element tree, figure out that one class was missing on that one `li` element, and remove that and only that from the real DOM.

---
