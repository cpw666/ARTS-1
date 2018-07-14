# Week 28th
## Algorithm
[868. Transpose Matrix](https://github.com/charleserious/leetcode/tree/master/JavaScript/Algorithms/TransposeMatrix)
```javascript
/**
 * @param {number[][]} A
 * @returns {number[][]}
 */

const transpose = function (A) {
  const result = new Array(A[0].length);
  for (let i = 0; i < result.length; i++) {
    result[i] = new Array(A.length);
    for (let j = 0; j < result[i].length; j++) {
      result[i][j] = A[j][i];
    }
  }

  return result;
};
```

Two for loops. First we initial an array result as A’s child elements’ length, and we loop in it’s(A’s child elements’) length, and initial an array as A’s length push it into array result. Second we loop in A’s length; And we give the A[j][i] to result[i][j]. Thats all about my solution.

But I found a solution more efficiency
```javascript
/**
 * @param {number[][]} matrix
 * @return {number[][]}
 */
let transpose = (matrix) => {
  return matrix[0].map((col, i) => matrix.map(row => row[i]));
}
```

## Review
[A Quick Introduction to Functional Javascript – Hacker Noon](https://hackernoon.com/a-quick-introduction-to-functional-javascript-7e6fe520e7fa)
This week I want to compliment functional programming with Javascript. As Angelos said in his article, Functional programming allows us to write cleaner, leaner and meaner code without having to worry about side-effects and changing-state. Javascript’s `Array.prototype` methods are really useful in many everyday situations and allow us to apply simple and complex transformations to arrays without repeating ourselves.

We should really think functional programming try programming paradigm in frontend development. Unlike the article mentions nothing of the immutability of the different methods. Some methods mutate the array (such as sort) while others return a new one (such as map).

And this article talks too much about `Array.prototype` s, functional programming in Javascript comes much more, than with the array. I may write a series of articles on that topic.

## Technique
Recently I got a business requirement, self parking payment for a mall, situation is that, customer has parked their car for a while, and want to leave, so they should pay first.

With WeChat pay, we can easily accomplish that, but comes with requirement, customer is has integral and have bought some parking coupon. 
	1. 4 parking coupons per day for VIP;
	2. 800 integral per day for VIP;
	3. 2 parking coupon per day for normal member;
	4. 400 integral per day for normal member;
	5. available with 4 discount hours per day for VIP;
	6. available with 2 discount hours per day for normal member;
	7. initially give the customer best offer for discount;

So, it’s can be done with a normal filter 
```javascript
/**
 * @param {Number} rest_hour available discount hour left per day;
 * @param {Number} rest_integral available integral left per day;
 * @param {Number} rest_coupon available parking coupons left per day;
 */
function initiative_best_offer_combination (need_hour, rest_integral, rest_coupon, rest_hour) {
	const available = {
		integral: 0,
		coupon: 0
	};
	available.coupon    = rest_hour >= rest_coupon ? rest_coupon : rest_hour;
	available.coupon    = available.coupon >= need_hour ? need_hour : available.coupon;
	available.integral  = (available.coupon < need_hour && rest_integral > 0) ? (need_hour - available.coupon) : 0;
	available.integral  = available.integral >= rest_integral ? rest_integral : available.integral;
	available.integral  = available.integral + available.coupon - rest_hour > 0 ? rest_hour - available.coupon : available.integral;
	return available;
}
```

That’s it for best offer.

## Share
Following [Webpack from Nothing - WTF is a Webpack](https://what-problem-does-it-solve.com/webpack/intro.html)
- What problem does webpack solve?
Webpack exists to give us a feature of JavaScript that exists in most other languages by default - modularization.

Webpack implements a module system as well as a way to translate JavaScript code that doesn’t work in any web browser to JavaScript code that works in most web browsers. It’s like a C compiler.

It allows you to write code like this, which is normal in most other modern languages:
```javascript
// inside main.js
import address from 'address';
import billing from 'billing';

billing.some_function();
address.some_other_function();
```

- Webpack from First Principles
Install [Node.js](https://nodejs.org) and comes along with NPM, but we should use [Yarn](https://yarnpkg.com/en/).

```shell
> yarn -y init
yarn init v1.7.0
warning The yes flag has been set. This will automatically answer yes to all questions, which may have security implications.
success Saved package.json
✨  Done in 0.04s.
```

This will create an empty `package.json` for us. Now, let’s install Webpack!

```shell
> yarn add webpack
```

```shell
yarn add v1.7.0
info No lockfile found.
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
[4/4] 📃  Building fresh packages...
success Saved lockfile.
success Saved 239 new dependencies.
info Direct dependencies
└─ webpack@4.16.0
info All dependencies
├─ @webassemblyjs/floating-point-hex-parser@1.5.13
├─ @webassemblyjs/helper-code-frame@1.5.13
├─ @webassemblyjs/helper-fsm@1.5.13
├─ @webassemblyjs/helper-wasm-section@1.5.13
├─ @webassemblyjs/wasm-edit@1.5.13
├─ abbrev@1.1.1
├─ acorn-dynamic-import@3.0.0
├─ acorn@5.7.1
├─ ansi-regex@2.1.1
├─ anymatch@2.0.0
├─ aproba@1.2.0
├─ are-we-there-yet@1.1.5
├─ arr-flatten@1.1.0
├─ asn1.js@4.10.1
├─ assert@1.4.1
├─ assign-symbols@1.0.0
├─ async-each@1.0.1
├─ atob@2.1.1
├─ balanced-match@1.0.0
├─ base@0.11.2
├─ base64-js@1.3.0
├─ big.js@3.2.0
├─ binary-extensions@1.11.0
├─ bluebird@3.5.1
├─ brace-expansion@1.1.11
├─ braces@2.3.2
├─ browserify-aes@1.2.0
├─ browserify-cipher@1.0.1
├─ browserify-des@1.0.2
├─ browserify-sign@4.0.4
├─ browserify-zlib@0.2.0
├─ buffer-from@1.1.0
├─ buffer-xor@1.0.3
├─ buffer@4.9.1
├─ builtin-status-codes@3.0.0
├─ cacache@10.0.4
├─ cache-base@1.0.1
├─ chokidar@2.0.4
├─ chownr@1.0.1
├─ chrome-trace-event@1.0.0
├─ class-utils@0.3.6
├─ code-point-at@1.1.0
├─ collection-visit@1.0.0
├─ commander@2.13.0
├─ commondir@1.0.1
├─ concat-map@0.0.1
├─ concat-stream@1.6.2
├─ console-browserify@1.1.0
├─ console-control-strings@1.1.0
├─ constants-browserify@1.0.0
├─ copy-concurrently@1.0.5
├─ copy-descriptor@0.1.1
├─ core-util-is@1.0.2
├─ create-ecdh@4.0.3
├─ create-hmac@1.1.7
├─ crypto-browserify@3.12.0
├─ cyclist@0.2.2
├─ date-now@0.1.4
├─ decode-uri-component@0.2.0
├─ deep-extend@0.6.0
├─ delegates@1.0.0
├─ des.js@1.0.0
├─ detect-libc@1.0.3
├─ diffie-hellman@5.0.3
├─ domain-browser@1.2.0
├─ duplexify@3.6.0
├─ emojis-list@2.1.0
├─ enhanced-resolve@4.1.0
├─ errno@0.1.7
├─ eslint-scope@3.7.3
├─ esrecurse@4.2.1
├─ estraverse@4.2.0
├─ events@1.1.1
├─ expand-brackets@2.1.4
├─ extglob@2.0.4
├─ fast-deep-equal@2.0.1
├─ fast-json-stable-stringify@2.0.0
├─ fill-range@4.0.0
├─ find-cache-dir@1.0.0
├─ find-up@2.1.0
├─ flush-write-stream@1.0.3
├─ for-in@1.0.2
├─ from2@2.3.0
├─ fs-minipass@1.2.5
├─ fs.realpath@1.0.0
├─ fsevents@1.2.4
├─ gauge@2.7.4
├─ get-value@2.0.6
├─ glob-parent@3.1.0
├─ glob@7.1.2
├─ has-unicode@2.0.1
├─ has-value@1.0.0
├─ has-values@1.0.0
├─ hash.js@1.1.5
├─ hmac-drbg@1.0.1
├─ https-browserify@1.0.0
├─ iconv-lite@0.4.23
├─ ieee754@1.1.12
├─ ignore-walk@3.0.1
├─ indexof@0.0.1
├─ inflight@1.0.6
├─ ini@1.3.5
├─ is-accessor-descriptor@1.0.0
├─ is-binary-path@1.0.1
├─ is-data-descriptor@1.0.0
├─ is-descriptor@1.0.2
├─ is-extglob@2.1.1
├─ is-fullwidth-code-point@1.0.0
├─ is-glob@4.0.0
├─ is-plain-object@2.0.4
├─ is-windows@1.0.2
├─ isarray@1.0.0
├─ json-parse-better-errors@1.0.2
├─ json-schema-traverse@0.4.1
├─ json5@0.5.1
├─ kind-of@3.2.2
├─ loader-runner@2.3.0
├─ loader-utils@1.1.0
├─ locate-path@2.0.0
├─ lodash.debounce@4.0.8
├─ lru-cache@4.1.3
├─ make-dir@1.3.0
├─ map-visit@1.0.0
├─ memory-fs@0.4.1
├─ micromatch@3.1.10
├─ miller-rabin@4.0.1
├─ minimalistic-crypto-utils@1.0.1
├─ minimatch@3.0.4
├─ minimist@0.0.8
├─ minizlib@1.1.0
├─ mississippi@2.0.0
├─ mixin-deep@1.3.1
├─ mkdirp@0.5.1
├─ move-concurrently@1.0.1
├─ nan@2.10.0
├─ nanomatch@1.2.13
├─ needle@2.2.1
├─ node-libs-browser@2.1.0
├─ node-pre-gyp@0.10.3
├─ nopt@4.0.1
├─ npm-bundled@1.0.3
├─ npm-packlist@1.1.10
├─ npmlog@4.1.2
├─ number-is-nan@1.0.1
├─ object-assign@4.1.1
├─ object-copy@0.1.0
├─ os-browserify@0.3.0
├─ os-homedir@1.0.2
├─ os-tmpdir@1.0.2
├─ osenv@0.1.5
├─ p-limit@1.3.0
├─ p-locate@2.0.0
├─ p-try@1.0.0
├─ pako@1.0.6
├─ parallel-transform@1.1.0
├─ pascalcase@0.1.1
├─ path-browserify@0.0.0
├─ path-dirname@1.0.2
├─ path-exists@3.0.0
├─ pify@3.0.0
├─ pkg-dir@2.0.0
├─ posix-character-classes@0.1.1
├─ process-nextick-args@2.0.0
├─ process@0.11.10
├─ promise-inflight@1.0.1
├─ prr@1.0.1
├─ pseudomap@1.0.2
├─ public-encrypt@4.0.2
├─ pump@2.0.1
├─ pumpify@1.5.1
├─ punycode@1.4.1
├─ querystring-es3@0.2.1
├─ querystring@0.2.0
├─ randomfill@1.0.4
├─ rc@1.2.8
├─ readable-stream@2.3.6
├─ readdirp@2.1.0
├─ remove-trailing-separator@1.1.0
├─ repeat-element@1.1.2
├─ resolve-url@0.2.1
├─ ret@0.1.15
├─ rimraf@2.6.2
├─ ripemd160@2.0.2
├─ run-queue@1.0.3
├─ safer-buffer@2.1.2
├─ sax@1.2.4
├─ schema-utils@0.4.5
├─ semver@5.5.0
├─ serialize-javascript@1.5.0
├─ set-blocking@2.0.0
├─ set-immediate-shim@1.0.1
├─ set-value@2.0.0
├─ setimmediate@1.0.5
├─ signal-exit@3.0.2
├─ snapdragon-node@2.1.1
├─ snapdragon-util@3.0.1
├─ source-list-map@2.0.0
├─ source-map-resolve@0.5.2
├─ source-map-url@0.4.0
├─ split-string@3.1.0
├─ ssri@5.3.0
├─ static-extend@0.1.2
├─ stream-browserify@2.0.1
├─ stream-each@1.2.2
├─ stream-http@2.8.3
├─ string_decoder@1.1.1
├─ string-width@1.0.2
├─ strip-ansi@3.0.1
├─ strip-json-comments@2.0.1
├─ tar@4.4.4
├─ through2@2.0.3
├─ timers-browserify@2.0.10
├─ to-arraybuffer@1.0.1
├─ to-regex-range@2.1.1
├─ tslib@1.9.3
├─ tty-browserify@0.0.0
├─ typedarray@0.0.6
├─ uglify-es@3.3.9
├─ uglifyjs-webpack-plugin@1.2.7
├─ union-value@1.0.0
├─ unique-filename@1.1.0
├─ unique-slug@2.0.0
├─ unset-value@1.0.0
├─ upath@1.1.0
├─ uri-js@4.2.2
├─ urix@0.1.0
├─ url@0.11.0
├─ use@3.1.1
├─ util-deprecate@1.0.2
├─ util@0.10.4
├─ vm-browserify@0.0.4
├─ watchpack@1.6.0
├─ webpack-sources@1.1.0
├─ webpack@4.16.0
├─ wide-align@1.1.3
├─ worker-farm@1.6.0
├─ xtend@4.0.1
├─ y18n@4.0.0
└─ yallist@3.0.2
✨  Done in 10.19s.
```

That is a lot of stuff!

```shell
> $(yarn bin)/webpack --version
4.16.0
```

> You’ve now taken your first step into a larger world, which is rife with version incompatibilities, masked or incorrect error messages, and inconsistent behavior, all so you can try to make your life easier while using one of the worst programming languages ever designed! Webpack is one of the least bad things you’ll deal with.  

- A Very Simple Project
Let’s make a directory for our code called `js`:
```shell
> mkdir -p js
```

Now, we’ll make our entry point in `js/index.js` like so:
```javascript
console.log('Hello from index.js!');
import address from './address';
import billing from './billing';

address.announce();
billing.announce();
```

This is referencing two modules, address and billing. We’ll create both of those in `js/.`

This is` js/address.js`:
```javascript
console.log('Hello from address.js');
export default {
	announce: () => {
		console.log('Announcing address.js');
	}
};
```

And this is `js/billing.js`:
```javascript
console.log('Hello from billing.js');
export default {
	announce: () => {
		console.log('Announcing billing.js');
	}
};
```

What we want is to produce a single file called `bundle.js` that uses all this code.

We can do this without configuration per se, and just use CLI options:
```shell
> $(yarn bin)/webpack --entry ./js/index.js  --output-filename=bundle.js
Hash: 8884cfa718ae4c4d06e9
Version: webpack 4.16.0
Time: 113ms
Built at: 2018-07-14 17:51:46
    Asset      Size  Chunks             Chunk Names
bundle.js  1.14 KiB       0  [emitted]  null
[0] ./js/index.js + 2 modules 383 bytes {0} [built]
    | ./js/index.js 143 bytes [built]
    | ./js/address.js 120 bytes [built]
    | ./js/billing.js 120 bytes [built]
```

Now, let’s load this in a browser. Create index.html like so:
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
	<h1>Open the Web Inspector</h1>
</body>
<script src="./dist/bundle.js"></script>
</html>
```

Open this in a browser, then open the JavaScript console. You should see all our messages:

```
Hello from address.js
Hello from billing.js
Hello from index.js!
Announcing address.js
Announcing billing.js
```

We don’t want to be building our JavaScript bundle from an ever-increasingly-complex command-line invocation, so let’s set-up a tiny project structure to keep things organized.

Make `webpack.config.js` look like so:

```javascript
const path = require('path');

module.exports = {
	entry: './js/index.js',
	output: {
		path: path.resolve(__dirname, 'dist'),
		filename: 'bundle.js'
	}
};
```

This will do what we did before with Webpack. 

With this configuration in place, we can run it like so:

```shell
> $(yarn bin)/webpack
Hash: e4c1a4317deb93ba6fcf
Version: webpack 4.16.0
Time: 113ms
Built at: 2018-07-14 18:08:15
    Asset      Size  Chunks             Chunk Names
bundle.js  1.14 KiB       0  [emitted]  main
[0] ./js/index.js + 2 modules 383 bytes {0} [built]
    | ./js/index.js 143 bytes [built]
    | ./js/address.js 120 bytes [built]
    | ./js/billing.js 120 bytes [built]
```

We can open the `index.html` in browser, open the JavaScript console, and see the same messages as before.

The configuration file saves us some keystrokes, but even typing our `$(yarn bin)/webpack` is a bit cumbersome. We’ll use a handy feature of `package.json` to create an alias for running webpack so we can just type `yarn webpack`.

We’ll add a `scripts` key to `package.json`:
```json
"scripts": {
		"webpack": "webpack --config webpack.config.js --display-error-details"
	}
```

Yes, we omit `$(yarn bin)` inside `package.json` like this, it knows to find `webpack` in the right place.

Your entire `package.json` looks like so:
```shell
cat package.json 
```

```json
{
  "name": "wtf-webpack",
  "version": "1.0.0",
  "main": "index.js",
	"license": "MIT",
	"scripts": {
		"webpack": "webpack --config webpack.config.js --display-error-details"
	},
  "dependencies": {
    "webpack": "^4.16.0"
  },
  "devDependencies": {
    "webpack-cli": "^3.0.8"
  }
}
```

And now:

```
> yarn webpack
```

```shell
yarn run v1.7.0
$ webpack --config webpack.config.js --display-error-details
Hash: e4c1a4317deb93ba6fcf
Version: webpack 4.16.0
Time: 136ms
Built at: 2018-07-14 18:29:52
    Asset      Size  Chunks             Chunk Names
bundle.js  1.14 KiB       0  [emitted]  main
[0] ./js/index.js + 2 modules 383 bytes {0} [built]
    | ./js/index.js 143 bytes [built]
    | ./js/address.js 120 bytes [built]
    | ./js/billing.js 120 bytes [built]

```
This is slightly better than a shell alias, we can even check it into source control.

So that’s it. And we’re not even getting started -- this was just an overview of what Webpack even is and why it exists.

Next round we’ll talk about third-party libraries.
