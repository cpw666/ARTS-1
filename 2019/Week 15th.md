# Week 15th

## Algorithm

### [350. Intersection of Two Arrays II](https://leetcode.com/problems/intersection-of-two-arrays-ii/)

#### Description

Given two arrays, write a function to compute their intersection.

#### Example 1

```example
Input: nums1 = [1, 2, 2, 1], nums2 = [2, 2]
Output: [2, 2]
```

#### Example 2

```example
Input: nums1 = [4, 9, 5], nums2 = [9, 4, 9, 8, 4]
Output: [4, 9]
```

#### Note

- Each element in the result should be appear as many times as it shows in both arrays.
- The result can be in any order.

#### Follow up

- What if the given array is already sorted? How would you optimize your algorithm?
- What if *nums1’s* size is small compared to *nums2’s* size? Which algorithm is better?
- What if elements of *nums2* are stored on dist, and the memory is limited such that you cannot load all elements into the memory at once?

#### Solution

```javascript
const intersect = (nums1, nums2) => {
  const sorter = (a, b) => a - b;
  nums1.sort(sorter);
  nums2.sort(sorter);
  let i1 = 0;
  let i2 = 0;
  const ln1 = nums1.length;
  const ln2 = nums2.length;
  const intersectors = [];
  while (i1 < ln1 && i2 < ln2) {
    if (nums1[i1] === nums2[i2]) {
      intersectors.push(nums1[i1]);
      i1 += 1;
      i2 += 1;
    } else if (nums1[i1] > nums2[i2]) {
      i2 += 1;
    } else {
      i1 += 1;
    }
  }
  return intersectors;
};
const nums1 = [4,9,5];
const nums2 = [9,4,9,8,4];
const intersectors = intersect(nums1, nums2);
console.log(JSON.stringify(intersectors));
```


## Review

 [Design patterns in modern JavaScript development](https://levelup.gitconnected.com/design-patterns-in-modern-javascript-development-ec84d8be06ca)

There is some good stuff here, but some specific things are misapplied particularly the singleton/click counter example.

Singletons are not an answer to managing scope. By using a singleton to accomplish this task you are: 

- Introducing global logic to the application (re-initializing the singleton when you want to count again from zero, for instance)
- Preventing another instance from existing. You can only never count this one set of buttons. This is the biggest club that a singleton is exactly the wrong pattern.

Use your DI container or just plain old javascript scope to create objects that live for the same lifetime as the things you are counting. Choosing a singleton for this is the modern equivalent of the age-old “global-variables” sin.

Singletons are for when it’s dangerous/illogical to have two instances of something, and that’s it.

## Technique

Capitalize every worlds.

```javascript
/**
 * Capitalizes the first letter of every word in a string.
 * Use `String.prototype.replace()` to match the first character of each word and `String.prototype.toUpperCase()` to capitalize it.
 * @param {String} str
 * @returns {String}
 */
const capitalizeEveryWord = str => str.replace(/\b[a-z]/g, char => char.toUpperCase());
```

## Share

Count my time, manage my time. Too much this need to be done, they should be on a priority todo list.
