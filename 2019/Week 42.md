# Week 42

## Algorithm

### [155. Min Stack](https://leetcode.com/problems/min-stack/)

#### Description

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

- push(x) — Push element x onto stack.
- pop() — Removes the element on top of the stack.
- top() — Get the top element.
- getMin() — Retrieve the minimum element in the stack.

#### Example

```java
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); --> return -3;
minStack.pop();
minStack.top(); --> return 0.
minStack.getMin(); --> return -2;
```

#### Solution

```javascript
/**
 * initialize your data structure here.
 */
const MinStack = function () {
  this.stack = [];
  this.minimum = null;
};

/**
 * @returns {undefined}
 */
MinStack.prototype.min = function () {
  this.minimum = Math.min(…this.stack);
};

/**
 * @param {Number} x
 * @returns {undefined}
 */
MinStack.prototype.push = function (x) {
  this.stack.unshift(x);
  this.min();
};

/**
 * @returns {undefined}
 */
MinStack.prototype.pop = function () {
  this.stack.shift();
  this.min();
};

/**
 * @returns {Number}
 */
MinStack.prototype.top = function () {
  return this.stack[0];
};

/**
 * @returns {Number}
 */
MinStack.prototype.getMin = function () {
  return this.minimum;
};

const minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // —> Returns -3.
minStack.pop();
minStack.top(); // —> Returns 0.
minStack.getMin(); // —> Returns -2.
```


## Review

[High-performance array transformations - codeburst](https://codeburst.io/high-performance-array-transformations-68aae138a5f2)

Creating intermediate data structures, especially large ones, is almost always going to result in severe punishment. **Garbage collection may not look like much, but if it happens often enough, it just makes everything very slow.**

**Don’t get to hung up on what the code looks like.** You can always use comments to make it look better. (Or, you could try to come up with iterator-based solution that does not use generators as suggested by one of the commenters.)


## Technique

### Hamburger Button

#### [Check me out](https://codepen.io/charleserious/pen/MWWKdEY)

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

.hb,
.hb:before,
.hb:after {
  position: relative;
  width: 30px;
  height: 5px;
  border: none;
  outline: none;
  background-color: #333;
  border-radius: 3px;
  transition: 0.5s;
  cursor: pointer;
}

.hb:before,
.hb:after {
  content: '';
  position: absolute;
  left: 0;
}

.hb:before {
  top: -7.5px;
}

.hb:after {
  top: 7.5px;
}

.hb:hover {
  background-color: transparent;
}

.hb:hover:before,
.hb:hover:after {
  top: 0;
}

.hb:hover:before {
  transform: rotate(45deg)
}

.hb:hover:after {
  transform: rotate(-45deg)
}
```

```html
<!DOCTYPE html>
<html lang=“en”>
<head>
  <meta charset=“UTF-8”>
  <meta name=“viewport” content=“width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <link rel="stylesheet" href="./main.css">
  <title>Hamburguer Button</title>
</head>
<body>
  <button class="hb"></button>
</body>
</html>
```

#### Explanation

- Use `<button>` element for the middle bar of the hamburger icon.
- Use the `:before` and `:after` pseudo-elements to create the top and bottom bars of the icon.
- Use `position: relative` on the `<button>` and `position: absolute` on the pseudo-elements to place them appropriately.
- Use the `:hover` pseudo-selector to rotate `:before` to `45deg` and `:after` to `-45deg` and hide the center bar using `background-color: transparent`.

## Share

Before you coding, draw the flowchart and the timing diagram for you program, then do the coding stuff, finally write your code a document. This will help the feature you understand easily