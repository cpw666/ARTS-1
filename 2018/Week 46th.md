# Week 46th
## Algorithm
### [566. Reshape the Matrix](https://leetcode.com/problems/reshape-the-matrix/description/)

#### Description
In MATLAB, there is a very useful function called `reshape`, which can reshape a matrix into a new one with different size but keep its original data.  

You're given a matrix represented by a two-dimensional array, and two *positive* integers `r` and `c` representing the `row` number and `column` number of the wanted reshaped matrix, respectively.  

The reshaped matrix need to be filled with all the elements of the original matrix in the same `row-traversing` order as they were.  

If the `reshaped` operation with given parameters is possible and legal, output the new reshaped matrix; Otherwise, output the original matrix.  

#### Example 1
```
Input: 
nums = [
	[1, 2],
	[3, 4]
];
r = 1;
c = 4;
Output:
[
	[1, 2, 3, 4]
]
Explanation: The `row-traversing` of nums is [1, 2, 3, 4]. The new respaed matrix is a 1 * 4 matrix, fill it row by row by using the previous list.
```

#### Example 2
```
nums = [
	[1, 2],
	[3, 4]
]
r = 2;
c = 4;
Output: 
[
	[1, 2],
	[3, 4]
]
Explanation: There is no way to reshape a 2 * 2 matrix to a 2 * 4 matrix. So output the original matrix.
```

#### Note
1. The height and with of the given matrix is in range [1, 100].
2. The given r and c are all positive.

#### Solution
```javascript
/**
 * reshape the two-dimensional matrix
 * Use `Array.prototype.reduce()` and `Array.prototype.concat()` to flat the two-dimensional matrix into one-dimensional flated matrix.
 * Use `Array.prototype.from()` to generate a slot matrix with specified `row` and `column`.
 * Use `Array.prototype.map()` to fulfill the slot matrix using the flated matrix elements.
 * @param {Array} matrix
 * @param {Number} r
 * @param {Number} c
 * @returns {Array[r][c]}
 */
const matrixReshape = (matrix, r, c) => {
	if (!matrix || matrix.length === 0 || matrix.length > 100) {
		return matrix;
	}
	const width = matrix.length;
	const height = matrix[0].length;
	const isValid = width * height >= r * c;
	if (!isValid) {
		return matrix;
	}
	const flated = matrix.reduce((acc, val) => acc.concat(val));
	const column = Array.from({ length: c }, (v, i) => i + 1);
	const slots = Array.from({ length: r }, _ => column);
	let index = 0;
	const reshaped = slots.map(row => row.map(_ => flated[index++]));
	return reshaped;
};

const matrix = [ [1, 2], [3, 4] ];
const reshaped = matrixReshape(matrix, 4, 1);
console.log(`original: ${JSON.stringify(matrix)}`);
console.log(`reshpaed: ${JSON.stringify(reshaped)}`);

```

## Review
[Is Vue.js a good choice for a large-scale application?](https://medium.com/js-dojo/is-vue-js-a-good-choice-for-a-large-scale-application-908263e3a88)  
I don’t agree with the inheritance thing in the post,  
Always prefer composition over inheritance, React explained once well in [Composition vs Inheritance – React](https://reactjs.org/docs/composition-vs-inheritance.html), and in paradigm speaking we should always prefer composition over inheritance, I repeat.

## Technique
Returns `true` if the bottom of the page is visible, `false` otherwise.
Use `scrollY`, `scrollHeight` and `clientHeight` to determine if the bottom of the page is visible.  

With pure javascript:
```javascript
const bottomVisible = () => 
	document.documentElement.clientHeight + window.scrollY >= 
	(document.documentElement.scrollHeight || document.documentElement.clientHeight);
```

## Share
**Callback**  
In computer programming, a callback, also known as “call-after” function, is any executable code that is passed as an argument to other code that is expected to *call back* the argument at a given moment. This execution may be immediate as in a synchronous callback, or it might happened at a latter time as in an asynchronous callback. 
