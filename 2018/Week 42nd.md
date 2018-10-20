# Week 42nd
## Algorithm
### [884. Uncommon Words from Two Sentences](https://leetcode.com/problems/uncommon-words-from-two-sentences/description/)
#### Description
We are given two sentences `A` and `B`. (A *sentence* is a string of space separated words. Each *word* consists only of lowercase letters.)  

A word is *uncommon* if it appears exactly once in one of the sentences, and does not appear in the other sentence.  

Return a list of all uncommon words.  

You may return the list in any order.  

#### Example 1
```
Input: A = 'this apple is sweet', B = 'this apple is sour'
Output: [ 'sweet', 'sour' ]
```

#### Example 2
```
Input: A = 'apple apple', B = 'banana'
Output: [ 'banana' ]
```

#### Note
1. `0 <= A.length <= 200`
2. `0 <= B.length <= 200`
3. `A` and `B` both contain only spaces and lowercase letters.

#### Solution
```javascript
/**
 * @param {String} A
 * @param {String} B
 * @returns {Array}
 */
const uncommonFromSentences = (A, B) => {
  // concat two strings in the same pattern (space gapped)
  const merge = A.concat(' ', B);
  const sentences = merge.split(' ');
  // filter out the common word using the indexOf function
  const common = sentences.filter((word, index, list) => list.indexOf(word) !== index);
  // filter out the uncommons using the common words through the whole sentance.
  const uncommon = sentences.filter(word => !common.includes(word));
  return uncommon;
};

const A = 'this apple is sweet';
const B = 'this apple is sour';
const uncommons = uncommonFromSentences(A, B);
console.log(uncommons);
```

## Review
[So You Want to be a Functional Programmer (Part 1) – Charles Scalfani – Medium](https://medium.com/@cscalfani/so-you-want-to-be-a-functional-programmer-part-1-1f15e387e536)  

Functional Programming, may be the most popular concept in programming languages these years.  

This intro like the tons of others. Explained What is, Why is, How is, and of cause history staff.  

Here is what I’m thinking, do we really need to understand the difference between programming diagrams? Answer is YES!  

We should know what methodology every programming diagram based on, and what the main contradictories it’s trying to solve, so that we can write our service more efficiently and more maintainable.  

It’s a long way to know every thing.  

## Technique
I’m implementing a park pay pos app on an android pos device. So structure is that Android App as shell, call native function, such as payment and print invoice. Web app do the logic communicate with backend server through api calls.  

Due to the network unpredictable, we’ve test so many times, there always some issue can’t be fixed. and  can’t be certain. So we add a WebSocket to check the network connection issue. So that we can find out our bug very efficiently.  

## Share 
In daily development we often occur some “best practices” and many “conventional convention”, we should obey these fundamental rules to make our code more readable and maintainable.  

Program is firstly for human to understand and then for machine to process. Keep this in mind.
