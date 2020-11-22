# Javascript Empty Shells

#### Comments
```js
// single line comment

/* multi
line comment */
```
### Declarations
```js
let, var, const
```

#### Function Declaration
```
function fnName(parameters) {
}
```
#### Function Expression
```
const fnName = function(parameters){
}
```
#### Arrow Function
```
const fnName = (parameter) => {
}
```
#### Rest Parameter
```
function f(a, b, ...theArgs) {
  // ...
}
```
#### Spread Operator
```
// for function calls:
myFunction(...iterableObj);

// For array literals or strings:
[...iterableObj, '4', 'five', 6];

// For object literals (new in ECMAScript 2018):
let objClone = { ...obj };
```
#### Compound Assignment Operators
| Name                            | Shorthand operator |
|---------------------------------|--------------------|
| Assignment                      | `x = y`              |
| Addition assignment             | `x += y`             |
| Subtraction assignment          | `x -= y`             |
| Multiplication assignment       | `x *= y`             |
| Division assignment             | `x /= y`             |
| Remainder assignment            | `x %= y`             |
| Exponentiation assignment       | `x **= y`            |
| Left shift assignment           | `x <<= y`            |
| Right shift assignment          | `x >>= y`            |
| Unsigned right shift assignment | `x >>>= y`           |
| Bitwise AND assignment          | `x &= y`             |
| Bitwise XOR assignment          | `x ^= y`             |
| Bitwise OR assignment           | `x \|= y`            |
| Logical AND assignment          | `x &&= y`            |
| Logical OR assignment           | `x \|\|= y`          |
| Logical nullish assignment      | `x ??= y`            |

#### Comparison Operators
| Operator |                       |
|:--------:|-----------------------|
|    `==`    | Equal                 |
|    `!=`    | Not equal             |
|    `===`   | Strict equal          |
|    `!==`   | Strict not equal      |
|     `>`    | Greater than          |
|    `>=`    | Greater than or equal |
|     `<`    | Less than             |
|    `<=`    | Less than or equal    |
|     `%`    | Remainder             |

| Operator |             |
|----------|-------------|
| `&&`     | Logical AND |
| `|| `    | Logical OR  |
| `!`      | Logical NOT |

### Iteration & Loops
#### for...of
```
for ([initialExpression]; [conditionExpression]; [incrementExpression]) {
  statement  
}
```
#### while
```
while (condition) {
  statement
}  
```
#### do...while
```
do {
  statement
} while (condition);
```
#### for...in
```
for (const property in object) {
  console.log(`${property}: ${object[property]}`);
}
```
#### for...of
```
for (variable of object) {
  statement
}
```
###
####
```js

```
### Conditionals

#### if...else
```
if (condition) {
  statement
} else {
  statement
}
```

#### Ternary Operators
```
condition ? true : false
```

### Objects
#### Define Objects and Properties
##### Dot Notation
```
let objectName = new Object()
objectName.propertyName = 'value';
objectName.propertyName = 'value';
```
##### Bracket Notation
```
let objectName = new Object()
objectName['propertyName'] = 'value';
objectName['propertyName'] = 'value';
```
#### Object Initializor
```
let objectName = {
  propertyName: 'value',
  propertyName: 'value'
};
```
#### Access Properties
##### Dot Notation
```
objectName.propertyName
```
##### Bracket Notation
```
objectName['propertyName']
```
#### Object Constructor Function
```
function Object(property, property, property) {
  this.property = property;
  this.property = property;
  this.property = property;
}
```
#### Defining Object Methods
```
objectName.methodname = functionName;

let myObj = {
  myMethod: function(params) {
    statement
  }
```
 OR
```  
  myOtherMethod(params) {
    statement
  }
};
```
##### Calling Object Methods
```
object.methodname(params);
```
#### Deleting Properties
```
delete objectName.propertyName;
```

### Classes
```
class ClassName {
  constructor(name) {
    this.name = name
  }
}
```
#### Inherting Properties
```
let newObj = new Object;
```

### Promises
#### Create a Promise
```
new Promise((resolve, reject) => {				
  // do some async stuff						
  // call resolve(value) to make the Promise succeed
  // call reject(reason) to make the Promise fail	 
});
```
#### Static Methods
```
static methodName() { ... }
static propertyName [= value];
```
#### Chaining Promises
```
const promise = doSomething();
const promise2 = promise.then(successCallback, failureCallback);
// OR
const promise2 = doSomething().then(successCallback, failureCallback);
```
#### Composition
```
Promise.all([func1(), func2(), func3()])
.then(([result1, result2, result3]) => { /* use result1, result2 and result3 */ });
```
#### try...catch
```
try {
  try_statements
}
[catch [(exception_var)] {
  catch_statements
}]
[finally {
  finally_statements
}]
```
- ##### Unconditional catch-block
```
try {
  throw 'myException'; // generates an exception
} catch (e) {
  // statements to handle any exceptions
  logMyErrors(e); // pass exception object to error handler
}
```
- ##### Conditional catch-block
```
try {
  myroutine(); // may throw three types of exceptions
} catch (e) {
  if (e instanceof TypeError) {
    // statements to handle TypeError exceptions
  } else if (e instanceof RangeError) {
    // statements to handle RangeError exceptions
  } else if (e instanceof EvalError) {
    // statements to handle EvalError exceptions
  } else {
    // statements to handle any unspecified exceptions
    logMyErrors(e); // pass exception object to error handler
  }
}
```
#### Extends
```
class ChildClass extends ParentClass { ... }
```
