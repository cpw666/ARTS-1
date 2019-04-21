# Week 16th

## Algorithm
### [283. Move Zeros](https://leetcode.com/problems/move-zeroes/)

#### Description

Given an array `nums`, write a function to move all `0`’s to the end of it while maintaining to relative order of the non-zero elements.

#### Example

```example
Input: [0, 1, 0, 3, 12]
Output: [1, 3, 12, 0, 0]
```

#### Note

1. You must do this **in-place** without making a copy of the array.
2. Minimize the total number of operations

#### Solution

```javascript
/**
 * 1. Shift non-zero values as for forward as possible.
 * 2. Fill remaining space with zeros.
 * @param {Array} nums
 * @returns {undefined}
 */
const moveZeros = (nums) => {
  if (!nums || nums.length === 0) return [];
  let insertPosition = 0;
  nums.forEach(num => {
    if (num !== 0) nums[insertPosition++] = num;
  });
  while (insertPosition < nums.length) {
    nums[insertPosition++] = 0;
  }
};

const nums = [0, 1, 0, 3, 12];
moveZeros(nums);
console.log(JSON.stringify(nums));
```


## Review

[TDD Changed My Life – JavaScript Scene – Medium](https://medium.com/javascript-scene/tdd-changed-my-life-5af0ce099f80)

Test Driven Development is very simple:

1. Before you write implementation code, write some code the proves that the implementation works or fails. Watch the test fail before moving to next step (this is how we know that a passing test is not a false positive — how we test our tests).
2. Write the implementation code and watch the test pass.
3. Refactor if needed. You should feel confident refactoring your code now that you have a test to tell you if you’ve broken something.

## Technique

Escape HTML tags in string.

```javascript
/**
 * Escapes a string for use in HTML
 * Use `String.prototype.replace()` with a regexp that matches the characters that need to be escaped,
 * using a callback function to replace each character instance with its associated escaped character using a directionary (object).
 * @param {String} str
 * @returns {String}
 */
const escapeHTML = str =>
  str.replace(
    /[&<>'"]/g,
    tag => ({
      '&': '&amp;',
      '<': '&lt;',
      '>': '&gt;',
      "'": '&#39;',
      '"': '&quot;'
    }[tag] || tag)
  );
```

## Share

Work smartly, don’t work for you boss, work for yourself.
