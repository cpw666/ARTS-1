# Week 27th
## Algorithm
[832. Flipping An Image](https://github.com/charleserious/leetcode/tree/master/JavaScript/Algorithms/FlippingAnImage)
```javascript
const flipAndInvertImage = function(A) {
  const reverse = A.map(function (element) {
    return element.reverse();
  });
  const invert = reverse.map(function (element) {
    return element.map(function (single) {
      return Number(!single);
    });
  });
  return invert;
};
```

I thought this test my array manipulation, **Array.prototype.reverse** method and **Array.prototype.map** method.

But wait, I don’t need to do the map three times, Two maps and I should get the same result.
```javascript
const flipAndInvertImage = function (A) {
  const invert = A.map(function (element) {
    element = element.reverse();
    return element.map(function (single) {
      return Number(!single);
    });
  });
  return invert;
};
``` 

 **Array.prototype.reverse** method make me think about make my own version of array reverse.
```javascript
/**
 * half of interactive way
 * I don't like the recursive way
 * @param {nubmer[]} asc
 * @return {number[]}
 */
const reverse = function (asc) {
  const reverse = asc.slice();
  const count = asc.length;
  for (let i = 0; i * 2 < count; i++) {
    const start = reverse[i];
    const endIndex = count - i - 1;
    reverse[i] = reverse[endIndex];
    reverse[endIndex] = start;
  }
  return reverse;
};
```


## Review
[JavaScript — Map vs. ForEach – codeburst](https://codeburst.io/javascript-map-vs-foreach-f38111822c0f)
We need to think in big picture.
As functional paradigm of programming, we should consider one of the pillars of functional design is to create something new when something changes. 
Let’s take a look at an example. Say we need to produce an array that adds `1` to each value in that array.
```javascript
const nums = [5, 9, 7];
```

Procedural style:
```javascript
nums.forEach(function (num, index) {
	const increased = nums[index] = num + 1;
	return increased;
});
```

Functional style:
```javascript
const nums = nums.map(function (num) {
	const increased = num + 1;
	return increased;
});
```

forEach operates on our original array, on the other hand map create a new array in same size. You may be wondering why that matters. The idea is that a functional application is easier to debug because data structures are treated as immutable entities. In other words, we know what value of `nums` will be throughout our application. In the procedural style, the `nums` value is variable, which makes debugging more difficult. Any logic which considers `nums`, will also need to consider its current state, the functional version has no such issue.

Another benefit of the `.map()` method here, is that it allows more hackability for the future. For instance, let’s say you have decided to sort the array at some point, with `.map()`, you can merely chain on the `.sort()` method.
```javascript
const onums = inums.map(function (num) {
	const increased = num + 1;
	return increased;
}).sort();
```

## Technique
This week is still about Flexbox Layout module.

Cause there are so many kinds of mobile devices with so many versions of  CSS Specification implementations. This week I had a very strange problem, that start with flexbox and I finished it with flexbox. I firstly wrote a view as flex container, Above the Android 4.4 this view and it’s child elements works perfectly as I expected.

I initially thought iOS would be fine. But my QE has an iPad with iOS 9.3 and of cause it failed me. **Child elements overlapping together within a singe viewport  and can’t scroll**. I mean Seriously iOS with such high level version. still don’t work with flex perfectly? 

After many hours debugging, found out that iOS 10.3 start perfectly in Mar 27 2017 began to work perfectly with Flexbox  Layout Module. Ha!!!

I solved this problem with a little tricky property, give all the child elements a `flex-shrink: 0` css property. 

Yes!

Problem: flex child elements overlapping together.
Solution:  `flex-shrink: 0`.

Maybe this is not the solution work for you. But I have an ultimate solution for you. Once your CSS don’t work as your expected. Go check it on [Can I use… Support tables for HTML5, CSS3, etc](https://caniuse.com), it helps me a lot.

## Share
> At its core, **Webpack** is a static module bundler for modern JavaScript applications. When webpack process your application, it internally builds a  dependencies graph which maps every module your project needs and generates one or more bundles.  

Above is the official concept.

For beginners, lets say the file formats and structure that are most convenient for your website are not the most convenient for your to work with. Webpack applies automatic transformations on your working files to make them into production files that are more useful for your users. Those transformed files are copies and they go to different folders. so the original files are never modified on this process and stuff keeps tidy.

Webpack is mostly focused on the files the end user receives, that is, HTML, CSS, Javascript, but in theory, it can process anything you throw it if you “explain” to Webpack how to proceed.

Let me say it first. You may consider webpack, is it the right tool for me? Webpack solves a problem that only exists if your project has a certain size and use certain technologies: SASS, LESS, Stylus, Javascript ES2015, JSX, Typescript, Coffee Script… The bigger, longer and more advanced the project, the more valuable it is. For small project, it can be overkill.

- So what problems does webpack solve?
**First, it’s much better for maintenance to keep everything in its own file, but computers don’t like it that way.** Every HTML, CSS, Javascript file is a request to the server, and that’s extra work for it. Extra work means the user waiting more time. Organizing your code into different files makes sense for the developer, no one likes working with a single file contains several thousands lines.

But computers see it in a different way. For computer, one file of size 10 is much faster to get and process than 10 files of size 1. Webpack takes care of this issue and packs all your code in a way that makes sense.

**Second, your files are perfectly correct, but they are not efficient on the inside.** Consider that a machine doesn’t need comments, line breaks or spaces for a file to be understood. These stuff is for humans to be able to read the code, but for users’ computer, this is just fat. Another thing Webpack does is remove that fat. My wife would be love with this feature.

**Third, there are file formats that require transformation before becoming valid HTML, CSS, Javascript.**
*HTML -> HTML*
Webpack deals with the required includes and links in your HTML automatically.

[SASS](https://sass-lang.com), [LESS](http://lesscss.org), [Stylus](http://stylus-lang.com) *other languages on top of CSS -> CSS*
Browsers only understand CSS

*Javascript ES2015 -> Javascript*
Too new for most browsers. Webpack transforms for compatibility. One day, this transformation won’t be needed anymore.

*Typescript, Coffeescript -> Javascript*
Those languages are “better looking versions” of Javascript. Their code is supposed to be more readable and easy to understand, but in the end, they are meant to be translated into plain Javascript.

*SVG -> SVG*
SVN files generated by graphic suites usually contain information that is useful while you are editing the image, but not for the final version.

- How does it work?
Webpack is a command line tool that runs on the top of Node.JS.

And put your configuration file `webpack.config.js`  in the root of your project. If you want to learn about how to write this `webpack.config.js` file, a great starting point is the free course [React Fundamentals](https://tylermcginnis.com/courses/react-fundamentals/). The course is about React, but the Setup section explains how to configure your first Webpack project.

- What about debugging?
Question is “How am I going to debug something that get transformed before runtime?”, this very good question was has been solved by very smart people, [Use a source map - Firefox Developer Tools | MDN](https://developer.mozilla.org/en-US/docs/Tools/Debugger/How_to/Use_a_source_map)
