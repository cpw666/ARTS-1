# Week 52nd
## Algorithm

### [112. Path Sum](https://leetcode.com/problems/path-sum/description/)

#### Description

Given a binary tree and a sum, determine if tree has a root-to-leaf path such thad adding up all the values along the path equals the given sum.

#### Note

A leaf is a node with no children.

#### Example

Given the below binary tree and `sum = 22`,

```javascript
        5
      /   \
     4     8
    /     / \
   11    13  4
  / \         \
 7   2         1
```

return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.

#### Solution

```javascript
function TreeNode (val) {
  this.val = val;
  this.left = this.right = null;
}

const hasPathSum = (root, sum) => {
  if (!root) return false;
  if (!root.left && !root.right) return !(sum - root.val);
  return hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val);
};

// const tree = new TreeNode(5);
// tree.left = new TreeNode(4);
// tree.left.left = new TreeNode(11);
// tree.left.left.left = new TreeNode(7);
// tree.left.left.right = new TreeNode(2);
// tree.right = new TreeNode(8);
// tree.right.left = new TreeNode(13);
// tree.right.right = new TreeNode(4);
// tree.right.right.right = new TreeNode(1);

// const has = hasPathSum(tree, 22);
const tree = new TreeNode(0);
tree.left = new TreeNode(1);
tree.right = new TreeNode(1);
const has = hasPathSum(tree, 1);
console.log(has);
```


## Review

[Mocking is a Code Smell – JavaScript Scene – Medium](https://medium.com/javascript-scene/mocking-is-a-code-smell-944a70c90a6a)  

Unit test for functional programming may be the wrong answer, because the essence of software engineering is to break down a big problem into small pieces solutions and assemble these pieces solutions into a whole solution to solve the problem, and functional paradigm strictly obey this rule with no side effect, we assemble pieces of pure functions into a giant solution.  

But integration test still has its duty.

## Technique

Array Unique Elements By passing function

```javascript
/**
 * Returns all unique values of an array, based on a provided comparator function.
 * Use `Array.prototype.reduce()` and `Array.prototype.some()` for an array containing only the first unique occurence of each value,
 * based on the comparator function, `fn`. The comparator function takes two arguments: the values of the elements being compared.
 * @param {Array} arr
 * @param {Function} fn
 * @returns {Array}
 */
const uniqueElementsBy = (arr, fn) =>
  arr.reduce((acc, v) => {
    !acc.some(x => fn(v, x)) && acc.push(v);
    return acc;
  }, []);


const array = [
  { id: 0, value: 'a' },
  { id: 1, value: 'b' },
  { id: 2, value: 'c' },
  { id: 1, value: 'd' },
  { id: 0, value: 'e' },
];

const comparator = (a, b) => a.id === b.id;

const ub = uniqueElementsBy(array, comparator);

console.log(JSON.stringify(ub));  // [{"id":0,"value":"a"},{"id":1,"value":"b"},{"id":2,"value":"c"}]
```

## Share
> “OOP to me means only messaging, local retention and protection and hiding of state-process, and extreme late-binding of all things.”  
> — Alan Kay (inventor of Smalltalk)  

In other words, according to Alan Kay, the essential ingredients of OOP are: 
1. Message passing
2. Encapsulation
3. Dynamic binding
