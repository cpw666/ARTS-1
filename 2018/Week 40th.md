# Week 40th
## Algorithm
### [821. Shortest Distance to a Character](https://leetcode.com/problems/shortest-distance-to-a-character/description/)

#### Description
Given a string `S` and a character `C`, return an array of integers representing the shortest distance from the character `C` in the string.  

#### Example
```
Input: S = 'loveleetcode', C = 'e'
Output: [3, 2, 1, 0, 1, 0, 0, 1, 2, 2, 1, 0]
```

#### Note
1. `S` string length is `[1, 10000]`.
2.  `C` is a single character, and guaranteed to be in string `S`.
3. All letters in `S` and `C` are lowercase.

#### Solution
```javascript
const shortestToChar = (S, C) => {
	let distances = [];
	let cPointer = -1;
	// calc left
	for (let i = 0; i < S.length; i++) {
		if (S.charAt(i) === C) {
			cPointer = i;
		}
		if (cPointer < 0) {
			distances.push(S.length);
		} else {
			distances.push(i - cPointer);
		}
	}
	// calc right
	cPointer = -1;
	for (let i = S.length - 1; i >= 0; i--) {
		if (S.charAt(i) === C) {
			cPointer = i;
		}
		if (cPointer >= 0) {
			distances[i] = Math.min(distances[i], cPointer - i);
		}
	}
	return distances;
};

const S = 'loveleetcode';
const C = 'e';
const result = shortestToChar(S, C);
console.log(result);
```
Calculate two times from both side of string `S`,  
compare each times and get the min distance.  

## Review
[Master the JavaScript Interview: What is a Pure Function?](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-pure-function-d1c076bec976#.kt48h2bfa)  

A pure function is much easier to comprehend, especially as our codebase may scale, pure functions don’t modify external variables/state/data outside of the scope, and returns the same output given the same input.  

Pure functions are the best implementation of KISS, keep it simple and stupid.  

## Technique
Improve UX with reading article on [极客时间](https://time.geekbang.org/column).  
Move mini audio player fixed on bottom. This is the first version, just move its position, a lot  more requirement will come later this year.  
```javascript
// ==UserScript==
// @name         GeekTime Audio Player
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  time.geekbang.org reading exprience optimization
// @author       Charleserious
// @match        *://time.geekbang.org/column/*
// @grant        none
// ==/UserScript==

(function() {
	'use strict';

	// Your code here...
	const audioPlayer = () => {
		const player = document.querySelector('.mini-audio-player');
		player.style.width = '16rem';
		player.style.height = '5.25rem';
		player.style.position = 'fixed';
		player.style.bottom = '1rem';
		player.style.right = '1rem';
		player.style.left = 'auto';
		player.style.marginBottom = '0rem';
		player.style.borderColor = '#E57C39';
		player.style.borderRadius = '0.5rem';
	}

	const app = document.querySelector('#app');
	const config = { attribute: true, childList: true, subtree: true };
	const handler = (mutations) => {
		for (let mutation of mutations) {
			if (mutation.type !== 'childList') {
				continue;
			}
			if (mutation.removedNodes.length > 0 ) {
				continue;
			}
			if (mutation.addedNodes.length < 1) {
				continue;
			}
			const node = mutation.addedNodes[0];
			const classes = node.classList;
			if (classes && classes.contains('main-app')) {
				audioPlayer();
			}
		}
	}
	const ovserver = new MutationObserver(handler);
	ovserver.observe(app, config);
})();
```

## Share
I need to learn harder, in case of being abandoned by the times, and basic knowledge changes slow in computer science.  
