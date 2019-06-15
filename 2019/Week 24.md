# Week 24

## Algorithm

# [28. Implement strStr()](https://leetcode.com/problems/implement-strstr/)

## Description

Implement `strStr()`.

Return the index of the first occurrence of needle in haystack, or **-1** if needle is not part of haystack.

## Example 1

```example
Input: haystack = "hello" needle = "ll"
Output: 2
```

## Example 2

```example
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

## Clarification

What should we return when `needle` is an empty string? This is a great question to ask during an interview.
For the purpose of this problem, we will return 0 when `needle` is an empty string. This is consistent to C’s `strstr()` and Java’s `indexOf()`.

## Solution

```javascript
const strStr = (haystack, needle) => haystack.indexOf(needle);
```


## Review

[Why ‘1’, ‘7’, ’11’.map(parseInt) returns 1, NaN, 3 in Javascript](https://medium.com/dailyjs/parseint-mystery-7c4368ef7b21)

`['1', '7', '11'].map(parseInt)` doesn’t work as intended because `map` passes three arguments into `parseInt()` on each iteration. The second argument `index` is passed into `parseInt` as a `radix` parameter. So, each string in the array is parsed using a different radix. `'7'` is parked as radix 1, which is `NaN`, `'11'` is passed as radix 2, which is 3. `’1’` is passed as the default radix 10, because its index 0 is falsy.

## Technique

JavaScript words

```javascript
/**
 * Converts a given string into an array of words.
 * Use `String.prototype.split()` with a supplied pattern (defaults to non-alpha as a regexp) to convert to an array of strings.
 * Use `Array.prototype.filter()` to remove any empty strings, Omit second argument to use the default regexp.
 * @param {String} str
 * @param {String} pattern
 * @returns {Array}
 */
const words = (str, pattern = /[^a-zA-Z-]+/) => str.split(pattern).filter(Boolean);

console.log(words('I love javaScript!!')); // ["I", "love", "javaScript"]
console.log(words('python, javaScript & coffee')); // ["python", "javaScript", "coffee"]
```

## Share

Don’t just give answer to your mates, give them reference which let them solve the question they’re facing, level up with each other.