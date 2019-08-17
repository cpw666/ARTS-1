# Week 33

## Algorithm

### [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

#### Description

Given a linked list, determine if it has a cycle in it.

To represent a cycle in the given linked list, we use an integer `pos` which represents the position (0-indexed) in the linked list where tail connects to.
If `pos` is `-1`, then there is no cycle in the linked list.

#### Example 1

```example
Input: head = [ 3, 2, 0, -4 ], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

![3->2->0->-4](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

#### Example 2

```example
Input: head = [ 1, 2 ], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```

![1->2](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

#### Example 3

```example
Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list
```

![1](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)

#### Follow up

Can you solve it using O(1) (i.e. constant) memory?

#### Solution

```javascript
// Definition for singly-linked list.
function ListNode (val) {
  this.val = val;
  this.next = null;
}

/**
 * 1. Use two pointers, **walker** and **runner**
 * 2. **walker** moves step by step. **runner** moves two steps at time.
 * 3. If the linked list has a cycle **walker** and **runner** will meet at some point
 * *@param* ~{ListNode}~ head
 * *@returns* ~{Boolean}~
 */
const hasCycle = head => {
  if (head === null) return false;
  let runner = head;
  let walker = head;
  while (runner.next !== null && runner.next.next !== null) {
    walker = walker.next;
    runner = runner.next.next;
    if (walker === runner) return true;
  }
  return false;
};
```


## Review

[Beyond Memory Leaks in JavaScript - OutSystems Experts - Medium](https://medium.com/outsystems-experts/beyond-memory-leaks-in-javascript-d27fd48ae67e)

Since the garbage collector reclaims memory for execution and you can’t control when it happens, it may run while something else important is running, too. How many times have you been scrolling a page in your mobile phone and experience some kind of stutter or freeze, even if just for a few seconds? That may just be the trashcan collecting you garbage.

Don’t leave you trash in the house; it will leak and smell. Pimples do come from “garbage” that accumulates on your pores, you know? (Yeah, I needed to tie it all in, just like that.)

Now, while having your garbage collected is a good thing, because if frees up memory that no longer needs to be allocated, if performance suffers you may need to find ways to minimize that impact.

There are workarounds for optimizing your memory usage, Stuff like [Object Pooling]( https://github.com/miohtama/objectpool.js ), which helps minimize the garbage collector impact on performance: You create a pool of objects and reuse them instead of recreating them for garbage collection.

Garbage collectors nowadays are extremely optimized, so I only recommend using this if you’ve noticed it running too many times for your taste and that it’s taking a long time to run each time.


## Technique

JavaScript `promisify`

```javascript
/**
 * Converts an asynchronous function to return a promise.
 * Use currying to return a function returning a `Promise` that calls the original function.
 * Use the `...rest` operator to pass in all the paramaters, In Node 8+, you can use `util.promisify`.
 * @param {Function} func
 * @returns {Promise}
 */
const promisify = func => (...args) =>
  new Promise((resolve, reject) => func(...args, (err, result) => (err ? reject(err) : resolve(result))));

// test

const delay = promisify((d, cb) => setTimeout(cb, d));
delay(2000).then(_ => console.log('Hi')); // Hi after 2 second

```

## Share

Failures are not demons, afraid of failure is.
