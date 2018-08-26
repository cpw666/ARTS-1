# Week 34th
## Algorithm
### [876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/description/)

#### Description
Given a non-empty, singly linked list with head node `head`, return a middle node of linked list.  
If there are two middle nodes, return the second middle node.

#### Example 1
```
Input: [1, 2, 3, 4, 5]
Output: Node 3 from this list (Serialization: [3, 4, 5])
The returned node has value 3. (The judge's serialization of this node is [3, 4, 5]).
Note that we returned a ListNode object ans, such that:
ans.val = 3, ans.next.val = 4, ans.next.next.val = 5, and ans.next.next.next.val = NULL.
```

#### Example 2
```
Input: [1, 2, 3, 4, 5, 6]
Output: Node 4 from this list (Serialization: [4, 5, 6])
Since the list has two middle nodes with values 3 and 4, we return the second one.
```

#### Note
- The number of nodes in the given list will be between `1` and `100`.

#### Solution 1
```javascript
// class ListNode {
// 	constructor (val) {
// 		this.val = val;
// 		this.next = null;
// 	}
// }

/**
 * Middle Node of the LinedList
 * @param {ListNode} head
 * @returns {ListNode}
 */
const middleNode = (head) => {
	let fastPtr = head;
	let slowPtr = head;
	while (fastPtr !== null && fastPtr.next !== null) {
		fastPtr = fastPtr.next.next;
		slowPtr = slowPtr.next;
	}
	return slowPtr;
};
```

#### Explanation 1
It's just a fast pointer and slow pointer problem  
  
## Review
[How JavaScript works: Event loop and the rise of Async programming + 5 ways to better coding with async/await](https://blog.sessionstack.com/how-javascript-works-event-loop-and-the-rise-of-async-programming-5-ways-to-better-coding-with-2f077c4438b5)  

[Tutorial – SessionStack Blog](https://blog.sessionstack.com/tagged/tutorial) this link to a series article on **How JavaScript Works**.  

Here is my review on this fourth post.  
1. **Clean code**: Using async/await allows you to write a lot less code. Every time you use async/await you skip a few unnecessary steps: write `.then`, create an anonymous function to handle the response, name the response from that call back.  
2. **Error handling**: Async/await makes it possible to handle both sync and async errors with the same code construct `try/catch`.  
3. **Conditionals**: Writing conditional code with `async/await` is a lot more straightforward
4. **Stack Frames**: Unlike with `async/await`, the error stack returned from a promise chain gives no clue of where the error happened.
5. **Debugging**: If you have used promises, you know that debugging them is a nightmare. For example, if you set a breakpoint inside a `.then` block and use debug shortcuts like “step-over”, the debugger will not move to the following `.then` because it only “steps” though synchronous code. With `async/await` you can step through await calls exactly as if they were normal synchronous functions.  

## Technique
[Dictionary](https://github.com/charleserious/data-structures-and-algorithms-with-javascript/blob/master/Dictionary/dictionary.test.js)  

A dictionary is a data structure that stores data as *key-value* pairs, such as the way you phone contact stores it’s data as names and phone numbers.  

When you look for a phone number, you first search for the name, and you find the name, the phone number is found right next to the name.  

The key is the element you use to perform a search, and the value is the result of the search.  

The JavaScript Object class is designed to operate as a dictionary. In my implementation I’ll use the features of the Object Class to build a Dictionary.  

`datasource` for underlying store.  
`add()` add data to `datasourcd`.  
`find()` find value in `datasource` though key.  
`remove()` remove specific element match the key.  
`showAll()` show all the key-value pairs.  
`count()` count the total element in `datasource`.  
`clear()` clear `datasourcd`

Here is the code:  

```javascript
class Dictionary {
	constructor () {
		this.datasource = new Array();
	}

	add (key, value) {
		this.datasource[key] = value;
	}

	find (key) {
		return this.datasource[key];
	}

	remove (key) {
		delete this.datasource[key];
	}

	showAll () {
		Object.keys(this.datasource).sort().forEach(key => {
			console.log(key, '->', this.datasource[key]);
		});
	}

	count () {
		return Object.keys(this.datasource).length;
	}

	clear () {
		Object.keys(this.datasource).forEach(key => {
			delete this.datasource[key];
		});
	}
}
```

## Share
Following [Auto-reload Code When You Change It](https://what-problem-does-it-solve.com/webpack/dev_server.html)  

We’ve got all the right tools in places to build, manage, test, deploy, and debug our application. But it’s all really really slow. We can make this faster by using Webpack’s *dev server*. But first, a word on workflow.  

### A Reliable Development Workflow
We’ve been talking about JavaScript and CSS, but at the end of the day, you are building a web application, and that means there is some logic and code that must exist. This logic and code is likely the biggest source of complexity in your application. While CSS and UI is certainly complex, it pales in comparison to what is typically required to build an actual web application.  

Because of this, your default workflow should be a test-driven one. You should not run your application to verify that its underlying logic is working correctly — you should run a test of that logic.  

Granted, our markdown previewer doesn’t have a lot of such logic, but it is important to understand that a “week and reload” style of development is the slowest style of development.  

Unfortunately, for UI work, there isn’t a great substitute, so let’s see how Webpack helps.  

### Auto-reloading On Changes  
Webpack is super slow:  
```shell
> time yarn dev
```

```shell
yarn run v1.9.4
$ webpack --config ./webpack/development.config.js $npm_package_config_webpack_args
Hash: b1e42d255ad8582c38f1
Version: webpack 4.16.3
Time: 1400ms
Built at: 2018-08-22 12:31:08
     Asset       Size  Chunks             Chunk Names
 style.css    327 KiB    main  [emitted]  main
 bundle.js    204 KiB    main  [emitted]  main
index.html  693 bytes          [emitted]  
Entrypoint main = style.css bundle.js
[./css/styles.css] 39 bytes {main} [built]
[./js/index.js] 349 bytes {main} [built]
[./js/markdownPreviewer.js] 370 bytes {main} [built]
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
✨  Done in 3.38s.

real	0m4.213s
user	0m3.523s
sys	0m0.545s
```

When designing a UI, you need to change markup, CSS, and JavaScript. It’s often not possible to assure that JavaScript is providing UI interactions you want without trying it, and that’s lots of small changes that you reload in the browser. Having to wait 3+ seconds each time sucks.  

We can make this a bit better by using `webpack-dev-server`, which we can install with yarn:  

```shell
> yarn add webpack-dev-server -D
```

```shell
yarn add v1.9.4
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
warning " > karma-jasmine@1.1.2" has unmet peer dependency "jasmine-core@*".
[4/4] 📃  Building fresh packages...
success Saved lockfile.
success Saved 97 new dependencies.
info Direct dependencies
└─ webpack-dev-server@3.1.5
info All dependencies
├─ ansi-html@0.0.7
├─ array-flatten@1.1.1
├─ array-includes@3.0.3
├─ array-union@1.0.2
├─ array-uniq@1.0.3
├─ batch@0.6.1
├─ bonjour@3.5.0
├─ buffer-indexof@1.1.1
├─ builtin-modules@1.1.1
├─ camelcase-keys@2.1.0
├─ compressible@2.0.14
├─ compression@1.7.3
├─ connect-history-api-fallback@1.5.0
├─ content-disposition@0.5.2
├─ cookie-signature@1.0.6
├─ decamelize@1.2.0
├─ deep-equal@1.0.1
├─ del@3.0.0
├─ destroy@1.0.4
├─ detect-node@2.0.3
├─ dns-equal@1.0.0
├─ dns-packet@1.3.1
├─ dns-txt@2.0.2
├─ error-ex@1.3.2
├─ eventsource@0.1.6
├─ express@4.16.3
├─ faye-websocket@0.10.0
├─ forwarded@0.1.2
├─ get-stdin@4.0.1
├─ globby@6.1.0
├─ handle-thing@1.2.5
├─ hosted-git-info@2.7.1
├─ hpack.js@2.1.6
├─ html-entities@1.2.1
├─ http-deceiver@1.2.7
├─ http-parser-js@0.4.13
├─ http-proxy-middleware@0.18.0
├─ indent-string@2.1.0
├─ internal-ip@1.2.0
├─ ipaddr.js@1.8.0
├─ is-arrayish@0.2.1
├─ is-builtin-module@1.0.0
├─ is-finite@1.0.2
├─ is-path-cwd@1.0.0
├─ is-path-in-cwd@1.0.1
├─ is-path-inside@1.0.1
├─ is-utf8@0.2.1
├─ is-wsl@1.1.0
├─ json3@3.3.2
├─ killable@1.0.0
├─ load-json-file@1.1.0
├─ loglevel@1.6.1
├─ map-obj@1.0.1
├─ meow@3.7.0
├─ merge-descriptors@1.0.1
├─ methods@1.1.2
├─ multicast-dns-service-types@1.1.0
├─ multicast-dns@6.2.3
├─ node-forge@0.7.5
├─ normalize-package-data@2.4.0
├─ obuf@1.1.2
├─ on-headers@1.0.1
├─ opn@5.3.0
├─ original@1.0.2
├─ p-map@1.2.0
├─ parse-json@2.2.0
├─ path-is-inside@1.0.2
├─ path-to-regexp@0.1.7
├─ path-type@1.1.0
├─ portfinder@1.0.17
├─ proxy-addr@2.0.4
├─ querystringify@2.0.0
├─ read-pkg-up@1.0.1
├─ read-pkg@1.1.0
├─ redent@1.0.0
├─ repeating@2.0.1
├─ select-hose@2.0.0
├─ selfsigned@1.10.3
├─ serve-index@1.9.1
├─ serve-static@1.13.2
├─ sockjs-client@1.1.5
├─ sockjs@0.3.19
├─ spdx-correct@3.0.0
├─ spdx-exceptions@2.1.0
├─ spdy-transport@2.1.0
├─ spdy@3.4.7
├─ strip-bom@2.0.0
├─ strip-indent@1.0.1
├─ thunky@1.0.2
├─ trim-newlines@1.0.0
├─ url-parse@1.4.3
├─ validate-npm-package-license@3.0.4
├─ wbuf@1.7.3
├─ webpack-dev-middleware@3.1.3
├─ webpack-dev-server@3.1.5
├─ websocket-extensions@0.1.3
└─ yargs@11.0.0
✨  Done in 66.69s.
```

Once this is done, run it with the`--oepn` flag, and your application will pop up in your favorite browser: 

```shell
> $(yarn bin)/webpack-dev-server --open
```

This will compile your app and load it, so it will take the same 4+ seconds as before.  

Next, open up `css/styles.css` in your editor, and arrange your windows so that you can see both your editor *and* your browser. Make a change to the CSS, and viola, your browser refreshes with the change. Repeat with `html/index.html` and `js/index.js`. Not too bad.

The refresh isn’t as fast as we’d like, but it’s still not too bad. You could easily open up your code editor on one side of the screen, and your browser on the other, and get to work.  

Part of the reason is that we split our code into development and production. To re-run Webpack is development, we aren’t minifying, hashing, or generating a slow source map. That helps.  
