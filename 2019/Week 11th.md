# Week 11th

## Algorithm

### [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

#### Description

Say you have an array for which the `nth` element is the price of a given stock on day `n`.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

#### Example 1

```example
Input: [7, 1, 5, 3, 6, 4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profic = 6 - 1 = 5. Not 7 - 1 = 6, as selling price needs to be larger than buying price.
```

#### Example 2

```example
Input: [7, 6, 4, 3, 1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

#### Solution

```javascript
/**
 * solved with kadane's algorithm
 * @param {number[]} prices
 * @return {number}
 */
const maxProfit = (prices) => {
  let maxCurrent = 0;
  let maxSoFar = 0;
  for (let i = 1; i < prices.length; i++) {
    maxCurrent = Math.max(0, maxCurrent += prices[i] - prices[i - 1]);
    maxSoFar = Math.max(maxCurrent, maxSoFar);
  }
  return maxSoFar;
}

// const prices = [7, 1, 5, 3, 6, 4];
const prices = [2, 4, 1];
const profit = maxProfit(prices);
console.log(profit);
```


## Review

[JS scope: static, dynamic, and runtime-augmented – codeburst](https://codeburst.io/js-scope-static-dynamic-and-runtime-augmented-5abfee6223fe)

- Static/lexical scope is when function knows the *resolution environment* for *free variables* at time of creation.
- Closures is a natural continuation of the static scope. One can say: “closure == static scope”.
- Dynamic scope is when a *caller* provides the callee’s resolution environment at activation.
- Runtime-augmented scope is when own activation environment is not determined at static time, and can be mutated by the callee itself. 

## Technique

Object technique equal

```javascript
/**
 * Compares two objects to determine if the first one contains equivalent property values to the second one.
 * Use `Object.keys()` to get all the keys of the second object,
 * then `Array.prototype.every()`, `Object.hasOwnProperty()` and strict comparison to determine if all keys exist in the first object and have the same values.
 * @param {Object} obj
 * @param {Object} source
 * @returns {Object}
 */
console matches = (obj, source) =>
  Object.keys(source).every(key => obj.hasOwnProperty(key) && obj[key] === source[key]);

const obj = { age: 25, hair: 'long', beard: true };
const source = { age: 25, hair: 'long', beard: true };
const obj1 = { hair: 'long', beard: true };

const m1 = matches(obj, source);
const m2 = matches(obj1, source);
console.log(m1);	// true
console.log(m2);	// false
```

## Share

Algorithms and data structures are the fundamental skills for a developer, practice more harder.