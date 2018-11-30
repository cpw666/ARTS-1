# Week 48th
## Algorithm

### [637. Average of Levels in Binary Tree](https://leetcode.com/problems/average-of-levels-in-binary-tree/description/)

#### Description  

Given a non-empty binary tree, return the average value of the nodes on each level in the form of an array.

#### Example

```code
Input:
  3
 / \
9  20
  /  \
 15   7

Output: [3, 14.5, 11]
Explanation:
The average value of nodes on level 0 is 3, on level 1 is 14.5, and on level 2 is 11. Hence return [3, 14.5, 11].
```

#### Note

1. The range of node's value is in the range of 32-bit signed integer

#### Solution

```javascript
class TreeNode {
  constructor (val) {
    this.val = val;
    this.left = this.right = null;
  }
}

/**
 * Calculate the average of each level in binary tree.
 * pre-order DFS usage.
 * @param {TreeNode} root
 * @param {Number} level
 * @param {Array} counts
 * @returns {Array}
 */
const averageOfLevels = (root, level = 0, counts = []) => {
  if (!root) {
    return [];
  }
  counts[level] = counts[level] || { sum: 0, nodes: 0 };
  counts[level].sum += root.val;
  counts[level].nodes++;
  averageOfLevels(root.left, level + 1, counts);
  averageOfLevels(root.right, level + 1, counts);
  return level || counts.map(count => count.sum / count.nodes);
};

const tree = new TreeNode(3);
tree.left = new TreeNode(9);
tree.right = new TreeNode(20);
tree.right.left = new TreeNode(15);
tree.right.right = new TreeNode(7);
const average = averageOfLevels(tree);
console.log(JSON.stringify(average));
```

## Review

[Composing Software: An Introduction – JavaScript Scene – Medium](https://medium.com/javascript-scene/composing-software-an-introduction-27b72500d6ea)  

When I was young, I read the Gang of Four, I was not sure about “Favor object composition over class inheritance” in book [Design Patterns: Elements of Reusable Object-Oriented Software](https://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612/ref=as_li_ss_tl?ie=UTF8&qid=1494993475&sr=8-1&keywords=design+patterns&linkCode=ll1&tag=eejs-20&linkId=6c553f16325f3939e5abadd4ee04e8b4). I didn’t have much experience of programming as productivity.  

Years later, trained by tons of business work flow and so much more dizzying requirements, I finally know what object composition is, and I may call it is one of  the best practices. In computer science, all Arrays, Sets, Maps, WeakMaps, TypedArrays, etc… are composite datatypes. Any time you bind any non-primitive data structure, you’re performing some kind of object composition.  

So object composition is a fundamental programming pattern. And of cause it is the most simple pattern to obey.  

## Technique

JavaScript Intersection with `Set`  
```javascript
/**
 * Returns a list of elements that exist in both arrays.
 * Create a `Set` from `b`, then use `Array.prototype.filter()` on `a` to only keep values contained in `b`.
 * @param {Array} a
 * @param {Array} b
 * @returns {Array}
 */
const intersection = (a, b) => {
  const s = new Set(b);
  return a.filter(x => s.has(x));
};
```

## Share

DON’T REPEAT YOURSELF.  
Some times it may be the evil rebellion, as you was tired, or not patient, etc…  
OR YOU’RE GOING TO EAT YOUR OWN DOG SHIT.  
