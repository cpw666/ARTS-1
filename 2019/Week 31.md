# Week 31

## Algorithm

### [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

#### Description

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

#### Example

```example
Input: 1 -> 2 -> 4, 1 -> 3 -> 4
Output; 1 -> 1 -> 2 -> 3 -> 4 -> 4
```

#### Solution

```javascript
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @returns {ListNode}
 */
const mergeTwoLists = (l1, l2) *=>* {
  if (l1 === null) return l2;
  if (l2 === null) return l1;

  let handler = null;
  if (l1.val < l2.val) {
    handler = l1;
    handler.next = mergeTwoLists(l1.next, l2);
  } else {
    handler = l2;
    handler.next = mergeTwoLists(l1, l2.next)
  }
  return handler;
}
```


## Review
[Object-Oriented Programming — The Trillion Dollar Disaster](https://medium.com/better-programming/object-oriented-programming-the-trillion-dollar-disaster-92a4b666c7c7)

I do have one point the speak.

The real world is not hierarchical. OOP attempts to model everything as a hierarchy of objects. Unfortunately. that is not how things work in real world. Objects in the real world interact with each other using messages, but they mostly are independent of each other.

OOP inheritance is not modeled after the real world. The parent object in the real world is unable to change the behavior of child objects at run-time. Even though you inherit your DNA from your parents, they’re unable to make changes to your DNA as the please. You do not inherit “behaviors” from your parents, you develop your own behaviors. And you’re unable to “override” your parents’ behaviors.

## Technique

JavaScript version ordinal suffix

```javascript
/**
 * Adds an ordinal suffix to a number.
 * Use the modulo operator (`%`) to find values of single and tens digits.
 * Find which ordinal pattern digits match.
 * If digit is found in teens pattern, use teens ordinal.
 * @param {Number} num
 * @returns {String}
 */
const toOrdinalSuffix = num => {
  const int = parseInt(num);
  const digits = [ int % 10, int % 100 ];
  const ordinals = [ 'st', 'nd', 'rd', 'th' ];
  const oPattern = [ 1, 2, 3, 4 ];
  const tPattern = [ 11, 12, 13, 14, 15, 16, 17, 18, 19 ];
  return oPattern.includes(digits[0]) && !tPattern.includes(digits[1])
    ? int + ordinals[digits[0] - 1]
    : int + ordinals[3];
}

```

## Share
We need to perform refactoring everyday.
