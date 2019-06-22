# Week 25

## Algorithm

### [38. Count and Say](https://leetcode.com/problems/count-and-say/)

#### Description

The count-and-say sequence is the sequence of integers with the first five terms as following:

1. 1
2. 11
3. 21
4. 1211
5. 111221

`1` is read off as `"one 1"` or `11`.
`11` is read off as `"two 1s"` or `21`.
`21` is read off as `"one 2"`, then `one 1"` or `1211`.

Given an integer *n* where 1 ≤ *n* ≤ 30, generate the nth term of the count-and-say sequence.

#### Note

Each term of the sequence of integers will be represented as a string.

#### Example 1

```example
Input: 1
Output: "1"
```

#### Example

```example
Input: 4
Output: "1211"
```

#### Solution

```javascript
const countAndSay = (n) => {
  if (n === 1) { return '1'; }
  const say = str => {
    let idx = 0;
    let newStr = '';
    while (idx < str.length) {
      let occurences = 1;
      while (str[idx + 1] && str[idx + 1] === str[idx]) {
        idx++;
        occurences++;
      }
      newStr += occurences + str[idx];
      idx++
    }
    return newStr;
  };
  return say(countAndSay(n - 1));
};
```

## Review

[Micro frontends—a microservice approach to front-end web development - Medium](https://medium.com/@tomsoderlund/micro-frontends-a-microservice-approach-to-front-end-web-development-f325ebdadc16)

As frontend codebase continue to get more complex over the years, we see a growing need for more scalable architectures. We need to be able to draw clear boundaries that establish the right levels of coupling and cohesion between technical and domain entities. We should be able to scale software delivery across independent, autonomous teams.

While far from the only approach, we have seen many real-world cases where micro frontends deliver these benefits, and we’ve been able to apply the technique gradually over time to legacy codebases as well as new ones. Whether micro frontends are the right approach for you and your organization or not, we can only hope that this will be part of a continuing trend where frontend engineering and architecture is treated with the seriousness that we know it deserves.

## Technique

JavaScript empty check.

```javascript
/**
 * Returns true if the value is an empty object, collection, has no enurmerable properties or is any type that is not considered a collection.
 * Check if the provided value is `null` or if its `length` is equal to `0`.
 * @param {Object} val
 * @returns {Boolean}
 */
const isEmpty = val *=>* val == null || !(*Object*.keys(val) || val).length;
```

## Share

Keep your code clean from keep your functions as single responsibility.