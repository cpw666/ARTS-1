# Week 45

## Algorithm

### [191. Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)

#### Description

Write a function that takes an unsigned integer and return the number of ‘1’ bits it has (also know as the [Hamming weight](http://en.wikipedia.org/wiki/Hamming_weight)).

#### Example 1

```example
Input: 00000000000000000000000000001011
Output: 3
Explanation: The input binary string 00000000000000000000000000001011 has a total of three '1' bits.
```

#### Example 2

```example
Input: 00000000000000000000000010000000
Output: 1
Explanation: The input binary string 00000000000000000000000010000000 has a total of one ‘1’ bit.
```

#### Example 3

```example
Input: 11111111111111111111111111111101
Output: 31
Explanation: The input binary string 11111111111111111111111111111101 has a total thirty one '1' bits.
```

#### Note

- Note that in some languages such as Java, there is no unsigned integer type. In this case, the input will be given as a signed integer type and should not effect your implementation, as the internal binary representation of the integer is the same whether it is signed or unsigned.
- In Java, the compiler represents the singed integers using [2's complement notation](https://en.wikipedia.org/wiki/Two%27s_complement). Therefore, in **Example 3** above the input represents the signed integer `-3`

#### Solution

```javascript
/**
 * n & (n - 1) drops the lowest set bit. It’s a neat little bit trick.
 *
 * Let’s use n = 00101100 as an example. This binary representation has three 1s.
 *
 * If n = 00101100, then n - 1 = 00101011, so n & (n - 1) = 00101100 & 00101011 = 00101000. Count = 1.
 *
 * If n = 00101000, then n - 1 = 00100111, so n & (n - 1) = 00101000 & 00100111 = 00100000. Count = 2.
 *
 * If n = 00100000, then n - 1 = 00011111, so n & (n - 1) = 00100000 & 00011111 = 00000000. Count = 3.
 *
 * n is now zero, so the while loop ends, and the final count (the numbers of set bits) is returned.
 *
 * @param {Number} n
 * @returns {Number}
 */
const hammingWeight = n => {
  let count = 0;
  while (n) {
    n &= (n - 1);
    count++;
  }
  return count;
};
```

## Review

[Data Encapsulation in JavaScript - JavaScript in Plain English - Medium](https://medium.com/javascript-in-plain-english/data-encapsulation-in-javascript-76730d89c3dc)

The Trade-offs
1. It uses Proxy to support instance and static non-public members and the corresponding syntax. This will make it a bit slow by comparison, but not so much as to make it unusable unless execution speed becomes a critical factor.
2. Since static support require the constructor function to be Proxied, WebComponents cannot be directly constructed. This is remedied by extending the ClassicJS class and using that extension as the WebComponent.
3. Either `_` or `$` must be used to access private members. As such, no new property beginning with the chosen character can be create after the declaration.
4. New own properties will only appear if you define them or the base class don’t have a property by that name. All assignment to a property of a base class go directly to that class.

## Technique

### Box-sizing reset

#### [Check me out](https://codepen.io/charleserious/pen/GRRdWaL)

```html
<!DOCTYPE html>
<html lang=“en”>
<head>
  <meta charset=“UTF-8”>
  <meta name=“viewport” content=“width=device-width, initial-scale=1.0”>
  <meta http-equiv=“X-UA-Compatible" content="ie=edge">
  <link rel="stylesheet" href="./main.css">
  <title>Box-sizing reset</title>
</head>
<body>
  <div class="box">border-box</div>
  <div class=“box content-box”>content-box</div>
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

*,
*::before
*::after {
  box-sizing: inherit;
}

.box {
  display: inline-block;
  width: 150px;
  height: 150px;
  padding: 10px;
  background: tomato;
  color: white;
  border: 10px solid red;
}

.content-box {
  box-sizing: content-box;
}
```

#### Explanation

1. `box-sizing: border-box` makes the addtion of `padding` or `border`s not affect an element's `width` or `height`.
2. `box-sizing: inherit` makes an element respect its parent's `box-sizing` rule.

## Share
Design and then make your design become the code.
