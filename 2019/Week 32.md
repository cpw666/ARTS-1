# Week 32

## Algorithm

### [234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)

#### Description

Given a singly linked list, determine if it is a palindrome.

#### Example 1

```example
Input: 1 -> 2
Output: false
```

#### Example 2

```example
Input: 1 -> 2 -> 1
Output: false
```

#### Follow up

Could you do it in O(n) time and O(1) space?

#### Solution

```javascript
function ListNode (val) {
  this.val = val;
  this.next = null;
};

/**
 * This can be solved by reversing the 2nd half and compare the two havles.
 * Let's start with an example `[1, 1, 2, 1]`.
 * In the beginning, set two points `fast` and `slow` starting at the head.
 * 1 -> 1 -> 2 -> 1 -> null
 * sf
 *
 * 1) Move: `fast` pointer goes to the end, and `slow` point goes to the middle.
 * 1 -> 1 -> 2 -> 1 -> null
 *           s          f
 *
 * 2) Reverse: the right half is reversed, and `slow` pointer becomes the 2nd head
 * 1 -> 1 null <- 2 <- 1
 * f                   s
 *
 * 3) Compare: run the two points `fast` and `slow` together and compare.
 * 1 -> 1 null <- 2 <- 1
 *      f         s
 *
 * @param {ListNode} head
 * @returns {Boolean}
 */
const isPalindrome = head => {
  let fast = head;
  let slow = head;
  while (fast !== null && fast.next !== null) {
    fast = fast.next.next;
    slow = slow.next;
  }
  if (fast !== null) { // odd nodes: let right half smaller
    slow = slow.next;
  }
  slow = reverse(slow);
  fast = head;
  while (slow !== null) {
    if (fast.val !== slow.val) {
      return false;
    }
    fast = fast.next;
    slow = slow.next;
  }
  return true;
};

const reverse = head => {
  let prev = null;
  while (head !== null) {
    const next = head.next;
    head.next = prev;
    prev = head;
    head = next;
  }
  return prev;
}
```


## Review

 [https://medium.com/javascript-scene/elements-of-javascript-style-caa8821cb99f](https://medium.com/javascript-scene/elements-of-javascript-style-caa8821cb99f) 

Reading this page again, and here is what i get this time.

**Code Should Be Simple, Not Simplistic.**

> Vigorous writing is concise. A sentence should contain no unnecessary words, a paragraph no unnecessary sentences, for the same reason that a drawing should have no necessary lines and a machine no unnecessary parts. *This requires not that the writer make all sentences short, or avoid all detail and treat subjects only in outline, but that every word tell.**  
> ~ William Strunk, Jr., The Elements of Style.  

ES6 was standardized in 2015, yet in 2019, many developers avoid features such as concise arrow functions, implicit return, rest and spread operators, etc… in the guise of writing code that is easier to read because it is more familiar. That is a big mistake. Familiarity comes with practice, and with familiarity, the concise features in ES6 are clearly superior to the ES5 alternatives: concise code is simple compared to the syntax-heavy alternative.

Code should be simple, not simplistic.

Give that concise code is:

- Less bug prone
- Easier to debug

And given that bugs:

- Are extremely expensive to fix
- Tend to cause more bugs
- Interrupt the flow on normal feature development

And given that concise code is also:

- Easier to write
- Easier to read
- Easier to maintain

It is worth the training investment to bring developers up to speed using techniques such as concise syntax, currying & composition. When we fail to do so for the sake of familiarity, we talk down to readers of our code so that they can better understand it, like an adult speaking baby-talk to a toddler.

Assume the reader knows nothing about the implementation, but do not assume that the reader is stupid, or that the reader doesn’t know the language.

Be clear, but don’t dumb it down. To dumb things down is both wasteful and insulting. Make the investment in practice and familiarity in order to gain a better programming vocabulary, and a more vigorous style.


## Share

Pipe async functions

```javascript
/**
 * Performs left-to-right function composition for asynchronous functions.
 * Use `Array.prototype.reduce()` with the spread operator (`...`) to perform left-to-right function composition using `Promise.then()`.
 * The functions can return a combination of: simple values, `Promise`'s, or they can be defined as `async` ones returning through `await`.
 * All functions muest be unary.
 * @param  {...Function} fns
 * @returns {Function}
 */
const pipeAsyncFunctions = (...fns) => arg => fns.reduce((p, f) => p.then(f), Promise.resolve(arg));

// test

const sum = pipeAsyncFunctions(
  x => x + 1,
  x => new Promise(resolve => setTimeout(() => resolve(x + 2), 1000)),
  x => x + 3,
  async x => (await x) + 4
);

(
  async _ => {
    console.log(await sum(5));
  }
)();

// output is 15 after 1 second
```

## Technique

Keep your code clean and your function stupid enough, practice everyday you can.

