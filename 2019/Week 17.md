# Week 17

## Algorithm

### [66. Plus One](https://leetcode.com/problems/plus-one/)

#### Description

Given a **non-empty** array of digits representing a non-negative integer, plus one to integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.

#### Example 1

```example
Input: [1, 2, 3]
Output: [1, 2, 4]
Explanation: The array represents the integer 123.
```

#### Example 2

```example
Input: [4, 3, 2, 1]
Output: [4, 3, 2, 2]
Explanation: The array represents the integer 4321.
```

#### Solution

```javascript
const plusOne = (digits) => {
  const length = digits.length;
  for (let i = length - 1; i >= 0; i--) {
    if (digits[i] < 9) {
      digits[i] += 1;
      return digits;
    }
    digits[i] = 0;
  }
  digits.unshift(1);
  return digits;
};

const digits = [6,1,4,5,3,9,0,1,9,5,1,8,6,7,0,5,5,4,3];
const added = plusOne(digits);
console.log(JSON.stringify(added)); // [6,1,4,5,3,9,0,1,9,5,1,8,6,7,0,5,5,4,4]
```


## Review

[Understand JavaScript closure. Once and for all. – Aseem Taneja – Medium](https://medium.com/@atej/learn-javascript-closure-nth-prime-d0cf7bc5ef47)

Three things JavaScript programmer should remember.

1. The Thread
JavaScript is single threaded. This simply means that it can only do one thing at a time.

2. The Execution Context
Everything that goes on in JavaScript has an execution context. The default is global context. **Each call to a function creates a new execution context**. Each execution context is associated with its own variable environment.

Once the function is done executing, we loose access to its execution context. The only thing we retain access to is what the function returns.

3. The Call Stack
To keep track of where it is in the execution of a program, JavaScript uses a call stack. When a function is called it is **pushed on top** of the call stack. When it’s done executing it is **popped off the top** of the call stack.

If an expression which tries to use the value held or referenced by a variable is encountered, JavaScript starts from the execution context the expression is encountered in and travels outwards (i.e., from the top of the call stack, downwards). As soon as a declaration of a variable of the same name is found in a particular scope, the latest value of that variable in the scope is used.

## Technique

```javascript
/**
 * Checks if a string is an anagram of another string (case-insensitive, ignores spaces, punctuation and special characters).
 * Use `String.toLowerCase()`, `String.prototype.replace()` with an appropriate regular expression to remove unnecessary characters,
 * `String.prototype.split()`, `Array.prototype.sort()` and `Array.prototype.join()` on both strings to normalize them, then check if their normalized forms are equal.
 * @param {String} str1
 * @param {String} str2
 * @returns {Boolean}
 */
const isAnagram = (str1, str2) => {
  const normalize = str =>
    str
      .toLowerCase()
      .replace(/[^a-z0-9]/gi, '')
      .split('')
      .sort()
      .join('')
  return normalize(str1) === normalize(str2);
}
```

## Share

Learn with you knowledge, not only with your insist.