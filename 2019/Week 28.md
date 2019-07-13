# Week 28

## Algorithm

### [237. Delete Node in a Linked List](https://leetcode.com/problems/delete-node-in-a-linked-list/)

#### Description

Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.

Given linked list — head = [4, 5, 1, 9], which looks like following:

`[4] --> [5] --> [1] --> [9]`

#### Example 1

```example
Input: head = [4, 5, 1, 9], node = 5
Output: [4, 1, 9]
Explanation: You are given the second node with value 5, the linked list should become 4 -> 1 -> 9 after calling your function.
```

#### Example 2

```example
Input: head = [4, 5, 1, 9], node = 1
Output: [4, 5, 9]
Explanation: You are given the third node with value 1, the linked list should become 4 -> 5 -> 9 after calling your function.
```

#### Note

- The linked list will have at least two elements.
- All of the nodes’ values will be unique.
- The given node will not be the tail and it will always be a valid node of the linked list.
- Do not return anything from your function.

#### Solution

```javascript
function ListNode (val) {
  this.val = val;
  this.next = null;
}

/**
 * @param {ListNode} node
 * @return {undefined} Do not return anything, modify node in-place instead.
 */
const deleteNode = (node) => {
  node.val = node.next.val;
  node.next = node.next.next;
}
```

## Review

[The deepest reason why modern JavaScript frameworks exist](https://medium.com/dailyjs/the-deepest-reason-why-modern-javascript-frameworks-exist-933b86ebc445)

- The main problem modern JavaScript frameworks solve is keeping the UI in sync with the state.
- It is not possible to write complex, efficient and easy to maintain UIs with Vanilla JavaScript.
- Web Components do not provide a solution for this problem.
- It’s not that hard to make your own framework using an existing Virtual DOM library. But it’s not suggested.

## Technique

JavaScript CoalesceFactory

```javascript
/**
 * Returns a customized coalesce function that returns the first argument that returns `true` from the provided argument validation function.
 * Use `Array.prototype.find()` to return the first argument that returns `true` from the provided argument validation function.
 * @param {Function} valid
 * @return {Function}
 */
const coalesceFactory = valid => (...args) => args.find(valid);
```

## Share
Software engineering is about designing, writing, testing, and maintaining computer programs with the purpose of solving problems for many users. It is about creating robust and safe solutions that will withstand the test of time and will work for some of the unknown problems around the original obvious ones.

Softer engineers understand everything about the problems they solve, the solutions they provide, the limitations of those solutions, their privacy implications, and their security implications.

**If someone does not understand the problem, they should not be allowed to program a solution for it.**