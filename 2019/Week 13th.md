# Week 13th

## Algorithm

### [189. Rotate Array](https://leetcode.com/problems/rotate-array/)

#### Description

Given an array, rotate the array to the right by *k* steps, where *k* is non-negative.

#### Example 1

```example
Input: [1, 2, 3, 4, 5, 6, 7] and k = 3
Output: [5, 6, 7, 1, 2, 3, 4]
Explanation:
rotate 1 steps to the right: [7, 1, 2, 3, 4, 5, 6]
rotate 2 steps to the right: [6, 7, 1, 2, 3, 4, 5]
rotate 3 steps to the right: [5, 6, 7, 1, 2, 3, 4]
```

#### Example 2

```example
Input: [-1, -100, 3, 99] and k = 2
Output: [3, 99, -1, -100]
Explanation:
rotate 1 steps to the right: [99, -1, -100, 3]
rotate 2 steps to the right: [3, 99, -1, -100]
```

#### Note

- Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
- Could you do it in-place with O(1) extra space?

#### Solution 1

```javascript
/**
 * rotate the array `nums` to with `k` steps.
 * Solve this with loop
 * @param {Array} nums - Array to be rotate
 * @param {Number} k - number of steps
 * @returns {Array} - rotated array to be returned
 */
const rotate = (nums, k) => {
  if (nums.length < 2) {
    return nums;
  }
  for (let i = 0; i < k; i++) {
    const last = nums.pop();
    nums.unshift(last);
  }
  return nums;
};
```

#### Solution 2

```javascript
/**
 * Solve this with reverse 3 times in O(1)
 * nums = "----->-->"; k =3
 * result = "-->----->";
 *
 * reverse "----->-->" we can get "<--<-----"
 * reverse "<--" we can get "--><-----"
 * reverse "<-----" we can get "-->----->"
 * @param {Array} nums - Array to be rotate
 * @param {Number} k - number of steps
 * @returns {Array} - rotated array to be returned
 */
const rotateWithReverse = (nums, k) => {
  const reverse = (nums, start, end) => {
    while (start < end) {
      const temp = nums[start];
      nums[start] = nums[end];
      nums[end] = temp;
      start++;
      end--;
    }
  }
  k %= nums.length;
  reverse(nums, 0, nums.length - 1);
  reverse(nums, 0, k - 1);
  reverse(nums, k, nums.length - 1);
  return nums;
};
```


## Review

[Measure, Optimize & Monitor. – Addy Osmani – Medium](https://medium.com/@addyosmani/measure-optimize-monitor-33e36108e014)

- Lin performance to your business goals. Help stakeholders measure how performance impacts the core business metrics they care about.
- Real-world performance is diverse. Measure performance on mobile devices & network connection common to your actual users.
- When optimizing, load only what you need when you need it. Actively manage your payloads and start-up times short.
- Add performance budgets to continuous integration. Enable engineers and PMs to visualize the **cost** of each new feature. Often businesses don’t understand what is **acceptable** performance or the user-impact to perf of introduction new features.
- Ensure tests measuring lab conditions collect the same (or similar) metrics from the real-world (RUM). Performance impact on metrics in the real-world can be highly variable due to differences in devices, networks and other conditions.
- Measure optimizations had the intended effect (e.g A/B test). A **fix** may not be correct if it improves on metric at the cost of another.
- Add regular proactive reporting on performance progress to highlight success (e.g emails, dashboards, alerts). This ensure performance is a regular part of the conversation and is converted in a way that can be digested by more people.

## Technique

Order object by property

```javascript
/**
 * Returns a sorted array of objects ordered by properties and orders.
 * Use `Array.prototype.sort()`, `Array.prototype.reduce()` on the `props` array with a default value of `0`,
 * use array destructuring to swap the properties position depending on the order passed.
 * If no `orders` array is passed it sort by `asc` by default.
 * @param {Array} arr
 * @param {String} props
 * @param {Array} orders
 * @returns {Array}
 */
const orderBy = (arr, props, orders) =>
  [...arr].sort((a, b) =>
    props.reduce((acc, prop, i) => {
      if (acc === 0) {
        const [p1, p2] = orders && orders[i] === 'desc' ? [b[prop], a[prop]] : [a[prop], b[prop]];
        acc = p1 > p2 ? 1 : p1 < p2 ? -1 : 0;
      }
      return acc;
    }, 0)
  );
```

## Share

I’m now in the surveillance industry, which once I spitting on. With the world view changed, I think I need to stuck into as many industries as I can, so I can be the one which dreamed to be. The guy who knows the digital world and who can take his species conquer the universe.