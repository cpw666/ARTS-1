# Week 34

## Algorithm

### [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)

#### Description

Given a binary search tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

- The left subtree of a node contains only nodes with keys **less than** the node’s key.
- The right subtree of a node contains only nodes with keys **great than** the nodes key.
- Both the left and right subtrees must also be binary search trees.

#### Example 1

```example
  2
 / \
1   3

Input: [2, 1, 3]
Output: true
```

#### Example 2

```example
  5
 / \
1   4
   / \
  3   6

Input: [5, 1, 4, null, null, 3, 6]
Output: false
Explanation: The root node's value is 5 but its right child's vaue is 4.
```

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
 * Let us talk about `Min` and `Max`, first with a wrong solution
 *
 * Buggy code
 * const isValidBST = (root) {
 *    const helper = node => {
 *      if (!node) return true;
 *      if (node.left && node.left >= node.val) return false;
 *      if (node.right && node.right <= node.val) return false;
 *      return helper(node.left) && helper(node.right)
 *    }
 *    return helper(root);
 * }
 *
 * this buggy function seems ok, except for scenary like bellow
 *   5
 *  / \
 * 1   4
 *    / \
 *   3   6
 *
 * Why? we do two things for each layer's root
 * 1. check `root.left.val` is less than `root.val`
 * 2. check `root.right.val` is great than `root.val`
 *
 * But Binary Search Tree got another rule, that
 * 1. all the left children must less than `root.val`
 * 2. all the right children must great than `root.val`
 *
 * the wrong senary is leaf layer `3` is less than top layer `5`
 *
 * So how do we solve this issue? by pass a range, for example:
 *
 * Tell all the left children `1` of top layer `5` your range is (-infinite, 5)
 * Tell all the right children `4` of top layer `5` your range is (5, infinite)
 *
 * bring these paramaters into our program name our left as `leftBound`, and our right as `rightBound`.
 *
 * @param {TreeNode} root
 * @returns {Boolean}
 */
const isValidBST = (root, lowerBound = Number.MIN_SAFE_INTEGER, upperBound = Number.MAX_SAFE_INTEGER) => {
  if (!root) return true;
  if (lowerBound >= root.val || root.val >= upperBound) return false;
  return isValidBST(root.left, lowerBound, root.val) && isValidBST(root.right, root.val, upperBound);
}
```


## Review

[A Better Alternative to Screen-sharing for Enterprise Customer Support](https://blog.sessionstack.com/a-better-alternative-to-screen-sharing-for-enterprise-customer-support-99b5f204ba76)

Co-browsing solution allows you to interact with your customers’ screen with just a lick on a button, without any downloads and installations. This allows you to remove all of the setup friction when you need to start a support session.

The co-browsing solutions are integrated directly inside your product via a small JavaScript snippet (like Google Analytics). Yes, there is some small integration effort but it offloads all of the future efforts from all of your users. The great thing about co-browsing solutions (at least the good ones) is that they have zero impact on your web app’s performance due to the way the technology works.

Here is how co-browsing solves all of the issues we care:

- **Sensitive dat** — with a co-browsing solution, you have the ability to mask sensitive data in your product. This means that once the support agent joins your customer’s screen, the data that has been masked as sensitive won’t be shown to the support agent. Better yet, it won’t even leave your customer’s browser.
- **Permission to install software** — since the co-browsing solution is directly integrated with your product, your customers **don’t need to do anything**. They have the ability whether to grant or decline access to their screen by the support agent but the don’t have to spend time setting up anything.
- **Addition recording software** — some co-browsing solutions allow you to automatically record the whole support session. This means that no screenshots or additional recording software is needed. As soon as the support session ends, you can instantly link it’s recording to your support ticket.

## Technique

### Bouncing Loader
[Check me out](https://codepen.io/charleserious/pen/rNBWRwr)

#### Sample

```css
/* main.css */
html, body {
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
}

@keyframes bouncing-loader {
  to {
    opacity: 0.1;
    transform: translate3d(0, -1rem, 0);
  }
}

.bouncing-loader {
  display: flex;
  justify-content: center;
}

.bouncing-loader > div {
  width: 1rem;
  height: 1rem;
  margin: 3rem 0.2rem;
  background: #8385aa;
  border-radius: 50%;
  animation: bouncing-loader 0.6s infinite alternate;
}

.bouncing-loader > div:nth-child(2) {
  animation-delay: 0.2s;
}

.bouncing-loader > div:nth-child(3) {
  animation-delay: 0.4s;
}
```

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <link rel="stylesheet" href="./main.css">
  <title>Bouncing loading</title>
</head>
<body>
  <div class="bouncing-loader">
    <div></div>
    <div></div>
    <div></div>
  </div>
</body>
</html>
```

#### Explanation

Note: `1rem` is usually `16px`.

1. `@keyframes` defines an animation that has two states, where the element changes `opacity` and is translated up on the 2D plane using `transform: translate3d()`. Using a single axis translation on `transform: translate3d()` improves the performance of the animation.
2. `.bouncing-loader` is the parent container of the bouncing circles and uses `display: flex` and `justify-content: center` to position them in the center.
3. `.bouncing-loader > div`, targets the three child `div`s of the parent to be styled. The `div`s are given a width and height of `1rem`, using `border-radius: 50%` to tern them from squares to circles.
4. `margin: 3rem 0.2rem` specifies that each circle has a top/bottom margin of `3rem` and left/right margin of `0.2rem` so that they do not directly touch each other, giving them some breathing room.
5. `animation` is a shorthand property for the various animations properties: `animation-name`, `animation-duration`, `animation-iteration-count`, `animation-direction` are used.
6. `nth-child(n)` targets the element which is the nth child of its parent.
7. `animation-delay` is used on the second and third `div` respectively, so that each element does not start the animation at the same time.

## Share
**KEEP YOUR CODE CLEAN, AND KEEP YOUR SOLUTION CLEAN**