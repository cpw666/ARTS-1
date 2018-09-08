# Week 36th
## Algorithm
### (872. Leaf-Similar Trees)[https://leetcode.com/problems/leaf-similar-trees/description/]

#### Description
Consider all the leaves of a binary tree. From left to right order, the value of those leaves form a *leaf value sequence*
![Tree](http://pc97r6al4.bkt.clouddn.com/tree.png)

For example, in the given tree above, the leaf value sequence is `(6, 7, 4, 9, 8)`.  

Two binary trees are considered *leaf-similar* if their leaf value sequence is the same.  

Return `true` if and only if the two given trees with head nodes `root1` and `root2` are leaf-similar.  

#### Note
- Both of the given trees will have between `1` and `100` nodes. 

#### Solution 1
```javascript
/**
 * Definition for a binary tree node.
 */
class TreeNode {
	constructor (val) {
		this.val = val;
		this.left = this.right = val;
	}
}
/**
 * @param {TreeNode} root1
 * @param {TreeNode} root2
 * @returns {boolean}
 */
const leafSimilar = (root1, root2) => {
	const root1Leaves = [];
	const root2Leaves = [];
	leaves(root1, root1Leaves);
	leaves(root2, root2Leaves);
	const equality = JSON.stringify(root1Leaves) === JSON.stringify(root2Leaves);
	return equality;
};

/**
 * calc leaf nodes from a binary tree
 * @param {TreeNode} node
 * @param {Array} array
 */
const leaves = (node, array) => {
	if (!node.left && !node.right) {
		array.push(node.val);
	}
	if (node.left) {
		leaves(node.left, array);
	}
	if (node.right) {
		leaves(node.right, array);
	}
};

const root1 = [3, 5, 1, 6, 2, 9, 8, null, null, 7, 4];
const root2 = [3, 5, 1, 6, 7, 4, 2, null, null, null, null, null, null, 9, 8];
const similar = leafSimilar(root1, root2);
console.log(similar);
```

Since there is a recursive, it can be replace with dynamic programming.  

Solution 2 to be implemented.  

## Review
[How JavaScript works: tracking changes in the DOM using MutationObserver](https://blog.sessionstack.com/how-javascript-works-tracking-changes-in-the-dom-using-mutationobserver-86adc7446401)  

I have barely tried this API, this is awesome.  
 
Take a scenery as we are creating WYIWYG editor for web, undo and redo are the fundamental features as we frequently use during our daily writing.     

Once I implemented these two features with a `Stack ` data structure. This is a JavaScript Level implementation, and it consume the more computation than this browser level API(MutationObserver).  

MutationObserver built in with DOM changes, MutationRecord as a list of changes. We can use that as a full list of changes to implement the undo and redo.

Digging for more scenarios for MutationObserver suit.

## Technique
This week is about Binary Search Tree.  

Talk less, show me the code:  
```javascript
class Node {
	constructor (data, left, right) {
		this.data = data;
		this.left = left;
		this.right = right;
	}

	show () {
		return this.data;
	}
}

module.exports = Node;
```

```javascript
const Node = require('./Node');

class BinarySearchTree {
	constructor () {
		this.root = null;
	}

	insert (data) {
		const node = new Node(data, null, null);
		if (this.root === null) {
			this.root = node;
		} else {
			let current = this.root;
			let parent;
			while (true) {
				parent = current;
				if (data < current.data) {
					current = current.left;
					if (current === null) {
						parent.left = node;
						break;
					}
				} else {
					current = current.right;
					if (current === null) {
						parent.right = node;
						break;
					}
				}
			}
		}
	}

	inOrder (node) {
		if (node) {
			this.inOrder(node.left);
			console.log(node.show());
			this.inOrder(node.right);
		}
	}

	preOrder (node) {
		if (node) {
			console.log(node.show());
			this.preOrder(node.left);
			this.preOrder(node.right);
		}
	}

	postOrder (node) {
		if (node) {
			this.postOrder(node.left);
			this.postOrder(node.right);
			console.log(node.show());
		}
	}

	getMin () {
		let current = this.root;
		while (current.left) {
			current = current.left;
		}
		return current.data;
	}

	getMax () {
		let current = this.root;
		while (current.right) {
			current = current.right;
		}
		return current.data;
	}

	find (data) {
		let current = this.root;
		while (current.data !== data) {
			if (data < current.data) {
				current = current.left;
			} else {
				current = current.right;
			}
			if (current === null) {
				return null;
			}
		}
		return current;
	}

	smallest (node) {
		if (!node.left) {
			return node;
		} else {
			return this.smallest(node.left);
		}
	}

	removeNode (node, data) {
		if (!node) {
			return null;
		}
		if (data === node.data) {
			// node has no children
			if (!node.left && !node.right) {
				return null;
			}
			// node has no left child
			if (!node.left) {
				return node.right;
			}
			// node has no right child
			if (!node.right) {
				return node.left;
			}
			// node has two chindren
			const temp = this.smallest(node.right);
			node.data = temp.data;
			node.right = this.removeNode(node.left, data);
			return node;
		} else if (data < node.data) {
			node.left = this.removeNode(node.left, data);
			return node;
		} else {
			node.right = this.removeNode(node.right, data);
			return node;
		}
	}
}

module.exports = BinarySearchTree;
```

## Share
I’ve been coding for a few years, since I was 16 I picked this road to be my life through career, at that time I loved coding, loved to solve problems, loved to fix bugs.   

In past few years I lost myself, I spend too much time in business logic and  not trying to learn new stuff, always thought things need to be learned as it to be need.  

Last year after our first child came to life, I began to think what I wanna do, what I can teach him. I realize that problem I need to LEARN. I quit learning new stuff for a long time. And been in many years in industry, I realize basic techs are the long terms. So I pick up book again, things I lost I will get them back.
