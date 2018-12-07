# Week 49th
## Algorithm

### [563. Binary Tree Tilt](https://leetcode.com/problems/binary-tree-tilt/description/)

#### Description

Given a binary tree, return the tilt of the **whole tree**.  

The title of the **tree node** is defined as the **absolute difference** between the sum of all left subtree node values and the sum of all right subtree node values. Null node has title 0.  

The tilt of the **whole tree** is defined as the sum of all nodes' tilt.

#### Example

```code
Input:
    1
   / \
  2   3
Output: 1
Explanation:
Tilt of node 2: 0
Tilt of node 3: 0
Tilt of node 1: |2 - 3| = 1
Tilt of binary tree: 0 + 0 + 1 = 1
```

#### Note

1. The sum of node values in an subtree won't exceed the range of 32-bit integer.
2. All the tilt values won't exceed the range of 32-bit integer.

#### Solution

```javascript
class TreeNode {
  constructor (val) {
    this.val = val;
    this.left = this.right = null;
  }
}

const findTilt = (root) => {
  let tilt = 0;
  const postOrder = (root) => {
    if (root === null) {
      return 0;
    }
    const left = postOrder(root.left);
    const right = postOrder(root.right);

    tilt += Math.abs(left - right);
    return left + right + root.val;
  };
  postOrder(root);
  return tilt;
};

const tree = new TreeNode(1);
tree.left = new TreeNode(2);
tree.right = new TreeNode(3);
const tilt = findTilt(tree);
console.log(tilt);
```

## Review

[Why Learn Functional Programming in JavaScript? (Composing Software)](https://medium.com/javascript-scene/why-learn-functional-programming-in-javascript-composing-software-ea13afc7a257)  

JavaScript has the most important features need for functional programming are:  
1. **First class functions:** The ability to use function as data values: pass functions as arguments, return functions, and assign functions to variables and object properties. This property allows for higher-order functions, which enable partial application, currying, and composition.
2. **Anonymous functions and concise lambda syntax:** `x => x * 2` is a valid function expression in JavaScript. Concise lambdas make it easier to work with higher-order functions.
3. **Closures:** A closure is the bundling of a function with its lexical environment. Closures are created at function creation time. When a function is defined inside another function, it has access to the variable bindings in the outer function, even after the outer function exists. Closures are how partial applications get their fixed arguments. A fixed argument is an argument bound in the closure scope of a returned function. In `add2(1)(2)`, `1` is a fixed argument in the function returned by  `add2(1)`.


## Technique

We often do `break` in `for` loop, but how can we achieve this in the functional way?
```javascript
const employees = [
  { name: 'Bailey Parry',     gender: 'male'    },
  { name: 'Mason Thompson',   gender: 'male'    },
  { name: 'Rory Barker',      gender: 'male'    },
  { name: 'Zachary Cooke',    gender: 'male'    },
  { name: 'Jack Cox',         gender: 'male'    },
  { name: 'Graham Shepherd',  gender: 'male'    },
  { name: 'Ariel Berger',     gender: 'male'    },
  { name: 'Corey Herman',     gender: 'male'    },
  { name: 'Thomas Sullivan',  gender: 'male'    },
  { name: 'Armando Faulkner', gender: 'male'    },
  { name: 'Yasmin Atkinson',  gender: 'female'  }
];
```

```javascript
// procedural way
let hasFemale = false;

for ({name, gender} of employees) {
  if (gender === 'female') {
    hasFemale = true;
    break;
  }
}

console.log(`${hasFemale ? 'has' : 'doesn\'t have'} female employee`);
```

```javascript
// functional way
const hasFemale = employees.some(({name, gender}) => gender === 'female');
console.log(`${hasFemale ? 'has' : 'doesn\'t have'} female employee`);
```

See function way is more easy and secure without side effects.

## Share

[Custom Elements](https://w3c.github.io/webcomponents/spec/custom/#custom-element) provide a way for authors to build their own full-featured DOM elements. Although authors could always use non-standard elements in their documents, with application-specific behaviour added after the fact by scripting or similar, such elements have historically been non-conforming and not very functional. By defining a custom element, authors can inform the parser how to properly construct an element and how elements of that class should react to changes.  

