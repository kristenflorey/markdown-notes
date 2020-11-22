# Testing

### Testing Frameworks
  - runs tests and presents them to a user
  - an assertion library is the code used to write tests
  - some testing libraries have built in assertion libraries, others will need you to import to utilize them
####	Mocha
  - Javascript testing framework that specializes in running tests and presenting them in an organized user friendly way
  - widely used because of its flexibility
  - supports a whole variety of different assertion libraries and DSL interfaces to best suit the developer
    - **DSL (Domain Specific Language)** refers to a computer language specialized for a particular purpose
    - will usually be familiar but syntactically slightly different from other languages

Assertion libraries are used to actually write tests. Node has a library called **Chai** and **Assert**
  - Use Chai to structure your tests using behavior-driven development principles.
to set up chai and chai spies:

```
// first npm install chai and chai-spies
const chai = require("chai");
const expect = chai.expect;
const spies = require("chai-spies");
chai.use(spies);
```

Importing assert module:
`const assert = require(“assert")`
#### `describe()`
- `describe()` is an organizational function. takes two parameters: descriptive string and a callback
the callback passed to describe is where we insert the actual tests
#### `it()`
- `it` goes inside the callback passed to describe
- accepts a descriptive string and a callback to set up our test
#### `context`
- an alias for the describe function
- denotes that we are setting up the context for a particular set of tests


- Use the pre- and post-test hooks provided by Mocha
- **Mocha Hooks** are a way to set up before running the individual tests
    - `before` happens once before all tests
    - `beforeEach` happens before each test
    - `after` happens once at the end
    - `afterEach` happens after each test

#### The Testing Pyramid
- **Unit Tests**: used to test the smallest pieces of your application in isolation to ensure each piece works before you attempt to put those pieces together.
  - Each unit test should focus on testing one thing. These are generally the fastest tests to write and run.
- **Integration Tests**: test the interactions between two pieces of your application. will ensure the units you've written work coherently together.
- **End-to-End (E2E) Tests**: test the whole of your application. Closest automated tests come to testing the an actual user experience of your application. These are generally the slowest tests to write and run.

####	Test-Driven Development (TDD)
- writing the test first—so you have to think about what you want your code to do and what it would mean for the code to be successful before you start writing it
1. Writing tests before code ensures that the code written works.
    - Code written to pass specs is guaranteed to be testable.
    - Code with pre-written tests easily allows other developers to add and test new code while ensuring nothing else breaks along the way.
2. Only required code is written.
    - In the face of having to write tests for every piece of added functionality TDD can help reduce bloated un-needed functionality.
    - TDD and YAGNI ("you ain't gonna need it") go hand in hand!
3. TDD helps enforce code modularity.
    - A TDD developer is forced to think about their application in small, testable chunks - this ensures the developer will write each chunk to be modular and capable of individual testing.
4. Better understanding of what the code should be doing.
    - Writing tests for a piece of code ensures that the developer writing that code knows what the piece of code is trying to achieve.

####TDD Workflow
  - Red: Write the tests and watch them fail (a failing test is red). It's important to ensure the tests initially fail so that you don't have false positives.
  - Green: Write the minimum amount of code to ensure the tests pass (a passing test will be green).
  - Refactor: Refactor the code you just wrote. Your job is not over when the tests pass! One of the most important things you do as a software developer is to ensure the code you write is easy to maintain and read.
