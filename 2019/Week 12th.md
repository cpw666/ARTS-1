# Week 12th

## Algorithm

### [122. Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/)

#### Description

Say you have an array for which the i^th element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

#### Note

You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

#### Example 1

```example
Input: [7, 1, 5, 3, 6, 4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit  = 5-1 = 4.
Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
```

#### Example 2

```example
Input: [1, 2, 3, 4, 5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are engaging multiple transactions at the same time. You must sell before buying again.
```

#### Example 3

```example
Input: [7, 6, 4, 3, 1]
Output: 0
Explanation: Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

#### Solution

```javascript
/**
 * @param {Array} prices
 * @returns {Number}
 */
const maxProfit = (prices) *=>* {
 	let i = 0;
  let buy = 0;
  let sell = 0;
  let profit = 0;
  let n = prices.length - 1;
  while (i < n) {
    while (i < n && prices[i + 1] <= prices[i]) i++;
    buy = prices[i];

    while (i < n && prices[i + 1] >= prices[i]) i++;
    sell = prices[i];

    profit += sell - buy;
  }
  return profit;
}
const prices = [7, 1, 5, 3, 6, 4];
// const prices = [2, 4, 1];
const profit = maxProfit(prices);
console.log(profit); // 7
```


## Review

[JavaScript Start-up Performance – reloading – Medium](https://medium.com/reloading/javascript-start-up-performance-69200f43b201)

**Start-up performance matters.**  A combination of slow parse, compile an execution times can be a real bottleneck for pages that wish to boot-up quickly. **Measure** how long your pages spend in this phase. Discover what you can do to make it faster. 


## Technique

Object from Array aka map from array.
```javascript
/**
 * Creates an object from the given key-value pairs.
 * Use `Array.prototype.reduce()` to create and combine key-value pairs
 * @param {Array} arr
 * @returns {Object}
 */
const objectFromPairs = arr => arr.reduce((a, [k, v]) => ((a[k] = v), a), {});

const pairs = [['a', 1], ['b', 2]];
const object = objectFromPairs(pairs);
console.log(JSON.stringify(object));  // {a: 1, b: 2}
```

## Share

I don’t have so much time for take cover the freelancer job along with a full-time job in the mean time for learning staff. too busy for me. may be you need to consider this more carefully.