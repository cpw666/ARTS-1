# Week 38

## Algorithm

### [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)

#### Description

You are climbing a stair case. It takes *n* steps to reach to the top.

Each time you can either climb 1 or 20 steps. In how many distinct ways can you climb to the top?

#### Note

Given *n* will be a positive integer.

#### Example 1

```example
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

#### Example 2

```example
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1: 1 step + 1 step + 1 step
2: 1 step + 2 steps
3: 2 steps + 1 step
```

#### Solution Brutal Recursion

```javascript
/**
 *
 * @param {Number} n
 * @returns {Number}
 */
const climbStairs = n => {
  if (n === 1) return 1;
  if (n === 2) return 2;
  return climbStairs(n - 1) + climbStairs(n - 2);
};
```

#### Solution Recursion with O(N)

```javascript
const climbStairs = n => {
  const dp = (n, result) => {
    if (result[n] === -1) {
      result[n] = dp(n - 1, result) + dp(n - 2, result);
    }
    return result[n];
  }
  if (n === 1) return 1;
  const result = Array.from(new Array(n), (_, i) => i < 2 ? i + 1 : -1);
  return dp(n - 1, result);
};
```

## Review
 [Great developers never stop learning](https://towardsdatascience.com/great-developers-never-stop-learning-77b9ce867eac) 

We often fail to understand that our career is no longer the end product of out education, but itself is an education for us! If we keep the learning habit, we are likely to extend our longevity and improve our employability. Another common pitfall is using time as an excuse for not adopting continuous learning. We all have time! In fact, we all have exactly the same amount of time. **The difference is how we choose to spend it!**

## Technique

### Hover shadow box animation

[Check me out](https://codepen.io/pen/)

#### Sample

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

.hover-shadow-box-animation {
  display: inline-block;
  vertical-align: middle;
  transform: perspective(1px) translateZ(0);
  box-shadow: 0 0 1px transparent;
  margin: 10px;
  transition-duration: 0.3s;
  transition-property: box-shadow, transform;
}

.hover-shadow-box-animation:hover,
.hover-shadow-box-animation:focus,
.hover-shadow-box-animation:active {
  box-shadow: 1px 10px 10px -10px rgba(0, 0, 24, 0.5);
  transform: scale(1.2);
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
  <title>Hover shadow box animation</title>
</head>
<body>
  <p class="hover-shadow-box-animation">Box it!</p>
</body>
</html>
```

#### Explanation

1. `display: inline-block` to set width and length for `p` element thus making it an `inline-block`.
2. Set `transform: perspective(1px)` to give element a 3D space by affecting the distance between the Z plane and the user and `translateZ(0)` to reposition the `p` element along z-axis in 3D space.
3. `box-shadow` to set up the box.
4. `transparent` to make box transparent.
5. `transition-property` to enable transitions for both `box-shadow` and `transform`.
6. `:hover` to activate whole css when hovering is done until `active`.
7. `transform: scale(1.2)` to change the scale, magnifying the text.

## Share

Too much time wasted for the day work, urging to learn timing balance technique.