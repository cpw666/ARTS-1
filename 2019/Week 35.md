# Week 35

## Algorithm

### [108. Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)

#### Description

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of *every* node never differ by more than 1.

#### Example

```example
Given the sorted array: [-10, -3, 0, 5, 9]
One possible answer is: [0, -3, 9, -10, null, 5]
    0
   / \
  -3  9
  /  /
-10 5
```

#### Solution

```javascript
function TreeNode (val) {
  this.val = val;
  this.left = this.right = null;
}

/**
 * @param {Array} nums
 * @returns {TreeNode}
 */
const sortedArrayToBST = nums => {
  const helper = (nums, low, high) => {
    if (low > high) return null;
    const mid = Math.floor((low + high) / 2);
    const node = new TreeNode(nums[mid]);
    node.left = helper(nums, low, mid - 1);
    node.right = helper(nums, mid + 1, high);
    return node;
  };

  if (nums.length === 0) return null;
  const head = helper(nums, 0, nums.length - 1);
  return head;
}

const sa = [-10, -3, 0, 5, 9];
const head = sortedArrayToBST(sa);
/**
 * {
 *  "val": 0,
 *  "right": {
 *    "val": 5,
 *    "right": {
 *      "val": 9,
 *      "right": null,
 *      "left": null
 *    },
 *  "left": null
 *  },
 *  "left": {
 *    "val": -10,
 *    "right": {
 *      "val": -3,
 *      "right": null,
 *      "left": null
 *    },
 *  "left": null
 *  }
 * }
 */
console.log(JSON.stringify(head));
```

## Review

[The TypeScript Tax - JavaScript Scene - Medium](https://medium.com/javascript-scene/the-typescript-tax-132ff4cb175b)

I love a lot of things about TypeScript, and I’m still hopeful that it improves. Some of these cost concerns may be adequately addressed in the future by adding new features and improving documentation.

However, we shouldn’t brush these problems under the rug, and it’s irresponsible for developers to overstate the benefits of TypeScript without addressing the costs.

TypeScript can and should get better at type inference, higher order function, and generics. The TypeScript team also has a huge opportunity to improve documentation, including tutorials, videos, best practices, and an easy-to-find rundown of TypeScript’s limitations, which will help TypeScript developers save a lot of time and significantly reduce the costs of using TypeScript.

I’m hopeful that as TypeScript continues to grow, more of its users will get past the honeymoon phase and realize its costs and current limitations.

The conclusion is ironic because the TypeScript tagline is “JavaScript that Scales”. A more honest tagline might add a word: “JavaScript that Scales awkwardly.”

## Technique

### Donut spinner

[Check me out](https://codepen.io/charleserious/pen/jONmvXx)

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

@keyframes donut-spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.donut {
  display: inline-block;
  border: 4px solid rgba(0, 0, 0, 0.1);
  border-left-color: #7983ff;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  animation: donut-spin 1.2s linear infinite;
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
  <title>Donut spinner</title>
</head>
<body>
  <div class="donut"></div>
</body>
</html>
```

#### Explanation

- Use a semi-transparent `border` for the whole element, except one side that will serve as the loading indicator for the donut. Use `animation` to rotate the element.

## Share

Take your chance, be a better developer.