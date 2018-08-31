# Week 35th
## Algorithm
### [806. Number of Lines To Write String](https://leetcode.com/problems/number-of-lines-to-write-string/description/)

#### Description
We are to write the letters of a given string `S`, from left to right into lines. Each line has maximum width 100 units, and if writing a letter would cause the width of the line to exceed 100 units, it is written on the next line. We are given an array `widths`, an array where `widths[0]` is the width of 'a', `widths[1]` is the width of 'b', ..., and `widths[25]` is the width of 'z'.  

Now answer two questions: how many lines have at least one character from `S`, and what is the width used by the last such line? Return your answer as an integer list of length 2.  

#### Example 1
```
Input: 
widths = [10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10]
S = 'abcdefghijklmnopqrstuvwxyz'
Output: [3, 60]
Explanation:
All letters have the same length of 10. To write all 26 letters, we need two full lines and one line with 60 units.
```

#### Example 2
```
Input:
widths = [4, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10]
S = 'bbbcccdddaaa'
Output: [2, 4]
Explanaiton:
All letters except 'a' have the same length of 10, and 'bbbcccdddaaa' will cover 9 * 10 + 2 * 4 = 98 units. For the last 'a', it is written on the second line because there is only 2 units left in the first line. So the answer is 2 lines, plus 4 units in the second line.
```

#### Note
- The length of `S` will be in the range[1, 1000].
- `S` will only contain lowercase letters.
- `widths` is an array of length `26`.
- `widths[i]` will be in the range of `[2, 10]`

#### Solution
```javascript
/**
 * Number of lines to write string
 * @param {Array} widths
 * @param {string} S
 */
const numberOfLines = (widths, S) => {
	const result = [1, 0];
	const length = S.length;
	for (let i = 0; i < length; i++) {
		const charWidth = widths[S.charCodeAt(i) - 97];
		if (result[1] + charWidth > 100) {
			result[0] += 1;
			result[1] = charWidth;
		} else {
			result[1] += charWidth;
		}
	}
	return result;
};
```

#### Explanation
Add up every char's width, greater than 100 go to next line add line number up, and assign current char's width to last line width.  

## Review
[The Cost Of JavaScript – Dev Channel – Medium](https://medium.com/dev-channel/the-cost-of-javascript-84009f51e99e)  

For the past few years diving deep into front end development, something always bothering me: does same size image and JavaScript do the same cost? I always doubted that.  

Thanks Addy for clarifying this question for me and of cause same thing related to this question.  

As Addy wrote in the post we should take this issue separately, into network concern, and hardware concern.  

Take the JavaScript and Image example:  
170K JavaScript bytes === 170K JPEG bytes with Network transmission;
Under Resource Processing things not that easy, JPEG decoded and show, but JavaScript need to be parse and compile and execution.  

So, JavaScript and image bytes have very different costs. And Images usually don’t block the main thread or prevent interfaces from getting interactive while being decoded and rasterized. JavaScript however can delay interactivity due to parse, compile and execution costs.  

Learned that!!!! 

So solutions maybe like below:  
**PRPL Pattern**: for network concern;
**Progressive bootstrapping**: for client side hardware concern;

## Technique
[Sets](https://github.com/charleserious/data-structures-and-algorithms-with-javascript/tree/master/Sets)  

Set is a data structure that consists only of unique elements, such as a list of each unique word in the text.  

Talk less, show me the code:  
```javascript
class Set {
	constructor () {
		this.dataStore = [];
	}

	add (data) {
		const finder = this.dataStore.find(item => item === data);
		const existence = Boolean(finder);
		if (!existence) {
			this.dataStore.push(data);
		}
		return !existence;
	}

	remove (data) {
		const position = this.dataStore.indexOf(data);
		if (position > -1) {
			this.dataStore.splice(position, 1);
			return true;
		}
		return false;
	}

	show () {
		return this.dataStore;
	}

	contains (data) {
		if (this.dataStore.indexOf(data) > -1) {
			return true;
		}
		return false;
	}
	
	union (set) {
		const result = new Set();
		this.dataStore.forEach(element => {
			result.add(element);
		});
		set.show().forEach(element => {
			if (!result.contains(element)) {
				result.add(element);
			}
		});
		return result;
	}

	intersect (set) {
		const result = new Set();
		this.dataStore.forEach(element => {
			if (set.contains(element)) {
				result.add(element);
			}
		});
		return result;
	}

	subset (set) {
		if (this.size() > set.size()) {
			return false;
		}
		const including = (child) => {
			return set.contains(child);
		};
		return this.dataStore.every(including);
	}
	
	size () {
		return this.dataStore.length;
	}

	difference (set) {
		const result = new Set();
		const diff = set.dataStore.filter(child => !this.contains(child));
		diff.forEach(item => result.add(item));
		return result;
	}
}

module.exports = Set;
```

## Share
Following [Webpack from Nothing - Writing Code in Another Language](https://what-problem-does-it-solve.com/webpack/preprocess-js.html)  

JavaScript is not a great programming language. Even with Webpack giving us the ability to write modular code, JavaScript is still a bit weak.  

For example, we have to remember to use `===` everywhere or things get weird. We also have to type keyword `function` a lot. Scoping is a mess, we can’t make constants, and it would be nice to define a proper class that handles `this`.  

[ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) addresses all of these failures in JavaScript, but we can’t run it in a browser. What we can do is translate it *to* JavaScript, allowing us to write modern code that will runs in a browser.  

### Write Modern JavaScript, Ship Compatible JavaScript
To do this with Webpack, we’ll need to set up [Babel · The compiler for next generation JavaScript](https://babeljs.io), which will do the work. Babel advertises itself as a “Compiler” which is also kind of Webpack is. The confusion lies around what is meant by the word “JavaScript”. In Babel’s case, it means “a newer version of JavaScript than your browser can produce”, which is *soft of* what Webpack can do as well. Suffice it to say, Babel handles the newest version of JavaScript *most properly*, so we do need it to accomplish our goal of writing entirely in ES2015.  

Let’s write some! Replace `js/markdownPreviewer.js` with this:  
```javascript
import { markdown } from 'markdown';

const attachPreviewer = ($document, sourceId, previewId) => {
	return (event) => {
		const text = $document.getElementById(sourceId).value;
		const preview = $document.getElementById(previewId);

		preview.innerHTML = markdown.toHTML(text);
		event.preventDefault();
	}
};

export default {
	attachPreviewer: attachPreviewer
}
```

It’s fairly similar, because we don’t have that much, but note what we’ve changed from `function` to using [arrows](https://github.com/lukehoban/es6features#arrows) and we’ve changed our use of `var` to [const](https://github.com/lukehoban/es6features#let--const), since the variables never get assigned more than once.  

Also note that if your run Webpack now, and your are using a modern browser, this code has a good chance of working. But, it won’t work for all browsers, including ones we want to support. Let’s continue.  

First, we’ll install babel. Which, sadly, cannot be accomplished via `yarn add babel`. Instead we muse:  
```shell
> yarn add -D babel-core
```

```shell
yarn add v1.9.4
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
warning " > karma-jasmine@1.1.2" has unmet peer dependency "jasmine-core@*".
[4/4] 📃  Building fresh packages...
success Saved lockfile.
success Saved 17 new dependencies.
info Direct dependencies
└─ babel-core@6.26.3
info All dependencies
├─ babel-core@6.26.3
├─ babel-generator@6.26.1
├─ babel-helpers@6.24.1
├─ babel-register@6.26.0
├─ babel-template@6.26.0
├─ convert-source-map@1.5.1
├─ detect-indent@4.0.0
├─ globals@9.18.0
├─ home-or-tmp@2.0.0
├─ invariant@2.2.4
├─ jsesc@1.3.0
├─ loose-envify@1.4.0
├─ private@0.1.8
├─ slash@1.0.0
├─ source-map-support@0.4.18
├─ to-fast-properties@1.0.3
└─ trim-right@1.0.1
✨  Done in 56.35s.
```

We’ll also need to Babel loader for Webpack:  
```shell
> yarn add -D babel-loader
```

```shell
yarn add v1.9.4
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
warning " > karma-jasmine@1.1.2" has unmet peer dependency "jasmine-core@*".
[4/4] 📃  Building fresh packages...
success Saved lockfile.
success Saved 1 new dependency.
info Direct dependencies
└─ babel-loader@7.1.5
info All dependencies
└─ babel-loader@7.1.5
✨  Done in 4.96s.
```

Babel should prices all JavaScript, so we configure the loader in `webpack/basic.config.js` to handle all `.js` files, save for those in `node_modules`, which are already assumed to be ready for distribution to a browser:  
```javascript
const HtmlPlugin = require('html-webpack-plugin');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
	module: {
		rules: [
			{
				test: /.js$/,
				exclude: /node_modules/,
				loader: 'babel-loader'
			},
			{
				test: /.css$/,
				use: [
					{
						loader: MiniCssExtractPlugin.loader,
						options: {
              publicPath: '../'
            }
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

Of course, Babel doesn’t automatically do anything, so we need more configuration and more modules. Babel has the concept of presets, but of course, none of them are actually pre-set. We’ll use the recommend “env” preset, which means “generally do the right thing without have to configure stuff”, which is a godsend, so we’ll take it.
```shell
> yarn add -D babel-preset-env
```

```shell
yarn add v1.9.4
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
warning " > karma-jasmine@1.1.2" has unmet peer dependency "jasmine-core@*".
[4/4] 📃  Building fresh packages...

success Saved lockfile.
success Saved 40 new dependencies.
info Direct dependencies
└─ babel-preset-env@1.7.0
info All dependencies
├─ babel-helper-builder-binary-assignment-operator-visitor@6.24.1
├─ babel-helper-call-delegate@6.24.1
├─ babel-helper-define-map@6.26.0
├─ babel-helper-explode-assignable-expression@6.24.1
├─ babel-helper-remap-async-to-generator@6.24.1
├─ babel-plugin-check-es2015-constants@6.22.0
├─ babel-plugin-syntax-async-functions@6.13.0
├─ babel-plugin-syntax-exponentiation-operator@6.13.0
├─ babel-plugin-syntax-trailing-function-commas@6.22.0
├─ babel-plugin-transform-async-to-generator@6.24.1
├─ babel-plugin-transform-es2015-arrow-functions@6.22.0
├─ babel-plugin-transform-es2015-block-scoped-functions@6.22.0
├─ babel-plugin-transform-es2015-block-scoping@6.26.0
├─ babel-plugin-transform-es2015-classes@6.24.1
├─ babel-plugin-transform-es2015-computed-properties@6.24.1
├─ babel-plugin-transform-es2015-destructuring@6.23.0
├─ babel-plugin-transform-es2015-duplicate-keys@6.24.1
├─ babel-plugin-transform-es2015-for-of@6.23.0
├─ babel-plugin-transform-es2015-function-name@6.24.1
├─ babel-plugin-transform-es2015-literals@6.22.0
├─ babel-plugin-transform-es2015-modules-amd@6.24.1
├─ babel-plugin-transform-es2015-modules-commonjs@6.26.2
├─ babel-plugin-transform-es2015-modules-systemjs@6.24.1
├─ babel-plugin-transform-es2015-modules-umd@6.24.1
├─ babel-plugin-transform-es2015-object-super@6.24.1
├─ babel-plugin-transform-es2015-parameters@6.24.1
├─ babel-plugin-transform-es2015-shorthand-properties@6.24.1
├─ babel-plugin-transform-es2015-spread@6.22.0
├─ babel-plugin-transform-es2015-sticky-regex@6.24.1
├─ babel-plugin-transform-es2015-template-literals@6.22.0
├─ babel-plugin-transform-es2015-typeof-symbol@6.23.0
├─ babel-plugin-transform-es2015-unicode-regex@6.24.1
├─ babel-plugin-transform-exponentiation-operator@6.24.1
├─ babel-plugin-transform-regenerator@6.26.0
├─ babel-plugin-transform-strict-mode@6.24.1
├─ babel-preset-env@1.7.0
├─ browserslist@3.2.8
├─ caniuse-lite@1.0.30000878
├─ electron-to-chromium@1.3.61
└─ regenerator-transform@0.10.1
✨  Done in 8.17s.
```

Now, create a config file for Babel in the root directory called `.babelrc`(note that this file is JSON and not JavaScript, so it’s far easier to mess up, and you can be sure you won’t get a good error message if you do):
```json
{
	"presets": [
		"env"
	]
}
```

And now, re-run Webpack:
```shell
> yarn dev
```

```shell
yarn run v1.9.4
$ webpack --config ./webpack/development.config.js $npm_package_config_webpack_args
Hash: 39ce64da7870da5fa8c6
Version: webpack 4.16.5
Time: 1629ms
Built at: 2018-08-27 11:16:52
     Asset       Size  Chunks             Chunk Names
 style.css    327 KiB    main  [emitted]  main
 bundle.js    204 KiB    main  [emitted]  main
index.html  696 bytes          [emitted]  
Entrypoint main = style.css bundle.js
[./css/styles.css] 39 bytes {main} [built]
[./js/index.js] 543 bytes {main} [built]
[./js/markdownPreviewer.js] 480 bytes {main} [built]
[./node_modules/webpack/buildin/global.js] (webpack)/buildin/global.js 489 bytes {main} [built]
    + 9 hidden modules
Child html-webpack-plugin for "index.html":
     1 asset
    Entrypoint undefined = index.html
    [./node_modules/html-webpack-plugin/lib/loader.js!./html/index.html] 818 bytes {0} [built]
    [./node_modules/webpack/buildin/global.js] (webpack)/buildin/global.js 489 bytes {0} [built]
    [./node_modules/webpack/buildin/module.js] (webpack)/buildin/module.js 497 bytes {0} [built]
        + 1 hidden module
Child mini-css-extract-plugin node_modules/css-loader/index.js!css/styles.css:
    Entrypoint mini-css-extract-plugin = *
    [./node_modules/css-loader/index.js!./css/styles.css] ./node_modules/css-loader!./css/styles.css 368 bytes {mini-css-extract-plugin} [built]
        + 1 hidden module
Child mini-css-extract-plugin node_modules/css-loader/index.js!node_modules/tachyons/css/tachyons.css:
    Entrypoint mini-css-extract-plugin = *
       2 modules
✨  Done in 2.92s.
```

If you inspect `dev/bundle.js`, you can see that the fancy arrows and use of `const` is gone, replace with old school JavaScript.  

Now, we can write modern JavaScript and note worry about what browsers actually support it.
