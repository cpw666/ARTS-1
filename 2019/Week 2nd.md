# Week 2nd
## Algorithm

### [543. Diameter of Binary tree](https://leetcode.com/problems/diameter-of-binary-tree/)

#### Description

Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the **longest** path between any two nodes in a tree. This path may or may not pass through the root.

#### Example

```javascript
    1
   / \
  2   3
 / \
4   5
```

Returns **3**, which is the length of the path [4, 2, 1, 3] or [5, 2, 1, 3].

#### Note

The length of path between two nodes is represented by the number of edges between them.

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
 * Givan a binary tree, you need to compute the length of the diameter of the tree. 
 * The diameter of a binary tree is the length of the **longest** path between any two nodes in a tree. 
 * This path may or may not pass through the root.
 * @param {TreeNode} root
 * @returns {Number}
 */
const diameterOfBinaryTree = (root) => {
  if (!root) return 0;
  let diameter = 0;
  const depth = (root) => {
    if (root.left === null || root.right === null) return 0;
    let leftDepth = 0;
    let rightDepth = 0;
    if (root.left !== null) leftDepth = 1 + depth(root.left);
    if (root.right !== null) rightDepth = 1 + depth(root.right);
    diameter = Math.max(diameter, leftDepth + rightDepth);
    return Math.max(leftDepth, rightDepth);
  }
  depth(root);
  return diameter;
}

const tree = new TreeNode(1);
tree.left = new TreeNode(2);
tree.right = new TreeNode(3);
tree.left.left = new TreeNode(4);
tree.left.right = new TreeNode(5);

const diameter = diameterOfBinaryTree(tree);
console.log(diameter);
```

## Review

[Nested Ternaries are Great – JavaScript Scene – Medium](https://medium.com/javascript-scene/nested-ternaries-are-great-361bddd0f340)  

My beloved greatest nested ternaries.  

The most elegant, purest, and least memory lack style ever.  

F🖕K you all divergents.  

## Technique

Show off, factorial in functional style, and yes with my beloved greatest nested ternaries.

```javascript
/**
 * Caculates the factorial of a number.
 * 
 * Use recursion. If `n` is less than or equal to `1`, return `1`.
 * Otherwise, return the product of `n` and the factorial of `n - 1`.
 * Throws an exception if `n` is a negative number.
 * @param {Number} n
 * @returns {Number}
 */
const factorial = n =>
  n < 0
    ? (() => {
      throw new TypeError('Negative numbers are not allowed')
    })()
    : n <= 1
      ? 1
      : n * factorial(n - 1);


const six = factorial(6);
console.log(six); // 720
```

## Share

> In computer science, a mutator method is a method used to control changes to a variable. The are also known as **setter** methods. Often a setter is accompanied by a **getter** (also known as an *accessor*), which returns the value of the private variable.  
> The mutator method is most often used in object-oriented programming, in keeping with the principle of encapsulation. According to this principle, member variables of a class are med private to hide and protect them from other code, and can only be modified by a public member function (the mutator method), which takes the desired new value as a parameter, optionally validates it, and modifies the private member variable. Mutator methods can be compared to assignment operator overloading but they typically appear at different levels of the object hierarchy.  
> Mutator methods may also be used in non-object-oriented enviroments. In this case, a reference to the variable to be modified is passed to a mutator, along with the new value. In this scenario, the compiler cannot restrict code from bypassing the mutator method and changing the variable directly. The onus falls to the developers to ensure the variable is only modified through the mutator method and not modified directly.  

— Quote from [Mutator method - Wikipedia](https://en.wikipedia.org/wiki/Mutator_method)
