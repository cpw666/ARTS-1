# Week 46

## Algorithm

### [190. Reverse Bits](https://leetcode.com/problems/reverse-bits/)

#### Description

Reverse bits of a given 32 bits unsigned integer.

#### Example 1

```example
Input: 00000010100101000001111010011100
Output: 00111001011110000010100101000000
Explanation: The input binary string 00000010100101000001111010011100 represents the unsinged integer 43261596, so return 964176192 which its binary representation is 00111001011110000010100101000000.
```

#### Example 2

```example
Input: 11111111111111111111111111111101
Output: 10111111111111111111111111111111
Explanation: The input binary string 11111111111111111111111111111101 represents the unsigned integer 4293967293, so return 3221225471 which its binary representation is 10111111111111111111111111111111.
```

#### Note

- Note that in some languages such as Java, there is no unsinged integer type. In this case, boty input and output will be given as singed integer type and should not affect your implementation, as the internal representation of the integer is the same whether it is singed or unsigned.
- In java, the compiler represents the signed integers using [2's complement notation](https://en.wikipedia.org/wiki/Two%27s_complement). Therefore, in **Example 2** above the input represents the signed integer `-3` and the output represents the signed integer `-1073741825`.

#### Solution

```javascript
const reverseBits = n => {
  let result = 0;
  let count = 32;

  while (count—) {
    result *= 2;
    result += n & 1;
    n = n >> 1;
  }
  return result;
};
```

## Review

[Master the JavaScript Interview: What’s the Difference Between Class & Prototypal Inheritance?](https://medium.com/javascript-scene/master-the-javascript-interview-what-s-the-difference-between-class-prototypal-inheritance-e4cd0a7562e9)

We do need to understand that there are three different kins of prototypal OO.

**Concatenative inheritance:** The process of inheriting features directly from one object to another by copying the source objects properties. In JavaScript, source prototypes are commonly referred to as **mixins.** Since ES6, this feature has a convenience utility in JavaScript called `Object.assign()`. Prior to ES6, this way commonly done with Underscore/Lodash's `.extend()` jQuery's `$.extend()`, and so on...The composition example in artical uses concatenative inheritance.

**Prototype delegation:** In JavaScript, an object may have a link to a prototype for **delegation**. If a prototype is not found on the object, the lookup is **delegated** to the **delegated prototype,** which may have a link to own delegate prototype, and so on up the chain until you arrive at `Object.prototype`, which is the root delegate. This is the prototype that gets hooked up when you attach to a `Constructor.prototype` and inheritiate with `new`. You can also use `Object.create()` for this purpose, and even mix this techinque with concatenation in order to flatten multiple prototypes to a single delegate, or extend the object instance after creation.

**Functional inheritance:** in JavaScript, any function can create an object. When that function is not a constructor (or `class`), it’s called a **factory function**. Functional inheritance works by producing an object from a factory, and extending the produced object by assigned properties to it directly (using concatenative inheritance). Dogulas Crokford coined the term, but functional inheritance has been in common use in JavaScript for a long time.

As you’re probably starting to realize, **concatenative inheritance is the secret sauce that enables object composition in JavaScript,** which makes both prototype delegation and functional inheritance a lot more interesting.

When most people think of prototypal OO in JavaScript, *they think of prototype delegation.* By now you should see that they’re missing out on a lot. Delegate prototypes aren't the great alternative to class inheritance __ **Object composition is.**


## Technique

### Clearfix

#### [Check me out](https://codepen.io/charleserious/pen/RwweVbg)

```html
<!DOCTYPE html>
<html lang=“en”>
<head>
  <meta charset=“UTF-8”>
  <meta name=“viewport” content=“width=device-width, initial-scale=1.0”>
  <meta http-equiv=“X-UA-Compatible” content=“ie=edge”>
  <link rel="stylesheet" href="./main.css">
  <title>Clearfix</title>
</head>
<body>
  <div class="clearfix">
    <div class="floated">float a</div>
    <div class=“floated”>float b</div>
    <div class=“floated”>float c</div>
  </div>
</body>
</html>
```

```css
html, body {
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  display: flex;
  flex-flow: row nowrap;
  align-items: center;
  justify-content: space-evenly;
}

.clearfix::after {
  content: '';
  display: block;
  clear: both;
}

.floated {
  float: left;
}
```

#### Explanation

1. `.clearfix::after` defines a pseudo-element.
2. `content: ‘’` allows the pseudo-element to affected layout.
3. `clear: both` indicates that the left, right or both sides of the element cannot be adjacent to earlier floated elements within the same block formatting context.

## Share

Draw your design, then code the test, then business code.