# Week 29th
## Algorithm
### [461. Hamming Distance](https://leetcode.com/problems/hamming-distance/description/)

### Description
The [Hamming distance](https://en.wikipedia.org/wiki/Hamming_distance) between two integers is the number of positions at which the corresponding bits are different.  
Given two integers x and y, calculate the Hamming distance

### Note
0 ≤ x, y < 2^31.

### Example
```
Input: x = 1, y = 4;
Output: 2

Explanation:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑

The above arrows point to positions where the corresponding bits are different.
```


### Solution
```javascript
/**
 * convert given number into it's corresponsding bits.
 * @param {number} number
 * @returns {string} bits
 */
const convertToBits = (number) => {
	const bits = number.toString(2);
	return bits;
};

/**
 * prepend 0 on given bits reach the given length
 * @param {string} bits
 * @param {number} length
 */
const unshiftBits = (bits, length) => {
	const full = new Array((length - bits.length) + 1).join(0) + bits;
	return full;
};

/**
 * @param {number} x
 * @param {number} y
 * @returns {number}
 */
const hammingDistance = (x, y) => {
	const length = 31;
	const xbits = convertToBits(x);
	const ybits = convertToBits(y);
	let xFull = unshiftBits(xbits, length);
	let yFull = unshiftBits(ybits, length);
	let difference = 0;
	for (let i = 0; i < length; i++) {
		if (xFull[i] !== yFull[i]) {
			difference += 1;
		}
	}

	return difference;
};
```

I initially don't understand this problem, till I figure what is Hamming distance.  
So it's a string manipulation problem.  
First get corresponding bits of x and y.  
Second prepending 0 on the bits, length = 31 is because 32 bits will be represented as EPSILON, as noted in [Note](#note).  
And now, we compare the difference and added it up;  
  
But what the heck of other submission do with [XOR](https://leetcode.com/problems/hamming-distance/discuss/94698/Java-1-Line-Solution-:D), I should learn these awesome skills now.


## Review
[Web Workers: Concurrency in JavaScript](https://medium.com/@soshace/web-workers-concurrency-in-java-script-6ed365821944)
This week I wanna talk about Web Workers.
> Web Workers are not part of JavaScript, they’re a browser feature which can be accessed through JavaScript.    
We should already be familiar with the fact that JavaScript runs on a single thread. JavaScript, however, gives developers the opportunity to write asynchronous code too.  
Async programming enables your UI to be responsive, by ’scheduling’ parts of the code to be executed a bit later in the event loop, thus allowing the UI rendering to be performed first. AJAX request is a good use case of that. However, requests are handled by the WEB API of the browser, but how can other code be made asynchronous? For example, what if the code that in inside the success callback is very CPU intensive? suck as a huge `for` loop. That’s the case Web Worker deals.  
Web Workers are in-browser **threads** that can be used to execute JavaScript code without blocking the event loop.

## Technique
A stack is a list of elements that are accessible only from one end of the list, which is called the top. The stack is know as a last-in, first-out (LIFO) data structure.  
Because of the last-in, first-out nature of the stack, any element that is not currently at the top of the stack cannot be accessed. To get to an element at the bottom of the stack, you have to dispose of all the elements above it first.  

In JavaScript I implement Stack as blow:
```javascript
class Stack {
	constructor () {
		this.dataStore = [];
		this.top = 0;
	}

	push (element) {
		this.dataStore[this.top++] = element;
	}

	peek () {
		return this.dataStore[this.top - 1];
	}

	pop () {
		return this.dataStore[--this.top];
	}

	clear () {
		this.top = 0;
	}

	length () {
		return this.top;
	}
}
```
`dataStore` is the underlying data structure to store the stack elements, it’s an array.  
`top` keeps track of the top of the stack and is initially set to 0 by the constructor.  
`push()` is the function of push new element onto a stack.  
`pop()` is the function does the return element job in the top position of the stack.  
`peek()` return the top element of the stack by accessing the element at the `top - 1` position of the array, but won’t decreasing the `top`.  
  
One area where stacks are used is in implementing recursion.  
Normal recursive way of factorial:
```javascript
const factorial = (n) => {
	if (n === 0) {
		return 1;
	} else {
		return n * factorial(n - 1);
	}
};
```

Stack way:
```javascript
const stack_factorial = (n) => {
	const stack = new Stack();
	while (n > 1) {
		stack.push(n--);
	}
	let result = 1;
	while (stack.length() > 0) {
		result *= stack.pop();
	}
	return result;
};
```

Working demonstrating see [Recursion with Stack](https://github.com/charleserious/data-structures-and-algorithms-with-javascript/blob/master/Stack/stack.test.recursion.js). 

## Share
Following [Webpack from Nothing - Third Party Libraries](https://what-problem-does-it-solve.com/webpack/third_party_libs.html)

In the World Before Webpack, we’d often add library’s CDN URL to a `<script>` tag and be on your way.  

That would work because the library would dump itself into the global namespace. That’s not what we want to do for a few reasons.  

Firstly, this means that every library everywhere has to agree on a unique set of names so as to not squash each other. That is insane.  

Secondly, it means that we have no control over when or how these libraries are loaded, which becomes important for writing tests.  

Thirdly, this isn’t how third-party JavaScript libraries are build - they mostly assume you are using module bundler like Webpack.  

Point is, dumping into global namespace bad.  

- A Real Project: Markdown Previewing
The simplest this I could think of is a markdown previewer. There is a markdown module we can use, so that will be our third-part library.

First, add it to our `package.json` file using `yarn add`:   
```shell
> yarn add markdown
```

```shell
yarn add v1.7.0
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
[4/4] 📃  Building fresh packages...
success Saved 1 new dependency.
info Direct dependencies
└─ markdown@0.5.0
info All dependencies
└─ markdown@0.5.0
✨  Done in 15.13s.
```

Let’s create our HTML first in `dist/index.html`:
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>Markdown Previewer</title>
</head>
<body>
	<h1>Markdown Previewer</h1>
	<form id="editor">
		<textarea id="source" cols="80" rows="10"></textarea>
		<input type="submit" value="Preview!">
	</form>
	<hr>
	<section id="preview"></section>
</body>
<script src="bundle.js"></script>
</html>
```

The app will work by listening to a submit event on that form and, when the button is pressed, render a preview of the markdown. Rather than put this all in line, we’ll make our module that constructs this function.  

This function will use the `markdown` library to do the actual rendering, so the module we need to write should take some inputs — where to find the source and where to render the preview, and produce a side-effect, namely the formatted markdown gets written to the part of DOM were the preview should go.  

Our entry point is `js/index.js`, so let’s create that like so:
```javascript
import markdownPreviewer from './markdownPreviewer';

window.onload = () => {
	document.getElementById('editor').addEventListener(
		'submit',
		markdownPreviewer.attachPreviewer(
			document,	// pass in document
			'source',	// id of source textarea
			'preview'	// id of preview DOM element
		)
	);
}
```

`markdownPreviewer` is a file we’ll create in a moment.  

Now, let’s create `js/markdownPreviewer.js`, which does all the work.
```javascript
import { markdown } from 'markdown';

var attachPreviewer = function ($document, sourceId, previewId) {
	return function (event) {
		var text = $document.getElementById(sourceId).value;
		var preview = $document.getElementById(previewId);

		preview.innerHTML = markdown.toHTML(text);
		event.preventDefault();
	}
};

export default {
	attachPreviewer: attachPreviewer
}
```

Let’s package everything up and see if it works.
```shell
> yarn webpack
```

```shell
yarn run v1.7.0
$ webpack --config webpack.config.js --display-error-details
Hash: a879ad28c25ddcf8706e
Version: webpack 4.16.0
Time: 1035ms
Built at: 2018-07-22 13:53:31
    Asset      Size  Chunks             Chunk Names
bundle.js  25.3 KiB       0  [emitted]  main
[1] ./js/index.js + 1 modules 677 bytes {0} [built]
    | ./js/index.js 302 bytes [built]
    | ./js/markdownPreviewer.js 370 bytes [built]
[5] (webpack)/buildin/global.js 489 bytes {0} [built]
    + 6 hidden modules
✨  Done in 2.37s.
```

Open up `dist/index.html`, we should see our UI:

![Initial  look](http://pc97r6al4.bkt.clouddn.com/nocontent.png)

Type in some markdown and hit the submit button.  

![Preview look](http://pc97r6al4.bkt.clouddn.com/hascontent.png)
