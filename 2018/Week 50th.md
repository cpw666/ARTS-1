# Week 50th
## Algorithm

### [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/description/)

#### Description

Given a binary tree, return the *level order* traversal of its nodes' value. (ie. from left to right, level by level).

For example:  
Given binary tree `[3, 9, 20, null, null, 15, 7]`,

```javascript
    3
    / \
  9   20
      /  \
    15   7
```

return its level order traversal as:

```javascript
[
 [3],
 [9, 20],
 [15, 7]
]
```

#### Solution

```javascript

function TreeNode (val) {
  this.val = val;
  this.left = this.right = null;
}

/**
 * Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).
 * For example:
 * Given binary tree [3, 9, 20, null, null 15, 7]
 *      3
 *     / \
 *    9   20
 *       /  \
 *      15   7
 * return its level order traversal as:
 * [
 *  [3],
 *  [9, 20],
 *  [15, 7]
 * ]
 * @param {TreeNode} root
 * @return {Array}
 */
const levelOrder = (root) => {
  const result = [];
  level(result, root, 0);
  return result;
};

const level = (result, root, height) => {
  if (!root || root.val === null) {
    return;
  }
  if (height >= result.length) {
    result.push([]);
  }
  result[height].push(root.val);
  level(result, root.left, height + 1);
  level(result, root.right, height + 1);
};

const tree = new TreeNode(3);
tree.left = new TreeNode(9);
tree.right = new TreeNode(20);
tree.right.left = new TreeNode(15);
tree.right.right = new TreeNode(7);
const levels = levelOrder(tree);
console.log(JSON.stringify(levels));
```

## Review

[Reduce (Composing Software) – JavaScript Scene – Medium](https://medium.com/javascript-scene/reduce-composing-software-fe22f0c39a1d)

> Fold (aka: reduce, accumulate, aggregate, compress, or inject) refers to a family of higher-order functions that analyze a recursive data structure and though use of a given combining operation, recombine the results of recursively processing its constituent parts, building up a return value. Typically, a fold is presented with a combining function, a top node of data structure, and possibly some default values to e used under certain conditions. The fold then proceeds to combine elements of the data structure’s hierarchy, using the function in a systematic way.  

Quote from [Wikipedia](https://en.wikipedia.org/wiki/Fold_\(higher-order_function\))

Reduce is versatile, It’s easy to define `map()`, `filter()` and lot’s of other interesting things using reduce:

Map
```javascript
const map = (fn, arr) => arr.reduce((newArray, item, index, arr) => {
  return newArray.concat([fn(item, index, arr)]);
}, []);
```

Filter
```javascript
const filter = (fn, arr) => arr.reduce((newArray, item, index, arr) => {
  return fn(item, index, arr) ? newArray.concat([item]) : newArray;
}, []);
```

Compose
```javascript
const compose = (...fns) => x => fns.reduceRight((v, f) => f(v), x);

const add1 = n => n + 1;
const double = n => n * 2;

const add1ThenDouble = compose(double, add1);

const result = add1ThenDouble(2);
console.log(result);  // 6
```

pipe
```javascript
const pipe = (...fns) => x => fns.reduce((v, f) => f(v), x);

const add1 = n => n + 1;
const double = n => n * 2;

const add1ThenDouble = pipe(add1, double);
const result = add1ThenDouble(2);
console.log(result);  // 6

const doubleThenAdd1 = pipe(double, add1);
const dresult = doubleThenAdd1(2);
console.log(dresult); // 5
```

badass curriedPipe
```javascript
const curiedPipe = val => {
  const pipe = (...fns) => {
    const piped = (...args) => (args[0]) ? pipe(...fns, ...args) : fns.reduce((x, fn) => fn(x), val);
    return (fns[0]) ? piped : val;
  }
  return pipe;
};

const doubleThenPlus1 = curiedPipe(42)(x => x * 2)(x => x + 1)(x => x / 2)();
console.log(doubleThenPlus1); // 42.5
```

Given me an array and reducer, and I shall do everything.  

## Technique

We have `Array.prototype.filter()` , and we wanna `reject` too
```javascript
/**
 * Takes a predicate and array, like `Array.prototype.filter()`, but only keeps `x` if `pred(x) === false`.
 * @param {Function} pred
 * @param {Array} array
 * @returns {Array}
 */
const reject = (pred, array) => array.filter((...args) => !pred(...args));

// test
const numberic = reject(x => x % 2 === 0, [1, 2, 3, 4, 5]);
const stringify = reject(word => word.length > 4, ['Apple', 'Pear', 'Kiwi', 'Banana']);
console.log(JSON.stringify(numberic));  // [1,3,5]
console.log(JSON.stringify(stringify)); // ["Pear","Kiwi"]
```

## Share

Functors.  

> A functor data type is something you can map over. It’s a container which has an interface which can be used to apply a function to the values inside it. When you see a functor, you should think “mappable”. Functor types are typically represented as an object with a `.map()`method that maps from inputs to outputs while preserving structure. In practice, “preserving structure” means that the return is the same type of functor (though values inside the container may be a different type).  

Quote from [Functors & Categories – JavaScript Scene – Medium](https://medium.com/javascript-scene/functors-categories-61e031bac53f)

Big Thanks to [Eric Elliott – Medium](https://medium.com/@_ericelliott?source=post_header_lockup)

