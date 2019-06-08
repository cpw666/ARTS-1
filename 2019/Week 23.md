# Week 23

## Algorithm

# [8. String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/)

## Description

Implement `atoi` which converts a string to an integer.

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned.

## Note

- Only the space character ‘ ‘ is considered as whitespace character.
- Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. If the numerical value is out of the range of representable values, INT_MAX (231 − 1) or INT_MIN (−231) is returned.

## Example 1

```example
Input: "42"
Output: 42
```

## Example 2

```example
Input: "   -42"
Output: -42
Explanation: The first non-whitespace character is '-', which is the minus sign. Then take as many numerical digits as possible, which gets 42.
```

## Example 3

```example
Input: "4193 with words"
Output: 4193
Explanation: Conversion stops at digit '3' as the next character is not a numerical digit.
```

## Example 4

```example
Input: "words and 987"
Output: 0
Explanation: The first non-whitespace character is 'w', which is not a numerical digit or a +/- sign. Therefore no valid conversion could be performed.
```

## Example 5

```example
Input: "-91283472332"
Output: -2147483648
Explanation: The number "-91283472332" is out of the range of a 32-bit signed integer. Thefore INT_MIN (−231) is returned.
```

## Solution

```javascript
/**
 * using `parseInt` 😘
 * @param {String} str
 */
const myAtoi = (str) => {
  return Math.max(Math.min(parseInt(str) || 0, 2147483647), -2147483648)
};
```


## Review

[What is `this`? The Inner Workings of JavaScript Objects](https://medium.com/javascript-scene/what-is-this-the-inner-workings-of-javascript-objects-d397bfa0708a)

A good understanding of how `this` behaves in JavaScript will save you a lot of time debugging tricky issues. If you got any of the answers wrong, it would serve you well to practice. Play with the examples, then come back and test yourself again until you can both ace the test, and explain to somebody else why the methods return what they return.

If that was harder than you expected, you’re not alone. I’ve tested quite a few developers on this topic, and I think only one developer has aced it so far.

What started as dynamic method lookups that you could redirect with `.call()`, `.bind()` , or `.apply()` has become significantly more complex with the addition of `class` and arrow function behavior. It may be helpful to compartmentalize a little. Remember that arrow functions always delegate `this` to the lexical scope, and that `class` `this` is actually lexically scoped to the constructor functions under the hood. If you’re ever in doubt about what `this` is, remember to use your debugger to verify the object is what you think it is.

Remember also that in JavaScript, you can do a lot without ever using `this`. In my experience, almost anything can be reimplemented in terms of pure functions which take all the arguments they apply to as explicit parameters (you can think of `this` as an implicit parameter with mutable state). Logic encapsulated in pure functions is deterministic, which makes it more testable, and has no side-effects, which means that unlike manipulating `this`, you’re unlikely to break anything else. Every time you mutate `this`, you take the chance that something else dependent on the value of `this` will break.

That said,  `this` is sometimes useful. For instance, to share methods between a large number of objects. Even in functional programming, `this` can be useful to access other methods on the object to implement algebraic derivations to build new algebras on top of existing ones. For instance, a generic `.flatMap()` can be derived by accessing `this.map()` and `this.constructor.of()`.



## Technique
```javascript
/**
 * Converts a string to camelcase.
 * Break the string into words and combine them capitalizing the first letter of each each word, using a regexp.
 * @param {String} str
 * @returns {String}
 */
const toCamelCase = str => {
  let s =
    str &&
    str
      .match(/[A-Z]{2,}(?=[A-Z][a-z]+[0-9]*|\b)|[A-Z]?[a-z]+[0-9]*|[A-Z]|[0-9]+/g)
      .map(x *=>* x.slice(0, 1).toUpperCase() + x.slice(1).toLowerCase())
      .join('');
  return s.slice(0, 1).toLowerCase() + s.slice(1);
};
```

## Share
PMP should just a way, not the only way, terms should be clarify, so we can manage projects properly.