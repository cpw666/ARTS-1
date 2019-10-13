# Week 41

## Algorithm

### [384. Shuffle an Array](https://leetcode.com/problems/shuffle-an-array/)

#### Description

Shuffle a set of numbers without duplicates.

#### Example

```java
// Init an array with set 1, 2 and 3.
int [] nums = {1, 2, 3};
Solution solution = new Solution(nums);

// Shuffle the array [1, 2, 3] and return its result.
// Any permutation of [1, 2, 3] must equally likely to be returned.
solution.shuffle();

// Resets the array back to its original configuration [1, 2, 3].
solution.reset();

// Returns the random shuffling of array [1, 2, 3].
solution.shuffle();
```

#### Solution

```javascript
/**
 * @param {Array} nums
 */
const Solution = function (nums) {
  this.nums = nums;
};

/**
 * Resets the array to its original configuration and return it.
 * @returns {Array}
 */
Solution.prototype.reset = function () {
  return this.nums;
};

/**
 * Returns a random shuffling of the array.
 * @returns {Array}
 */
Solution.prototype.shuffle = function () {
  const copy = [ ...this.nums ];
  const border = copy.length;
  for (let i = 0; i < border; i++) {
    const j = Math.floor(i * Math.random());
    [copy[i], copy[j]] = [copy[j], copy[i]];
  }
  return copy;
};
```

## Review

[Functional JS #7: Point-free style - DailyJS - Medium](https://medium.com/dailyjs/functional-js-7-point-free-style-b21a1416ac6a)

Point-free style is a code-style choice and it’s not essential to make your code more functional. Understanding this concept, however, makes reading and discussing others code easier.

As with many things in life (and especially in programming), overusing it might introduce more problems than it solves, and you need to trust your intuition (and experience) on where the balance is.

Keep it reasonable and think twice if removing an explicit variable reference makes the code easier or harder to read. Use point-free style in moderation and make your code easier to read and follow.

## Technique

### Pulse loader

#### [Check me out](https://codepen.io/charleserious/pen/zYYrLaa)

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

.ripple-loader {
  position: relative;
  width: 64px;
  height: 64px;
}

.ripple-loader div {
  position: absolute;
  border: 4px solid #76ff03;
  border-radius: 50%;
  animation: ripple-loader 1s ease-out infinite;
}

.ripple-loader div:nth-child(2) {
  animation-delay: -0.5s;
}

@keyframes ripple-loader {
  0% {
    top: 32px;
    left: 32px;
    width: 0;
    height: 0;
    opacity: 1;
  }
  100% {
    top: 0;
    left: 0;
    width: 64px;
    height: 64px;
    opacity: 0;
  }
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
  <title>Pulse loader</title>
</head>
<body>
  <div class="ripple-loader">
    <div></div>
    <div></div>
  </div>
</body>
</html>
```

#### Explanation

- Use `@keyframes` to define an animation at two points in the cycle, start (0%), where two `<div>` elements have no `width` and `height` and are positioned at the center and end `(100%)` where both `<div>` elements have increased `width` and `height`, but their `position` is reset to `0`.
- Use `opacity` to transition from `1` to `0` when animating to give the `<div>` elements a disappearing effect as they expand.
- `.ripple-loader`, which is the parent container, has a predefined `width` and `height`. It uses `position: relative` to position its children.
- Use `animation-delay` on the second `<div>` element, so that each element starts its animation at a different time.

## Share

Don’t do anything before you got something prepared. Especially for a business trip.
