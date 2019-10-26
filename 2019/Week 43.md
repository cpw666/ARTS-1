# Week 43

## Algorithm

### [204. Count Primes](https://leetcode.com/problems/count-primes/)

## Description

Count the number of prime numbers less than a non-negative number, **n**.

#### Example

```example
Input: 10
Output: 4
Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.
```

#### Hint

#### Hint 1

Let's start with a `isPrimve` function, To determine if a number is prime, we need to check if it is not divisible by any number less than *n*. The runtime complexity of `isPrime` function would be **O(n)** and hence counting the total prime numbers up to *n* would be **O(n^2)**. Could we do better?

#### Hint 2

As we know the number must not be divisible by any number > n / 2, we can immediately cut the total iterations half by dividing only up to *n / 2*. Could we still do better?

#### Hint 3

Let’s write down all of 12’s factor:

2 x 6 = 12

3 x 4 = 12

4 x 3 = 12

6 x 2 = 12

As you can see, calculations of 4 x 3 and 6 x 2 are not necessary. Therefore, we only need to consider factors up to √n because, if *n* is divisible by some number *p*, then *n = p x q* and since *p <= q*, we could derive that *p <= √n*

Our total runtime has now improved to **O(n^1.5)**, which is slightly better, Is there a faster approach?

```java
public int countPrimes(int n) {
  int count = 0;
  for (int i = 1; i < n; i++) {
    if (isPrime(i)) count++
  }
  return count;
}
```

```java
private boolean isPrime(int num) {
  if (num <= 1) return false;
  for (int i = 2; i * i <= num; i++) {
    if (num % i == 0) return false;
  }
  return true;
}
```

#### Hint 4

The [Sieve of Eratosthenes](http://en.wikipedia.org/wiki/Sieve_of_Eratosthenes) is one of the efficient ways to find all prime numbers up to *n*. But don’t let that name scare you, I promise that the concept is surprisingly simple.

![Sieve of Eratosthenes](https://leetcode.com/static/images/solutions/Sieve_of_Eratosthenes_animation.gif)

*Sieve of Eratosthenes: algorithm steps fro primes below 121. “[Sieve of Eratosthenes Animation](https://commons.wikimedia.org/wiki/File:Sieve_of_Eratosthenes_animation.gif)" by [SKopp](http://de.wikipedia.org/wiki/Benutzer:SKopp) is licensed under [CC BY 2.0](http://creativecommons.org/licenses/by/2.0/)*

We start off with a table of *n* numbers. Let’s look at the first number, 2. We know all multiples of 2 must not be primes, so we mark them off as non-primes. The we look at the next number, 3. Similarly, all multiples of 3 such as 3 x 2 = 6, 3 x 3 = 9, … nyst bit be orunesm is we mark them off as well. Now we look at the next number. 4, which was already marked off. What does this tell you? Should you mark off all multiples of 4 as well?

#### Hint 5

4 is not a prime because it is divisible by 2, which means all multiples of 4 must also be divisible by 2 and were already marked off. So we can skip 4 immediately and go to the next number 5. Now, all multiples of 5 such 5 x 2 = 10, 5 x 3 = 15, 5 x 4 = 20, 5 x 5 = 25, … can be marked off. There is a slight optimization here, we do not need to start from 5 x 2 = 10. Where should we start marking off?

#### Hint 6

In fact, we can mark off multiples of 5 starting 5 x 5 = 25, because 5 x 2 = 10 was already marked off by multiple of 2, similarly 5 x 3 = 15 was already marked off by multiple of 3. Therefore , if the current number is *p*, we can always mark off multiples of *p* starting at *p^2*, then increments of *p: p^2 + p, p^2 + 2p, …* Now what should be the terminating loop condition?

#### Hint 7

It is easy to say that the terminating loop condition is *p < n*, which is certainly correct but not efficient. Do you still remember Hint #3?

#### Hint 8

Yes, the terminating loop condition can be *p < √n*, as all non-primes >= √n must have already been marked off. When the loop terminates, all the numbers in the table that are non-marked are prime.

The Sieve of Eratosthenes uses an extra O(n) memory and its runtime complexity is O(n log log n). For the more mathematically inclined readers, you can read more about its algorithm complexity on [Wikipedia](http://en.wikipedia.org/wiki/Sieve_of_Eratosthenes#Algorithm_complexity).

```java
public int countPrimes (int n) {
  boolean [] isPrime = new Boolean[n];
  for (int i = 2; i < n; i++) {
    isPrime[i] = true;
  }
  // Loop’s ending condition is i * i < n instead of i < sqrt(n)
  // to avoid repeatedly calling an expensive function sqrt().
  for (int i = 2; i * i < n; i++) {
    if (!isPrime[i]) continue;
    for (int j = i * i; j < n; j += 1) {
      isPrime[j] = false;
    }
  }
  int count = 0;
  for (int i = 2; i < n; i++) {
    if (isPrime[i]) count++;
  }
  return count;
}
```

#### Solution

```javascript
/**
 * @param {Number} n
 * @returns {Number}
 */
const countPrimes = n => {
  if (n < 3) {
    return 0;
  }

  const sieve = new Array(n).fill(true);
  sieve[0] = sieve[1] = false;

  for (let i = 4; i < n; i += 2) {
    sieve[i] = false;
  }

  const max = Math.floor(Math.sqrt(n));

  for (let i = 3; i <= max; i += 2) {
    if (!sieve[i]) {
      continue;
    }

    for (let j = i * i; j < n; j += i) {
      sieve[j] = false;
    }
  }

  return sieve.reduce((fold, current) => current ? fold + 1 : fold, 0);
};
```

## Review

[Behavior Driven Development (BDD) and Functional Testing](https://medium.com/javascript-scene/behavior-driven-development-bdd-and-functional-testing-62084ad7f1f2)

Dos and Don’ts of Functional Tests

- Don’t alter the DOM. If you do, you test runner (e.g. TestCafe) may not be able to understand how the DOM changed, and that DOM alteration could impact the other assertions which may be relaying on the DOM output.
- Don’t share mutable state between tests. Because they’re so slow, it’s incredibly important that functional tests can be run in parallel, and the can’t do that deterministically if they’re competing for the same shared mutable state, which could cause nondeterminism due to race conditions. Because you’re running system tests, keep in mind that if you’re modifying user data, you should have different user data in the database for different tests so they don’t randomly fail due to race coiditions.
- Don’t mix functional tests in with unit tests. Unit tests and functional tests should be written from different perspectives, and at different times. Unit tests should be written from the developer's perspective and run every time the developer makes a change, and should complete in less than 3 seconds. Functional tests should be written from the user’s perspective, and involve asynchronous I/O which can make test runs too slow for a developers immediate feedback on every code change. It should be easy to run the unit tests without triggering functional test runs.
- Do run tests in headless mode, if you can, which means that the browser UI doesn’t actually need to be launched, and tests can run faster. Headless mode is a great way to speed up most functional tests, but there is a small subset of tests which can't be run in headless mode, simply because the funtionality they rely on doesn’t work in headless mode. Some CI/CD pipelines will require you to run functional tests in headless mode, so if you have some tests which can’t run in headless mode, you may need to exclude them from the CI/CD run. Be sure the quality team is on the lookout for that scenario.
- Do run test on multiple devices. Do your tests still pass on mobile devices? TestCafe can run on remote browsers without installing TestCafe to the remote devices. However, screenshot functionality does not work on remote browsers.
- Do grab screenshots on test failures. It can be useful to take a screenshot if your test fail to help diagnose what went wrong. TestCafe studio has a run configuration option for that.
- Do keep your functional test runs under 10 minutes. Any longer will create too much lag between the developer working on a feature and fixing something that went wrong. 10 minutes is long enough for a developer to get busy working on the next feature, and if the test fails after longer than 10 minutes, it will likely interrupt the developer who has moved on to the next task. An interrupted task takes an average of twice as long to complete and contains roughly twice as many errors. TestCafe allows you to run many tests concurrently, and the remote browser option can do so across a fleet of test servers. I recommend taking advantage of those features to keep your test runs as short in duration as possible.
- Do halt the continuous delivery pipeline when tests fail. One of the great benefits of automated tests in the ability to protect your customers against regressions — bugs in features that used to work. This safety net process can be automated so that you have good confidence that your release is relatively free of bugs. Tests in CI/CD pipeline effectively eliminate a development team’s fear of change, which can be a serious drain on develop productivity.

## Technique

### Popout menu

#### [Check me out](https://codepen.io/charleserious/pen/ZEEyKqK)

Reveals an interactive popout menu on hover and focus.

```html
<!DOCTYPE html>
<html lang=“en”>
<head>
  <meta charset=“UTF-8”>
  <meta name=“viewport” content=“width=device-width, initial-scale=1.0”>
  <meta http-equiv=“X-UA-Compatible” content=“ie=edge”>
  <link rel="stylesheet” href=“./main.css”>
  <title>Popout menu</title>
</head>
<body>
  <div class=“reference” tabindex=“0”>
    <div class=“popout-menu”>Popout menu</div>
  </div>
</body>
</html>
```

```css
html, body {
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
}

body {
  display: flex;
  flex-flow: column nowrap;
  align-items: center;
  justify-content: center;
}

.reference {
  position: relative;
  background: tomato;
  width: 100px;
  height: 100px;
}

.popout-menu {
  position: absolute;
  visibility: hidden;
  left: 100%;
  background-color: #333;
  color: #fff;
  padding: 15px;
}

.reference:hover > .popout-menu,
.reference:focus > .popout-menu,
.reference:focus-within > .popout-menu {
  visibility: visible;
}
```

#### Explanation

1. `position: relative` on the reference parent establishes a Cartesian positioning context for its child.
2. `position: absolute` takes the popout menu out of the flow of the document and positions it in relation to the parent.
3. `left: 100%` moves the popout menu 100% of the parent’s width from the left.
4. `visibility: hidden` hides the popout menu initially and allows for transitions (unlike `display: none`).
5. `.reference:hover > .popout-menu` means that when `.renference` is hovered over, select immediate children with a class of `.popout-menu` and change their `visibility` to `visible`, which shows the popout.
6. `.reference:focus > .popout-menu` means that when `.reference` is focused, that popout would be shown.
7. `.reference:focus-within > .popout-menu` ensures that the popout is shown when the focus is *within* the reference.

## Share
Don’t waste your time in a company that those professors don’t go.