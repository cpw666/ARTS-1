# Week 37

## Algorithm

### [278. First Bad Version](https://leetcode.com/problems/first-bad-version/)

#### Description

You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have `n` versions `[1, 2, ..., n]` and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API `bool isBadVersion(version)` which will return whether `version` is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

#### Example

```example
Given n = 5, and version = 4 is the first bad version.

call isBadVersion(3) -> false
call isBadVersion(5) -> true
call isBadVersion(4) -> true

Then 4 is the first bad version.
```

#### Solution

```javascript
/**
 * @param {Number} version - version number
 * @returns {Boolean} - whether the version is bad
 */
// const isBadVersion = version => {};

/**
 * @param {Function} isBadVersion
 * @returns {Function}
 */
const solution = (isBadVersion) => {
  return n => {
    let start = 1;
    let end = n;
    while (start < end) {
      let mid = Math.floor(start + (end - start) / 2);
      if (isBadVersion(mid)) {
        end = mid; // look on left side of mid
      } else {
        start = mid + 1; // look on right side of mid
      }
    }
    return start;
  };
};
```

## Review

 [https://levelup.gitconnected.com/how-to-use-mixins-in-vuejs-a40cc3fb4428](https://levelup.gitconnected.com/how-to-use-mixins-in-vuejs-a40cc3fb4428) 

Mixins considered harmful, it introduce implicit dependencies, it causes name clashes, it causes snowballing complexity. When these three problems begin bother you, switch to High Order Component.

## Technique

### Height transition

[Check me out](https://codepen.io/charleserious/pen/xxKjbPb)

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

.el {
  transition: max-height 0.5s;
  overflow: hidden;
  max-height: 0;
}

.trigger:hover > .el {
  max-height: var(--max-height);
}
```

```javascript
(_ => {
  const el = document.querySelector('.el');
  const height = el.scrollHeight;
  el.style.setProperty('--max-height', `${height}px`);
})();
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <link rel="stylesheet" href="./main.css">
  <title>Height transition</title>
</head>
<body>
  <div class="trigger">
    Hover me to see a height transition
    <div class="el">content</div>
  </div>
</body>
<script src="./main.js"></script>
</html>
```

#### Explanation

1. `transition: max-height 0.5s cubic-bezier(...)` specifies that changes to `max-height` to be transitioned over 0.5 seconds, using an `ease-out-quint` timing function.
2. `over-flow: hidden` prevents the contents of the hidden element from overflowing its container.
3. `max-height: 0` specifies that the element has no height initially.
4. `.target:hover > .el` specifies that when the parent is hovered over, target a child `.el` within it and use the `--max-height` variable which was defined by JavaScript.
5. `el.scrollHeight` is the height of the element including overflow, which will change dynamically based on the content of element.
6. `el.style.setProperty(...)` sets the `--max-height` CSS variable which is used to specify the `max-height` of the element the target is hovered over, allowing to transition smoothly from 0 to auto.

## Share
Engineer who solve a problem independently is the entry(No. 5) level engineer. Teach and lead college solve problems is the No. 4 level engineer. Design and invent a product and achieve success in the market is the No. 3 level engineer. Create a product from vacuum is the No. 2 level engineer. Create an industry is the No. 1 level engineer.
Go pick up your goal.