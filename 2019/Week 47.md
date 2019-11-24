# Week 47

## Algorithm

### [118. Pascal’s Triangle](https://leetcode.com/problems/pascals-triangle/)

#### Description

Given a non-negative integer *numRows*, generate the first *numRows* of Pascal’s triangle.

![In Pascal’s Triangle, each number is the sum of the two numbers directly above it.](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

In Pascal’s Triangle, each number is the sum of the two numbers directly above it.

#### Example

```exampe
Input: 5
Output: [
       [ 1 ],
      [ 1, 1 ],
     [ 1, 2, 1 ],
    [ 1, 3, 3, 1 ],
   [ 1, 4, 6, 4, 1 ]
]
```

#### Solution

```javascript
const generate = numRows => {
  if (numRows === 0) return [];
  const result = [];
  for (let i = 0; i < numRows; i++) {
    let currRow = [];
    for (let j = 0; j <= i; j++) {
      if (j === 0 || j === i) {
        currRow.push(1);
      } else {
        currRow.push(result[i - 1][j - 1] + result[i - 1][j]);
      }
    }
    result.push(currRow);
  }
  return result;
};
```

## Review

[Master the JavaScript Interview: What is a Promise?](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-promise-27fc71e77261)

Promises have become an integral part of several idioms in JavaScript, including the [WHATWG Fetch](https://fetch.spec.whatwg.org/) standard used for most modern ajax requests, and the [Async Functions](https://tc39.github.io/ecmascript-asyncawait/) standard used to make asynchronous code to look synchronous.

Async functions are wildly used at the time of the writing.

For instance, if you’re using Redux, I suggest that you check out [redux-saga](https://github.com/redux-saga/redux-saga): A library used to manage side-effects in Redux which depends on async functions throughout the documentation.

I hope even experienced promise users have a better understanding of what promises are and how the work, and how to use them better after reading this Eric’s writing.

## Technique

### Constant width to height ratio

#### [Check me out](https://codepen.io/charleserious/pen/Rwwvvgr)

```html
<!DOCTYPE html>
<html lang=“en”>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <link rel="stylesheet" href="./main.css">
  <title>Constant width to height ratio</title>
</head>
<body>
  <div class="constant-width-to-height-ratio"></div>
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

.constant-width-to-height-ratio {
  background: #333;
  width: 50%;
}

.constant-width-to-height-ratio::before {
  content: '';
  padding-top: 100%;
  float: left;
}

.constant-width-to-height-ratio::after {
  content: '';
  display: block;
  clear: both;
}
```

#### Explanation

- `padding-top` on the `::before` pseudo-element causes the height of the element to equal a percentage ot its width. `100%` therefore means the element's height will always be `100%` of the width, creating a responsive square.
- This method also allows content to be placed inside the element normally

## Share

Learn the fundamental staff will help you understand the basic law of computation.