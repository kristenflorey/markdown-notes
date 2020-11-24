# <b>Big-O Notation</b>

### Jump to...

- [Complexity Classes](#complexityclasses)
- [Sorting Algorithms](#sortingalgorithms)
- [Memoization](#memoization)
- [Tabulation](#tabulation)
---

- We use the Big-O notation to classify algorithms based on their running time or space (memory used) as the input grows. The O function is the growth rate in function of the input size n.
  - describes an algorithm's _worst_ case
  - We can measure both time and space complexity, but are mostly concerned with time (memory is cheap and abundant)
  - should be simplified to show only its most dominant mathematical term
- #### Asymptomatic Behavior
  - The asymptotic behavior of a function refers to its rate of growth as its input size approaches infinity
    - Allows us to focus on the big picture and compare algorithms from a high level
    - Big-O notation is a tool for understanding asymptotic behavior

### Time Complexity

- estimates how an algorithm performs regardless kind of machine it runs on
  - calculated by “counting” the number of operations performed

### Complexity Classes <a id="complexityclasses"></a>

- Algorithms are ranked by efficiency
  - _Smaller growth_ complexity classes are more efficient because they require fewer resources
- The following are in order from smallest growth to largest:

| Time Complexity      | Algorithm                             |
| -------------------- | ------------------------------------- |
| O(1)                 | [Constant](#constant)                 |
| O(log n)             | [Logarithmic](#logarithmic)           |
| O(n)                 | [Linear](#linear)                     |
| O(n log n)           | [Linearithmic](#linearithmic)         |
| O(n \* log(n))       | [Loglinear](#loglinear)               |
| O(n<sup>2</sup>)     | [Polynomial](#polynomial) (Quadratic) |
| O(n <sup> 3 </sup> ) | [Polynomial](#polynomial) (Cubic)     |
| O(2 <sup> n </sup> ) | [Exponential](#exponential)           |
| O(n!)                | [Factorial](#factorial)               |

_Click algorithm name for more details_

<img src="https://miro.medium.com/max/2928/1*5ZLci3SuR0zM_QlZOADv8Q.jpeg" width="550"/>

### <b>O(1) Constant</b> <a name="constant"></a>

- ##### Take roughly the same number of steps for any input size
- there is no relationship between the size of the input and the number of steps required
- Examples of constant runtime algorithms:
  - Find if a number is even or odd.
  - Check if an item on an array is null.
  - Print the first element from a list.
  - Find a value on a map.
- Constant growth indicates the behavior stays constant for all values of n

###

#### Constant Growth

| n   | O(1) |
| --- | ---- |
| 1   | ~1   |
| 2   | ~1   |
| 3   | ~1   |
| ... | ...  |
| 128 | ~1   |

#### Example Constant Code

```js
function constant1(n) {
  return n * 2 + 1;
}

function constant2(n) {
  for (let i = 1; i <= 100; i++) {
    console.log(i);
  }
}
```

### <b>O(log(n)) Logarithmic</b>

- ##### Halves the size of the input
- Typically, the hidden base of O(log(n)) is 2, meaning O(log2(n))
- don't have to access every element of the input
  - every time we double the size of the input, we only require one additional step
- a large increase of input size will increase the number of steps required by a small amount
- Logarithmic growth only requires one additional “step” when the input size is doubled:

#### Logarithmic Growth

| n   | O(log<sub>2</sub>(n)) |
| --- | --------------------- |
| 2   | ~1                    |
| 4   | ~2                    |
| 8   | ~3                    |
| 16  | ~4                    |
| ... | ...                   |
| 128 | ~7                    |

#### Example Logarithmic Code

```js
function logarithmic1(n) {
  if (n <= 1) return;
  logarithmic1(n / 2);
}

function logarithmic2(n) {
  let i = n;
  while (i > 1) {
    i /= 2;
  }
}
```

### <b>O(n) Linear</b>

- ##### Will access each item of the input _once_
- Algorithms that iterate through the input without nested loops or recurse by reducing the size of the input by "one" each time are typically linear.
- Linear time complexity O(n) means that as the input grows, the algorithms take proportionally longer to complete.
- Examples of linear time algorithms:
  - Get the max/min value in an array.
  - Find a given element in a collection.
  - Print all the values in a list.

#### Linear Growth:

| n   | O(n) |
| --- | ---- |
| 1   | ~1   |
| 2   | ~2   |
| 3   | ~3   |
| ... | ...  |
| 128 | ~128 |

#### Example Linear Code

```js
function linear1(n) {
  for (let i = 1; i <= n; i++) {
    console.log(i);
  }
}

function linear2(array) {
  for (let i = 0; i < array.length; i++) {
    console.log(i);
  }
}

function linear3(n) {
  if (n === 1) return;
  linear3(n - 1);
}
```

### <b>O(n \* log(n)) Loglinear</b>

- ##### Combination of linear and logarithmic behaviors
- Will use both recursion and iteration
  - the recursive calls will halve the input each time (logarithmic) but iterations are also performed on the input (linear).

#### Loglinear Growth:

| n   | O(n \* log<sub>2</sub>(n)) |
| --- | -------------------------- |
| 2   | ~2                         |
| 4   | ~8                         |
| 8   | ~24                        |
| ... | ...                        |
| 128 | ~896                       |

#### Example Loglinear Code

```js
function loglinear(n) {
  if (n <= 1) return;

  for (let i = 1; i <= n; i++) {
    console.log(i);
  }

  loglinear(n / 2);
  loglinear(n / 2);
}
```

### <b>O(n<sup>c</sup>) Polynomial</b>

- ##### `n` is the size of the input, `c` is a fixed constant
- Nested loops are usually the indicator of this class

#### Polynomial Growth:

| n   | O(n<sup>2</sup>) |
| --- | ---------------- |
| 1   | ~1               |
| 2   | ~4               |
| 3   | ~9               |
| ... | ...              |
| 128 | ~16,384          |

| n   | O(n<sup>3</sup>) |
| --- | ---------------- |
| 1   | ~1               |
| 2   | ~8               |
| 3   | ~27              |
| ... | ...              |
| 128 | ~2,097,152       |

#### Example Polynomial Code

```js
// O(n^2)
function quadratic(n) {
  for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= n; j++) {}
  }
}

// O(n^3)
function cubic(n) {
  for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= n; j++) {
      for (let k = 1; k <= n; k++) {}
    }
  }
}
```

### <b>O(c<sup>n</sup>) Exponential</b> <a id="exponential"></a>

- ##### `n` is the size of the input and `c` is some fixed constant
  - A common indicator of this complexity class is recursive code where there is a constant number of recursive calls in each stack frame.
  - The c will be the number of recursive calls made in each stack frame.
  - Algorithms with this complexity are considered quite slow.

#### Exponential Growth:

| n   | O(2<sup>n</sup>)           |
| --- | -------------------------- |
| 1   | ~2                         |
| 2   | ~4                         |
| 3   | ~8                         |
| ... | ...                        |
| 128 | ~3.4028 \* 10<sup>38</sup> |

| n   | O(2<sup>3</sup>)           |
| --- | -------------------------- |
| 1   | ~3                         |
| 2   | ~9                         |
| 3   | ~27                        |
| 3   | ~81                        |
| ... | ...                        |
| 128 | ~1.1790 \* 10<sup>61</sup> |

#### Example Exponential Code

```js
// O(2^n)
function exponential2n(n) {
  if (n === 1) return;
  exponential_2n(n - 1);
  exponential_2n(n - 1);
}

// O(3^n)
function exponential3n(n) {
  if (n === 0) return;
  exponential_3n(n - 1);
  exponential_3n(n - 1);
  exponential_3n(n - 1);
}
```

### <b>O(n!) Factorial</b>

- ##### Variable number of recursive calls in each stack frame
  - Largest/worst complexity class

#### Factorial Growth:

| n   | O(n!)                       |
| --- | --------------------------- |
| 1   | ~1                          |
| 2   | ~2                          |
| 3   | ~6                          |
| ... | ...                         |
| 128 | ~3.8562 \* 10<sup>215</sup> |

#### Example Factorial Code

```js
function factorial(n) {
  if (n === 1) return;

  for (let i = 1; i <= n; i++) {
    factorial(n - 1);
  }
}
```

---

# **Sorting Algorithms** <a id="sortingalgorithms"></a>

### Complexity Classes of Common Sorting Methods

| Sort Name                   | Time Complexity   | Space Complexity |
| :-------------------------- | :---------------- | :--------------- |
| [bubble](#bubblesort)       | O(n^2)            | O(1)             |
| [selection](#selectionsort) | O(n^2)            | O(1)             |
| [insertion](#insertionsort) | O(n^2)            | O(1)             |
| [merge](#mergesort)         | O(n log n)        | O(n)             |
| [quick](#quicksort)         | O(n log n)/O(n^2) | O(n)/O(log n)    |
| [binary](#binarysearch)     | O(log(n))         | O(1)             |

_Click sort name for more details_

## <b>Bubble Sort</b> <a id="bubblesort"></a>

**Time Complexity**: Quadratic O(n^2)

- The inner for-loop contributes to O(n), however in a worst case scenario the while loop will need to run n times before bringing all n elements to their final resting spot.

**Space Complexity**: O(1)

- Bubble Sort will always use the same amount of memory regardless of n.

```js
function bubbleSort(array) {
  let sorted = false;
  while (!sorted) {
    sorted = true;
    for (let i = 0; i < array.length; i++) {
      if (array[i] > array[i + 1]) {
        let temp = arr[i];
        array[i] = array[i + 1];
        array[i + 1] = temp;
        sorted = false;
      }
    }
  }
  return array;
}
```

#### Bubble Sort Pseudocode

- Start looping from the end of the array towards the beginning
  - Start an inner loop from the beginning until `i - 1`
    - If the current value of the outer loop is greater than the current value of the inner loop, swap those two values

<img src="https://s3-us-west-1.amazonaws.com/appacademy-open-assets/data_structures_algorithms/naive_sorting_algorithms/bubble_sort/images/BubbleSort.gif" />

---

## <b>Selection Sort</b> <a id="selectionsort"></a>

**Time Complexity**: Quadratic O(n^2)

- Our outer loop will contribute O(n) while the inner loop will contribute O(n / 2) on average. Because our loops are nested we will get O(n^2);

**Space Complexity**: O(1)

- Selection Sort will always use the same amount of memory regardless of n.

```js
function selectionSort(array) {
  for (let i = 0; i < array.length; i++) {
    let lowest = i;
    for (let j = 0; j < array.length; j++) {
      if (array[j] < array[i]) {
        lowest = j;
      }
    }
    if (lowest !== i) {
      let temp = array[i];
      array[i] = array[lowest];
      array[lowest] = temp;
    }
  }
  return array;
}
```

#### Selection Sort Pseudocode

- Store the first element as the smallest value you've seen so far
  - Compare current element to the next element in the array until you find a smaller number.
    - If a smaller number is found, designate that smaller number to be the new _minimum_ and continue until the end of the array.
  - If the _minimum_ is not the value you initially began with, swap the two values.
  - Repeat this with the next element until the array is sorted.

![selection](https://s3-us-west-1.amazonaws.com/appacademy-open-assets/data_structures_algorithms/naive_sorting_algorithms/selection_sort/images/SelectionSort.gif)

---

## <b>Insertion Sort</b> <a id="insertionsort"></a>

**Time Complexity**: Quadratic O(n^2)

- Our outer loop will contribute O(n) while the inner loop will contribute O(n / 2) on average. Because our loops are nested we will get O(n^2);

**Space Complexity**: O(n)

- Because we are creating a subArray for each element in the original input, our Space Comlexity becomes linear.

```js
function insertionSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    let current = arr[i];
    let j = i - 1;
    while (j > -1 && current < arr[j]) {
      arr[j + 1] = arr[j];
      j--;
    }
    arr[j + 1] = current;
  }
  return arr;
}
```

#### Insertion Sort Pseudocode

- Loop through array elements and compare first element with all other elements
  - Swap if necessary
  - Repeat until array is sorted

<img src=https://s3-us-west-1.amazonaws.com/appacademy-open-assets/data_structures_algorithms/naive_sorting_algorithms/insertion_sort/images/InsertionSort.gif />

## <b>Merge Sort</b> <a id="mergesort"></a>

**Time Complexity**: Log Linear O(nlog(n))

- Since our array gets split in half every single time we contribute O(log(n)). The while loop contained in our helper merge function contributes O(n) therefore our time complexity is O(nlog(n))

**Space Complexity**: O(n)

- We are linear O(n) time because we are creating subArrays.

```js
// Iterative merge
function merge(arr1, arr2) {
  let result = [];
  while (arr1.length && arr2.length) {
    if (arr1[0] < arr2[0]) {
      result.push(arr1.shift());
    } else {
      result.push(arr2.shift());
    }
  }
  return [...result, ...arr1, ...arr2];
}

// Recursive merge
function mergeSort(arr) {
  if (arr.length <= 1) return arr;

  const mid = Math.floor(arr.length / 2);
  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));

  return merge(left, right);
}
```

#### Merge Sort Pseudocode

- Create an empty array to store smallest values
  - While there are still values in each array
    - Compare current values from both arrays
      - Remove whichever is smaller from its array and add it to the results array

![mergesort](https://s3-us-west-1.amazonaws.com/appacademy-open-assets/data_structures_algorithms/efficient_sorting_algorithms/merge_sort/images/MergeSort.gif)

---

## <b>Quick Sort</b> <a id="quicksort"></a>

**Time Complexity**: Quadratic O(n^2)

- Even though the average time complexity O(nLog(n)), the worst case scenario is always quadratic.

**Space Complexity**: O(n)

- Our space complexity is linear O(n) because of the partition arrays we create.

```js
function quickSort(array) {
  if (array.length <= 1) return array;

  let pivot = array.shift();

  let left = array.filter((x) => x < pivot);
  let right = array.filter((x) => x >= pivot);

  let sortedLeft = quickSort(left);
  let sortedRight = quickSort(right);

  return [...sortedLeft, pivot, ...sortedRight];
}
```

#### Quick Sort Pseudocode

- Set up a stop case for when the array is empty
  - Create a pivot variable to compare array values with
  - Create an array that will store all array values smaller than the pivot
  - Create an array that will store all array values greater than the pivot
  - Call the quickSort function on both array recursively until they are empty
  - Return an array containg values smallest to largest in order

![quick](https://s3-us-west-1.amazonaws.com/appacademy-open-assets/data_structures_algorithms/efficient_sorting_algorithms/quick_sort/images/QuickSort.gif)

---

## <b>Binary Search</b>

**Time Complexity**: Log Time O(log(n))

**Space Complexity**: O(1)

> Recursive Solution

```js
function binarySearch(array, target) {
  if (array.length === 0) return false;

  let midPt = Math.floor(array.length / 2);

  if (array[midPt] === target) {
    return true;
  } else if (list[midPt] > target) {
    return binarySearch(list.slice(0, mid), target);
  } else {
    return binarySearch(list.slice(midPt + 1), target);
  }
}
```

> Min Max Solution

```js
function binarySearch(array, target) {
  let start = 0;
  let end = array.length - 1;

  while (start <= end) {
    let midpoint = Math.floor((start + end) / 2);

    if (target === array[midpoint]) {
      return midpoint;
    }

    if (target > array[midpoint]) {
      start = midpoint + 1;
    }

    if (target < array[midpoint]) {
      end = midpoint - 1;
    }
  }
  return -1;
}
```

---

## **Memoization** <a id="memoization"></a>

- **Memoization** is a design pattern used to reduce the overall number of calculations that can occur in algorithms that use recursive strategies to solve
- There are two features that comprise memoization:

  - the function is recursive
  - the additional data structure used is typically an object (we refer to this as the memo!)

  ##### Main steps for memoizing a problem:

  1. Write out the brute force recursion
  2. Add the memo object as an additional argument

  - Keys on this object represent input, values are the corresponding output

  3. Add a base condition that returns the stored value if the argument is already in the memo
  4. Before returning a calculation, store the result in the memo for future use

  ##### Example of a standard and memoized fibonacci:

  ```javascript
  // Standard Implementation
  // Time Complexity: O(2^n)
  //   - For each call to fib, we have to make two branches, with n levels to this tree
  function fib(n) {
    if (n === 1 || n === 2) return 1;
    return fib(n - 1) + fib(n - 2);
  }

  // Using memoization
  // Time Complexity: O(n)
  //   - We only ever have to calculate fib(x) one time, every other time that we use it in a larger problem, the result is immediately accessible in our memo
  //   - The memo removes the repeated trees of calculations from our original code
  function fib(n, memo = {}) {
    if (n in memo) return memo[n]; // If we already calculated this value, return it
    if (n === 1 || n === 2) return 1;

    // Store the result in the memo first before returning
    // Make sure to pass the memo in to your calls to fib!
    memo[n] = fib(n - 1, memo) + fib(n - 2, memo);
    return memo[n];
  }
  ```

---

## **Tabulation** <a id="tabulation"></a>

- **Tabulation** has to look through the entire search space; memoization does not
  - tabulation requires careful ordering of the subproblems is; memoization doesn’t care much about the order of recursive calls.

##### Main considerations for using tabulation:

- Figure out how big is your table
  - Typically going to be base on input size (number in fibonacci, length of string in wordBreak)
- What does my table represent?
  - You are generally building up your answer.
  - In fibonacci, we used the table to store the fib number at the corresponding index.
  - In stepper, we stored the boolean of whether it was possible to get to that location.
- What initial values do I need to seed?
  - Consider what your end result should be (boolean, number, etc.).
  - Your seed data is generally going to be the immediate answer that we know from our base condition.
  - In fibonacci, we knew the first two numbers of the series.
  - In stepper, we knew that it was possible to get to our starting location, so we seeded it as true, defaulting the rest to false so that we could later change its value if we could make that step.
- How do I iterate and fill out my table?
  - We typically need to iterate over or up to our input in some way in order to update and build up our table until we get our final result.
  - In fibonacci, we iterated up to our input number in order to calculate the fib number at each step.
  - In stepper, we iterated over each possible stepping location. If we could have made it to that point from our previous steps (ie that index was true in our table), we continued updating our table by marking the possible landing spots as true.

##### Example of a tabulated fibonacci:

```javascript
// Using tabulation
// Time Complexity: O(n)
//   - We are iterating through an array directly related to the size of the input and performing a constant number of calculations at each step (adding our two previous values together and storing the result in the array).
function fib(n) {
  // We create a table to track our values as we build them up
  // We're making it n+1 here so that table[n] lines up with the nth fib number
  // This is because arrays are zero-indexed.
  // We could have used an array of length n, but we would have to remember that
  // the nth fib number would then be stored at table[n-1]. Completely doable,
  // but I think making them line up is more intuitive.
  let table = new Array(n + 1);
  // Seed our table with our starting values.
  // Again, if we had a table of length n, we could have seeded table[0] = 1
  // and table[1] = 1 and had the same final result with our indices shifted.
  table[0] = 0;
  table[1] = 1;

  // Iterate through our input and fill out our table as we go.
  for (let i = 2; i < table.length; i++) {
    table[i] = table[i - 1] + table[i - 2];
  }

  // At the end, the final entry in our table is the result we are looking for.
  // The table holds all of the sub-answers that we used to get to this result.
  return table[n];
}
```
