# Week 26

## Algorithm

### [14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)

#### Description

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

#### Example 1

```example
Input: [ "flower", "flow", "flight" ]
Output: "fl"
```

#### Example 2

```example
Input: [ "dog", "racecar", "car" ]
Output: ""
```

#### Note

All given inputs are in lowercase letters `a-z`

#### Solution

```javascript
/**
 * longest commmon prefix
 * `recude` was design for it.
 * @returns {Array} strs
 * @returns {String}
 */
const longestCommonPrefix = (strs) => {
  if (strs === undefined || strs.length === 0 ) return '';
  const common = (prev, next) => {
    let i = 0;
    while (prev[i] && next[i] && prev[i] === next[i]) i++;
    return prev.slice(0, i);
  }
  return strs.reduce(common);
};
```


## Review

 [https://hackernoon.com/understanding-micro-frontends-b1c11585a297?source=search_post---------0](https://hackernoon.com/understanding-micro-frontends-b1c11585a297?source=search_post---------0) 

There is a framework already out there called [single-spa](https://single-spa.js.org/). The project relies on naming conventions of each app to resolve and load **micro-apps**. Easy to grasp the idea and follow the patterns. So it can be a good initial introduction for experimenting the idea on my local environment. But the downside of the project is you have to build each **micro-app**in a specific way so they can play nice with the framework.

## Technique
JavaScript ArrayLike check trick.

```javascript
/**
 * Checks if the provided argument is array-like (i.e. is iterable).
 * Check if the provided argument is not `null` and thaat its `Symbol.iterator` property is a function.
 * @param {Object} obj
 * @returns {Boolean}
 */
const isArrayLike = obj => obj != null && typeof obj[Symbol.iterator] === 'function';
```

## Share

How to reuse these frontend component with different UI style, and combine them into one project which should supply to the end user a seamless experience? HOW?