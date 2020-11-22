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
#### Enumerate Object Properties



### Classes
```
class ClassName {
  constructor(name) {
    this.name = name
  }
}
```
