# Week 6th

## Algorithm

### [231. Power of Two](https://leetcode.com/problems/power-of-two/)  

#### Description

Given an integer, write a function to determine if it is a power of two.

#### Example 1

```javascript
Input: 1
Output: true
Explanation: 2^0 = 1
```

#### Example 2

```javascript
Input: 16
Output: true
Explanation: 2^4 = 16
```

#### Example 3

```javascript
Input: 218
Output: false
```

#### Solution Recursively

```javascript
const isPowerOfTwo = (n) => {
  if (n < 1) {
    return false;
  } else if (n === 1) {
    return true;
  } else {
    return isPowerOfTwo( n /= 2);
  }
};
```


## Review

[What is Hoisting in Javascript? – JavaScript In Plain English – Medium](https://medium.com/javascript-in-plain-english/https-medium-com-javascript-in-plain-english-what-is-hoisting-in-javascript-a63c1b2267a1)  

Hoisting only lift the variables declaration to the top of the function scope or to the global scope and lift the functions declaration under the variables. With the variables value stay in the original place as their lexical scope are.  

One technique to keep the value hosting is give the variable a **IIFE**, for the further follow this wiki [Immediately invoked function expression - Wikipedia](https://en.wikipedia.org/wiki/Immediately_invoked_function_expression). 

## Technique

```javascript
/**
 * Assigns default values for all properties in an object that are `undefined`.
 * Use `Object.assign()` to create a new empty object and copy the original one to maintain key order,
 * use `Array.prototype.reverse()` and the spread operator `...` to combine the default values from left to right,
 * finally use `obj` again to overwrite propertiew that originally had a value.
 * @param {Object} obj
 * @param  {...any} defs
 * @returns {Object}
 */
const defaults = (obj, ...defs) => Object.assign({}, obj, ...defs.reverse(), obj);

const d = defaults({ a: 1 }, { b: 2 }, { b: 6 }, { a: 3 });
console.log(JSON.stringify(d)); // {"a":1,"b":2}

```

## Share

Don’t be rude to your parents, they raised you, and offer their whole life for you life comfort, I’m practicing to be more gentle to my parents.
