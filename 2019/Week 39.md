# Week 39

## Algorithm

### [53. Maximum Array](https://leetcode.com/problems/maximum-subarray/)

#### Description

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and rether its sum.

#### Example

```example
Input: [ -2, 1, -3, 4, -1, 2, 1, -5, 4 ]
Output: 6
Explanation: [ 4, -1, 2, 1 ] has the largest sum = 6
```

#### Follow up

If you have figured out the O(*n*) solution, try coding another solution using the divide and conquer approach, which is more subtle.

#### Solution

```javascript
/**
 * assume the sub problem into max = nums[0:i], that comes with a easy solution.
 * @param {Array} nums
 * @returns {Number}
 */
const maxSubArray = nums => {
  const length = nums.length;
  const dp = new Array(length);
  dp[0] = nums[0];
  let max = dp[0];
  for (let i = 0; i < length; i++) {
    dp[i] = nums[i] + (dp[i - 1] > 0 ? dp[i - 1] : 0);
    max = Math.max(max, dp[i]);
  }
  return max;
};
```

## Review

[Understanding Null and Undefined in JavaScript - Bits and Pieces](https://blog.bitsrc.io/understanding-null-and-undefined-in-javascript-77ceb44cf7db)

`null` is an assigned value, it must be explicitly assigned by the programmer.

I think there’s some cases where we might get `null`, like getting localStorage key that is not exist will return null, or `String.match()` might return null as well.

The other thing: instead of `if (!ab && typeof ab == ‘object’)` why no doing `if (ab === null)` ?

## Technique

### Hover underline animation

#### [Check me out](https://codepen.io/charleserious/pen/VwZgrvo)

```css
html, body {
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
}

body {
  display: flex;
  align-items: center;
  justify-content: center;
}

.hover-underline-animation {
  display: inline-block;
  position: relative;
  color: #0087ca;
}

.hover-underline-animation::after {
  content: '';
  position: absolute;
  width: 100%;
  transform: scaleX(0);
  height: 2px;
  bottom: 0;
  left: 0;
  background-color: #0087ca;
  transform-origin: bottom right;
  transition: transform 0.25s ease-out;
}

.hover-underline-animation:hover::after {
  transform: scaleX(1);
  transform-origin: bottom left;
}
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <link rel="stylesheet" href="./main.css">
  <title>Hover underline animation</title>
</head>
<body>
  <p class="hover-underline-animation">Hover this text to see the effect!</p>
</body>
</html>
```

#### Explanation

1. `display: inline-block` makes the block `p` an `inline-block` to prevent to underline from spanning the entire parent width rather than just the content (text).
2. `position: relative` on the element establishes a Cartesian position context for pseudo-elements.
3. `::after` defines a pseudo-element.
4. `position: absolute` takes the pseudo element out of the flow of the document and positions it in relation to the parent.
5. `width: 100%` ensures the pseudo-element spans the entire width of the text block.
6. `transform: scaleX(0)` initially scales the pseudo element to 0 so it has no width and is not visible.
7. `bottom: 0` and `left: 0` position it to the bottom left of the block.
8. `transition: transform 0.25s ease-out` means changes to `transform` will be transitioned over 0.25 seconds with an `ease-out` timing function.
9. `transform-origin: bottom right` means the transform anchor point is positioned at the bottom right of the block.
10. `:hover::after` then uses `scaleX(1)` to transition the width to 100%, then changes the `transform-origin` to bottom left so that the anchor point is reversed, allowing it transition out in the other direction when hovered off.

## Share

I wanna quit this job, but need to prepare for next interview.
