# Week 29

## Algorithm

### [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

#### Description

Given a linked list, remove then `n-th` node from the end of list and return its head.

#### Example

```example
Given linked list: 1 -> 2 -> 3 -> 4 -> 5, and n = 2.
After removing the second node from the end, the linked list becomes 1 -> 2 -> 3 -> 5.
```

#### Note

Given n will always be valid.

#### Follow up

Could you do this in one pass?

#### Solution

```javascript
function ListNode (val) {
  this.val = val;
  this.next = null;
}

/**
 * @param {ListNode} head
 * @param {Nubmer} n
 * @returns {ListNode}
 */
const removeNthFromEnd = (head, n) => {
  let start = new ~ListNode~(0);
  let slow = start;
  let fast = start;
  slow.next = head;
  // Move fast in front so that the gap between slow and fast becomes `n`
  for (let i = 1; i <= n + 1; i++) {
    fast = fast.next;
  }
  // Move fast to the end, maintaining the gap
  while (fast != null) {
    slow = slow.next;
    fast = fast.next;
  }
  // Skip the desired node
  slow.next = slow.next.next;
  return start.next;
};
```


## Review

[Software Engineering is different from Programming - jsComplete EdgeCoders - Medium](https://medium.com/edge-coders/software-engineering-is-different-from-programming-b108c135af26)

No one can learn software in two months, or six, or even a year. You do not learn to be a software engineer in a bootcamp. I have been learning for the past 7+ years and I am still learning today. I became confident enough to call myself an experienced programmer in today after learning, designing, building, and maintaining applications that are used by thousands of users.

Software engineering is not for everyone, but everyone should learning to solve their own problems with computers. If you can learn to write simple programs you should. If you can learn to use generic software services you should. If you can learn to use open-source software you will have a lot of power.

Problems evolve and so should software engineering. The future of this profession is to enable regular computer users to use their computers without needing to study five years to do so. Enable users to solve the easy problems on their own with easy-to-use tools. Software engineers would then move on create better tools, solve bigger known problems, and do their best to prevent unknown ones.

## Technique

In JavaScript we need HEX to RGB/A

```javascript
/**
 * Converts a color code to a `rgb()` or `rgba()` string if alpha value is provided.
 * Use bitwise right-shift operator and mask bits with `&` (and) operator to convert a hexadecimal color code (with or without prefixed with `#`)
 * to a string with the RGB values.
 * If it's 3-digit color code, first convert to 6-digit version. If an alpha value is provided alongside 6-digit hex, give `rgba()` string in return.
 * @param {String} hex
 * @returns {String}
 */
const hexToRGB = hex => {
  let alpha = false;
  let h = hex.slice(hex.startsWith('#') ? 1 : 0);
  if (h.length === 3) {
    h = [...h].map(x *=>* x + x).join('');
  } else if (h.length === 8) {
    alpha = true;
  }
  h = parseInt(h, 16);
  return (
    'rgb' +
    (alpha ? 'a' : '') +
    '(' +
    (h >>> (alpha ? 24 : 16)) +
    ', ' +
    ((h & (alpha ? 0x00ff0000 : 0x00ff00)) >>> (alpha ? 16 : 8)) +
    ', ' +
    ((h & (alpha ? 0x0000ff00 : 0x0000ff)) >>> (alpha ? 8 : 0)) +
    (alpha ? `, ${h & 0x000000ff}` : '') +
    ')'
  );
};
```


## Share

When they tell you to give up, give yourself another chance to try one move time.