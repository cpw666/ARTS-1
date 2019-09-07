# Week 36

## Algorithm

### [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)

#### Description

Given two sorted integer arrays *nums1* and *nums2*, merge *nums2* into *nums1* as one sorted array.

#### Note

- The number of elements initialized in *nums1* and *nums2* are *m* and *n* respectively.
- You may assume that *nums1* has enough space (size that is greater or equal to *m + n*) to hold additional elements from *nums2*

#### Example

```example
Input:
nums1 = [1, 2, 3, 0, 0, 0], m = 3
nums2 = [2, 5, 6]           n = 3
Output: [1, 2, 2, 3, 5, 6]
```

#### Solution

```javascript
/**
 * @param {Array} nums1
 * @param {Number} m
 * @param {Array} nums2
 * @param {Number} n
 * @returns {Array}
 */
const merge = (nums1, m, nums2, n) => {
  let i = m - 1;
  let j = n - 1;
  let k = m + n - 1; // calculate the index of the last element of the merged array
  // go from the back by `nums1` and `nums2` and compare and put to `nums1` element which is larger
  while (i >= 0 && j >= 0) {
    if (nums1[i] >= nums2[j]) {
      nums1[k--] = nums1[i--];
    } else {
      nums1[k--] = nums2[j--];
    }
  }
  // if `nums2` is longer than `nums1` just copy rest of `nums2` into `nums1` location, otherwise no need to do anything
  while (j >= 0) {
    nums1[k--] = nums2[j--];
  }
};
```

## Review

[What exactly is functional programming? - ITNEXT](https://itnext.io/what-exactly-is-functional-programming-ea02c86753fd)

While this only covers the basics and basis of functional programming, it is not the final and definitive guide.

When learning FP, a lot of people get hit with the technicalities straight away rather than the ideology behind it. Functional programming is a pattern and way to write code that is not tied to a set procedure that can cause errors if something blips out. Once understood properly, functional patterns can be applied inside object oriented patterns.

Topics in functional programming that needs further discussion includes and is not limited to are immutability, observation, referential transparency, first-class entities, higher order function, filters, map, and reduce, maybe, either, monad are a few of the many thins. 

## Technique

### Easing variables

[Check me out](https://codepen.io/charleserious/pen/dybVJYe)

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

:root {
  /* Place variables in here to use globally */
}

.easing-variables {
  --ease-in-quad: cubic-bezier(0.55, 0.085, 0.68, 0.53);
  --ease-in-cubic: cubic-bezier(0.55, 0.055, 0.675, 0.19);
  --ease-in-quart: cubic-bezier(0.895, 0.03, 0.685, 0.22);
  --ease-in-quint: cubic-bezier(0.755, 0.05, 0.855, 0.06);
  --ease-in-expo: cubic-bezier(0.95, 0.05, 0.795, 0.035);
  --ease-in-circ: cubic-bezier(0.6, 0.04, 0.98, 0.335);

  --ease-out-quad: cubic-bezier(0.25, 0.46, 0.45, 0.94);
  --ease-out-cubic: cubic-bezier(0.215, 0.61, 0.355, 1);
  --ease-out-quart: cubic-bezier(0.165, 0.84, 0.44, 1);
  --ease-out-quint: cubic-bezier(0.23, 1, 0.32, 1);
  --ease-out-expo: cubic-bezier(0.19, 1, 0.22, 1);
  --ease-out-circ: cubic-bezier(0.075, 0.82, 0.165, 1);

  --ease-in-out-quad: cubic-bezier(0.455, 0.03, 0.515, 0.955);
  --ease-in-out-cubic: cubic-bezier(0.645, 0.045, 0.355, 1);
  --ease-in-out-quart: cubic-bezier(0.77, 0, 0.175, 1);
  --ease-in-out-quint: cubic-bezier(0.86, 0, 0.07, 1);
  --ease-in-out-expo: cubic-bezier(1, 0, 0, 1);
  --ease-in-out-circ: cubic-bezier(0.785, 0.135, 0.15, 0.86);

  display: flex;
  align-items: center;
  justify-content: center;
  width: 75px;
  height: 75px;
  padding: 10px;
  color: white;
  background-color: #333;
  transition: transform 1s var(--ease-out-quart);
}

.easing-variables:hover {
  transform: rotate(45deg);
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
  <title>Easing variables</title>
</head>
<body>
  <div class="easing-variables">Hover</div>
</body>
</html>
```

#### Explanation

- The variables are defined globally with the `:root` CSS pseudo-class which matches the root element of a tree representing the document.
- In HTML, `:root` represents the `<html>` element and is identical to the selector `html`, except that its specificity is higher.

## Share

Knowledge make you  strong,  make you smart, make you wise.