# Week 40

## Algorithm
### [198. House Robber](https://leetcode.com/problems/house-robber/)

#### Description

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

#### Example 1

```example
Input: [1, 2, 3, 1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3). Total amount you can rob = 1 + 3 = 4.
```

#### Example 2

```example
Input: [2, 7, 9, 3, 1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1). Total amount you can rob = 2 + 9 + 1 = 12.
```

#### Solution

Recursive `top-down`

```javascript
const rob = nums => {
  const memo = Array.from({ length: nums.length - 1 }, x => -1);
  const worker = (nums, i, memo) => {
    if (i < 0) return 0;
    if (memo[i] >= 0) return memo[i];
    const max = Math.max(worker(nums, i - 2, memo) + nums[i], worker(nums, i - 1, memo));
    memo[i] = max;
    return max;
  }
  return worker(nums, nums.length - 1, memo);
};
```

## Review

[Make your code easier to read with Functional Programming](https://www.freecodecamp.org/news/make-your-code-easier-to-read-with-functional-programming-94fb8cc69f9d/)

Pure functions are easier to read and reason about.

Functional Programming will break list operations in steps like: filter, map, reduce, sort. At the same time, it will require to define new pure small functions to support those operations.

Combining Functional Programming with the practice of giving intention revealing names greatly improves the readability of the code.

## Technique

### Disable selection

#### [Check me out](https://codepen.io/pen/?editors=1100#0)

```css
html, body {
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
}

body {
  display: flex;
  flex-flow: column nowrap;
  align-items: center;
  justify-content: center;
}

.unselectable {
  user-select: none;
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
  <title>Disable selection</title>
</head>
<body>
  <p>You can select me.</p>
  <p class="unselectable">You can't select me.</p>
</body>
</html>
```

#### Explanation

- `user-select: none` specifies that the text cannot be selected.

## Share

Work for the job you like, don’t work only for money, think about the sociality, think about your family, don’t do evil.
