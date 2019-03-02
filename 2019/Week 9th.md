# Week 9th

## Algorithm

### [551. Student Attendance Record I](https://leetcode.com/problems/student-attendance-record-i/)

#### Description

You are given a string representing an attendance record for a student. The record only contains following three characters:

1. **A**: Absent.
2. 2. **L**: Latee.
3. 3. **P**: Present.

A student could be rewarded if his attendance record doesn’t contain **more than one ‘A’ (absent)** or **more than two ‘L’ (late)**.

You need to return whether the student could be rewarded according to his attendance record.

#### Example 1

```javascript
Input: "PPALLP"
Output: true
```

#### Example 2

```javascript
Input: "PPALLL"
Output: false
```

#### Solution

```javascript
/**
 * ## Description
 *
 * You are given a string representing an attendance record for a student. The record only contains following three characters:
 *
 * 1. **A**: Absent.
 * 2. **L**: Late.
 * 3. **P**: Present.
 *
 * A student could be rewarded if his attendance record doesn't contain **more than one 'A' (absent)** or **more than two 'L' (late)**.
 *
 * You need to return whether the student could be rewarded according to his attendance record.
 *
 * ## Example 1
 *
 * ```javascript
 * Input: "PPALLP"
 * Output: true
 * ```
 *
 * ## Example 2
 *
 * ```javascript
 * Input: "PPALLL"
 * Output: false
 * ```
 * @param {String} s
 * @returns {Boolean}
 */
const checkRecord = (s) => {
  if (s.includes('LLL'))  return false;
  if (s.indexOf('A') !== s.lastIndexOf('A')) return false;
  return true;
}

const attendances = 'LALL';
const isRewarded = checkRecord(attendances);
console.log(isRewarded);
```


## Review

[The future of JavaScript state management is less state management…](https://medium.com/@amcdnl/the-future-of-javascript-state-management-is-less-state-management-ba1d97b99308)

Many times I create a state on that state tree, I ask myself do I really need it?  

Every time I create a project, I ask myself, do I need the state tree?

The way we think frontend went from single page to massive project. From   jump link to SPA. what about next? What we really need? 

I don’t have the answer now. I’m gonna find them out.

## Technique

find all own functions in an object.  

```javascript
/**
 * Returns an array of function property names from own (and optionally inherited) enumerable properties of an object.
 * Use `Object.keys()` to iterate over the object's own properties. If `inherited` is `true`, use `Object.getPrototypeOf()` to also get the object's inherited properties.
 * Use `Array.prototype.filter()` to keep only those properties that are functions.
 * Omit the second argument, `inherited`, to not include inherited properties by default.
 * @param {Object} obj
 * @param {Boolean} inherited
 * @returns {Array}
 */
const functions = (obj, inherited = false) =>
  (inherited
    ? [...Object.keys(obj), ...Object.keys(Object.getPrototypeOf(obj))]
    : Object.keys(obj)
  ).filter(key => typeof obj[key] === 'function');

function Foo () {
  this.a = () => 1;
  this.b = () => 2;
}

Foo.prototype.c = () => 3;

const ninher = functions(new ~Foo~());
const inher = functions(new ~Foo~(), true);
console.log(JSON.stringify(ninher));
console.log(JSON.stringify(inher));

``` 

## Share
Develop your self is the fundamental skill if you want to become a successful developer.