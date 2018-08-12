# Week 32ed
## Algorithm
### [617. Merge Two Binary Trees](https://leetcode.com/problems/merge-two-binary-trees/description/)  

## Description
Given two binary trees and imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the others are not.  

You need to merge them into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged one. Otherwise, the NOT null node will be used as the node of new tree.  

#### Example:
```
Input: 
	Tree 1                     Tree 2                  
          1                         2                             
         / \                       / \                            
        3   2                     1   3                        
       /                           \   \                      
      5                             4   7                  
Output: 
Merged tree:
	     3
	    / \
	   4   5
	  / \   \ 
	 5   4   7
```

#### Note
The merging process must start from the root nodes of both trees.

#### Solution 1
Shared TreeNode class
```javascript
class TreeNode {
	constructor (val) {
		this.val = val;
		this.left = null;
		this.right = null;
	}
}
```

```javascript
/**
 * Merge Two Binary Trees
 * @param {TreeNode} t1
 * @param {TreeNode} t2
 * @returns {TreeNode}
 */
const mergeTrees = (t1, t2) => {
	if (t1 === null) {
		return t2;
	}
	if (t2 === null) {
		return t1;
	}
	t1.val += t2.val;
	t1.left = mergeTrees(t1.left, t2.left);
	t1.right = mergeTrees(t1.right, t2.right);

	return t1;
};
```
This is too slow 183 / 183 test cases passed with 128ms, damn slow;

#### Solution 2
```javascript
/**
 * Merge Two Binary Trees
 * @param {TreeNode} t1
 * @param {TreeNode} t2
 * @returns {TreeNode}
 */
const mergeTrees = (t1, t2) => {
	if (t1 === null) {
		return t2;
	}
	if (t2 === null) {
		return t1;
	}
	const root = t1.val + t2.val;
	const newTree = new TreeNode(root);
	newTree.left = mergeTrees(t1.left, t2.left);
	newTree.right = mergeTrees(t1.right, t2.right);
	return newTree;
};
```
No effect... DAMN. Digging how to optimize.

## Review
[How JavaScript works: inside the V8 engine + 5 tips on how to write optimized code](https://blog.sessionstack.com/how-javascript-works-inside-the-v8-engine-5-tips-on-how-to-write-optimized-code-ac089e62b12e)  

[Tutorial – SessionStack Blog](https://blog.sessionstack.com/tagged/tutorial) this link to a series article on **How JavaScript Works**.  

This is my review of the second post of this series.  

So, there are several kinds of JavaScript engine implementation, we talked about [Chrome V8 - Wikipedia](https://en.wikipedia.org/wiki/V8_%28JavaScript_engine%29) developed by Google, written in C++.  

V8 was first designed to increase the performance of JavaScript execution inside web browsers. In order to obtain speedy, V8 translate JavaScript code into more efficient machine code instead of using an interpreter. It compiles JavaScript code into machine code at execution by implementing a **JIT (Just-In-Time) compiler** like a lot of modern JavaScript engines do such as SpiderMonkey or Rhino. The main difference here is that V* doesn’t produce bytecode or any intermediate code.  

According author’s opinion, they use a list of best practices to write optimized JavaScript:
1. **Order of object properties**: always instantiate your object properties in the same order so that hidden classes, and subsequently optimized code, can be shared.
2. **Dynamic properties**: adding properties to an object after instantiation will force a hidden class change and slow down any methods that were optimized fo the previous hidden class. Instead, assign all of an object’s properties in its constructor.
3. **Methods**: code that executes the same method repeatedly will run faster than code that executes many different methods only once (due to inline caching).
4. **Array**: avoid sparse arrays where keys are not incremental numbers. Sparse arrays which don’t have every element inside them are a **hash table**. Elements in such arrays are more expensive to access. Also, try to avoid pre-allocation large arrays. It’s better to grow as you go. Finally, don’t delete elements in arrays. It makes the keys sparse.
5. **Tagged values**: V8 represents object and numbers with 32 bits. It uses a bit to know if it is an object (flag = 1) or an integer (flag = 0) called SMI (Small Integer) because of its 31 bits. Then, if a numeric value is bigger than 31 bits, V8 will box the number, turning it into a double` and creating a new object to put the number inside. Try to use 31 bit signed numbers whenever possible to avoid the expensive boxing operation into a JS object.

There a lot of thing in this post, I haven’t fully understand. be hold.

## Technique
[Doubly Linked Lists](https://github.com/charleserious/data-structures-and-algorithms-with-javascript/blob/master/LinkedLists/DoublyLinkedLists/linkedList.test.js)  

Although traversing a linked list from the first node to the last node is straightforward, it is not as easy to traverse a linked list backward. We can simplify this procedure if we add a property to our Node class that stores a link to the previous node. When we insert a node into the list, we’ll have to perform more operations to assign the proper links for the next and previous nodes, but we gain efficiency when we have to remove a node form the list, since we no longer have to search for the previous node. ![Doubly Linked List](http://pc97r6al4.bkt.clouddn.com/doubly-linked-list.png)   
illustrates how a doubly linked list works.  

Not to say too much, this is my implementation:  
```javascript
class Node {
	constructor (element) {
		this.element = element;
		this.next = null;
		this.previous = null;
	}
}

class LinkedList {
	constructor () {
		this.head = new Node('head');
	}

	dispReverse () {
		let currentNode = this.head;
		currentNode = this.findLast();
		while (currentNode.previous !== null) {
			console.log(currentNode.element);
			currentNode = currentNode.previous;
		}
	}

	findLast () {
		let currentNode = this.head;
		while (currentNode.next !== null) {
			currentNode = currentNode.next;
		}
		return currentNode;
	}

	remove (item) {
		let currentNode = this.find(item);
		if (currentNode.next !== null) {
			currentNode.previous.next = currentNode.next;
			currentNode.next.previous = currentNode.previous;
			currentNode.next = null;
			currentNode.previous = null;
		}
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

	insert (newElement, item) {
		const newNode = new Node(newElement);
		const current = this.find(item);
		newNode.next = current.next;
		newNode.previous = current;
		current.next = newNode;
	}
}
```
## Share
Following [Wrangling CSS, too](https://what-problem-does-it-solve.com/webpack/css.html)  

For out simple app, we *could* inline our CSS into the `<head>`, but the second we need another template, that ceases to work, and we’d like to manage CSS in separate files, the same as out JavaScript.  

Webpack can totally handle this, even though it feels way outside its wheelhouse, since it’s not JavaScript. I’m not even sure *why* Webpack has features to support this, but it does, and it keeps us from having to find another tool to manage CSS.  

We talked before about *plugins*, but we didn’t talk about *loaders*. Loaders are the fourth core concept in Webpack and the have to do with the way in which `import` behaves on files that aren’t JavaScript.  

First, Let’s write some CSS for our app so we have something real to work with.  

### Styling out App
We’re going to use a third-party CSS library later on, so let’s use a light touch here. Let’s make our text a bit lighter, make the background a bit darker, but keep our `<textarea>` black on white. We’ll also change to one of those sans-serif fonts the kids like so much.  

We’ll put this in `css/styles.css`:  
```css
html {
	color: #111111;
	background-color: #EEEEEE;
	font-family: avenir next, avenir, Helvetica, sans-serif;
}

textarea {
	color: #000000;
	background-color: #FFFFFF;
}
```

We can now reference this in `html/index.html`:  
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>WTF Webpack</title>
	<link rel="stylesheet" href="styles.css">
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

Run Webpack:  
```shell
> yarn dev
```

```shell
yarn run v1.7.0
$ webpack --config ./webpack/development.config.js $npm_package_config_webpack_args
Hash: ae377b49207bae2b023f
Version: webpack 4.16.3
Time: 496ms
Built at: 08/09/2018 1:26:20 PM
     Asset       Size  Chunks             Chunk Names
 bundle.js   83.4 KiB    main  [emitted]  main
index.html  543 bytes          [emitted]  
[./js/index.js] 302 bytes {main} [built]
[./js/markdownPreviewer.js] 370 bytes {main} [built]
[./node_modules/webpack/buildin/global.js] (webpack)/buildin/global.js 489 bytes {main} [built]
    + 6 hidden modules
Child html-webpack-plugin for "index.html":
     1 asset
    [./node_modules/html-webpack-plugin/lib/loader.js!./html/index.html] 699 bytes {0} [built]
    [./node_modules/webpack/buildin/global.js] (webpack)/buildin/global.js 489 bytes {0} [built]
    [./node_modules/webpack/buildin/module.js] (webpack)/buildin/module.js 497 bytes {0} [built]
        + 1 hidden module
✨  Done in 2.13s.
```

And then manually copy our stylesheet into `dev/`:  
```shell
> cp css/styles.css dev/
```

Now, our app looks like a bit nicer:
![Preview with a bit CSS](http://pc97r6al4.bkt.clouddn.com/preview-with-bit-css.png)  
This has the same problems with `bundle.js`. We want it minified and we want it hashed and we generally don’t want to deal with it. We know Webpack can do those thins for JavaScript, and it can do them for CSS.  

Surprisingly, we make this happen by importing our CSS into `js/index.js`!

### Loader Can Load Anything
When you write an `import` statement, and Webpack compiles your code, it *loads* the file referenced in the `import`. By default, Webpack assumes the file is JavaScript and that you are trying to write module code. Cool!  

But, you can change that default, basically controlling Webpack’s internal machinery to do things *other* than create JavaScript bundles. To do that, you tell Webpack to use a specific loader.  

To load CSS, we’ll install `css-loader`:  
```shell
yarn add css-loader -D
```

```shell
yarn add v1.7.0
(node:58072) [DEP0005] DeprecationWarning: Buffer() is deprecated due to security and usability issues. Please use the Buffer.alloc(), Buffer.allocUnsafe(), or Buffer.from() methods instead.
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
warning " > karma-jasmine@1.1.2" has unmet peer dependency "jasmine-core@*".
[4/4] 📃  Building fresh packages...

success Saved lockfile.
success Saved 18 new dependencies.
info Direct dependencies
└─ css-loader@1.0.0
info All dependencies
├─ babel-code-frame@6.26.0
├─ css-loader@1.0.0
├─ cssesc@0.1.0
├─ fastparse@1.1.1
├─ icss-replace-symbols@1.1.0
├─ icss-utils@2.1.0
├─ js-tokens@3.0.2
├─ jsesc@0.5.0
├─ lodash.camelcase@4.3.0
├─ postcss-modules-extract-imports@1.2.0
├─ postcss-modules-local-by-default@1.2.0
├─ postcss-modules-scope@1.1.0
├─ postcss-modules-values@1.3.0
├─ postcss-value-parser@3.3.0
├─ regenerate@1.4.0
├─ regexpu-core@1.0.0
├─ regjsgen@0.2.0
└─ regjsparser@0.1.5
✨  Done in 19.85s.
```

To use this loader, we’ll add a new section to our Webpack configuration, called `module`. This gives us a peek into how Webpack views itself. The `modules` section controls how Webpack treats different types of modules we might import. This statement implies that there *are* types other than just JavaScript. It’s starting to make sense.  

Inside `module:`, we create a `rules:` array, which will itemize out all rules for handling modules that aren’t JavaScript. Each rule has a test, and a loader to use. This goes in `Webpack/basic.config.js`, since we need it for dev and prod:  

```javascript
const HtmlPlugin = require('html-webpack-plugin');

module.exports = {
	module: {
		rules: [
			{
				test: /.css$/,
				use: 'css-loader'
			}
		]
	},
	plugins: [
		new HtmlPlugin({
			template: './html/index.html'
		})
	],
	entry: './js/index.js'
};
```

With this in place, we can modify `js/index.js` to import our CSS:  
```javascript
import '../css/styles.css';
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

Note that we’re importing `../css/styles.css`, because imports that have dots in front of them are relative to the directory where the file being processed is located.  

Let’s clean up our test so we can sure what’s happening:  
```shell
> rm dev/*.*
```

Now, we can run Webpack:  
```shell
> yarn dev
```

```shell
yarn run v1.7.0
$ webpack --config ./webpack/development.config.js $npm_package_config_webpack_args
Hash: be4144d3a942cec5d313
Version: webpack 4.16.3
Time: 705ms
Built at: 2018-08-09 14:08:25
     Asset       Size  Chunks             Chunk Names
 bundle.js   87.2 KiB    main  [emitted]  main
index.html  543 bytes          [emitted]  
Entrypoint main = bundle.js
[./css/styles.css] 343 bytes {main} [built]
[./js/index.js] 330 bytes {main} [built]
[./js/markdownPreviewer.js] 370 bytes {main} [built]
[./node_modules/webpack/buildin/global.js] (webpack)/buildin/global.js 489 bytes {main} [built]
    + 7 hidden modules
Child html-webpack-plugin for "index.html":
     1 asset
    Entrypoint undefined = index.html
    [./node_modules/html-webpack-plugin/lib/loader.js!./html/index.html] 699 bytes {0} [built]
    [./node_modules/webpack/buildin/global.js] (webpack)/buildin/global.js 489 bytes {0} [built]
    [./node_modules/webpack/buildin/module.js] (webpack)/buildin/module.js 497 bytes {0} [built]
        + 1 hidden module
✨  Done in 1.97s.
```

If we open up `dev/index.html` in your browser, the CSS isn’t being applied, BUT, if you look inside the `bundle.js` file, your can see our CSS in there:  
```shell
> grep textarea dev/bundle.js

eval("exports = module.exports = __webpack_require__(/*! ../node_modules/css-loader/lib/css-base.js */ \"./node_modules/css-loader/lib/css-base.js\")(false);\n// imports\n\n\n// module\nexports.push([module.i, \"html {\\n\\tcolor: #111111;\\n\\tbackground-color: #EEEEEE;\\n\\tfont-family: avenir next, avenir, Helvetica, sans-serif;\\n}\\n\\ntextarea {\\n\\tcolor: #000000;\\n\\tbackground-color: #FFFFFF;\\n}\", \"\"]);\n\n// exports\n\n\n//# sourceURL=webpack:///./css/styles.css?");
eval("__webpack_require__.r(__webpack_exports__);\n/* harmony import */ var _css_styles_css__WEBPACK_IMPORTED_MODULE_0__ = __webpack_require__(/*! ../css/styles.css */ \"./css/styles.css\");\n/* harmony import */ var _css_styles_css__WEBPACK_IMPORTED_MODULE_0___default = /*#__PURE__*/__webpack_require__.n(_css_styles_css__WEBPACK_IMPORTED_MODULE_0__);\n/* harmony import */ var _markdownPreviewer__WEBPACK_IMPORTED_MODULE_1__ = __webpack_require__(/*! ./markdownPreviewer */ \"./js/markdownPreviewer.js\");\n\n\n\nwindow.onload = () => {\n\tdocument.getElementById('editor').addEventListener(\n\t\t'submit',\n\t\t_markdownPreviewer__WEBPACK_IMPORTED_MODULE_1__[\"default\"].attachPreviewer(\n\t\t\tdocument,\t// pass in document\n\t\t\t'source',\t// id of source textarea\n\t\t\t'preview'\t// id of preview DOM element\n\t\t)\n\t);\n}\n\n//# sourceURL=webpack:///./js/index.js?");
```

There is a loader called the style-loader that would dynamically create a `<style>` tag in our DOM and put the CSS in there, but that’s no good. We want the browser to load CSS separately, so it can download both the CSS and the JavaScript in parallel.  

We need to tell Webpack that our CSS that gets loaded should be placed into a separate output file. This can be done with the [MiniCssExtractPlugin](https://webpack.js.org/plugins/mini-css-extract-plugin/). Despite it’s its generic name, it appears created to solve this specific problem.  

```shell
> yarn add mini-css-extract-plugin -D
```

```shell
yarn add v1.7.0
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
warning " > karma-jasmine@1.1.2" has unmet peer dependency "jasmine-core@*".
[4/4] 📃  Building fresh packages...
success Saved lockfile.
success Saved 3 new dependencies.
info Direct dependencies
└─ mini-css-extract-plugin@0.4.1
info All dependencies
├─ @webpack-contrib/schema-utils@1.0.0-beta.0
├─ mini-css-extract-plugin@0.4.1
└─ text-table@0.2.0
✨  Done in 4.34s.
```

Here’s what our basic Webpack configuration now looks like:  
```javascript
const HtmlPlugin = require('html-webpack-plugin');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
	module: {
		rules: [
			{
				test: /\.css$/,
				use: [
					{
						loader: MiniCssExtractPlugin.loader
					},
					'css-loader'
				]
			}
		]
	},
	plugins: [
		new HtmlPlugin({
			template: './html/index.html'
		})
	],
	entry: './js/index.js'
};
```

We also need to tell **MiniCssExtractPlugin** what name to use. Because we want this file hashed, the same as our JavaScript, We’ll need to specify some configuration in `webpack/development.config.js` and `webpack/production.config.js`. Here’s what `webpack/development.config.js` will look like:  
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
	plugins: [
		new MiniCssExtractPlugin({
			filename: 'style.css'
		})
	]
});
```

Here’s what `webpack/production.config.js` will look like:  
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
	plugins: [
		new MiniCssExtractPlugin({
			filename: '[chunkhash]-style.css'
		})
	]
});
```

With this in place, we can remove the `<link>` tag we put in:  
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

Now, when we run Webpack, our CSS file is being created separately and is available in `dev/`:  
```shell
> yarn dev
```

```she’ll
yarn run v1.7.0
$ webpack --config ./webpack/development.config.js $npm_package_config_webpack_args
Hash: b0eab68035331abff4b2
Version: webpack 4.16.3
Time: 591ms
Built at: 2018-08-11 17:34:44
     Asset       Size  Chunks             Chunk Names
 style.css  171 bytes    main  [emitted]  main
 bundle.js     84 KiB    main  [emitted]  main
index.html  540 bytes          [emitted]  
Entrypoint main = style.css bundle.js
[./css/styles.css] 39 bytes {main} [built]
[./js/index.js] 330 bytes {main} [built]
[./js/markdownPreviewer.js] 370 bytes {main} [built]
[./node_modules/webpack/buildin/global.js] (webpack)/buildin/global.js 489 bytes {main} [built]
    + 7 hidden modules
Child html-webpack-plugin for "index.html":
     1 asset
    Entrypoint undefined = index.html
    [./node_modules/html-webpack-plugin/lib/loader.js!./html/index.html] 655 bytes {0} [built]
    [./node_modules/webpack/buildin/global.js] (webpack)/buildin/global.js 489 bytes {0} [built]
    [./node_modules/webpack/buildin/module.js] (webpack)/buildin/module.js 497 bytes {0} [built]
        + 1 hidden module
Child mini-css-extract-plugin node_modules/css-loader/index.js!css/styles.css:
    Entrypoint mini-css-extract-plugin = *
    [./node_modules/css-loader/index.js!./css/styles.css] ./node_modules/css-loader!./css/styles.css 343 bytes {mini-css-extract-plugin} [built]
        + 1 hidden module
✨  Done in 1.80s.
```

```shell
> ls dev/*.css 
dev/style.css
```

```shell
> cat dev/index.html
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
</body>
<script src="./dist/bundle.js"></script>
</html>Charles-MacBook-Pro:wtf-webpack charles$ cat dev/index.html 
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>WTF Webpack</title>
<link href="style.css" rel="stylesheet"></head>
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

**And**, when we build for production, it uses the tased name:  

```sheen
> yarn prod
```

```shell
yarn run v1.7.0
$ webpack --config ./webpack/production.config.js $npm_package_config_webpack_args
Hash: 5b0d8ee69f5039dc47af
Version: webpack 4.16.3
Time: 1427ms
Built at: 2018-08-11 17:40:44
                         Asset       Size  Chunks             Chunk Names
db2b02f8d360059a4175-style.css  171 bytes       0  [emitted]  main
db2b02f8d360059a4175-bundle.js   25.4 KiB       0  [emitted]  main
                    index.html  582 bytes          [emitted]  
Entrypoint main = db2b02f8d360059a4175-style.css db2b02f8d360059a4175-bundle.js
[1] ./css/styles.css 39 bytes {0} [built]
[5] (webpack)/buildin/global.js 489 bytes {0} [built]
[9] ./js/index.js + 1 modules 710 bytes {0} [built]
    | ./js/index.js 330 bytes [built]
    | ./js/markdownPreviewer.js 370 bytes [built]
    + 7 hidden modules
Child html-webpack-plugin for "index.html":
     1 asset
    Entrypoint undefined = index.html
    [0] ./node_modules/html-webpack-plugin/lib/loader.js!./html/index.html 655 bytes {0} [built]
    [2] (webpack)/buildin/global.js 489 bytes {0} [built]
    [3] (webpack)/buildin/module.js 497 bytes {0} [built]
        + 1 hidden module
Child mini-css-extract-plugin node_modules/css-loader/index.js!css/styles.css:
    Entrypoint mini-css-extract-plugin = *
    [0] ./node_modules/css-loader!./css/styles.css 343 bytes {0} [built]
        + 1 hidden module
✨  Done in 2.85s.
```

```shell
> ls production/*.css
production/db2b02f8d360059a4175-style.css
```

```shell
> cat production/index.html
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>WTF Webpack</title>
<link href="db2b02f8d360059a4175-style.css" rel="stylesheet"></head>
<body>
	<h1>Markdown Previewer</h1>
	<form id="editor">
		<textarea id="source" cols="80" rows="10"></textarea>
		<input type="submit" value="Preview!">
	</form>
	<hr>
	<section id="preview"></section>
<script type="text/javascript" src="db2b02f8d360059a4175-bundle.js"></script></body>
</html>
```

Sure enough, if we open up either `dev/index.html` or `production/index.html`, the CSS is working:  

![Preview with a bit CSS](http://pc97r6al4.bkt.clouddn.com/preview-with-bit-css.png)  

Nice!  

Let’s bring in a third-party CSS library to make sure that works as expected.  

### Third-party CSS Libraries
I do like writing CSS. But *do* like using re-usable/functional CSS more and of cause not snowflake/“semantic” CSS, which is why we’re going to use [Tachyons](http://tachyons.io). 

First, let’s bring in tachyons:  
```shell
> yarn add tachyons
```

```shell
yarn add v1.7.0
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
warning " > karma-jasmine@1.1.2" has unmet peer dependency "jasmine-core@*".
[4/4] 📃  Building fresh packages...

success Saved lockfile.
success Saved 1 new dependency.
info Direct dependencies
└─ tachyons@4.11.1
info All dependencies
└─ tachyons@4.11.1
✨  Done in 4.40s.
```
(Refreshingly free of dependencies)  

Much of the styling we’ve added is pretty simple stuff, so we’ll let Tachyons handle all that for us. We’ll leave the font setting in `css/styles.css` just to demonstrate that we can merge our styles with Tachyons’. Replace all of `css/styles.css` with:  

```css
html {
	font-family: avenir next, avenir, Helvetica, sans-serif;
}
```

To bring in Tachyons to our CSS bundle we `import` it just like anything else:  
```javascript
import 'tachyons';
import '../css/styles.css';
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

If you run Webpack now, you’ll see the size of our CSS bundle increase, due to the inclusion of Tachyons. But, let’s actually use it so we can see it working.  

We’ll use some of Tachyons’ styles on `<body>` to set colors, as well as pad the UI a bit (since Tachyons includes a reset): 
```html
<body class="dark-gray bg-light-gray ph4">
```

We’d like our `<textarea>` look a bit nicer, so let’s set it to fill the width of the body, have a 30% black border, with a slight borders radius, and a bit of padding inside:  
```html
<textarea 
  id="source" 
  rows="10" 
  cols="80" 
  class="w-100 ba br2 pa2 b--black-30"></textarea>
```

We’d also like our preview button to be a bit fancier, so let’s set that to be s slightly washed-out green, and give it some padding and borders so it looks like a button. We’ll also set it to zoom on hover, so it feels like a real app:  
```html
<input 
  type="submit" 
  value="Preview!" 
  class="grow pointer ba br3 bg-washed-green ph3 pv2">
```
(If you are incredulous at all this “mixing” of presentation and markup, please do read the linked article above. Trust me, this way of writing CSS is *soooooo* much better than snowflaking every single thing. But, this isn’t the point. The point is we are using third party CSS with Webpack.)  

All told, our template look like so:  
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>WTF Webpack</title>
</head>
<body class="dark-gray bg-light-gray ph4">
	<h1>Markdown Previewer</h1>
	<form id="editor">
		<textarea 
			id="source" 
			rows="10" 
			cols="80" 
			class="w-100 ba br2 pa2 b--black-30">
		</textarea>
		<input 
			type="submit" 
			value="Preview!" 
			class="grow pointer ba br3 bg-washed-green ph3 pv2">
	</form>
	<hr>
	<section id="preview"></section>
</body>
</html>
```

Ok, now we can run Webpack:  
```shell
> rm dev/*.*
```

```shell
yarn dev
```

```shell
yarn run v1.7.0
$ webpack --config ./webpack/development.config.js $npm_package_config_webpack_args
Hash: 7283999e9fec5037eb81
Version: webpack 4.16.3
Time: 1041ms
Built at: 2018-08-11 18:03:23
     Asset       Size  Chunks             Chunk Names
 style.css    112 KiB    main  [emitted]  main
 bundle.js   84.7 KiB    main  [emitted]  main
index.html  696 bytes          [emitted]  
Entrypoint main = style.css bundle.js
[./css/styles.css] 39 bytes {main} [built]
[./js/index.js] 349 bytes {main} [built]
[./js/markdownPreviewer.js] 370 bytes {main} [built]
[./node_modules/webpack/buildin/global.js] (webpack)/buildin/global.js 489 bytes {main} [built]
    + 9 hidden modules
Child html-webpack-plugin for "index.html":
     1 asset
    Entrypoint undefined = index.html
    [./node_modules/html-webpack-plugin/lib/loader.js!./html/index.html] 819 bytes {0} [built]
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
✨  Done in 2.38s.
```

If we open up `dev/index.html`, we’ll see our nicely styled app, courtesy of Tachyons!

![Curtesy of Tachyons!](http://pc97r6al4.bkt.clouddn.com/tachyons-styled-preview.png)  

Don’t get too wrapped up in a) Tachyons or b) how we’ve styled our app The point is that we can mix a third-party CSS framework, along with our own CSS, just like we are doing with JavaScript. This demonstrates that Webpack is a full-fledged asset pipeline.  

And *this* meets our needs as web developers.

