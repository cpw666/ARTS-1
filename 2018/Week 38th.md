# Week 38th
## Algorithm
### [476. Number Complement](https://leetcode.com/problems/number-complement/description/)

#### Description
Given a positive integer, output its complement number. The complement strategy is to flip the bits of the binary representation.  

#### Note
1. The given integer is guaranteed to fit within the range of a 32-bit signed integer.
2. You could assume no leading zero bit in the integer's binary representation. 

#### Example 1:
```
Input: 5
Output: 2
Explanation: The binary representation of 5 is 101 (no leading zero bits), and its complement is 010. So you need to output 2. 
```

#### Example 2:
```
Input: 1
Output: 0
Explanation: The binary representation of 1 is 1 (no leading zero bits), and its complement is 0. So you need to output 0.
```

#### Solution
```javascript
/**
 * Given a positive integer, output its complement number.
 * The complement strategy is to flip the bits of its binary representation
 * @param {number} num
 * @returns {number}
 */
const findComplement = (num) => {
	const binary = num.toString(2);
	const complementBinary = binary.split('').map(digit => digit ^ 1).join('');
	const complement = parseInt(complementBinary, 2);
	return complement;
};
```

1. get the binary representation of the `num`
2. get the complement in binary representation
	- map each digit of the binary
	- return digit xor 1 as the complement of each digit
	- return whole complement represent in string
3. output `num` complement number.

## Review
[How JavaScript works: Under the hood of custom elements + Best practices on building reusable…](https://blog.sessionstack.com/how-javascript-works-under-the-hood-of-custom-elements-best-practices-on-building-reusable-e118e888de0c)

[Tutorial – SessionStack Blog](https://blog.sessionstack.com/tagged/tutorial) this link to a series article on **How JavaScript Works**.  

This post is about reusable elements, in big picture — web components. It’s a relatively new W3C standard that has already been approved by all major browsers, and of cause it can be used in production environments, with some polypill library.  

By providing us with Custom Elements API, browsers natively support to creating small, modular, and reusable elements. Which Angular’s directives and React’s components try to solve.  

I should think the web more modularly.  

## Technique
To-do app on slack, arrange for my wife, my child, my whole family.
RSS app on slack, I have lots of interests, this help me to gathering them around.

## Share
To be honest, I don’t know how to share my opinion, and more precisely I don’t what to share.  

I know that share my opinion is the highest level of learning new stuff. Does that means I don’t know what I’ve learned or I don’t know what exactly that is I’ve learned. I don’t take note, I don’t review. I think this is my main problem of not efficient enough. 

I need to pay more attention of these two basic problems, take note, do review.
