<img src="https://i.pinimg.com/originals/0f/60/19/0f6019e15f1d8ae07e7e8ea16d242676.png" width="400"/>

#### Jump to...
- [Data Types](#datatypes)
  - [Numbers](#numbers)
    - [Arithmetic Operators](#arithmeticops)
  - [Strings](#strings)
    - [Range](#range)
    - [String Methods](#string-methods)
---

### Python REPL
start command line: `$ python3`
help: `help()`
exit: `exit()`

### Comments
```
# single line comment
```

```
"""
multi-line comment
"""
```

### Print to console
```py
print('this will be printed to the console')
```
---
## Data Types <a id="datatypes"></a>
### Numbers <a id="numbers"></a>
#### Integer
- Counting numbers, both positive and negative, are called integers. They have no decimal point.
- Integers are created by a literal number with no decimal point or through the use of the `int()` constructor.
```py
print(3)         # => 3
print(int(19))   # => 19
print(int())     # => 0
```

#### Decimals
- The decimal numbers in Python are called **floating point numbers**.
- Floating point numbers are created using numbers with a decimal point, with the `float()` constructor, or using scientific notation.
```py
print(2.24)      # => 2.24
print(2.)        # => 2.0
print(float())   # => 0.0
print(27e-5)     # => 0.00027
```

##### [Complex Numbers](https://open.appacademy.io/learn/js-py---sep-2020-online/week-17-sep-2020-online/number-data-type)

##### Number Conversion
- When once type of number is converted to another, the process used is called **type casting**.  It is performed using built-in functions for each type.
```py
# int -> float
print(17)               # => 17
print(float(17))        # => 17.0

# float -> int
print(17.0)             # => 17.0
print(int(17.0))        # => 17

# float || int -> string
print(str(17.0) + ' and ' + str(17))        # => 17.0 and 17
```
#### Arithmetic Operators <a id="arithmeticops"></a>
|      |                  |
|------|------------------|
| `+`  | addition         |
| `-`  | subtraction      |
| `*`  | multiplication   |
| `/`  | division         |
| `%`  | modulo           |
| `**` | exponent         |
| `//` | integer division |

- Remember modulo `%` gives the remainder that results from a division.
  - The `//` operator gives the other part of that division. This is the equivalent to the floor of the answer.
```py
print(47 // 8)         # => 5
print(47 % 8)          # => 7
```
---
### Strings <a id="strings"></a>
#### Valid strings
```py
"This is cool!"
'a1b2c3'
```
#### Invalid string
```py
"Tom shouted, "Go outside!""
```
#### Escaping Characters
```py
'Jodi asked, "What\'s up, Sam?"'
```
#### Multiline strings
```py
print('''My instructions are very long so to make them
more readable in the code I am putting them on
more than one line. I can even include "quotes"
of any kind because they won't get confused with
the end of the string!''')
```
#### String length
```py
print(len("Spaghetti"))    # => 9
```
#### String index
```py
print("Spaghetti"[4])    # => h
print("Spaghetti"[-4])    # => e
```

#### Range <a id="range"></a>
- A range consists of a start value followed by a colon then an end value.
  - Important: The series returned does not include the end value.
```py
print("Spaghetti"[1:4])  # => pag
print("Spaghetti"[4:-1])    # => hett
print("Spaghetti"[4:4])  # => (empty string)
```
- Omit the first number for the beginning of a string:
  ```py
  print("Spaghetti"[:4])  # => Spag
  print("Spaghetti"[:-1])    # => Spaghett
  ```
- Omit the second number for the end of a string:
  ```py
  print("Spaghetti"[1:])  # => paghetti
  print("Spaghetti"[-4:])    # => etti
  ```
#### String Functions
- ##### Index
  - Calculate the first position of a character within a string using `index`.
  ```py
  print("Spaghetti".index("h"))    # => 4
  ```
- ##### Count
  - Find out how many times a substring appears in the primary string using `count`. It returns zero if the substring is not there.
  ```py
  print("Spaghetti".count("t"))    # => 2
  print("Spaghetti".count("s"))    # => 0
  ```

#### Concatenation
- Addition operation `+` stitches strings together
```py
print("gold" + "fish")    # => goldfish
```
- Multiplication operation `*` repeats string a given number of times
```py
print("s"*5)              # => sssss
```
#### Formatting
```py
first_name = "Billy"
last_name = "Bob"
print('Your name is {0} {1}'.format(first_name, last_name))  # => Your name is Billy Bob
```
- Use `f` flag:
```py
print(f'Your name is {first_name} {last_name}')
```

#### String Methods <a id="string-methods"></a>
| Value               | Method               | Result                    |
|---------------------|----------------------|---------------------------|
| `s = "Hello"`       | `s.upper()`          | `"HELLO"`                 |
| `s = "Hello"`       | `s.lower()`          | `"hello"`                 |
| `s = "Hello"`       | `s.islower()`        | `False`                   |
| `s = "hello"`       | `s.islower()`        | `True`                    |
| `s = "Hello"`       | `s.isupper()`        | `False`                   |
| `s = "HELLO"`       | `s.isupper()`        | `True`                    |
| `s = "Hello"`       | `s.startswith("He")` | `True`                    |
| `s = "Hello"`       | `s.endswith("lo")`   | `True`                    |
| `s = "Hello World"` | `s.split()`          | `["Hello", "World"]`      |
| `s = "i-am-a-dog"`  | `s.split("-")`       | `["i", "am", "a", "dog"]` |

## String Testing methods

|     Method    |                                                           Purpose                                                           |
|:-------------:|:---------------------------------------------------------------------------------------------------------------------------:|
| `isalpha()`   | returns `True` if the string consists only of letters and is not blank.                                                     |
| `isalnum()`   | returns `True` if the string consists only of letters and numbers and is not blank.                                         |
| `isdecimal()` | returns `True` if the string consists only of numeric characters and is not blank.                                          |
| `isspace()`   | returns `True` if the string consists only of spaces, tabs, and newlines and is not blank.                                  |
| `istitle()`   | returns `True` if the string consists only of words that begin with an uppercase letter followed by only lowercase letters. |
