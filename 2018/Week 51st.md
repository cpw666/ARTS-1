# Week 51st
## Algorithm

### [101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/description/)

#### Description

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).  

For example, this binary tree `[1, 2, 2, 3, 4, 4, 3]` is symmetric:

```javascript
      1
    /   \
   2     2
  / \   / \
 3   4 4   3
```

But the following `[1, 2, 2, null, 3, null, 3]` is not:

```javascript
      1
    /   \
   2     2
    \     \
     3     3
```

Note:
Bonus points if you could solve it both recursively and iteratively.

#### Solution Recursively

```javascript
function TreeNode (val) {
  this.val = val;
  this.left = this.right = null;
}

/**
 * Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).  
 *
 * For example, this binary tree `[1, 2, 2, 3, 4, 4, 3]` is symmetric:
 *
 * ```javascript
 *      1
 *    /   \
 *   2     2
 *  / \   / \
 * 3   4 4   3
 * ```
 *
 * But the following `[1, 2, 2, null, 3, null, 3]` is not:
 *
 * ```javascript
 *     1
 *   /   \
 *  2     2
 *   \     \
 *    3     3
 * ```
 *
 * @param {TreeNode} root
 * @returns {Boolean}
 */
const isSymmetric = (root) => {
  if (root === null || root.val === null) return true;
  const is = recursively(root.left, root.right);
  return is;
};

const recursively = (left, right) => {
  if (!left && !right) return true;
  if (!left || !right) return false;
  if (left.val !== right.val) return false;
  return recursively(left.left, right.right) && recursively(left.right, right.left);
};

const tree = new TreeNode(1);
tree.left = new TreeNode(2);
tree.left.left = new TreeNode(3);
tree.left.right = new TreeNode(4);
tree.right = new TreeNode(2);
tree.right.left = new TreeNode(4);
tree.right.right = new TreeNode(3);

const symmetricly = isSymmetric(tree);
console.log(symmetricly);
```

#### Solution Iteratively

```javascript
const isSymmetricIteratively = (root) => {
  if (root === null || root.val === null) return true;
  const is = iteratively(root, []);
  return is;
};

const iteratively = (tree, queue) => {
  queue.push(tree.left);
  queue.push(tree.right);
  while (queue.length > 0) {
    const left = queue.shift();
    const right = queue.shift();
    if (!left && !right) continue;
    if (!left || !right) return false;
    if (left.val !== right.val) return false;
    queue.push(left.left);
    queue.push(right.right);
    queue.push(left.right);
    queue.push(right.left);
  }
  return true;
};

const itree = new TreeNode(9);
itree.left = new TreeNode(-42);
itree.right = new TreeNode(-42);
itree.left.right = new TreeNode(76);
itree.right.left = new TreeNode(76);
itree.left.right.right = new TreeNode(13);
itree.right.left.right = new TreeNode(13);
const itSymmetricly = isSymmetricIteratively(itree);
console.log(itSymmetricly);
```

## Review

[Functional Mixins – JavaScript Scene – Medium](https://medium.com/javascript-scene/functional-mixins-composing-software-ffb66d5e731c)  

Functional mixing are compassable factory functions which add properties and behaviors to objects like station in an assembly line. They are a great way to compose behaviors from multiple source features (**has-a**, **use-a**, **can-do**), as opposed to inheriting all the features of a given class (**is-a**).  

Be aware, “functional mixing” doesn’t imply “functional programming” — it simply means “mixing using functions”. Functional mixing can be written using a functional programming style, avoiding side-effects and preserving referential transparency, but that is not guaranteed. There may be side-effects and nondeterminism in third-party mixing.  
  
Anyway try [Stamp](https://stampit.js.org/), you gonna love it.
  

## Technique

Array remove.
```javascript
/**
 * Removes elements from an array for which the given function returns `false`.
 * Use `Array.prototype.filter()` to find array elements that return truthy values 
 * and `Array.prototype.reduce()` to remove elements using `Array.prorotype.splice()`.
 * The `func` is invoked with three arguments (`value`, `index`, `array`).
 * @param {Array} arr
 * @param {Function} func
 * @returns {Array}
 */
const remove = (arr, func) =>
  Array.isArray(arr)
    ? arr.filter(func).reduce((acc, val) => {
      arr.splice(arr.indexOf(val), 1);
      return acc.concat(val);
    }, [])
    : [];

const rest = remove([1, 2, 3, 4], n => n % 2 === 0);
console.log(JSON.stringify(rest));    // [2,4]
```


## Share

Publish-subscribe pattern.  

> In software architecture, **publish-subscribe** is a messaging pattern where senders of messages, called publishers, do not program the messages to be sent directly to specific receivers, called subscribers, but instead categorize published messages into class without knowledge of which subscribers, if any, there may be. Similarly, subscribers express interest in one or more classes and only receive messages that are of interest, without knowledge of which publishers, if any, there are.  

Quote from [Publish–subscribe pattern - Wikipedia](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern)  

And hell yeah, [Vue Custom Events — Vue.js](https://vuejs.org/v2/guide/components-custom-events.html)is kind of this approach.  

