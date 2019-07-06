# Week 27

## Algorithm

### [15. 3Sum](https://leetcode.com/problems/3sum/)

#### Description

Given an array `nums` of *n* integers, are there elements *a, b, c* in `nums` such that `a + b + c = 0`? Find all unique triplets in the array which gives the sum of zero.

#### Note

The solution set must not contain duplicate triplets.

#### Example

```example
Given array nums = [-1, 0, 1, 2, -1, -4]
A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

#### Solution

```javascript
/**
 * @param {Array} nums
 * @param {Number} target - if the question asks us for a custom target, we can control it here
 * @returns {Array}
 */
const threeSum = (nums, target = 0) => {
  const results = [];
  // obviously irrelevant if we don't have at least 3 numbers to play with!
  if (nums.length < 3) return results;
  // having the numbers in ascending order will make this problem much easier.
  // also, knowing the overall problem will take at least O(N^2) times,
  // we can afford the O(NlogN) sort operation
  nums.sort((a, b) *=>* a - b);
  for (let i = 0; i < nums.length - 2; i++) {
    // `i` represents the "left" most number in our sorted set.
    // once this number hits 0, there's no need to go further
    // since postive numbers cannot sum to a negative number
    if (nums[i] > target) break;
    // we don't want repeats, so skip numbers we've already seen
    if (i > 0 && nums[i] === nums[i - 1]) continue;
    // `j` represents the "middle" element `i` and `k`.
    // we will increment this up through the array while `i` and `k` are anchored to their positions.
    // we will decrement `k` for each pass through the array,
    // and finally increment `i` once `j` and `k` meet.
    let j = i + 1;
    // `k` represents the "right" most element
    let k = nums.length - 1;
    // to sumarize our setup, we have `i` that starts at the beginning,
    // `k` that starts at the end, and `j` that races in between the two.
    // note that `i` is controlled by our outer for-loop and wil move the slowest.
    // in the meantime, `j` and `k` will take turns inching towards each other
    // depending on some logic we'll set up follow. once the collide, `i` will be incremented up and we'll repeat the process.
    while (j < k) {
      const sum = nums[i] + nums[j] + nums[k];
      // if we find the target sum, increment `j` and decrement `k` for
      // other potential combos where `i` is the anchor
      if (sum === target) {
        // store valid threesum
        results.push([nums[i], nums[j], nums[k]]);
        // this is important! we need to continue to increment `j` and decrement `k`
        // as long as those values are duplicated. in other words. we wanna skip values
        // we've already seen. otherwise, an input array of [-2,0,0,2,2] would result in
        // [[-2,0,2], [-2,0,2]].
        while (nums[j] === nums[j + 1]) j++;
        while (nums[k] === nums[k - 1]) k--;
        // finally, we need to acturally move `j` forward and `k` backward to the
        // next unique elements. the previous while loops will not handle this.
        j++;
        k--;
      // if the sum is too small, increment `j` to get closer to the target
      } else if (sum < target) {
        j++;
      // if the sum is too large, decrement `k` to get closer to the target
      } else {
        k--;
      }
    }
  }
  return results;
};
```

## Review

 [https://medium.com/@hayavuk/why-virtual-dom-is-slower-2d9b964b4c9e](https://medium.com/@hayavuk/why-virtual-dom-is-slower-2d9b964b4c9e) 

Virtual DOM is ultimately a round-about way of performing DOM updates. However, it opens a door up to interesting architecture, such as treating views as *function of state*, or writing and composing view components. Three are many good things virtual DOM brings to the table, maybe insane levels of performance is not one of them. You could think of it as the difference between coding in Python or PHP vs coding in C. We get more developer ergonomic at the cost of performance. It’s a trade-off, in other words.

On the other hand, developer time *lost* is also a thing when it comes to some of the implementation. The part where virtual DOM tries to figure out what changes it needs to perform is implemented by humans, so it’s not always fool-proof. Sometimes you have to intervene. In some cases, it is not possible to intervene. For thins that are absolutely performance-critical, it may not even be an option.

The bottom line is that the virtual DOM is just one of the tools you have at your disposal. Measure your performance and decide according to hard data. Data binding is still quit viable, and we have already seen you can do everything manually as well. It’s definitely not a be all end all thing, and there is therefore no need to get married to virtual DOM.

## Technique

JavaScript `isNil`

```javascript
/**
 * Returns `true` if the specified values is `undefined`, `false` otherwise.
 * Use the strict equality operator to check if tha value and of `val` are equal to `null` or `undefined`.
 * @param {Object} val
 * @returns {Boolean}
 */
const isNil = val => val === undefined || val === null;
```

## Share

Finish my new house decorating project, can’t wait to move in!
