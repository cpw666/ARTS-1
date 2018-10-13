# Week 41st
## Algorithm
### [893. Groups of Special-Equivalent Strings](https://leetcode.com/problems/groups-of-special-equivalent-strings/description/)

#### Description
You are given an array `A` of strings.  
Two strings `S` and `T` are *special-equivalent* if after any number of *moves*, `S == T`.  
A *move* consists of choosing two indices `i` and `j` with `i % 2 == j % 2`, and swapping `S[i]` with `S[j]`.  
Now, a group of special-equivalent strings from `A` is a non-empty subset of `A` such that any string not in `S` is not special-equivalent with any string in `S`.  
Return the number of groups of special-equivalent strings from `A`.  

#### Example 1
```
Input: ['a', 'b', 'c', 'a', 'c', 'c']
Output: 3
Explanation: 3 groups ['a', 'a'], ['b'], ['c', 'c', 'c']
```

#### Example 2
```
Input: ['aa', 'bb', 'ab', 'ba']
Output: 4
Explanation: 4 groups ['aa'], ['bb'], ['ab'], ['ba']
```

#### Example 3
```
Input: ['abc', 'acb', 'bac', 'bca', 'cab', 'cba']
Output: 3
Explanation: 3 groups ['abc', 'cba'], ['acb', 'bca'], ['bac', 'cab']
```

#### Example 4
```
Input: ['abcd', 'cdab', 'adcb', 'cbad']
Output: 1
Explanation: 1 group ['abcd', 'cdab', 'adcb', 'cbad']
```

#### Note
- `1 <= A.length <= 1000`
- `1 <= A[i].length <= 20`
- All `A[i]` have the same length.
- All `A[i]` consist of only lowercase letters.

#### Solution
```javascript
/**
 * I am practicing pure function.
 * And try to comments my function with WHY
 * @param {Array} A
 * @returns {Number}
 */
const numSpecialEquivGroups = (A) => {
	/**
	 * need odd character of every element in the `A` array
	 * @param {Array} A
	 * @returns {Array}
	 */
	const odder = (A) => {
		return A.map(w => {
			return [...w].reduce((a, c, i) => {
				return a + (i % 2 === 0 ? c : '');
			}, '');
		});
	};
	/**
	 * need ever character of every element in the `A` array
	 * @param {Array} A
	 * @returns {Array}
	 */
	const evener = (A) => {
		return A.map(w => {
			return [...w].reduce((a, c, i) => {
				return a + (i % 2 !== 0 ? c : '');
			}, '');
		});
	};
	/**
	 * need to sort as the same order
	 * @param {Array} list
	 * @returns {Array}
	 */
	const sorter = (list) => {
		return list.map(w => {
			return [...w].sort().join('');
		});
	};
	/**
	 * combine `odd` and `even` array into one list,
	 * Set is for unique element.
	 * So that size of set is the group of special-equivalent.
	 * @param {Array} odd
	 * @param {Array} even
	 * @returns {Set}
	 */
	const combine = (odd, even) => {
		const list = odd.map((w, i) => {
			return w + even[i];
		});
		const set = new Set();
		for (let w of list) {
			set.add(w);
		}
		return set;
	};
	const odd = odder(A);
	const even = evener(A);
	const oddOrdered = sorter(odd);
	const evenOrdered = sorter(even);
	const set = combine(oddOrdered, evenOrdered);
	return set.size;
};

const incoming = ['abc', 'acb', 'bac', 'bca', 'cab', 'cba']; // ['aa', 'bb', 'ab', 'ba'];
const outcoming = numSpecialEquivGroups(incoming);
console.log(outcoming);
```


## Review
[JavaScript Modules: A Beginner’s Guide – freeCodeCamp.org](https://medium.freecodecamp.org/javascript-modules-a-beginner-s-guide-783f7d7a5fcc)  
[JavaScript Modules Part 2: Module Bundling – freeCodeCamp.org](https://medium.freecodecamp.org/javascript-modules-part-2-module-bundling-5020383cf306?source=bookmarks---------0---------------------&gi=afdaaf05e480)  
This week we back to JavaScript Modules, from history till nowadays ES6 module.  

We all know JavaScript can run in backend (node) and frontend (browsers), so module patterns also divide into these two domains.  
CommonJS
```javascript
// myModule.js
function myModule () {
	this.hello = function () {
		return 'hello!';
	}

	this.goodbye = function () {
		return 'goodbye!'
	}
}

// testMyModule.js
var myModule = require('myModule');
var myModuleInstance = new myModule();
myModuleInstance.hello();		// hello!
myModuleInstance.goodbye();	// goodbye!
```

AMD/Asynchronous Module Definition
```javascript
// myModule.js
define([], function () {
	return {
		hello: function () {
			return 'hello!';
		},

		goodbye: function () {
			return 'goodbye!'
		}
	};
});

// testMyModule.js
define(['myModule', 'myOtherModule'], function (myModule, myOtherModule) {
	console.log(myModule.hello());
});
```

UMD/Universal Module Definition
```javascript
(function (root, factory) {
	if (typeof define === 'function' && define.amd) {
		// AMD
		define(['myModule', 'myOtherModule'], factory);
	} else if (typeof exports === 'object') {
		// CommonJS
		module.exports = factory(root.myModule, root.myOtherModule);
	} else {
		root.returnExports = factory(root.myModule, root.myOtherModule);
	}
}(this, function (myModule, myOtherModule) {
	// Methods
	function privateMethods() {};

	function hello () {
		return 'hello!';
	}

	function goodbye () {
		return 'goodbye!'
	}

	return {
		hello: hello,
		goodbye: goodbye
	};
}));
```

ES6
```javascript
// counter.js
export let counter = 1;
export function increment () {
	counter++;
}

export funciton decrement () {
	counter--;
}

// main.js
import * as counter from 'counter';
console.log(counter.counter); // 1
counter.increment()
console.log(counter.counter); // 2
```

Native Script/ES6 will win this module battle, of cause for a long time battle.  


## Technique
Using `ocLazyLoad` in `angular.js` to loading  page dependancies, such as module, that module should be a “pure” `angular.module` function call, also can be wrapped into an IIFE, but can’t be wrapped into AMD or CommonJS wrapper, and of cause not for UMD wrapper.

**WRONG**  
```javascript
(function (root, factory) {
  'use strict';
  if (typeof module !== 'undefined' && module.exports) {
    // CommonJS
    module.exports = factory(require('angular'));
  } else if (typeof define === 'function' && define.amd) {
    // AMD
    define(['angular'], factory);
  } else {
    // Global Variables
    factory(root.angular);
  }
}(window, function (angular) {
  'use strict';
	angular.module('angucomplete-alt',[]).directive('angucompleteAlt', [funciton () {

	}]);
}));
```

**CORRECT**
```javascript
(function (angular) {
	'use strict';
	'use strict';
	angular.module('angucomplete-alt',[]).directive('angucompleteAlt', [funciton () {

	}]);
})(window.angular)
```

## Share
Some definitions on declarative programming.
- Declarative programming is “the act of programming in languages that conform to mental model of the developer rather than the operational model of the machine”.
- Declarative programming is programming with declarations, *i.e. declarative sentences*.
- The declarative property is where there can exist only one possible set of statements that can express each specific modular semantic. The imperative property is the dual, where semantics are inconsistent under composition and/or can be expressed with variations of sets of statements.
- Declarative languages contrast with imperative languages which **specify explicit manipulation of the computer’s internal state**; or procedural languages which specify an explicit sequence of step to follow.
- In computer science, declarative programming is a programming paradigm that expresses the logic of a computation without describing its control flow.
