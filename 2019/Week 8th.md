# Week 8th

## Algorithm

### [622. Design Circular Queue](https://leetcode.com/problems/design-circular-queue/)

#### Description

Design your implementation of the circular queue. The circular queue is a linear data structure in which the operations are performed based on FIFO (First In First Out) principle and the last position is connected back to the first position to make a circle. It is also called "Ring Buffer".  

One of the benefits of the circular queue is that we can make use of the spaces in front of the queue. in a normal queue, once the queue becomes full, we cannot insert the next element even if there is a space in front of the queue. But using the circular queue, we can use the space to store new values.  

Your implementation should support following operations:

1. `MyCircularQueue(k)`: Constructor, set the size of the queue to be `k`.
2. `Front`: Get the front item from the queue. If the queue is empty, return -1.
3. `Rear`: Get the last item from the queue. If the queue is empty, return -1.
4. `enQueue(value)`: Insert an element from the circular queue. Return true if the operation is successful.
5. `deQueue()`: Delete an element from the circular queue. Return true if the operation is successful.
6. `isEmpty()`: Checks whether the circular queue is empty or not.
7. `isFull()`: Checks whether the circular queue is full or not.

#### Example

```javascript
MyCircularQueue circularQueue = new MyCircularQueue(3); // set the size to be 3
circularQueue.enQueue(1); // return true
circularQueue.enQueue(2); // return true
circularQueue.enQueue(3); // return true
circularQueue.enQueue(4); // return false, the queue is full
circularQueue.Rear(); // return 3
circularQueue.isFull(); // return true
circularQueue.deQueue(); // return true
circularQueue.enQueue(4); // return true
circularQueue.Rear(); // return 4
```

#### Note

- All values will be in the range of [0, 1000].
- The number of operations will be in the range of [1, 1000].
- Please do not use the build-in Queue library.

#### Solution

```javascript
/**
 * Initialize your data structure hear. Set the size of queue to be k.
 * @param {Number} k
 */
const MyCircularQueue = function (k) {
  this.capacity = k;
  this.length = 0;
  this.head = -1;
  this.tail = -1;
  this.queue = [];
};

/**
 * Insert an element into the circular queue. Return true if the operation is successful.
 * @param {Number} value
 * @return {Boolean}
 */
MyCircularQueue.prototype.enQueue = function (value) {
  if (this.isFull()) {
    return false;
  } else {
    this.tail = (this.tail + 1) % this.capacity;
    this.queue[this.tail] = value;
    this.length += 1;
    return true;
  }
};

/**
 * Delete an element from the circular queue. Return true if the operation is successful.
 * @return {Boolean}
 */
MyCircularQueue.prototype.deQueue = function () {
  if (this.isEmpty()) {
    return false;
  } else {
    this.head = (this.head + 1) % this.capacity;
    this.length -= 1;
    return true;
  }
};

/**
 * Get the front item from the queue.
 * @return {Number}
 */
MyCircularQueue.prototype.Front = function () {
  return this.head >= 0 ? this.queue[this.head] : this.head;
};

/**
 * Get the last item from the queue
 * @return {Number}
 */
MyCircularQueue.prototype.Rear = function () {
  return this.tail >= 0 ? this.queue[this.tail] : this.tail;
};

/**
 * Checks whether the circular queue is empty or not.
 * @returns {Boolean}
 */
MyCircularQueue.prototype.isEmpty = function () {
  return this.length === 0;
};

/**
 * Checks whether the circular queue is full or not.
 * @returns {Boolean}
 */
MyCircularQueue.prototype.isFull = function () {
  return this.length === this.capacity;
};

const queue = new MyCircularQueue(3);
queue.enQueue(1); // return true
queue.enQueue(2); // return true
queue.enQueue(3); // return true
queue.enQueue(4); // return false, the queue is full
let rear = queue.Rear(); // return 3
let isfull = queue.isFull(); // return true
queue.deQueue(); // return true
queue.enQueue(4); // return true
rear = queue.Rear(); // return 4
```

## Review

[Functional JS with ES6 -- Recursion Patterns](https://medium.com/dailyjs/functional-js-with-es6-recursive-patterns-b7d0813ef9e3)
  
Functional Programming obey the principle of building software and recursion is the most fundamental concerpt of programming languages. With ES6 the powerful weapon for frontend we could finally understand what is computer, how to create a computation system from the ground.

## Technique

I love JavaScript technique.  

Flatten Object.  

```javascript
/**
 * Flatten an object with the paths for keys.
 *  
 * Use recursion. Use `Object.keys()` combined with `Array.prototype.reduce()` to convert every leaf node to a flattened path node.
 * If value of a key is an object, the function calls itself with the appropriate `prefix` to create the path using `Object.assign()`.
 * Otherwise, it adds the appropriate prefixed key-value pair to the accumulator object.
 * You should always omit the the second argument, `prefix`, unless you want every key to have a prefix.
 * @param {Object} obj
 * @param {String} prefix
 * @returns {Object}
 */
const flattenObject = (obj, prefix = '') => 
  Object.keys(obj).reduce((acc, k) => {
    const pre = prefix.length ? prefix + '.' : '';
    if (typeof obj[k] === 'object') {
      Object.assign(acc, flattenObject(obj[k], pre + k));
    } else {
      acc[pre + k] = obj[k];
    }
    return acc;
  }, {});

const object = { a: { b : { c: 1}}, d: 1 };
const unprefixed = flattenObject(object);
const prefixed = flattenObject(object, 'e');
console.log(JSON.stringify(unprefixed)); // {a.b.c: 1, d:1}
console.log(JSON.stringify(prefixed)); // {e.a.b.c: 1, e.d:1}
```

## Share

We programmers should follow the Amazon's work flow, from requirements to operations do our own. Division of responsibilities, not by skill.