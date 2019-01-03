# Week 1st
## Algorithm

### [563. Binary Tree Tilt](https://leetcode.com/problems/binary-tree-tilt/)

#### Description

Given a binary tree, return the tilt of the **whole tree**.  

The tilt of a **tree node** is defined as the **absolute difference** between the sum of all left subtree node values and the sum of all right subtree node values. Null node has tilt 0.  

The tilt of the **whole tree** is defined as the sum of all nodes' tilt.

#### Example

```javascirpt
Input:
    1
   / \
  2   3

Output: 1
Explanation:
Tilt of node 2 : 0
Tilt of node 3 : 0
Tilt of node 1 : |2-3| = 1
TIlt of binary tree : 0 + 0 + 1 = 1
```

#### Note

1. The sum of node values in any subtree won't exceed the range of 32-bit integer.
2. All the tilt values won't exceed the range of 32-bit integer.

#### Solution

```javascript
/**
 * Definition for a binary tree node.
 * @param {Number} val 
 */
function TreeNode (val) {
  this.val = val;
  this.left = this.right = null;
}

/**
 * Given a binary tree, return the tilt of the **whole tree**.
 * The tilt of a **tree node** is defined as the **absolute difference** between the sum of all left subtree node values 
 * and the sum of all right subtree node values. Null node has tilt 0.
 * The tilt of the **whole tree** is defined as the sum of all nodes' tilt.
 * @param {TreeNode} root
 * @returns {Number}
 */
const findTilt = (root) => {
  let tilt = 0;
  (function postTraversal (root) {
    if (!root) return 0;
    const left = postTraversal(root.left);
    const right = postTraversal(root.right);
    tilt += Math.abs(left - right);
    return left + right + root.val;
  })(root);
  return tilt;
};

const tree = new TreeNode(1);
tree.left = new TreeNode(2);
tree.right = new TreeNode(3);
const tilt = findTilt(tree);
console.log(tilt);
```


## Review

[Elements of JavaScript Style – JavaScript Scene – Medium](https://medium.com/javascript-scene/elements-of-javascript-style-caa8821cb99f)  

In short:  
> The essence of software development is composition. We build applications by composing smaller modules, functions, and data structures.  

## Technique

Memoize with map:

```javascript
/**
 * Returns the memoized (cached) function.
 * 
 * Create an emptyy cache by instantiating a new `Map` object. Return a function which takes a single argument 
 * to be supplied to the memoized function by first checking if the function's output for that specific input value is already cached,
 * or store and return it if not. The `function` keyword must be used in order to allow the memoized function to have its `this` context changed if necessary.
 * Allow access to the `cache` by setting it as a property on the returned function.
 * @param {Function} fn
 * @returns {Function}
 */
const memoize = fn => {
  const cache = new Map();
  const cached = function (val) {
    return cache.has(val) ? cache.get(val) : cache.set(val, fn.call(this, val)) && cache.get(val);
  }
  cached.cache = cache;
  return cached;
}
```

## Share
> Any fool can write code that a computer can understand.  
> Good programmers write code that humans can understand.  
> — M. Fowler (1999)  

