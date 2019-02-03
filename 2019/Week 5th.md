# Week 5th

## Algorithm

### [258. Add Digits](https://leetcode.com/problems/add-digits/)

#### Description

Given a non-negative integer `num`, repeatedly add all its digits until the result has only one digit.

#### Example

```javascript
Input: 38
Output: 2
Explanation: The precess is like: 3 + 8 = 11, 1 + 1 = 2. Since 2 has only one digit, return it.
```

#### Solution with recursion

```javascript
/**
 * Recursionaly add every digits in the given integer until the only one digit left.
 * @param {Number} num
 * @returns {Number}
 */
const addDigits = (num) => {
  const digits = num.toString();
  if (digits.length === 1) {
    return Number(digits);
  } else {
    return addDigits(digits.split('').reduce(acculator, 0));
  }
};

const acculator = (acc, v) => acc + Number(v);

const digits = 38890;
const result = addDigits(digits);
console.log(result);
```

#### Solution with congruence formula

```javascript
/**
 * Since this is a *digit root* problem, use th congruence formula to solve it.
 * @param {Number} num
 * @returns {Number}
 */
const addDigits = (num) => 1 + (num - 1) % 9;

const digits = 0;
const result = addDigits(digits);
console.log(result);
```

#### Solution with loop

```javascript
/**
 * Solve with loop
 * *@param* ~{Number}~ num
 * *@returns* ~{Number}~
 */
const addDigits = (num) => {
  let digits = num.toString();
  while (digits.length !== 1) {
    digits = digits.split('').reduce(acculator, 0).toString();
  }
  return digits;
}
```

## Review

[Here is why appendChild moves a DOM node between parents](https://blog.angularindepth.com/here-is-why-appendchild-moves-a-dom-node-instead-of-cloning-it-f8ef7a31735c)  

According to the [DOM Standard](https://dom.spec.whatwg.org/#node-trees), DOM node won’t be cloned by adding it to another parent, it will bring heavy process of tree cloning, and of cause with duplicate IDs issue. Even with the `cloneNode()` method, it warns us `cloneNode()` may lead to duplicate element IDs in a document, we could lose the reference of the node.

## Technique

Deep Clone in JavaScript

```javascript
/**
 * Creates a deep clone of an object.
 * Use recursion. Use `Object.assign()` and an empty object(`{}`) to create a shallow clone of the original.
 * Use `Object.keys()` and `Array.prototype.forEach()` to determine which key-value pairs need to be deep cloned.
 * @param {Object|Array} obj 
 */
const deepClone = obj => {
  const clone = Object.assign({}, obj);
  Object.keys(clone).forEach(
    key => (clone[key] = typeof obj[key] === 'object' ? deepClone(obj[key]) : obj[key])
  );
  return Array.isArray(obj) && obj.length
    ? (clone.length = obj.length) && Array.from(clone)
    : Array.isArray(obj)
      ? Array.from(obj)
      : clone;
}
```

## Share

Communication skills for developers

- Speak clearly and with conviction.
- Listen.
- Don’t interrupt.
