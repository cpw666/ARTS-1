# Week 14th

## Algorithm

### [217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/description/)

#### Description

Given an array of integers, find if the array contains any duplicates.
Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

#### Example 1

```example
Input: [1, 2, 3, 1]
Output: true
```

#### Example 2

```example
Input: [1, 1, 1, 3, 3, 4, 3, 2, 4, 2]
Output: true
```

#### Solution

```javascript
/**
 * check if element in the array has duplicators and return `true`, otherwise return `false`.
 * Add the elements into a `Set`, and then compair set size with length of the incomming array.
 * If these two size/length are equal then return `false`, otherwise return `true`.
 * @param {Array} nums - integers array
 * @returns {Boolean}
 */
const containsDuplicate = (nums) => nums.length === 0 ? false : nums.length === (new Set(nums)).size ? false : true;

const nums = [1, 2, 3];
const hasDuplicators = containsDuplicate(nums);
console.log(hasDuplicators);
```

## Review

[What is `this`? The Inner Workings of JavaScript Objects](https://medium.com/javascript-scene/what-is-this-the-inner-workings-of-javascript-objects-d397bfa0708a)

A good understanding of how `this` behaves in JavaScript will save you a lot of time debugging tricky issues. Practices will help you understand, play with the examples. 

What started as dynamic method lookups that you could redirect with `.call()`, `.bind()`, or `.apply()` has become significantly more complex with the addition of `class` and arrow function behavior. It may be helpful to compartmentalize a little. Remember that arrow functions always delegate `this` to the lexical scope, and that `class` `this` is actually lexically scoped to the constructor functions under the hood. If you’re even in doubt about what `this` is, remember to use your debugger to verify the object is what you think it is.

## Technique

JavaScript truth check for a collection

```javascript
/**
 * Checks if the predicate (second argument) is truth on all elements of a collection (first argument).
 * Use `Array.prototype.every()` to check if each passed object has the specified property and if it returns a truthy value.
 * @param {Array} collection
 * @param {Object} collection[]
 * @param {String} pre
 * @return {Array}
 */
const truthCheckCollection = (collection, pre) => collection.every(obj => obj[pre]);
```

## Share

As we are developer, we do need to understand the these data structures and algorithms we’ve been taught at school. Not because we don’t need these at daily work, cause your job don’t need you to use these technique, go change one. 
