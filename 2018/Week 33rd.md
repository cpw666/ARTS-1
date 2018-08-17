# Week 33rd
## Algorithm
### [561. Array Partition I](https://leetcode.com/problems/array-partition-i/description/)

#### Description
Given an array of **2n** integers, your task is to group these integers into **n** pairs of integers, say (a1, b1), (a2, b2), ..., (an, bn) which makes sum of min(ai, bi) for all *i* from *1* to *n* as large as possible.  

#### Example 1
```
Input: [1, 4, 3, 2]

Output: 4
Explanation: n is 2, and to maximum sum of pairs is 4 = min(1, 2) + min(3, 4).
```

#### Note:
1. **n** is a positive integer, which is in the range of [1, 10000]
2. All the integers in the array will be in the range of [-10000, 10000]

#### Solution 1
```javascript
const asc = (a, b) => a > b;
const reducer = (accumulator, current) => accumulator + current;
/**
 * Array Partition I
 * @param {Array} nums
 */
const arrayPairSum = nums => {
	nums.sort(asc);
	const minimum = nums.filter((digit, index) => {
		if (index === 0 || index % 2 === 0) {
			return digit;
		}
	});
	const maximun = minimum.reduce(reducer);
	return maximun;
};
```
Proved I'm wrong in this `[11, 41, -9046, 2047, 1118, 8477, 8446, 279, 4925, 7380, -1719, 3855]` test case, cause this array contains negative number, my `asc` function won't work in this;

#### Solution 2
```javascript
/**
 * Array Partition I
 * @param {Array} nums
 */
const arrayPairSum = nums => {
	const asc = (a, b) => a - b;
	const reducer = (accumulator, current) => accumulator + current;
	const minmumer = (digit, index) => index % 2 === 0;
	nums.sort(asc);
	const minimum = nums.filter(minmumer);
	const maximum = minimum.reduce(reducer);
	return maximum;
};
```
That's right. this is my solution.  

I figured it our from the **Hints**:

> try come example like 1, 2, 3, 4    

Aha, maximums come from the pairs' minimum number. So we  
1. order the array in `asc`
2. filter the pairs' minimum number and store into an array
3. sum the minimum number array
4. got the right answer

## Review
[How JavaScript works: memory management + how to handle 4 common memory leaks](https://blog.sessionstack.com/how-javascript-works-memory-management-how-to-handle-4-common-memory-leaks-3f28b94cfbec)  

[Tutorial – SessionStack Blog](https://blog.sessionstack.com/tagged/tutorial) this link to a series article on **How JavaScript Works**.  

Here is my review on the third post.    

Alexander talk about in the topic of:  
1. what is memory
- Giant array of flip-flop  
2. memory life time
- Allocate memory  
- Use memory  
- Release memory  
3. Release memory through **garbage collector**
- Reverence-counting garbage collection `can’t solve cycles creating`
- Mark-and-sweep algorithm
	- All variables are linked to root, window in browser, global in node
	- Variables those not linked to root, been **marked** as unneeded
	- **Sweep** those **marked** `Cycles are not a problem anymore`
4. Memory leaks
- Global variables
	1. Make sure to assign it as numb or reassign it once you done with it  
- Timers or callbacks
	1. When using observers, you need to make sure you make an explicit call to remove them once you are done with them
- Closures
	1. Once a scope for closures is created for closures in the same parent scope, the scope is shared.
- Our of DOM references

## Technique
[Circularly Linked List](https://github.com/charleserious/data-structures-and-algorithms-with-javascript/blob/master/LinkedLists/CircularlyLinkedLists/linkedList.test.js)  

A circularly linked list is similar to a singly linked list and has the same type of nodes. The only difference is that a circularly linked list, when created, has its head node’s next property point back to itself. This means that the assignment:  

```javascript
this.head.next = this.head;
```

is propagated throughout the circularly linked list so that every new node has its next property pointing to the head of the list. In other words, the last node of the list is always pointing back to the head of the list, creating a circular list, as show in figure shows blow.  

![Circularly Linked List](http://pc97r6al4.bkt.clouddn.com/circularly-linked-list.png)  

Not to say too much, this is my implementation:  

```javascript
class Node {
	constructor (element) {
		this.element = element;
		this.next = null;
	}
}

class LinkedList {
	constructor () {
		this.head = new Node('head');
	}

	remove (item) {
		const previousNode = this.findPrevious(item);
		if (previousNode != null) {
			previousNode.next = previousNode.next.next;
		}
	}

	findPrevious (item) {
		let currentNode = this.head;
		while (currentNode.next !== null && currentNode.next.element !== item) {
			currentNode = currentNode.next;
		}
		return currentNode;
	}

	display () {
		let currentNode = this.head;
		while (currentNode.next !== null) {
			console.log(currentNode.next.element);
			currentNode = currentNode.next;
		}
	}

	find (item) {
		let currentNode = this.head;
		while (currentNode.element !== item) {
			currentNode = currentNode.next;
		}
		return currentNode;
	}

	insert (element, item) {
		const node = new Node(element);
		const current = this.find(item);
		node.next = current.next;
		current.next = node;
	}
}

class circularlyLinkedList extends LinkList {
	constructor () {
		super();
		this.head = new Node('head');
		this.head.next = this.head;
	}

	display () {
		let currentNode = this.head;
		while (currentNode.next !== null && currentNode.next.element !== 'head') {
			console.log(currentNode.next.element);
			currentNode = currentNode.next;
		}
	}
}
```


## Share
Following [Stack Traces and Line Numbers that Make Sense](https://what-problem-does-it-solve.com/webpack/sourcemaps.html)  

We’re getting a better and better setup for developing and deploying our applications. We can organize our JavaScript and CSS, we can use third party libraries for both, can deploy to production in a proper way, and run tests. But we’re still missing something every other programming language has: stack traces.  

Stack traces tell us where in our code errors are happening. In most programming languages, when an uncaught error happens, we see some information about what line of code raised the error, as well as the path through the code that led to that error. Even in a language like C, we can do this. Not so in JavaScript.  

The reason is that the file we’re editing is not the file that’s being executed. Webpack is compiling all of our files together, as well as minifying them and including our third party libraries.  

Let’s see the problem in action.  

Add a `throw` to the function in `markdownPreviewer.js`, after `event.preventDefault()`.  

Re-run Webpack and open up `dev/index.html`, then open the JavaScript console, and then click the “Preview” button:  

![throw stack](http://pc97r6al4.bkt.clouddn.com/markdown-stact-trace.png)  

The error came from line 1 of our bundle. This is technically true, since our bundle is minified and all the code is on one line. Since we aren’t editing this file directly, we have no idea where this error came from in our original source code.  

The solution to this is a feature that most browsers support called *sourcemaps*.  

### Sourcemaps
If a sourcemap file exists, browsers know to look at it when giving you a stack trace. The sourcemap lets the browser tell us that the problem wasn’t in line 1 of our bundle, but on line 13 of `markdownPreviewer.js`.  

The possible values for `devtool` are many, and poorly documented. Since we have different configurations for production and development, we can use different sourcemap strategies. For production, we’ll use `source-map` as that contains the most information and is designed for production.  

In `webpack/production.config.js`:  
```javascript
const path 				= require('path');
const Merge 			= require('webpack-merge');
const BasicConfig = require('./basic.config');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = Merge(BasicConfig, {
	mode: 'production',
	output: {
		path: path.join(__dirname, '../production'),
		filename: '[chunkhash]-bundle.js'
	},
	devtool: 'source-map',
	plugins: [
		new MiniCssExtractPlugin({
			filename: '[chunkhash]-style.css'
		})
	]
});
```

For development, we want the fastest thing possible that shows the most information. I *think* that’s `inline-source-map`.  
```javascript
const path 				= require('path');
const Merge 			= require('webpack-merge');
const BasicConfig = require('./basic.config');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = Merge(BasicConfig, {
	mode: 'development',
	output: {
		path: path.join(__dirname, '../dev'),
		filename: 'bundle.js'
	},
	devtool: 'inline-source-map',
	plugins: [
		new MiniCssExtractPlugin({
			filename: 'style.css'
		})
	]
});
```

Run Webpack:
```shell
> yarn dev
```

```shell
yarn run v1.7.0
$ webpack --config ./webpack/development.config.js $npm_package_config_webpack_args
Hash: f0c74278f1204b6e96fd
Version: webpack 4.16.3
Time: 1220ms
Built at: 2018-08-15 14:25:05
     Asset       Size  Chunks             Chunk Names
 style.css    327 KiB    main  [emitted]  main
 bundle.js    204 KiB    main  [emitted]  main
index.html  693 bytes          [emitted]  
Entrypoint main = style.css bundle.js
[./css/styles.css] 39 bytes {main} [built]
[./js/index.js] 349 bytes {main} [built]
[./js/markdownPreviewer.js] 382 bytes {main} [built]
[./node_modules/webpack/buildin/global.js] (webpack)/buildin/global.js 489 bytes {main} [built]
    + 9 hidden modules
Child html-webpack-plugin for "index.html":
     1 asset
    Entrypoint undefined = index.html
    [./node_modules/html-webpack-plugin/lib/loader.js!./html/index.html] 815 bytes {0} [built]
    [./node_modules/webpack/buildin/global.js] (webpack)/buildin/global.js 489 bytes {0} [built]
    [./node_modules/webpack/buildin/module.js] (webpack)/buildin/module.js 497 bytes {0} [built]
        + 1 hidden module
Child mini-css-extract-plugin node_modules/css-loader/index.js!css/styles.css:
    Entrypoint mini-css-extract-plugin = *
    [./node_modules/css-loader/index.js!./css/styles.css] ./node_modules/css-loader!./css/styles.css 343 bytes {mini-css-extract-plugin} [built]
        + 1 hidden module
Child mini-css-extract-plugin node_modules/css-loader/index.js!node_modules/tachyons/css/tachyons.css:
    Entrypoint mini-css-extract-plugin = *
       2 modules
✨  Done in 2.58s.
```

And, if we follow the same steps in the browser, we’ll see that we can now see the line number where our error is coming from!  

![Stack trace sourcemap](http://pc97r6al4.bkt.clouddn.com/stact-trace-sourcemap.png)  

If you click the stark, it even shows you the code where the error came from!  

![Stack trace in line 10](http://pc97r6al4.bkt.clouddn.com/stact-trace-line-10.png)  

Nice!  

Let’s check our production configuration to make sure there’s no issue:  
```shell
> yarn prod
```

```shell
yarn run v1.7.0
$ webpack --config ./webpack/production.config.js $npm_package_config_webpack_args
Hash: 3193b965d696c040ec75
Version: webpack 4.16.3
Time: 2237ms
Built at: 2018-08-15 14:36:58
                             Asset       Size  Chunks             Chunk Names
    6256fd3676153f14b4b1-style.css    112 KiB       0  [emitted]  main
    6256fd3676153f14b4b1-bundle.js   25.5 KiB       0  [emitted]  main
6256fd3676153f14b4b1-style.css.map    162 KiB       0  [emitted]  main
6256fd3676153f14b4b1-bundle.js.map    113 KiB       0  [emitted]  main
                        index.html  735 bytes          [emitted]  
Entrypoint main = 6256fd3676153f14b4b1-style.css 6256fd3676153f14b4b1-bundle.js 6256fd3676153f14b4b1-style.css.map 6256fd3676153f14b4b1-bundle.js.map
 [3] ./css/styles.css 39 bytes {0} [built]
 [7] (webpack)/buildin/global.js 489 bytes {0} [built]
[11] ./js/index.js + 1 modules 746 bytes {0} [built]
     | ./js/index.js 349 bytes [built]
     | ./js/markdownPreviewer.js 382 bytes [built]
    + 9 hidden modules
Child html-webpack-plugin for "index.html":
     1 asset
    Entrypoint undefined = index.html
    [0] ./node_modules/html-webpack-plugin/lib/loader.js!./html/index.html 815 bytes {0} [built]
    [2] (webpack)/buildin/global.js 489 bytes {0} [built]
    [3] (webpack)/buildin/module.js 497 bytes {0} [built]
        + 1 hidden module
Child mini-css-extract-plugin node_modules/css-loader/index.js!css/styles.css:
    Entrypoint mini-css-extract-plugin = *
    [0] ./node_modules/css-loader!./css/styles.css 343 bytes {0} [built]
        + 1 hidden module
Child mini-css-extract-plugin node_modules/css-loader/index.js!node_modules/tachyons/css/tachyons.css:
    Entrypoint mini-css-extract-plugin = *
       2 modules
✨  Done in 3.77s.
```

What about our CSS? Sometimes it’s nice to know where certain styles are defined or where they came from.  
