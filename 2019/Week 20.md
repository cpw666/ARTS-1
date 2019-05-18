# Week 20

## Algorithm

### [387. First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/)

#### Description

Given a string, find the first non-repeating character in it and return it’s index. If it doesn’t exist return -1.

#### Example

```example
s = 'leetcode'
return 0

s = 'loveleetcode'
return 2
```

#### Note

You may assume the string contain only lowercase letters.

#### Solution

```javascript
/**
 * reduce the string into a map which key's are the index of each char's unicode index, values are the increasing number based on each chars frequency
 * filter out the only 1 times chars
 * shift out the first element of array, cause map store that in the setted order.
 * if got no key shifted out return -1 otherwise return the index of the shifted out key which transform into letter using `String.fromCharCode()`
 * @param {String} s
 * @return {Number}
 */
const firstUniqChar = (s) => {
  const begin = 'a'.charCodeAt();
  const frequency = [...s].reduce((freq, c) => {
    const key = c.charCodeAt() - begin;
    const has = freq.has(key);
    let seed = has ? freq.get(key) + 1 : 1;
    freq.set(key, seed);
    return freq;
  }, new Map());
  const uniques = Array.from(frequency.entries()).filter(([_, times]) => times === 1);
  const firstCharKey = uniques.length && uniques.shift().shift() + begin;
  return firstCharKey ? s.indexOf(String.fromCharCode(firstCharKey)) : -1;
};
```

## Review

 [https://adamwathan.me/renderless-components-in-vuejs/](https://adamwathan.me/renderless-components-in-vuejs/) 

Adam Wathan gave us a fantastic talk on on creating reusable view components. 

Here is my thoughts:

> Splitting a components into a presentational component and a genderless component is an extremely useful pattern to master and can make code reuse a lot easier, but it’s to always worth. Use this approach if:  

1. You’re building a library and you want to make it easy for users to customize how your component looks.
2. You have multiple components in your project with very similar behavior but different layouts.

## Technique

Map String

```javascript
/**
 * Creates a new string with the results of calling a provided function on every character in the calling string.
 * Use `Array.prototype.split()` and `Array.prototype.map()` to call the provided function, `fn`, for each character in `str`.
 * Use `Array.prototype.join()` to recombine the array of characters into a string.
 * The callback function, `fn`, takes three arguments (the current character, the index of the current character and the string `mapString` was called upon).
 * *@param* {String} str
 * *@param* {Function} fn
 * *@returns* {Boolean}
 */
const mapString = (str, fn) =>
  str
    .split('')
    .map((c, i) => fn(c, i, str))
    .join('');
```


## Share

Design patterns are out productivity tools.