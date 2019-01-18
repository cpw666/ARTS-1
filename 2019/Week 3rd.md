# Week 3rd
## Algorithm

### [937. Reorder Log Files](https://leetcode.com/problems/reorder-log-files/)

#### Description

You have an array of `logs`. Each log is a space delimited string of words.  

For each log, the first word in each log is an alphanumeric *identifier*. Then, either:

- Each word after the identifier will consist only of lowercase letters, or;
- Each word after the identifier will consist only of digits.

We will call these two varieties of logs *letter-logs* and *digit-logs*. It is guaranteed that each log has at least one word after its identifier.  

Reorder the logs so that all of the letter-logs come before any digit-log. The letter-logs are ordered lexicographically ignoring identifier, with the identifier used in case of ties. The digit-logs should be put in their original order.  

Return the final order of the logs.

#### Example

```javascript
Input: ['a1 9 2 3 1', 'g1 act car', 'zo4, 4 7', 'ab1 off key dog', 'a8, act, zoo']
Output: ['g1 act car', 'a8, act, zoo', 'ab1 off key dog', 'a1 9 2 3 1', 'zo4, 4 7']
```

#### Note

1. `0 <= logs.length <= 100`
2. `3 <= logs[i].length <= 100`
3. `logs[i]` is guaranteed to have an identifier, and two words after the identifier

#### Solution

```javascript
const reorderLogFiles = (logs) => {
  const isDigitalLog = log => (/[0-9]/i).test(log[log.indexOf(' ') + 1]);
  const digitalLogs = logs.filter(log => isDigitalLog(log));
  const letterLogs = logs.filter(log => !isDigitalLog(log));
  const sorttor = (a, b) => {
    const aWithoutId = a.substr(a.indexOf(' '), a.length);
    const bWithoutId = b.substr(b.indexOf(' '), b.length);
    return aWithoutId.localeCompare(bWithoutId);
  }
  letterLogs.sort(sorttor);
  return [...letterLogs, ...digitalLogs];
}

const logs = ['a1 9 2 3 1', 'g1 act car', 'zo4, 4 7', 'ab1 off key dog', 'a8, act, zoo'];
const orderedLogs = reorderLogFiles(logs);
console.log(JSON.stringify(logs));
console.log(JSON.stringify(orderedLogs));
```

## Review

[The Top 5 CSS Gotchas, and a few bonus… – Spyros Argalias – Medium](https://medium.com/@sargalias/the-top-5-css-gotchas-and-a-few-bonus-d39755c79527)  

Try to understand CSS well now, with using the monster many years, not quite yet get the soul.  

CSS may be a tricky technique,  all because I don’t fully understand the behavior.

## Technique

In case we need safe integer in JavaScript

```javascript
const toSafeInteger = num =>
  Math.round(Math.max(Math.min(num, Number.MAX_SAFE_INTEGER), Number.MIN_SAFE_INTEGER));

const s3d2 = toSafeInteger(3.2);
const sInfi = toSafeInteger(Infinity);
console.log(s3d2);  // 3
console.log(sInfi); // 007199254740991
```

## Share

Pipeline  
In computer a **pipeline**, aka **data pipeline**, is a set of data processing element connected in series, where the output of one element is the input of the next one.

What a nice friend of functional programming.
 