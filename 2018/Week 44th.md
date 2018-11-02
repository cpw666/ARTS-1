# Week 44th
## Algorithm
### [463. Island Perimeter](https://leetcode.com/problems/island-perimeter/description/)

#### Description
You are given a map in form of a two-dimensional integer grid where 1 represents land and - represents water.  

Grid cells are connected horizontally/vertically (not diagonally). The grid is completely surrounded by water, and there is exactly one island (i.e, one or more connected land cells).  
The island doesn't have "lakes" (water inside that isn't connected to the water around the island). One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.  

#### Example 
```
Input: 
[
	[0, 1, 0, 0],
	[1, 1, 1, 0],
	[0, 1, 0, 0],
	[0, 1, 0, 0]
]

Output: 16
Explanation: The perimeter is the 16 yello stripes in the image below:
```
![Island preview](http://pc97r6al4.bkt.clouddn.com/island.png)

#### Solution
```javascript
/**
 * Algorithm
 * 1: Search though our grid for 1's
 * 2: Determine for two direction (down, right) if it is a 1
 * 3: the answer is islands * 4 - neighbour * 2
 * @param {Array} grid
 */
const islandPerimeter = (grid) => {
	if (grid.length === 0) {
		return 0;
	}
	const height = grid.length;
	const width = grid[0].length;
	let islands = 0;
	let neighbours = 0;
	for (let i = 0; i < height; i++) {
		for (let j = 0; j < width; j++) {
			if (grid[i][j] === 1) {
				islands++;
				// count down neighbours
				if (i < height - 1 && grid[i + 1][j] === 1) {
					neighbours++;
				}
				// count rignt neighbours
				if (j < width - 1 && grid[i][j + 1] === 1) {
					neighbours++;
				}
			}
		}
	}
	return islands * 4 - neighbours * 2;
};

const grid = [
	[0, 1, 0, 0],
	[1, 1, 1, 0],
	[0, 1, 0, 0],
	[0, 1, 0, 0]
];

const perimeter = islandPerimeter(grid);
console.log(perimeter);
```

## Review
[Javascript - Generator-Yield/Next & Async-Await – codeburst](https://codeburst.io/javascript-generator-yield-next-async-await-e428b0cb52e4)  

Generator and Async/Await these two syntax are use to writing parallel code which run in asynchronously.

Generator is based on Iterator, we programmer familiar with c++ do know what iterator can offer us, we can control the execution of our code, with this *Control* we can do so manny things like infinity loop without block the thread, listen on IO event while remain with other tasks.  

Async/Await, they make promise very easy, in other word this two syntax make heavy CPU task easy to maintain while still can do handle user interaction.  

## Technique
Gets the day of the year from the `Date` object.  
```javascript
/**
 * Get the day of the year from a `Data` objec.
 * Using `new Date()` and `Date.prototype.getFullYear()` to get the first day of the year as a `Date` object,
 * subtract it from the provided `date` and divid with the milliseconds in each day to get the result.
 * User `Math.floor()` to appropriatly round the resulting day count to an integer.
 * @param {Date} date
 * @return {Number}
 */
const dateOfYear = date => Math.floor((date - new Date(date.getFullYear(), 0, 0)) / 1000 / 60 / 60 / 24);

module.exports = dateOfYear;
```

`test.js`
```javascript
const doy = dateOfYear(new Date());
console.log(`Today is the ${doy} Date of Year `);
```

## Share
Let’s talk about One-Way Data flow and Two-Way Data Binding.  

In AngularJS we see code like below:  
```javascript
// script.js
(function () {
	angualr
		.module('myApp', [])
		.controller('MyCtrl', function ($scope) {
			$scope.text = '';
			$scope.$watch('text', function (newVal, oldVal) {
				console.log(`Old value: ${oldVal}, New value: ${newVal}`);
			});
		});
} ());
```

```html
<!-- index.html -->
<body ng-app="myApp">
	<div ng-controller="MyCtrl">
		<input typ="text" ng-model="text">
		<p>{{text}}</p>
	</div>
</body>
```

Above code is Two-Way Data Binding, `text` model in the model changes show in the `<input>` and `<input>` changes automagically affect into `text` model.  

Take a look at the following React example:  
```javascript
// one-way data flow with react
class OneWay extends React.Component {
	constructor () {
		super();
		this.handleChange = this.handleChange.bind(this);
		this.state = {
			text: ''
		};
	}
	handleChange (e) {
		this.setState({
			text: e.target.value
		});
	}
	render () {
		return (
			<div>
				<input type="text" onChange="this.handleChange">
				<p>Text: {this.state.text}</p>
			</div>
		);
	}
};
```

Only the `handleChange` function can modify the `text` ’s state through `setState` function, this One-Way Data flow.

Let’s see Angular’s Two-Way Data Binding:
```javascript
// ngModel directive: two-way data binding syntax
<input [(ngModel)]="text">
<p>{{text}}</p>

// ngModel property and event binding
<input [ngModel]="text" (ngModelChange)="text=$event">
<p>{{text}}</p>
```

`[()]` this is [Angular’s two-way binding syntax](https://angular.io/docs/ts/latest/guide/template-syntax.html%23!%23two-way).  

So why Angular abandoned AngularJS’s Two-Way Data Binding?  

Because One-Way Data Flow make application state easier to manage, updates, and more predictable, and performance can be better as well.  
