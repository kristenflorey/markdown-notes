## Regular Expressions

- Regular expressions are patterns used to match character combinations in strings.

| Regular  Expression | Description                    |
|---------------------|--------------------------------|
| *                   | zero or more repitions         |
| +                   | one or more repitions          |
| ?                   | once or none (optional)        |
| ^                   | start of input                 |
| $                   | end of input                   |
| .                   | any character                  |
| \                   | escapes a special character    |
| [abc]               | any of these characters        |
| [a-z]               | range of characters            |
| [^abc]              | not those characters           |
| \s                  | whitespace                     |
| \d                  | one digit (0 - 9)              |
| \w                  | any alphanumeric character     |
| \S                  | not whitespace                 |
| \D                  | not digit                      |
| \W                  | any non-alphanumeric character |
| {n}                 | n repetitions                  |
| {n }                | n or more repitions            |
| {x, y}              | x - y repitions                |

##### Using Regular expressions in Javascript
```js
const re = /EX$/
const str = "We're learning REGEX"

const li = [ 1, 2, di ];
const re = /regex/i;

console.log(re.test(`learning about regex`));
console.log(re.test(`LEARNING ABOUT REGEX`));

let count = 0;

const newStr = str.replace(/e/ig, match => {
      count += 1
      return count;
    });
    console.log(newStr);
const di = { name: `Mimi`, age: 2 };
const str = `My name is %name% and I am %age% years old`;
const str2 = `My name is ${name} and I am ${age} years old`;
const re = /%\w+%/g

const replaced = str.replace(re, match => {
  // match = %name%
  const key = match.replace(/%/g, ``);
  // key = name
  return di[key];
});
console.log(replaced);
```

##### You construct a regular expression in one of two ways:
- Using a regular expression literal, which consists of a pattern enclosed between slashes, as follows:
```js
let re = /ab+c/;
```

Regular expression literals provide compilation of the regular expression when the script is loaded. If the regular expression remains constant, using this can improve performance.

- Or calling the constructor function of the RegExp object, as follows:
```js
let re = new RegExp('ab+c');
```


#### Escaping
- If you need to use any of the special characters literally (actually searching for a "*", for instance), you must escape it by putting a backslash in front of it.
