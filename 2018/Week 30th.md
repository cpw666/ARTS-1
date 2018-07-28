# Week 30th
## Algorithm
[657. Judge Route Circle - LeetCode](https://leetcode.com/problems/judge-route-circle/description/)
### Description
Initially, there is a Robot a position (0, 0). Given a sequence of its moves, judge if this robot makes a circle, which means it moves back to **the original place**.  

The move sequence is represented by a string. And each move is represent by a character. The valid robot moves are `R`(Right), `L`(Left), `U`(Up) and `D`(down). The output should be true or false representing whether the robot makes a circle.

### Example 1:
```
Input: "UD"
Output: true
```

### Example 2:
```
Input: "LL"
Output: false
```

### Solution
```javascript
/**
 * judge robot's move sequence is a circle or not.
 * @param {string} moves
 * @returns {boolean}
 */
const judgeCircle = (moves) => {
	let x = 0;
	let y = 0;
	const length = moves.length;
	for (let i = 0; i < length; i++) {
		if (moves[i] === 'U') {
			x += 1;
		} else if (moves[i] === 'D') {
			x -= 1;
		} else if (moves[i] === 'L') {
			y -= 1;
		} else if (moves[i] === 'R') {
			y += 1;
		}
	}
	return x === 0 && y === 0;
};

const moves = 'LL';
const result = judgeCircle(moves);
console.log(result);
```

Sorry, I don’t know what is the purpose of this problem.

## Review
[Understanding Position in CSS – Jacob Greenaway – Medium](https://medium.com/@jacobgreenaway12/taming-the-css-beast-master-positioning-5882bad14458)  
This week I comment with this article. 
As author noted the Cheat Sheet:
### Static-Type positioning
`position: static`
	- Default position for all elements;
	- put element in normal flow;

### Relative-Type positioning
`position: relative`
	- Can be offset with **top**, **right**, **bottom** and **left**;
	- Offset relative to *itself*;
	- Creates relative-type positioning context for children.

`position: absolute`
	- Can be offset with **top**, **right**,  **bottom** and **left**;
	- Offset relative to its *nearest relative-type positioned parent*;
	- Creates relative-type positioning context for children;

`position: fixed`
	- Can be offset with **top**, **right**,  **bottom** and **left**;
	- Offset relative to *the viewport*;
	- Creates relative-type positioning context for children;

## Technique
[Queue in JavaScript](https://github.com/charleserious/data-structures-and-algorithms-with-javascript/blob/master/Queue/queue.test.sorting.data.js)  
A *queue* is a type of list where data are inserted at the end and are removed from the front. Queues are used to store data in the order in which they occur, as opposed to a stack, in which the last piece of data entered is the first element used for processing. Think of a queue like the line at your bank, where the first person into the line is the first person served, and as more customers enter a line, they wait in the back until it is their turn to be served.  

A queue is an example of the first-in, first-out(FIFO) data structure. Queues are used to order processes submitted to an operating system or a print spooler, and simulation applications used queues to modern scenarios such as customers standing in the line at bank or grocery store.  

In JavaScript I implement Queue as blow:
```javascript
class Queue {
	constructor () {
		this.dataStore = [];
	}

	enqueue (element) {
		this.dataStore.push(element);
	}

	dequeue () {
		return this.dataStore.shift();
	}

	front () {
		return this.dataStore[0];
	}

	back () {
		return this.dataStore[this.dataStore.length - 1];
	}

	toString () {
		let result = '';
		const length = this.dataStore.length;
		for (let i = 0; i < length; i++) {
			result += this.dataStore[i] + '\n';
		}
		return result;
	}

	empty () {
		if (this.dataStore.length === 0) {
			return true;
		} else {
			return false;
		}
	}
}
```

`dataStore` is the underlying data structure to store the queue elements, it’s an array.  
`enqueue` add elements to the end of a queue.
`dequeue` removes an element from the front of the queue.
`front` examine the front element of a queue.
`back` examine the back element of a queue.
`toString`display all the elements in a queue.
`empty` let us know if a queue is empty.

Let’s test this implementation with sort data:
```javascript
const Queue = require('./queue');

const distribute = (nums, queues, n, digit) => {
	for (let i = 0; i < n; i++) {
		if (digit === 1) {
			queues[nums[i] % 10].enqueue(nums[i]);
		} else {
			queues[Math.floor(nums[i] / 10)].enqueue(nums[i]);
		}
	}
};

const collect = (queues, nums) => {
	let i = 0;
	for (let digit = 0; digit < 10; digit++) {
		while (!queues[digit].empty()) {
			nums[i++] = queues[digit].dequeue();
		}
	}
};

const print = (array) => {
	console.log(array.join(' '));
};

const queues = [];
for (let i = 0; i < 10; i++) {
	queues[i] = new Queue();
}

const nums = [];
for (let i = 0; i < 10; i++) {
	nums[i] = Math.floor(Math.floor(Math.random() * 101));
}

console.log('Before radix sort: ');
print(nums);
distribute(nums, queues, 10, 1);
collect(queues, nums);
distribute(nums, queues, 10, 10);
collect(queues, nums);
console.log('After radix sort: ');
print(nums);
```

Bunch of result:
```shell
Before radix sort: 
23 56 12 16 28 17 72 41 29 6
After radix sort: 
6 12 16 17 23 28 29 41 56 72

Before radix sort: 
13 52 29 60 59 80 62 3 60 6
After radix sort: 
3 6 13 29 52 59 60 60 62 80
```

## Share
Following [Webpack from Nothing - Unit Testing](https://what-problem-does-it-solve.com/webpack/testing.html)  
Unit testing has always been possible in JavaScript, but early test runners required opening a page in a web browser that executed the tests. Because of Node, we now can execute JavaScript on the command line, whiteout a browser, and this is how we’d like to work, because it’s faster and easier to automate.  

Ideally, we want the ability to:  
	- test our modules in isolation;
	- execute a single test while we drive functionality in a module;
	- run tests without having to pop up a browser;
There are many JavaScript testing frameworks, through even the definition of what a *testing framework* is unclear. We’ll start by finding a reasonably complete library that allows us to write tests and assertions.  

[Jasmine](https://jasmine.github.io) fits that bill. It’s reasonably popular and easy to understand.  

First, we’ll add it to our `package.json`. We’ll use `yarn add -D jasmine` pass `-D` which means “this is a development dependency”. That’s important because when we get around to shipping our awesome Markdown previewer to production, we don’t need our development dependencies to be part of that.
```shell
> yarn add -D jasmine
```

```shell
yarn add v1.7.0
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
[4/4] 📃  Building fresh packages...

success Saved lockfile.
success Saved 2 new dependencies.
info Direct dependencies
└─ jasmine@3.1.0
info All dependencies
├─ jasmine-core@3.1.0
└─ jasmine@3.1.0
✨  Done in 2.67s.
```

This will install Jasmine which includes the command-line app jasmine:
```shell
> $(yarn bin)/jasmine -h
Usage: jasmine [command] [options] [files]

Commands:
      init  initialize jasmine
  examples  install examples
   help,-h  show help
version,-v  show jasmine and jasmine-core versions

If no command is given, jasmine specs will be run


Options:
        *--no-color  turn off color in spec output*
         *--filter=  filter specs to run only those that match the given string*
         *--helper=  load helper files that match the given string*
*--stop-on-failure=  [true|false] stop spec execution on expectation failure*
      *--fail-fast=  [true|false] stop Jasmine execution on spec failure*
         *--config=  path to your optional jasmine.json*
       *--reporter=  path to reporter to use instead of the default Jasmine reporter*

The given arguments take precedence over options in your jasmine.json
The path to your optional jasmine.json can also be configured by setting the JASMINE_CONFIG_PATH environment variable
```

Let’s try out that init command.
```shell
> $(yarn bin)/jasmine init
```

OK, now we have tests?
```shell
$(yarn bin)/jasmine
Randomized with seed 27887
Started


No specs found
Finished in 0.002 seconds
Incomplete: No specs found
Randomized with seed 27887 (jasmine --random=true --seed=27887)
```

Not quite. Let’s create a simple no-op spec in `spec/canary.spec.js`:
```javascript
describe('canary', () => {
	it('can run a test', () => {
		expect(true).toBe(true);
	});
});
```

Hopefully, Jasmine’s syntax and API is clear, but the idea is that we use describe to block off a bunch of tests we’ll write, and then it for each test. The idea is that these can be pieced together in some pidgen-like English that developers convince themselves is a specification. It’s silly, but works.  

And now we have a test:
```shell
> $(yarn bin)/jasmine
Randomized with seed 08383
Started
.


1 spec, 0 failures
Finished in 0.008 seconds
Randomized with seed 08383 (jasmine --random=true --seed=08383)
```

OK, what has this to do with Webpack? Well, we need to actually locate our files to test.  
Assuming we could do that, what is the test we’d like to write?  
We’re testing a function that returns a function, so our tests will be on the function that attachPreviewer returns to us. That function should:  
	* call `preventDefault` on the given `event`.
	* render HTML from the markdown in our source element to our preview element.
Let’s write that test first, before we figure out how to get a hold of `attachPreviewer`. In theory, Webpack should help us execute tests and not inform the way in which we write them. In theory.  
In a Jasmine test, your top-level `describe` should be for the module being tested, and then you’d have one `describe` each for the routines you’re going to test. That means our test file will have this form:
```javascript

describe('markdownPreviewr', function () {
	describe('attachPreviewer', function () {
		
	});
});
```
To write our test, we need to make some assumptions about some objects that will need to exist. In particular, we need to have some sort of object that exposes an `innerHTML` property that we can examine to make sure that we’ve rendered `HTML` to it. We also need another object that exposes a `value` property we can use to set the markdown being rendered. And, we need something to stand in for the global `document`, since, as you recall, we’re passing that into `attachPreviewer`. Oh, and an `event`. Don’t worry, we’ll define all these.  

Before we see where those come from, let’s assume they exist so we can write our test.  

First thing is to call `attachPreviewer` and get the function we’re going to execute. Let’s assume (I know, SO MANY assumptions…it’ll work out, I promise) that we have `markdownPreviewer` available, which is our code.
```javascript
var submitHandler = markdownPreviewer.attachPreviewer(document, 'source', 'preview');
```
`document` is assumed to exist, and we’re also assuming that calls to `document.getElementById(“source”)` and `document.getElementById(“preview”)` both work and return objects we can manipulate.
Next, we want to manipulate source:
```javascript
source.value = 'This is _some markdown_';
```

Now, we can call `submitHandler(event)`;
```javascript
submitHandler(event);
```

We also want to make sure that `preventDefault()` was called on `event`, so let’s hand-wave over that like so:
```javascript
expect(preview.innerHTML).toBe('<p>This is <em>some markdown</em></p>');
```

This means our entire test is:
```javascript
describe('markdownPreviewr', function () {
	describe('attachPreviewer', function () {
		it('renders markdown to the preview element', function () {
			var submitHandler = markdownPreviewer.attachPreviewer(document, 'source', 'preview');
			source.value = 'This is _some markdown_';
			submitHandler(event);

			expect(preview.innerHTML).toBe('<p>This is <em>some markdown</em></p>');
			expect(event.preventDefaultCalled).toBe(true);
		});
	});
});
```

We’ve made a ton of assumptions about objects that exist and have behavior, so let’s set that up now. We could use a mocking library, but I’m not willing to go to this level of the yak-shaving quite yet, so let’s hand-jam these.  

First, we’ll make `event`:
```javascript
var event = {
	preventDefaultCalled: false,
	preventDefault: function () { this.preventDefaultCalled = true; }
};
```

We know our code should call `preventDefault`, so we implement that to record that it was called in a way we can check in our test.  

Next, we need our `DOM` elements, source, and `preview`:
```javascript
var source = {
	value: ''
};

var preview = {
	innerHTML: ''
};
```

Pretty straightforward. Now, we need a mock `document` implementation that will return them. All this has to do is implement `getElementById` and we can hardcode its behavior:
```javascript
var document = {
  getElementById: function(id) {
    if (id === "source") {
      return source;
    }
    else if (id === "preview") {
      return preview;
    }
    else {
      throw "Don't know how to get " + id;
    }
  }
}
```

Again, mocking might be better for a larger project, but this is enough to get us going and our test should work.  

Except we still need access to *our* code.  

This is JavaScript. We know this.
```javascript
import markdownPreviewer from "../js/markdownPreviewer";
```

Seems like it should work. Here’s the entire test file:
```javascript
import markdownPreviewer from "../js/markdownPreviewer";

var event = {
	preventDefaultCalled: false,
	preventDefault: function () { this.preventDefaultCalled = true; }
};

var source = {
	value: ''
};

var preview = {
	innerHTML: ''
};

var document = {
	getElementById: function (id) {
		if (id === 'source') {
			return source;
		} else if (id === 'preview') {
			return preview;
		} else {
			throw 'Do\'t know how to get ' + id;
		}
	}
};

describe('markdownPreviewr', function () {
	describe('attachPreviewer', function () {
		it('renders markdown to the preview element', function () {
			var submitHandler = markdownPreviewer.attachPreviewer(document, 'source', 'preview');
			source.value = 'This is _some markdown_';
			submitHandler(event);

			expect(preview.innerHTML).toBe('<p>This is <em>some markdown</em></p>');
			expect(event.preventDefaultCalled).toBe(true);
		});
	});
});
```

Let’s run our test and be excited!
```shell
> $(yarn bin)/jasmine
```

Welp, no output. Isn’t this wonderful? While Jasmine *did* exit nonzero, which tells us that something failed, its seems to have straight-up crashed. In older versions of Jasmine we saw the real problem—Jasmine doesn’t understand `import` and can’t compile the code. Now, it just does nothing.  

What we need to do is use Webpack to compile our test code as well.  

Unfortunately, it isn’t that easy. This won’t work:

```shell
$(yarn bin)/webpack --entry=./spec/markdownPreviewer.spec.js --output-file=spec.js
```

But, even if it did, what do we *do* with `spec.js`? Jasmine’s test runner (the jasmine command-line app) is expecting some JavaScript files that call describe and it. We could try doing something like

```javascript
import describe from "jasmine"
```

But you’ll get an error about `fs` which you’ve never heard of and didn’t ask to use. Ugh.  

In my experience, when things Completely Fail to Work at Even a Basic Level™, it tells me that I’ve made the wrong choice at some level higher than the code.  

In this case, it’s our choice of test runner. Note that I didn’t say test *framework*, but test *runner*. Why are these even different things? What kind of test framework can’t run tests?  

In the JavaScript ecosystem: pretty much all of them.  

Because each project is a chance to artisnally hand-craft a small batch tool chain, and because the language we’re using can’t even agree on something basic like how to modularize code, we end up with lots of tools that cannot interoperate together at all.  

In this case, our desire to use import conflicts with Jasmine’s inability to handle it.  

What we need is a test runner that can both use Webpack to assemble our code, but also execute our tests using Jasmine.  

That test runner that is  [Karma](https://karma-runner.github.io/1.0/index.html) .  

### Karma: What Problem Does it Solve?
Karma executes tests, and is yet another tool where you learn about it by reading blog posts and pasting JSON boilerplate into your project and praying nothing goes wrong. As mentioned previously, that’s not good enough.


What we need is a test runner that can both use Webpack to assemble our code, but also execute our tests using Jasmine.
That test runner that is  [Karma](https://karma-runner.github.io/1.0/index.html) .
# Karma: What Problem Does it Solve?
Karma executes tests, and is yet another tool where you learn about it by reading blog posts and pasting JSON boilerplate into your project and praying nothing goes wrong. As mentioned previously, that’s not good enough.  

We know that it has the ability to solve our problelm (mostly because I’m telling you in advance that this is the case), so let’s see exactly how.  

First, we’ll install it
```shell
> yarn add -D karma
```

```shell
yarn add -D karma
yarn add v1.7.0
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
[4/4] 📃  Building fresh packages...
success Saved lockfile.
success Saved 162 new dependencies.
info Direct dependencies
└─ karma@2.0.4
info All dependencies
├─ accepts@1.3.5
├─ addressparser@1.0.1
├─ after@0.8.2
├─ amqplib@0.5.2
├─ array-slice@0.2.3
├─ arraybuffer.slice@0.0.7
├─ asn1@0.2.3
├─ ast-types@0.11.5
├─ async-limiter@1.0.0
├─ async@2.6.1
├─ aws-sign2@0.7.0
├─ aws4@1.7.0
├─ axios@0.15.3
├─ backo2@1.0.2
├─ base64id@1.0.0
├─ bcrypt-pbkdf@1.0.2
├─ bitsyntax@0.0.4
├─ bl@1.1.2
├─ blob@0.0.4
├─ body-parser@1.18.3
├─ buildmail@4.0.1
├─ callsite@1.0.0
├─ caseless@0.12.0
├─ circular-json@0.5.5
├─ colors@1.3.0
├─ combine-lists@1.0.1
├─ combined-stream@1.0.6
├─ component-bind@1.0.0
├─ component-inherit@0.0.3
├─ connect@3.6.6
├─ content-type@1.0.4
├─ cookie@0.3.1
├─ core-js@2.5.7
├─ cryptiles@2.0.5
├─ custom-event@1.0.1
├─ dashdash@1.14.1
├─ data-uri-to-buffer@1.2.0
├─ deep-is@0.1.3
├─ degenerator@1.0.4
├─ delayed-stream@1.0.0
├─ di@0.0.1
├─ dom-serialize@2.2.1
├─ double-ended-queue@2.1.0-0
├─ ecc-jsbn@0.1.1
├─ ee-first@1.1.1
├─ encodeurl@1.0.2
├─ engine.io-client@3.1.6
├─ engine.io-parser@2.1.2
├─ engine.io@3.1.5
├─ ent@2.2.0
├─ es6-promise@4.2.4
├─ es6-promisify@5.0.0
├─ escape-html@1.0.3
├─ escodegen@1.11.0
├─ esprima@3.1.3
├─ esutils@2.0.2
├─ eventemitter3@3.1.0
├─ expand-braces@0.1.2
├─ expand-range@0.1.1
├─ extend@3.0.1
├─ extsprintf@1.3.0
├─ fast-levenshtein@2.0.6
├─ file-uri-to-path@1.0.0
├─ finalhandler@1.1.0
├─ follow-redirects@1.5.1
├─ form-data@2.3.2
├─ ftp@0.3.10
├─ generate-function@2.0.0
├─ generate-object-property@1.2.0
├─ get-uri@2.0.2
├─ getpass@0.1.7
├─ har-schema@2.0.0
├─ har-validator@5.0.3
├─ has-ansi@2.0.0
├─ hawk@3.1.3
├─ hipchat-notifier@1.1.0
├─ http-errors@1.6.3
├─ http-proxy@1.17.0
├─ http-signature@1.2.0
├─ httpntlm@1.6.1
├─ httpreq@0.4.24
├─ inflection@1.12.0
├─ is-my-ip-valid@1.0.0
├─ is-my-json-valid@2.17.2
├─ is-property@1.0.2
├─ isbinaryfile@3.0.2
├─ json-schema@0.2.3
├─ jsonpointer@4.0.1
├─ karma@2.0.4
├─ levn@0.3.0
├─ log4js@2.11.0
├─ loggly@1.1.1
├─ mailcomposer@4.0.1
├─ mailgun-js@0.18.1
├─ media-typer@0.3.0
├─ mime-db@1.33.0
├─ mime@1.6.0
├─ negotiator@0.6.1
├─ netmask@1.0.6
├─ node-uuid@1.4.8
├─ nodemailer-direct-transport@3.3.2
├─ nodemailer-smtp-pool@2.8.2
├─ nodemailer-smtp-transport@2.7.2
├─ nodemailer@2.7.2
├─ oauth-sign@0.8.2
├─ object-component@0.0.3
├─ optimist@0.6.1
├─ optionator@0.8.2
├─ pac-proxy-agent@2.0.2
├─ pac-resolver@3.0.0
├─ path-proxy@1.0.0
├─ performance-now@2.1.0
├─ pinkie-promise@2.0.1
├─ pinkie@2.0.4
├─ promisify-call@2.0.4
├─ proxy-agent@3.0.1
├─ proxy-from-env@1.0.0
├─ qjobs@1.2.0
├─ qs@6.5.2
├─ range-parser@1.2.0
├─ raw-body@2.3.3
├─ redis-commands@1.3.5
├─ redis-parser@2.6.0
├─ redis@2.8.0
├─ request@2.87.0
├─ requestretry@1.13.0
├─ requires-port@1.0.0
├─ setprototypeof@1.1.0
├─ slack-node@0.2.0
├─ smart-buffer@1.1.15
├─ sntp@1.0.9
├─ socket.io-adapter@1.1.1
├─ socket.io-client@2.0.4
├─ socket.io@2.0.4
├─ socks-proxy-agent@4.0.1
├─ socks@1.1.9
├─ statuses@1.5.0
├─ streamroller@0.7.0
├─ stringstream@0.0.6
├─ thunkify@2.1.2
├─ timespan@2.3.0
├─ to-array@0.1.4
├─ tough-cookie@2.3.4
├─ tsscmp@1.0.5
├─ tunnel-agent@0.6.0
├─ tweetnacl@0.14.5
├─ type-is@1.6.16
├─ ultron@1.1.1
├─ underscore@1.7.0
├─ unpipe@1.0.0
├─ useragent@2.2.1
├─ utils-merge@1.0.1
├─ uuid@3.3.2
├─ uws@9.14.0
├─ verror@1.10.0
├─ void-elements@2.0.1
├─ when@3.7.8
├─ with-callback@1.0.2
├─ wordwrap@0.0.3
├─ xmlhttprequest-ssl@1.5.5
├─ xregexp@2.0.0
└─ yeast@0.1.2
✨  Done in 39.45s.
```

Check that it’s installed:
```shell
> $(yarn bin)/karma --version
Karma version: 2.0.4
```

Because Karma has no default test framework, we must install one for the framework we’re using. In this case, that’s Jasmine:
```
> yarn add -D karma-jasmine
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
└─ karma-jasmine@1.1.2
info All dependencies
└─ karma-jasmine@1.1.2
✨  Done in 3.42s.
```

Why not just instal `karma-jasmine` and have that pick up the dependency on `karma`? No idea. This is JavaScript, and we don’t get nice things.  

OK, now what? Karma’s homepage currently states:
> The main goal for Karma is to bring a productive testing environment to developers. The environment being one where they don’t have to set up loads of configurations, but rather a place where developers can just write the code and get instant feedback from their tests.  

It’s OK to chuckle at their proclaimation that we don’t need loads of configuration. Spoiler: we will.  

It’s common to use `karma init` to create a config file to start off with but this a) requires interactive input, b) places the file in the current directory, and c) creates a file with way more configuration than is technically needed. We don’t want any of that, so create `spec/karma.conf.js` yourself. The bare minimum information you have to provide is:
	- What testing frameworks are being used (Jasmine, in our case)
	- Where the actual test files are (spec/ in our case)
	- What browsers we want to run the code in. (See below for why we have to care about browsers)  
	- 
There’s no technical reason to have to provide any of this information, but JavaScript doesn’t want to tell you where to put your files or what testing frameworks to use. It’s cool with anything, so you do you (even though your job is to get things done and not evaluate a bunch of essentially equivalent testing frameworks).  

The mimimal configuration would the following, which you should place into `spec/karma.conf.js`:
```javascript
module.exports = function(config) {
  config.set({
    frameworks: ['jasmine'],
    files: [
      '**/*.spec.js'
    ],
    browsers: ['PhantomJS']
  })
}
```

Note that the location of our test files is relative to wherever the config file is. Since we put it in `spec/`, `**/*.spec.js` means “all the files in spec/ that end in `.spec.js`.  

But I’m burying the lede. We had to do something with browsers. I know and I’m really sorry, but this is how it has to be.  

On the one hand, this is terrible, because anything involving a browser will be incredibly slow and clunky. But, on the other hand, our code will only ever run in a browser, so as good developers that’s technically the right place to test it.

PhantomJS is a browser that runs headlessly, meaning it’s the only way to run our tests, with Karma, on the command line.  

I know this sucks, and you should brace yourself for a terrible testing experience that’s worse than all other ecosystems, but let’s just give thanks that it’s possible and that we don’t have to pop up Firefox and deal with all that.  

So…you’ll need to install  [PhantomJS](http://phantomjs.org/download.html)  if you haven’t. When you do that, you can test your install thusly:
```shell
> brew install phantomjs

> phantomjs --version
2.1.1
```

You’ll also need to install the PhantomJS launcher for Karma so it can execute PhantomJS. Because again, why would you want your testing tool telling you how to write tests? Clearly, what you want is a test runner that by default cannot run any tests in any browser. The JavaScript ecosystem is all about choices. Endless, endless choices.
```shell
> yarn add -D karma-phantomjs-launcher
```

```shell
yarn add v1.7.0
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
[4/4] 📃  Building fresh packages...
success Saved lockfile.
success Saved 14 new dependencies.
info Direct dependencies
└─ karma-phantomjs-launcher@1.0.4
info All dependencies
├─ extract-zip@1.6.7
├─ fd-slicer@1.0.1
├─ fs-extra@1.0.0
├─ hasha@2.2.0
├─ jsonfile@2.4.0
├─ karma-phantomjs-launcher@1.0.4
├─ kew@0.7.0
├─ klaw@1.3.1
├─ pend@1.2.0
├─ phantomjs-prebuilt@2.1.16
├─ progress@1.1.8
├─ request-progress@2.0.1
├─ throttleit@1.0.0
└─ yauzl@2.4.1
✨  Done in 5.91s.
```

With that done, we can now run our tests:
```shell
$(yarn bin)/karma start spec/karma.conf.js --single-run --no-color
```

```shell
16 07 2018 13:17:02.760:INFO [karma]: Karma v2.0.4 server started at http://0.0.0.0:9876/
16 07 2018 13:17:02.763:INFO [launcher]: Launching browser PhantomJS with unlimited concurrency
16 07 2018 13:17:02.769:INFO [launcher]: Starting browser PhantomJS
16 07 2018 13:17:04.146:INFO [PhantomJS 2.1.1 (Mac OS X 0.0.0)]: Connected on socket HlKQVOffHTTsEE6TAAAA with id 69066424
PhantomJS 2.1.1 (Mac OS X 0.0.0) ERROR
  {
    “message”: “An error was thrown in afterAll\nSyntaxError: Unexpected token ‘)’\nSyntaxError: Use of reserved word ‘import’”,
    “str”: “An error was thrown in afterAll\nSyntaxError: Unexpected token ‘)’\nSyntaxError: Use of reserved word ‘import’”
  }
PhantomJS 2.1.1 (Mac OS X 0.0.0): Executed 0 of 0 ERROR (0.006 secs / 0 secs)
```

The `—single-run` means “actually run the tests and report the results”. Without it, Karma sits there waiting for you to navigate to a web server it starts up that then runs the tests. Trust me, this is the best it gets for now.  

You’ll notice it failed with the same error as before. The difference here, is that Karma is sophisticated enough such that we can throw more JSON at it to fix the problem.  

We need to have our tests use Webpack to bundle up our JavaScript so we can access it and run tests against it.  

Karma’s configuration file has an option called preprocessors that allows us to do stuff to our code before it runs the tests. There is such a preprocessor called karma-webpack that we can install and configure. First, we’ll add it:
```shell
yarn add -D karma-webpack
```

```shell
yarn add v1.7.0
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies..
[4/4] 📃  Building fresh packages...
success Saved lockfile.
success Saved 20 new dependencies.
info Direct dependencies
└─ karma-webpack@3.0.0
info All dependencies
├─ array-find-index@1.0.2
├─ babel-runtime@6.26.0
├─ currently-unhandled@0.4.1
├─ define-properties@1.1.2
├─ es5-ext@0.10.45
├─ es6-iterator@2.0.3
├─ foreach@2.0.5
├─ function-bind@1.1.1
├─ has-symbols@1.0.0
├─ karma-webpack@3.0.0
├─ log-symbols@2.2.0
├─ loglevelnext@1.0.5
├─ loud-rejection@1.6.0
├─ next-tick@1.0.0
├─ object-keys@1.0.12
├─ object.assign@4.1.0
├─ regenerator-runtime@0.11.1
├─ url-join@2.0.5
├─ webpack-dev-middleware@2.0.6
└─ webpack-log@1.2.0
✨  Done in 8.26s.
```

Now, we’ll add it as a preprocessor and use require to bring in our existing Webpack config (not import. Sigh). Your entire `spec/karma.conf.js` will look like so:
```javascript
module.exports = function(config) {
  config.set({
    frameworks: ['jasmine'],
    files: [
      '**/*.spec.js'
    ],
*/* start new code */*
    preprocessors: {
      '**/*.spec.js': [ 'webpack' ]
    },
    webpack: require('../webpack.config.js'),
*/* end new code */*
    browsers: ['PhantomJS']
  })
}
```

And wouldn’t you know it, it works!
```shell
> $(yarn bin)/karma start spec/karma.conf.js  --single-run --no-color
```

```shell
(node:10949) DeprecationWarning: Tapable.plugin is deprecated. Use new API on `.hooks` instead
ℹ ｢wdm｣: wait until bundle finished: noop
ℹ ｢wdm｣: wait until bundle finished: noop
⚠ ｢wdm｣: Hash: d127ba45a6770c48cb40
Version: webpack 4.16.0
Time: 11123ms
Built at: 2018-07-16 14:06:09
                    Asset      Size  Chunks             Chunk Names
                     main  77.1 KiB       0  [emitted]  main
markdownPreviewer.spec.js  25.9 KiB       1  [emitted]  markdownPreviewer.spec.js
           canary.spec.js  1.05 KiB       2  [emitted]  canary.spec.js
Entrypoint main = main
Entrypoint canary.spec.js = canary.spec.js
Entrypoint markdownPreviewer.spec.js = markdownPreviewer.spec.js
 [0] ./node_modules/markdown/lib/index.js 143 bytes {0} {1} [built]
 [1] ./js/markdownPreviewer.js 370 bytes {0} {1} [built]
 [2] ./node_modules/inherits/inherits_browser.js 672 bytes {0} {1} [built]
 [3] ./node_modules/util/support/isBufferBrowser.js 203 bytes {0} {1} [built]
 [4] ./node_modules/process/browser.js 5.29 KiB {0} {1} [built]
 [5] (webpack)/buildin/global.js 489 bytes {0} {1} [built]
 [6] ./node_modules/util/util.js 15.2 KiB {0} {1} [built]
 [7] ./node_modules/markdown/lib/markdown.js 49.8 KiB {0} {1} [built]
 [8] ./spec/markdownPreviewer.spec.js 893 bytes {1} [built]
 [9] ./spec/canary.spec.js 104 bytes {2} [built]
[10] ./js/index.js 302 bytes {0} [built]

WARNING in configuration
The 'mode' option has not been set, webpack will fallback to 'production' for this value. Set 'mode' option to 'development' or 'production' to enable defaults for each environment.
You can also set it to 'none' to disable any default behavior. Learn more: https://webpack.js.org/concepts/mode/
ℹ ｢wdm｣: Compiled with warnings.
16 07 2018 14:06:09.572:INFO [karma]: Karma v2.0.4 server started at http://0.0.0.0:9876/
16 07 2018 14:06:09.573:INFO [launcher]: Launching browser PhantomJS with unlimited concurrency
16 07 2018 14:06:09.584:INFO [launcher]: Starting browser PhantomJS
16 07 2018 14:06:10.941:INFO [PhantomJS 2.1.1 (Mac OS X 0.0.0)]: Connected on socket MA-9_GmX4spCBZV-AAAA with id 804174
PhantomJS 2.1.1 (Mac OS X 0.0.0): Executed 2 of 2 SUCCESS (0.002 secs / 0.009 secs)
TOTAL: 2 SUCCESS
✨  Done in 3.63s.
```

I’m not going to lie, I was not expecting this to work at all, especially with this fairly minimal amount of configuration. While it’s not ergonomic or developer-friendly, it does work, and it was easy enough to figure out just by reading documentation. Take that Medium thinkpieces!  

Before we move on, let’s wrap this up into a script inside `package.json`, because typing all this out sucks.  
```json
"scripts": {
		"webpack": "webpack --config webpack.config.js --display-error-details",
		"karma": "karma start spec/karma.conf.js --single-run --no-color"
  }
```

Now, we can run tests with `yarn karma`:
```shell
> yarn karma*
```

```shell
yarn run v1.7.0
$ karma start spec/karma.conf.js --single-run --no-color
(node:10949) DeprecationWarning: Tapable.plugin is deprecated. Use new API on `.hooks` instead
ℹ ｢wdm｣: wait until bundle finished: noop
ℹ ｢wdm｣: wait until bundle finished: noop
⚠ ｢wdm｣: Hash: d127ba45a6770c48cb40
Version: webpack 4.16.0
Time: 11123ms
Built at: 2018-07-16 14:06:09
                    Asset      Size  Chunks             Chunk Names
                     main  77.1 KiB       0  [emitted]  main
markdownPreviewer.spec.js  25.9 KiB       1  [emitted]  markdownPreviewer.spec.js
           canary.spec.js  1.05 KiB       2  [emitted]  canary.spec.js
Entrypoint main = main
Entrypoint canary.spec.js = canary.spec.js
Entrypoint markdownPreviewer.spec.js = markdownPreviewer.spec.js
 [0] ./node_modules/markdown/lib/index.js 143 bytes {0} {1} [built]
 [1] ./js/markdownPreviewer.js 370 bytes {0} {1} [built]
 [2] ./node_modules/inherits/inherits_browser.js 672 bytes {0} {1} [built]
 [3] ./node_modules/util/support/isBufferBrowser.js 203 bytes {0} {1} [built]
 [4] ./node_modules/process/browser.js 5.29 KiB {0} {1} [built]
 [5] (webpack)/buildin/global.js 489 bytes {0} {1} [built]
 [6] ./node_modules/util/util.js 15.2 KiB {0} {1} [built]
 [7] ./node_modules/markdown/lib/markdown.js 49.8 KiB {0} {1} [built]
 [8] ./spec/markdownPreviewer.spec.js 893 bytes {1} [built]
 [9] ./spec/canary.spec.js 104 bytes {2} [built]
[10] ./js/index.js 302 bytes {0} [built]

WARNING in configuration
The 'mode' option has not been set, webpack will fallback to 'production' for this value. Set 'mode' option to 'development' or 'production' to enable defaults for each environment.
You can also set it to 'none' to disable any default behavior. Learn more: https://webpack.js.org/concepts/mode/
ℹ ｢wdm｣: Compiled with warnings.
16 07 2018 14:06:09.572:INFO [karma]: Karma v2.0.4 server started at http://0.0.0.0:9876/
16 07 2018 14:06:09.573:INFO [launcher]: Launching browser PhantomJS with unlimited concurrency
16 07 2018 14:06:09.584:INFO [launcher]: Starting browser PhantomJS
16 07 2018 14:06:10.941:INFO [PhantomJS 2.1.1 (Mac OS X 0.0.0)]: Connected on socket MA-9_GmX4spCBZV-AAAA with id 804174
PhantomJS 2.1.1 (Mac OS X 0.0.0): Executed 2 of 2 SUCCESS (0.002 secs / 0.009 secs)
TOTAL: 2 SUCCESS
✨  Done in 3.63s.
```

