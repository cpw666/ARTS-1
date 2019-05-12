# Week 19

## Algorithm

# [48. Rotate Image](https://leetcode.com/problems/rotate-image/)

## Description

You are given an *n x x* 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

## Note

You have to rotate the image **in-place**, which means you have to modify the input 2D matrix directly. **DO NOT** allocate another 2D matrix and do the rotation.

## Example 1

```example
Given input matrix =
[
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
],

rotate the input matrix **in-place** such that it becomes:
[
  [7, 4, 1],
  [8, 5, 2],
  [9, 6, 3]
]
```

## Example 2

```example
Given input matrix =
[
  [5, 1, 9, 11],
  [2, 4, 8, 10],
  [13, 3, 6, 7],
  [15, 14, 12, 16]
],

rotate the input matrix **in-place** such that it becomes:
[
  [15, 13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7, 10, 11]
]
```

## Solution

```javascript
/**
 * input: matrix = [
 *  [5, 1, 9, 11],
 *  [2, 4, 8, 10],
 *  [13, 3, 6, 7],
 *  [15, 14, 12, 16]
 * ];
 *
 * firstly reverse the matrix using `Array.prototype.reverse()`
 * [
 *  [15, 14, 12, 16],
 *  [13, 3, 6, 7],
 *  [2, 4, 8, 10],
 *  [5, 1, 9, 11]
 * ];
 *
 * and then we transpose the matrix, notice the nested loop, basically we exchange the two parts:
 * right-top
 * [
 *  [ ,  ,  ,  ],
 *  [13,  ,  , ],
 *  [2, 4,  ,  ],
 *  [5, 1, 9,  ]
 * ];
 *
 * left-bottom
 * [
 *  [ , 14, 12, 16],
 *  [ ,  , 6, 7],
 *  [ ,  ,  , 10],
 *  [ ,  ,  ,  ]
 * ];
 *
 * And result
 * [
 *  [15, 13, 2, 5],
 *  [14, 3, 4, 1],
 *  [12, 6, 8, 9],
 *  [16, 7, 10, 11]
 * ]
 * @ param {Array} matrix
 */
const rotate = (matrix) => {
  matrix.reverse();
  for (let i = 0, isize = matrix.length; i < isize; i++) {
    for (let j = 0; j < i; j++) {
      [matrix[i][j], matrix[j][i]] = [matrix[j][i], matrix[i][j]];
    }
  }
};
```


## Review

[The Cost Of JavaScript In 2018 – Addy Osmani – Medium](https://medium.com/@addyosmani/the-cost-of-javascript-in-2018-7d8950fbb5d4)

- **To stay fast, only load JavaScript needed for the current page.**
Prioritize what a use will need and lazy-load the rest with code-splitting. This gives you the best chance at loading and getting interactive fast. Stacks with route-based code-splitting by default are game-changers.

- **Embrace performance budgets and learn to live within them.**
For mobile, aim for a JS budget of < 170KB minified/compressed. Uncompressed this is still ~ 0.7MB of code. Budgets are critical to success, however, they can’t magically fix perf in isolation. Team culture, structure and enforcement matter. Building without a budget invites performance regressions and failure.

- **Learn how to audit and trim your JavaScript bundles.**
There’s a high chance you’re shipping full-libraries when you only need a fraction, polyfills for browsers that don’t need them, or duplicate code.

- **Every interaction is the start of a new ‘Time-to-interactive’; consider optimizations in this context.**
Transmission size is critical for low-end mobile networks and JavaScript parse time for CPU-bound devices.

- **If client-side JavaScript isn’t benefiting the user-experience, ask yourself if it’s really necessary.**
Maybe server-side-rendered HTML would actually be faster. Consider limiting the use of client-side frameworks to pages that absolutely require them. Server-rendering and client-rendering are a disaster if done poorly.

## Technique

Sort characters in string

```javascript
/**
 * Alphabetically sorts the characters in a string.
 * Use the spread operator (`...`), `Array.prototype.sort()` and `String.localeCompare()` to sort the characters in `str`, recombine using `Array.prototype.join()`.
 * *@param* ~{String}~ str
 * *@returns* ~{String}~
 */
const sortCharactersInString = str => [...str].sort((a, b) => a.localeCompare(b)).join('');
```


## Share

Learn to be good in data structures and algorithms not just in business, cause program = data structure + algorithm.