# Week 21

## Algorithm

### [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/)

#### Description

Given two strings `s` and `t`, write a function to determine if `t` is an anagram of `s`.

#### Example 1

```example
Input: s = "anagram", t = "nagaram"
Output: true
```

#### Example 2

```example
Input: s = "rat", t = "cat"
Output: false
```

#### Note

You may assume the string contains only lowercase alphabets.

#### Follow up

What if the inputs contain unicode characters? How would you adapt you solution to such case?

#### Solution 1

With single order solution

```javascript
const isAnagram = (s, t) => {
  if (s.length !== t.length) return false;
  const sChars = [...s].sort().join('');
  const tChars = [...t].sort().join('');
  return sChars === tChars;
};
```

#### Solution 2

With String iterator solution

```javascript
const isAnagram = (s, t) => {
  if (!s || !t || s.length !== t.length) return false;
  const alphaIndex = 'a'.charCodeAt();
  const alphabet = Array.from(new Array(26), _ => 0);
  for (let c of s) {
    const index = c.charCodeAt() - alphaIndex;
    alphabet[index]++;
  }
  for (let c of t) {
    const index = c.charCodeAt() - alphaIndex;
    alphabet[index]--;
  }
  for (let i = 0, length = alphabet.length; i < length; i++) {
    if (alphabet[i] !== 0) return false;
  }
  return true;
}
```


## Review

[What is a functor? – Thai Pangsakulyanont – Medium](https://medium.com/@dtinth/what-is-a-functor-dcf510b098b6)

Functor laws:
1. If you map over some functor with a function that simply returns the passed value (the identity function), the resulting functor should b equivalent to the original function.
2. Composing two functions and the mapping the resulting function over a functor should be the same as first mapping one function over the functor and then mapping the other one. If we can show that some type obeys both functor laws, we can rely on it having the same fundamental behaviors as other functors when it comes to mapping.

We’ve learned that a functor represents a set of things (in some structure) that can be mapped over to obtain a set of new things under that same structure.

We use the **map(f)** method to perform that mapping. An array is one popular functor.

Unfortunately, not many things in JavaScript provide a **.map(f)** method when it can somewhat be mapped over. To make a functor out of it, we either need to extend that type, or create a wrapper that acts as a functor.

Functors can be useful because we don’t have to care about its structure. We only care that we can map some function over it. Terms with  polymorphism? haha.

## Technique

JavaScript version escape regex

```javascript
/**
 * Escapes a string to use in a regular expression.
 * Use `String.prototype.replace()` to escape special characters.
 * @param {String} str
 * @returns {String}
 */
const escapeRegExp = str => str.replace(/[.*+?^${}()|[\]\\]/g, '\\$&');
```

## Share

I need a knowledge map for these I’ve learned and these I’m going to conquer.