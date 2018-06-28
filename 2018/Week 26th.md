# Week 26th
## Algorithm
[804.  Unique Morse Code Words](https://github.com/charleserious/leetcode/blob/master/JavaScript/Algorithms/UniqueMorseCodeWords/index.js)

```JavaScript
let uniqueMorseRepresentations = function (words) {
  let morse = ['.-', '-...', '-.-.', '-..', '.', '..-.', '--.', '....', '..', '.---', '-.-', '.-..', '--', '-.', '---', '.--.', '--.-', '.-.', '...', '-', '..-', '...-', '.--', '-..-', '-.--', '--..'];
  let seen = new Set();
  let begin = 'a'.charCodeAt(); // charcode of a
  for (let word of words) {
    let code = '';
    for (let char of word) {
      code += morse[char.charCodeAt() - begin];
    }
    seen.add(code);
  }
  return seen.size;
};
```

First come out of my mind was loop the `words` and each character of `word`, concatenation each char in morse, get a morse representation of the `word`, and put that morse representation into a Map as a key, thanks to Map you have unique key feature, WAIT! Set has the same feature too and save the **value** storage space. so above is my solutions.

Should be a more elegant way.

## Review
[Garbage collection in V8, an illustrated guide – Irina Shestak – Medium](https://medium.com/@_lrlna/garbage-collection-in-v8-an-illustrated-guide-d24a952ee3b8)
Honestly speaking, I don’t fully understand what she’s talking. This article brings me to think about the variables declaration through `var` keyword, with three facts.
1. They are function scoped;
```javascript
function printAlpha () {
	var alpha = 2;
	console.log(alpha); // inside of `printApha()`, `alpha` exists with value 2
}

console.log(alpha); // ReferenceError! outside of `printAlpha()`, `alpha` is not defined.
```

2. Their declarations get hoisted;
```javascript
function printBeta () {
	beta = 2; // using `beta` to hold number 2
	console.log(beta); // print `beta` in console

	var beta;	// instatiating b
} 

// above snippet compiled like below
function printBeta () {
	var beta;
	beta = 2;
	console.log(beta);
}
```

Compiler will look for a `var` for `charlie` from parent scope up to global scope. 
```javascript
function printCharlie () {
	charlie = 2;
	console.log(charlie); // we got 2 in console
}
```

3. They can be declared without a value;
```javascript
var alpha, bravo, charlie;

alpha = 1;
bravo = 2;
charlie = a + b;
```

Above three drawbacks of `var` bring the hell of messy to Garbage Collector in any browsers. We Frontenders shouldn’t pay any attention for GC during our coding period.(joking.)

**Times have changed**
Sant ECMAScript 6 bring two new keywords `let` and `const`
- `let` is block scoped;
- `let` cannot be accessed before its declaration;
- `let` share a common with `var` instantiate with empty;
- `let` can be reassigned;
- `const` is block scoped;
- `const` won’t allow for empty instantiation;
- `const` cannot be accessed prod to instantiation;
- `const` cannot be reassigned, won’t allow for multiple value types;
```javascript
const alpha = 'Werewolf';
alpha = 2; // TypeError: Assignment to constant variable.
```

I like the `const` strictest way, make me feel tougher.

According to Eric Elliot from his [JavaScript ES6+: var, let, or const? – JavaScript Scene – Medium](https://medium.com/javascript-scene/javascript-es6-var-let-or-const-ba58b8dcde75):
> `let`, is a signal that the variable may be reassigned, such as a counter in a loop, or a value swap in an algorithm. It also signals that the variable will be used only in the block it’s defined in, which is not always the entire containing function.  

SO `const` is the toughest and safest bet, `let` for look and mathematical algorithms. I’ll bring you guys more specifics of these two keywords in future.

Give back the shit to GC. We are free now.

## Technique
Technically, this is not a technique, this is just one little advice.

CSS with Flexbox Layout module aims to provide a more efficient way to layout, align and distribute space among items in a container, even when their size is unknown and/or dynamic.

But the problem is that, flexbox is a one dimension layout system. So when your want to create something like grid, your may need use Grid layout system. Grid Layout is a two dimensional system, meaning it can handle both columns and rows.

Checkout this two links for comparison:
[CodePen - Flexbox Layout demo](https://codepen.io/charleserious/full/ZRqXOW)
[CodePen - Grid Layout demo](https://codepen.io/charleserious/full/ZRqXje)

I wrote this two demo down is just because I once try to build a Flexbox Grid System without any margin, just let browsers do the calculation. with the courage I birth with. lol…..

Just don’t repeat my wrong.

## Share
I wanna share you guys with [RequireJS](http://requirejs.org).
With a long time we use `<script>` tag to maintain our scripts and their dependencies order. Mini sites or something like this will be ok till eternity. 

But we are now in the age of SPA, we’ll get into the age of PWA, we got tons of JavaScript files with our application,`<script>` is holding your neck. 
- Websites are turning into Web apps; 
- Code complexity grows as the sites get bigger; 
- Assembly gets harder; 
- Developer wants discrete JS files/modules;
- Development wants optimized code in just one or few HTTP calls;

Frontend developers need a solution with:
- Some sort of `#include/import/require`;
- Ability to load nested dependencies;
- Ease of use for developer but then backed by an optimization tool to that helps deployment;

Yes! We have RequireJS now. with this we can do:
- Load JavaScript Files;
```html
<!--This sets the baseUrl to the "scripts" directory, and loads a script that will have a module ID of 'main'-->
<script data-main="scripts/main.js" src="scripts/require.js"></script>
```
We just need this single `<script>` line everything we need should be contained into module main.
As the law of RequireJS, he will handle the rest of your need.
- Define modules;
```javascript
// define literial object
define({
	color: 'black',
	size: 'unsized'
});

// define a function
define(function () {
	return {
		color: 'black',
		size: 'unsized'
	}
});

// define functions with dependencies
define(['bowl', 'chopsticks'], function (bowl, chopsticks) {
	return {
		staple: 'rice',
		and: 'nothing else'
	}
});

// define module as a function
define(['bowl', 'chopsticks'], function (bowl, chopsticks) {
	return function (todaySpecial) {
		staple: 'rice',
		and: todaySpecial
	}
});
```

- Config your module dependencies and their order through `require.config()`;

Above three are his basic usage, he is so powerful for our daily work.

Webpack comes later.
