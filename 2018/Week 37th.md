# Week 37th
## Algorithm
### [557. Reverse Words in a String III](https://leetcode.com/problems/reverse-words-in-a-string-iii/description/)

#### Description
Given a string, you need to reverse to order of characters in each word within a sentence while still preserving whitespace and initial word order.  

#### Example
```
Input: "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"
```

#### Note
In the string, each word is separated by single space and there will not be any extra space in the string.  

#### Solution
```javascript
const reverseWords = (s) => {
	let result = s.split(' ');
	result = result.map(word => {
		let letters = word.split('');
		letters = letters.reverse();
		return letters.join('');
	});
	return result.join(' ');
};
```
1. split the string by single whitespace into an array;
2. map single words' array
3. split each word by empty string into letters array;
4. reverse the order of each word;
5. return each word in reverse order;
6. finally return the reversed string;

## Review
[How JavaScript works: Under the hood of CSS and JS animations + how to optimize their performance](https://blog.sessionstack.com/how-javascript-works-under-the-hood-of-css-and-js-animations-how-to-optimize-their-performance-db0e79586216)  

[Tutorial – SessionStack Blog](https://blog.sessionstack.com/tagged/tutorial) this link to a series article on **How JavaScript Works**.  

I know CSS animation stuff is great, but I don’t know animating some properties will causing layout and rendering, so that limits us to use `opacity` and `transform`. Careful with geometry change.  

And of cause CSS-based animations are handled on the thread known as the “compositor thread”. It’s different from the browser’s “main thread”, where styling, layout, painting, and JavaScript are executed.  

Here is the point with main thread handle layout and compositor thread handle css animation, means when we do geometry animations “compositor thread” will alert “man thread” to do layout tasks. It’s clear to avoid geometry animations through css-based animation. Let JavaScript handle these tasks.  

JavaScript animations in the mean time is more complex compared to using css-based animations, but that will work as the same. And of cause this also should to avoid animating expensive properties.  

## Technique
This week is about Graph.  

Here is some sort of code: 
```javascript
class Graph {
	constructor (v) {
		this.vertices = v;
		this.edges = 0;
		this.adj = [];
		this.marked = [];
		this.edgeTo = [];
		for (let i = 0; i < this.vertices; i++) {
			this.adj[i] = [];
			this.adj[i].push('');
			this.marked[i] = false;
		}
	}

	addEdge (v, w) {
		this.adj[v].push(w);
		this.adj[w].push(v);
		this.edges++;
	}

	showGraph () {
		for (let i = 0; i < this.vertices; i++) {
			const edges = this.adj[i];
			const vertices = edges.filter(v => v);
			const format = vertices.reduce((accumulator, vertex, index) => { return accumulator + (index > 0 ? ` ${vertex}` : `${vertex}`);}, '');
			console.log(i, '->', format);
		}
	}

	depthFristSearch (v) {
		this.marked[v] = true;
		if (this.adj[v] !== undefined) {
			console.log('Visited vertex:', v);
		}
		if (this.adj[v]) {
			this.adj[v].forEach(w => {
				if (!this.marked[w]) {
					this.depthFristSearch(w);
				}
			});
		}
	}

	breadthFirstSearch (s) {
		const queue = [];
		this.marked[s] = true;
		queue.push(s);
		while (queue.length > 0) {
			const v = queue.shift();
			if (v === undefined) {
				console.log('Visited vertex: ', v);
			}
			if (this.adj[v]) {
				this.adj[v].forEach(w => {
					if (!this.marked[w]) {
						this.edgeTo[w] = v;
						this.marked[w] = true;
						queue.push(w);
					}
				});
			}
		}
	}
}

module.exports = Graph;
```

## Share
### A few tips on study while full time job and raising family
1. Make a goal
First make your goal on what you’re trying to achieve, and consider  all angles of your goal. What outcomes are you aiming for? What is your course contain? how many modules or units?
2. Schedule with curriculum
Splice a big step into many more small pieces. Work our when your best study times are.
3. Make allowance for emergencies
As parents we know that children are frequently down with flu, some sort of infections, or have fight with others. Unpredictable are kids nature. But keeping track of your schedule is very important.  
5. Maximize your time
PUT YOUR PHONE ON SILENT, STUDY!!!
6. Simplify your life
Is that video game worth for the time your spend on? Is that party have to attendee?
8. Spend time with your children
Children are the big reason for the sacrifices that you’re making, So don’t let them be the excuse for not pushing yourself to fulfill your dreams. Instead, be inspired by them and hope that one day, they will be inspired by you.
9. Be confident
You can make that! Think of all the things you have already achieved.