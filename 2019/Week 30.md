# Week 30

## Algorithm

### [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

#### Description

Reverse a singly linked list.

#### Example

```example
Input: 1 -> 2 -> 3 -> 4 -> 5 -> NULL
Output: 5 -> 4 -> 3 -> 2 -> 1 -> NULL
```

#### Follow up

A linked list can be reversed either iteratively or recursively. Could implement both?

#### Solution recursively

```javascript
function ListNode (val) {
  this.val = val;
  this.next = null;
}

/**
 * recursively reverse list
 * @param {ListNode} head
 * @returns {ListNode}
 */
const reverseList = (head) => {
  const recursive = (head, newHead) => {
    if (head === null) {
      return newHead
    }
    const next = head.next;
    head.next = newHead;
    return recursive(next, head);
  };
  return recursive(head, null);
}
```

#### Solution iteratively

```javascript
function ListNode (val) {
  this.val = val;
  this.next = null;
}

/**
 * Iteratively reverse list
 * @param {ListNode} head
 * @returns {ListNode}
 */
const reverseList = (head) => {
  let newHead = null;
  while (head !== null) {
    const next = head.next;
    head.next = newHead;
    newHead = head;
    head = next;
  }
  return newHead;
}
```


## Review

[Why Cutting Costs is Expensive: How $9/Hour Software Engineers Cost Boeing Billions](https://medium.com/javascript-scene/why-cutting-costs-is-expensive-how-9-hour-software-engineers-cost-boeing-billions-b76dbe571957)

> In software, slow is fast.  

Fast is Slow and Cheap is Expensive, So why are so many mangers cheap?

To cut costs, engineering managers often rush developers, impose arbitrary unrealistic deadlines, or in case of Boeing, outsource engineering to cheap contractors to try to increase production bandwidth.

Boeing’s cultural emphasis on cost savings seems to have trickled all the way down to the engineers working on the 737. One 737 contract software engineer from HCL, an Indian company Boeing outsourced to, illustrates the cost cutting culture on his resume:

> “Provided quick workaround to resolve production issue which resulted in not delaying flight test of 737-Max (delay in each fight test will cost very big amount for Boeing).”  

Regardless of which systems these engineers worked on, if you foster an engineering culture where develops are made to feel that management values fast and cheap over continuous process and quality software, that will have a tremendously negative impact on both the quality and the timely delivery of your software, Buggy software takes longer to build.

## Technique

JavaScript Performance match

```javascript
/**
 * Returns the index of the function in an array of functions which executed the fastest.
 *
 * Use `Array.prototype.map()` to generate an array where each value is the total time taken to execute the function after `iterations` times.
 * Use the difference in `performance.now()` values before and after to get the total time in milliseconds to a high degree of accuracy.
 * Use `Math.min()` to find the minimum execution time, and return the index of that shortest time which corresponds to the index of the most performant function.
 * Omit the second argument, `iterations`, to use a default of 10,000 iterations.
 * The more iterations, the more reliable the result but the longer it will take.
 * @param {Array} fns
 * @param {Number} iterations
 * @returns {Number}
 */
const mostPerformant = (fns, iterations = 10000) => {
  const times = fns.map(fn => {
    const before = performance.now();
    for (let i = 0; i < iterations; i++) fn();
    return performance.now() - before;
  });
  return times.indexOf(Math.min(...times));
};
```

## Share
Be a software engineer not just a programmer.
