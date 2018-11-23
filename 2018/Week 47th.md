# Week 47th
## Algorithm
### [669. Trim a Binary Search Tree](https://leetcode.com/problems/trim-a-binary-search-tree/description/)

#### Description
Given a binary search tree and the lowest and highest boundaries as `L` and `R`, trim the tree so that all its elements lies in `[L, R]` (R > L). You might need to change the root of the tree, so the result should return the new root of the trimmed binary search tree.

#### Example 1
```
Input:
	1
 / \
0		2

L = 1
R = 2

Output:
1
 \
  2
```

#### Example 2
```
Input:
	3
 / \
0		4
 \
  2
 /
1

L = 1
R = 3

Output:
		3
	 /
	2
 /
1
```

#### Solution
```javascript
class TreeNode {
	constructor (val) {
		this.val = val;
		this.left = this.right = null;
	}
}
/**
 * Trim the binary search tree with the given lowest and highest boundariesas `L` and `R`.
 * classical binary search usage
 * @param {TreeNode} root
 * @param {Number} L
 * @param {Number} R
 * @returns {TreeNode}
 */
const trimBST = (root, L, R) => {
	if (root === null) {
		return null;
	}
	if (root.val < L) {
		return trimBST(root.right, L, R);
	}
	if (root.val > R) {
		return trimBST(root.left, L, R);
	}

	root.left = trimBST(root.left, L, R);
	root.right = trimBST(root.right, L, R);
	return root;
};

const tree = new TreeNode(1);
tree.left = new TreeNode(0);
tree.right = new TreeNode(2);
const L = 1;
const R = 2;
const trimmed = trimBST(tree, L, R);
console.log(JSON.stringify(trimmed));
```


## Review
[Change And Its Detection In JavaScript Frameworks](https://teropa.info/blog/2015/03/02/change-and-its-detection-in-javascript-frameworks.html)  
Managing the synchronization of app state and the user interface has long been a major source of complexity in UI development, and by now we have serval different approaches to dealing with it.  
	- Ember.js: Data Binding way
	- AngularJS: Dirty Checking way
	- React: Virtual Dom way
	- VueJS: Data Accessors way
all by conclusion with Immutable Data Structures.
I pretty like the VueJS Data Accessors way, its elegant, and maybe very efficient.


## Technique
Little JavaScript technique.  
```javascript
/**
 * Returns every nth element in the array.
 * Use `Array.prototype.filter()` to create a new array that contains every nth element of a given array.
 * @param {Array} arr
 * @param {Number} nth
 * @returns {Array}
 */
const everyNth = (arr, nth) => arr.filter((e, i) => i % nth === nth - 1);
```

## Share
Web components allow us to architect and import custom elements that automatically associate JS behavior with templates and utilize shadow DOM to provide CSS scoping and DOM encapsulation.

Web components consist of a set of web platform APIs. There are libraries (such as Polymer) and polyfills (such as webcomponents.js) to bridge the gap between current browser support and future web API support.

I think componentity is the future of Web UI interface and most important for productive.
