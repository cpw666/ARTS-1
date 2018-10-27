# Week 43rd
## Algorithm
### [868. Binary Gap](https://leetcode.com/problems/binary-gap/description/)

#### Description
Given a positive integer `N`, find and return the longest distance between two consecutive 1's representation of `N`.  

If there aren't two consecutive 1's, return 0.  

#### Example 1
```
Input: 22
Output: 2
Explanation: 
22 in binary is 0b10110.
In the binary representation of 22, there are three ones, and two consecutive paires of 1's.
The first consecutive pair of 1's have distance 2.
The second consecutive pair of 1's have distance 1.
The answer is the largest of these two distances, which is 2.
```

#### Example 2
```
Input: 5
Output: 2
Explanation:
5 in binary is 0b101.
```

#### Example 3
```
Input 6
Output: 1
Explanation:
6 in binary is 0b110.
```

#### Example 4
```
Input: 8
Output: 0
Explanation:
8 in binary is 0b1000.
There aren't any consecutive paires of 1's in the binary representation of 8, so we return 0.
```

#### Note
- `1 <= N <= 10^9`

#### Solution
```javascript
/**
 * @param {Number} N
 * @returns {Number}
 */
const binaryGap = (N) => {
	let max = 0;
	let position = 0;
	let lastPosition = -1;
	while (N !== 0) {
		position++;
		if ((N & 1) === 1) {
			if (lastPosition !== -1) {
				max = Math.max(max, position - lastPosition);
			}
			lastPosition = position;
		}
		N >>= 1;
	}
	return max;
};

const N = 22;
const gap = binaryGap(N);
console.log(gap);
```

## Review
[Glossary of Modern JavaScript Concepts: Part 1](https://auth0.com/blog/glossary-of-modern-javascript-concepts/)  

This is a post about almost all the modern concepts in frond end development, including programming diagram, functional programming, reactive programming, functional reactive programming, purity, statefulness and statelessness, immutability and mutability, imperative and declarative programming, high-order functions, observables.  

So this post to me is a key unlock  the fundamentals of frontend programming world. 

## Technique
Vue.js 2 component’s share Websocket using props:
```html
<router-view :socket="ws"></router-view>
```

```vue
{
	props: {
		socket: WebSocket
	}
}
```

## Share
JavaScript Closure: A closure is the combination of a function and the lexical environment within that function was declared. This environment consist of any local variables that were in-scope at the time the closure was created. And lexical scope is that nested functions have access to the variables of their outer functions/scope.