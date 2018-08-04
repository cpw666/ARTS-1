# Week 31st
## Algorithm
[728. Self Dividing Numbers](https://leetcode.com/problems/self-dividing-numbers/description/)  

### Description
A *self-dividing number* is a number that is divisible by every digit it contains.  
For example, 128 is a self-dividing number because `128 % 1 == 0`, `128 % 2 == 0`, and `128 % 8 == 0`.  
Also, a self-dividing number is note allowed to contain the digit zero.  
Given a lower and upper number bound, output a list of every possible self dividing number, include the bounds if possible.  

### Example 1:
```
Input: left = 1, right = 22
Output: [1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 12, 15, 22]
```

### Note
- The boundaries of each input argument are `1 <= left <= right <= 10000`.

### Solution 1
```javascript
const selfDividingNumbers = (left, right) => {
	const list = [];
	for (let i = left; i <= right; i++) {
		const digits = i.toString().split('');
		let divid = false;
		if (digits.includes('0')) {
			continue;
		}
		digits.forEach(digit => {
			divid = i % Number(digit) === 0 ? true : false;
		});
		if (divid) {
			list.push(i);
		}
	}
	return list;
};

const left = 1;
const right = 22;
const list = selfDividingNumbers(left, right);
console.log(list);
```
Output is  
```
[ 1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 12, 15, 21, 22 ]
```

Apparently, 21 is not a self-dividing number, wrong solution.  
Because the result of the ternary `divid = i % Number(digit) === 0 ? true : false;` always based on calculate of the last digit.

### Solution 2
```javascript
const selfDividingNumbers = (left, right) => {
	const list = [];
	for (let i = left; i <= right; i++) {
		const digits = i.toString().split('');
		const divied = digits.every(bit => i % parseInt(bit) === 0);
		if (divied) {
			list.push(i);
		}
	}
	return list;
};
```
Output is  
```
[ 1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 12, 15, 21, 22 ]
```
This time it pass all the test, but through using `every` prototype function, what about functional programming for this problem?  

## Review
[How JavaScript works: an overview of the engine, the runtime, and the call stack](https://blog.sessionstack.com/how-does-javascript-actually-work-part-1-b0bacc073cf)  
[Tutorial – SessionStack Blog](https://blog.sessionstack.com/tagged/tutorial) this link to a series article on **How JavaScript Works**, First post is an overview of the engine, the runtime, and the call stack.  
Honestly, before this article I don’t know anything about these topic, some blind spot existed during my daily development, now Alexander Zlatkov  help me to understand what the browser is packed up. How my code is executed. 
As post shows Event Loop is not in the JS Engine. But quote from [You Don’t Know JS](https://github.com/getify/You-Dont-Know-JS/blob/master/async%20%26%20performance/ch1.md#event-loop) 
> Note: We mentioned "up until recently" in relation to ES6 changing the nature of where the event loop queue is managed. It's mostly a formal technicality, but ES6 now specifies how the event loop works, which means technically it's within the purview of the JS engine, rather than just the hosting environment. One main reason for this change is the introduction of ES6 Promises, which we'll discuss in Chapter 3, because they require the ability to have direct, fine-grained control over scheduling operations on the event loop queue (see the discussion of setTimeout(..0) in the "Cooperation" section).  

So Event Loop is now in JS Engine from ES6? Need to digging deeper.

## Technique
[Linked List](https://github.com/charleserious/data-structures-and-algorithms-with-javascript/blob/master/LinkedLists/linkedList.test.js)  
A linked list is a collection of objects called *nodes*. Each node is linked to a successor node in the list using an object reference. The reference to another node is called a *link*.   

An example of a linked list is shown in [Figure Singly LinkedList](#single-linkedList)
![Singly LinkedList](http://pc97r6al4.bkt.clouddn.com/singly-linked-list.jpg)  

While array elements are referenced by their position, linked list elements are referenced by their relationship to the other elements of the linked list In [Figure Singly LinkedList](#single-linkedList), we say that “1201” follows “1200”, not “1201” in the second position.   

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
```

## Share
Following [Going to Production](https://what-problem-does-it-solve.com/webpack/production.html)  
We can write JavaScript code in modules and bring in third party libraries, and we can write unit test. That’s pretty good for a language that doesn’t support literally any of that in any way. Thanks to Webpack!  

But, we need to go production. Code that’s not live and solving user problems might as well not exist.  

Given that our amazing Markdown previewer totally works statically in a browser on localhost, it’s just a matter of dumping files up onto some server, right?  

Not exactly. It’s true that *would* fork, but for any reasonable application we’re going to want a bit more. At the very least we want to:
- minify / gzip / de-biggen the JavaScript we make the user download;
- create a unique name for our bundle so it works with CDNs, AKA ‘hashing’.  

### Minification saves time and money
Uncompressed assets like JavaScript waste bandwidth. The downstream user and their browser doesn’t care about whitespace or code comments. There literally no reason to send uncompressed JavaScript to a user other than laziness.  

Take a look at our existing `markdownPreviewer.js`
```javascript
import{m}from "markdown";
var a=function(d,s,p){
return function(e){
var t=d.getElementById(i).value,
q=d.getElementById(p);
q.innerHTML=m.toHTML(t);
e.preventDefault();};}
```

This takes up less space than our *uncompressed* version, but is terrible code. We can use tools to turn nice code into crappy but small code that works the same way.   

This, plus the use of a content-delivery network will make our application performant and fast without a ton of effort. To use a CDN, however, we need to be mindful about how we manage changes.

### Unique names for each version of our `bundle.js`
If We deployed our code to a content delivery network (which we are likely going to want to do at some point), and we used the name `bundle.js` it will be pretty hard to update it. **Some CDNs** don’t let your update assets (meaning people would use the original version of `bundle.js` forever, never getting our update or bugfixes), and others require your to wait for caches to expire, which can be hours or even days. The standard practice to deal with this is that each new version of your code has a unique name.  

This, along with minification, are basic needs for web development, and since Webpack is a monolithic system, we’d expect it be able to do this for us. Turns out, it can.  

### Something Automatic!
According [Webpack’s documentation](https://webpack.js.org/guides/production/), merely adding `mode: 'production'` to our config, it will perform minification! Let’s see if that’s true.

First, let’s see how big the bundle is:
```shell
> yarn webpack
```

```shell
yarn run v1.7.0
$ webpack --config webpack.config.js --display-error-details
Hash: a885f63e4c38b31885db
Version: webpack 4.16.3
Time: 228ms
Built at: 2018-08-02 14:44:44
    Asset      Size  Chunks             Chunk Names
bundle.js  77.1 KiB       0  [emitted]  main
[0] ./js/index.js 302 bytes {0} [built]
[1] ./js/markdownPreviewer.js 370 bytes {0} [built]
[5] (webpack)/buildin/global.js 489 bytes {0} [built]
    + 6 hidden modules
✨  Done in 1.30s.
```

```shell
> wc -c dist/bundle.js
78928 dist/bundle.js
```

Now, let’s try `mode: 'production'`
```shell
> yarn prod
```

```shell
yarn run v1.7.0
$ webpack --config ./webpack/production.config.js --display-error-details
Hash: 266735145cd68eecab7a
Version: webpack 4.16.3
Time: 258ms
Built at: 2018-08-02 14:47:49
                         Asset      Size  Chunks             Chunk Names
c265c23574d9fd20ec08-bundle.js  25.3 KiB       0  [emitted]  main
[3] (webpack)/buildin/global.js 489 bytes {0} [built]
[7] ./js/index.js + 1 modules 677 bytes {0} [built]
    | ./js/index.js 302 bytes [built]
    | ./js/markdownPreviewer.js 370 bytes [built]
    + 6 hidden modules
✨  Done in 1.50s.
```

```shell
> wc -c production/c265c23574d9fd20ec08-bundle.js 
25951 production/c265c23574d9fd20ec08-bundle.js
```

Not bad! One third the final size.

### Separating Production and Development Configuration
The way we made this work is by separating config through purpose, for development usage we use `development.config.js` and for production usage we use `production.config.js` these two config extend a `basic.config.js` for common configuration through dependency  `webpack-merge`.

Our general requirements at this point are:
- No minification or hashing in development
- Minification **and** hash in production
- Output development files in a different location that production files
- Avoid duplicating configuration if at-all possible

First, install webpack-merge:
```shell
> yarn add -D webpack-merge
```

```shell
yarn add v1.7.0
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
[4/4] 📃  Building fresh packages...
success Saved lockfile.
success Saved 1 new dependency.
info Direct dependencies
└─ webpack-merge@4.1.4
info All dependencies
└─ webpack-merge@4.1.4
✨  Done in 4.20s.
```

Now let’s `three` create our configurations. I’m willing to tolerate one configuration file at the top-level, but not three. So, we’ll be putting the development, production, and basic in a new directory, called `webpack`:

`basic.config.js`
```javascript
module.exports = {
	entry: './js/index.js',
};
```

`development.config.js`
```javascript
const path 				= require('path');
const Merge 			= require('webpack-merge');
const BasicConfig = require('./basic.config');

module.exports = Merge(BasicConfig, {
	mode: 'development',
	output: {
		path: path.join(__dirname, '../dev'),
		filename: 'bundle.js'
	}
});
```

`production.config.js`
```javascript
const path 				= require('path');
const Merge 			= require('webpack-merge');
const BasicConfig = require('./basic.config');

module.exports = Merge(BasicConfig, {
	mode: 'production',
	output: {
		path: path.join(__dirname, '../production'),
		filename: '[chunkhash]-bundle.js'
	}
});
```

Add these two scripts into `package.json`
```json
"dev": "webpack --config ./webpack/development.config.js --display-error-details",
    "prod": "webpack --config ./webpack/production.config.js --display-error-details"
```

One confusing thing that is confusing must are pointed out. All of our calls to `require` use a path *relative to the file* `require` *is called from*. Further, when we call `path.join(__dirname, '../prouction')`, the `../` is because this call, too, is executed relative to the file it’s executed in. **But**, our entry point is *relative to where Webpack is executed from*, which is to say, the root directory.  

Let that sink in. As an exercise for later, decide for yourself if any of this is an example of a good decision. Perhaps it’s my fault for insisting I tuck away these silly files in `webpack/`, but I find all of this unnecessarily arbitrary and confusing.  

Anyway, we should be able to run webpack as before:
```shell
> yarn dev
```

```shell
yarn run v1.7.0
$ webpack --config ./webpack/development.config.js --display-error-details
Hash: e9149a2dc882cef0e546
Version: webpack 4.16.3
Time: 295ms
Built at: 2018-08-02 15:38:48
    Asset      Size  Chunks             Chunk Names
bundle.js  83.4 KiB    main  [emitted]  main
[./js/index.js] 302 bytes {main} [built]
[./js/markdownPreviewer.js] 370 bytes {main} [built]
[./node_modules/webpack/buildin/global.js] (webpack)/buildin/global.js 489 bytes {main} [built]
    + 6 hidden modules
✨  Done in 1.62s.
```

This places our bundle in `dev`, so we’ll need to move our HTML file there:
```shell
cp dist/index.html dev/index.html
```

And now, our app should work as before.
![Initial  look](http://pc97r6al4.bkt.clouddn.com/nocontent.png)  

Next, we can build for production:
```shell
> yarn prod
```

```shell
yarn run v1.7.0
$ webpack --config ./webpack/production.config.js --display-error-details
Hash: 266735145cd68eecab7a
Version: webpack 4.16.3
Time: 275ms
Built at: 2018-08-02 15:44:02
                         Asset      Size  Chunks             Chunk Names
c265c23574d9fd20ec08-bundle.js  25.3 KiB       0  [emitted]  main
[3] (webpack)/buildin/global.js 489 bytes {0} [built]
[7] ./js/index.js + 1 modules 677 bytes {0} [built]
    | ./js/index.js 302 bytes [built]
    | ./js/markdownPreviewer.js 370 bytes [built]
    + 6 hidden modules
✨  Done in 1.54s.
```

```shell
> ls production/
c265c23574d9fd20ec08-bundle.js
```

Which brings us to a problem to solve, which is how do we got our `index.html` to reference to the file we just built.

### Accessing the Hashed Filename in our HTML
So far, our app doesn’t need a server to do anything, but we now need something dynamic. Rather than go through *that* pain, let’s hold what we’ve got, and get the generated filename in out HTML.  
 
In the previews section,  we copied our HTML around, and that’s not good. We’re building a build system here, and it shouldn’t include us typing `cp`!  

What we want is to treat our `index.html` as a rudimentary template, and include a reference to our bundle in there at build time. The [HtmlWebpackPlugin](https://github.com/jantimon/html-webpack-plugin) was designed to do this!  

First, install it:
```shell
> yarn add -D html-webpack-plugin
```

```shell
yarn add v1.7.0
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
[4/4] 📃  Building fresh packages...
success Saved lockfile.
warning Your current version of Yarn is out of date. The latest version is "1.9.2", while you're on "1.7.0".
info To upgrade, run the following command:
$ brew upgrade yarn
success Saved 30 new dependencies.
info Direct dependencies
└─ html-webpack-plugin@3.2.0
info All dependencies
├─ camel-case@3.0.0
├─ clean-css@4.1.11
├─ css-select@1.2.0
├─ css-what@2.1.0
├─ dom-converter@0.1.4
├─ dom-serializer@0.1.0
├─ domhandler@2.1.0
├─ domutils@1.1.6
├─ entities@1.1.1
├─ es-abstract@1.12.0
├─ es-to-primitive@1.1.1
├─ he@1.1.1
├─ html-minifier@3.5.19
├─ html-webpack-plugin@3.2.0
├─ htmlparser2@3.3.0
├─ is-callable@1.1.4
├─ is-date-object@1.0.1
├─ is-regex@1.0.4
├─ is-symbol@1.0.1
├─ lower-case@1.1.4
├─ nth-check@1.0.1
├─ object.getownpropertydescriptors@2.0.3
├─ param-case@2.1.1
├─ pretty-error@2.1.1
├─ relateurl@0.2.7
├─ renderkid@2.0.1
├─ toposort@1.0.7
├─ uglify-js@3.4.6
├─ upper-case@1.1.3
└─ util.promisify@1.0.0
✨  Done in 5.24s.
```

By default, this plugin will produce an `index.html` file from scratch that brings in our bundle. Since we have particular markup that we need for our app, we need a way to specify a template. `HtmlWebpackPlugin` allows us to specify one to use and, if it’s just straight-up normal `HTML`, this plugin will insert the `<script>` tag in the right place.  

Let’s place that file in a new directory called `html`. Note that we’ve omitted the `<script>` tag we had before.  
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>WTF Webpack</title>
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
</html>
```

Now, we’ll bring in the new plugin and configure it. This is common to both production and development, so we’ll put this in `webpack/basic.config.js`:  

```javascript
const HtmlPlugin = require('html-webpack-plugin');

module.exports = {
	plugins: [
		new HtmlPlugin({
			template: './html/index.html'
		})
	],
	entry: './js/index.js'
};
```

Note again the arbitrary natural of relative paths. The `template` will e accessed from the directory where run **Webpack**, so it’s just `./html`, and **note** `../html`.  

Let’s clean out the existing `dev` directory so we can be sure we did what we think we did:  
```shell
> rm dev/*.*
```

Now, run `dev`

```shell
yarn dev
```

```shell
yarn run v1.7.0
$ webpack --config ./webpack/development.config.js --display-error-details
Hash: 99d3c37dc61900263ede
Version: webpack 4.16.3
Time: 508ms
Built at: 2018-08-04 15:25:14
     Asset       Size  Chunks             Chunk Names
 bundle.js   83.4 KiB    main  [emitted]  main
index.html  500 bytes          [emitted]  
[./js/index.js] 302 bytes {main} [built]
[./js/markdownPreviewer.js] 370 bytes {main} [built]
[./node_modules/webpack/buildin/global.js] (webpack)/buildin/global.js 489 bytes {main} [built]
    + 6 hidden modules
Child html-webpack-plugin for "index.html":
     1 asset
    [./node_modules/html-webpack-plugin/lib/loader.js!./html/index.html] 655 bytes {0} [built]
    [./node_modules/webpack/buildin/global.js] (webpack)/buildin/global.js 489 bytes {0} [built]
    [./node_modules/webpack/buildin/module.js] (webpack)/buildin/module.js 497 bytes {0} [built]
        + 1 hidden module
✨  Done in 1.97s.
```

If you look ad `dev/index.html`, you can see Webpack inserted `<script>` tag (at bottom, and messing up our indentation):
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>WTF Webpack</title>
</head>
<body>
	<h1>Markdown Previewer</h1>
	<form id="editor">
		<textarea id="source" cols="80" rows="10"></textarea>
		<input type="submit" value="Preview!">
	</form>
	<hr>
	<section id="preview"></section>
<script type="text/javascript" src="bundle.js"></script></body>
</html>
```

**And**, if you run this for production, it works as we’d like!
```shell
> yarn prod
```

```shell
yarn run v1.7.0
$ webpack --config ./webpack/production.config.js --display-error-details
Hash: 3eae59d2a7e72de31d54
Version: webpack 4.16.3
Time: 1240ms
Built at: 2018-08-04 15:28:39
                         Asset       Size  Chunks             Chunk Names
c265c23574d9fd20ec08-bundle.js   25.3 KiB       0  [emitted]  main
                    index.html  521 bytes          [emitted]  
[3] (webpack)/buildin/global.js 489 bytes {0} [built]
[7] ./js/index.js + 1 modules 677 bytes {0} [built]
    | ./js/index.js 302 bytes [built]
    | ./js/markdownPreviewer.js 370 bytes [built]
    + 6 hidden modules
Child html-webpack-plugin for "index.html":
     1 asset
    [0] ./node_modules/html-webpack-plugin/lib/loader.js!./html/index.html 655 bytes {0} [built]
    [2] (webpack)/buildin/global.js 489 bytes {0} [built]
    [3] (webpack)/buildin/module.js 497 bytes {0} [built]
        + 1 hidden module
✨  Done in 2.66s.
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>WTF Webpack</title>
</head>
<body>
	<h1>Markdown Previewer</h1>
	<form id="editor">
		<textarea id="source" cols="80" rows="10"></textarea>
		<input type="submit" value="Preview!">
	</form>
	<hr>
	<section id="preview"></section>
<script type="text/javascript" src="c265c23574d9fd20ec08-bundle.js"></script></body>
</html>
```

Nice!
