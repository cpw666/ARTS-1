# Week 22

## Algorithm

# [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

## Description

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

## Note

For the purpose of this problem, we define empty string as valid palindrome.

## Example 1

```example
Input: "A man, a plan, a canal: Panama"
Output: true
```

## Example 2

```example
Input: "race a car"
output: false
```

## Solution

With JavaScript Array, things get easy.

```javascript
/**
 * @param {String} s
 * @return {Boolean}
 */
const isPalindrome = (s) => {
  const forward = s.replace(/\W/g, '').toLowerCase();
  const backward = [...forward].reverse().join('');
  return forward === backward;
};
```


## Review

[Behavior Driven Development (BDD) and Functional Testing](https://medium.com/javascript-scene/behavior-driven-development-bdd-and-functional-testing-62084ad7f1f2)  

- **Don’t alter the DOM.** If you do, your test runner (e.g., TestCafe) may not be able to understand how the DOM changed, and the DOM alteration could impact the other assertions which may be relying on the DOM output.
- **Don’t share mutable state between tests.** Because they’re so slow, it’s incredibly important that functional tests can be run in parallel, and the can’t do that deterministically if they’re competing for the same shared mutable state, which could cause nondeterminism due to race conditions. Because you’re running system tests, keep in mind that if you’re modifying user data, you should have different test user data in the database for different test so they don’t randomly fail due to race conditions.
- **Don’t mix functional tests in with unit tests.** Unit tests and functional tests should be written from different perspectives, and run at different times. Unit tests should be written from the developer’s perspective and run every time the developer makes a change, and should complete in less than 3 seconds. Functional tests should be written from the user’s perspective, and involve asynchronous I/O which can make test runs too slow for a developer’s immediate feedback on every code change. It should be easy to run the unit tests without triggering functional test runs.
- **Do run tests in headless mode,**if you can, which means that the browser UI doesn’t actually need to be launched, and tests can run faster. Headless mode is a great way to speed up most functional tests, but there is a small subset of tests which can’t be run in headless mode, simply because the functionality they rely on doesn’t work in headless mode. Some CI/CD pipelines will require you to run functional tests in headless mode, so if you have some tests which can’t run in headless mode, you may need to exclude them from the CI/CD run. Be sure the quality team is on the lookout for that scenario.
- **Do run tests on multiple devices.**Do your tests still pass on mobile devices? TestCafe can run on remote browsers without installing TestCafe to the remote devices. However, screenshot functionality does not work on remote browsers.
- **Do grab screenshots on test failures.**It can be useful to take a screenshot if your tests fail to help diagnose what went wrong. TestCafe studio has a run configuration option for that.
- **Do keep your functional test runs under 10 minutes.**Any longer will create too much lag between the developer working on a feature and fixing something that went wrong. 10 minutes is long enough for a developer to get busy working on the next feature, and if the test fails after longer than 10 minutes, it will likely interrupt the developer who has moved on to the next task. An interrupted task takes an average of [twice as long to complete and contains roughly twice as many errors](https://dl.acm.org/citation.cfm?doid=985692.985715) . TestCafe allows you to run many tests concurrently, and the remote browser option can do so across a fleet of test servers. I recommend taking advantage of those features to keep your test runs as short in duration as possible.
- **Do halt the continuous delivery pipeline when tests fail.**One of the great benefits of automated tests is the ability to protect your customers against regressions — bugs in features that used to work. This safety net process can be automated so that you have good confidence that your release is relatively free of bugs. Tests in the CI/CD pipeline effectively eliminates a development team’s fear of change, which can be a serious drain on developer productivity.


## Technique

String permutations

```javascript
/**
 * WARNING: This function's execution time increase exponentially with each character. Anything more than 8 to 10 characters will cause your browser to hang
 * as it tries to solve all the different combinations.
 *
 * Generates all permutations of a string (contains duplicates).
 * Use recursion. For each letter in the given string, create all the partial permutations for the rest of its letters.
 * Use `Array.prototype.map()` to combine the letter with each partial permutation,
 * then `Array.prototype.reduce()` to combine all permutations in one array. Base cases are for string `length` equal to `2` or `1`.
 * @param {String} str
 * @returns {Array}
 */
const stringPermutations = str => {
  if (str.length <= 2) return str.length === 2 ? [str, str[1] + str[0]] : [str];
  return str
    .split('')
    .reduce(
      (acc, letter, i) =>
        acc.concat(stringPermutations(str.slice(0, i) + str.slice(i + 1)).map(val => letter + val)),
      []
    )
};
```

## Share

Refactor show make your code more robustness.
