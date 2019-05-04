# Week 18

## Algorithm

### [36. Valid Sudoku](https://leetcode.com/problems/valid-sudoku/)

#### Description

Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validate **according to the following rules**:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the 9 `3x3` sub-boxes of the grid must contain the digits `1-9` without repetition.

![Sudoku 9x9](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

A partially filled sudoku which is valid.

The sudoku board could be partially filled. where empty cells are filled with the character `'.'`.

#### Example 1

```example
Input:
[
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: true
```

#### Example 2

```example
Input:
[
  ["8","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

#### Note

- A Sudoku board board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.
- The given board contain only digits `1-9` and the character `'.'`.
- The given board size is always `9x9`.

#### Solution

```javascript
/**
 * using Set
 * store digit from the row in format `${digit} in row ${row}`
 * store digit from the column in format `${digit} in row ${column}`
 * store digit from the block in formate `${digit} in block ${Math.floor(row / 3)}-${Math.floor(column / 3)}`
 *
 * check if the element was in set then return false, otherwise this is a valid sudoku return true.
 * @param {Array} board
 * @returns {Boolean}
 */
const isValidSudoku = board => {
  const seen = new Set();
  for (let i = 0; i < 9; ++i) {
    for (let j = 0; j < 9; ++j) {
      const digit = board[i][j];
      if (isNaN(digit)) continue;
      const inRow = `${digit} in row ${i}`;
      const inColumn = `${digit} in column ${j}`;
      const inBlock = `${digit} in block ${Math.floor(i / 3)}-${Math.floor(j / 3)}`;
      const hasRow = seen.has(inRow);
      const hasColumn = seen.has(inColumn);
      const hasBlock = seen.has(inBlock);
      if (hasRow || hasColumn || hasBlock) return false;
      seen.add(inRow);
      seen.add(inColumn);
      seen.add(inBlock);
    }
  }
  return true;
};

const validBoard = [
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
];

const isValid = isValidSudoku(validBoard);
console.log(isValid); // true
```


## Review

[The Value of Multi-Typeface Design – About Face – Medium](https://medium.com/s/about-face/the-value-of-multi-typeface-design-ccd67227b0ee)

Conclusion

- It’s less about the fonts themselves and more about how you seem them
- Focus on the differences of typefaces that are similar at first glance
- Start with relationships within a paring, then add from there
- Contrast in type parings is overacted; real contrast comes from content and hierarchy
- If you don’t have layered structures within your content, build them yourself
- Use different faces to distinguish distinctive elements in your content
- Use distinctive faces sparingly, with clear intention

## Technique

```javascript
/**
 * Replaces all but the last `num` of characters with the specified mask character.
 * Use `String.prototype.slice()` to grab the portion of the characters that will remain unmasked and use `String.padStart()` to fill the beginning of the string
 * with the mask character up to the orginal length.
 * Omit the second argument, `num`, to keep a default of `4` characters unmasked.
 * If `num` is negative, the unmasked characters will be at the start of the string.
 * Omit the third argument, `mask`, to use a default character of `*` for the mask.
 * @param {String} cc
 * @param {Number} num
 * @param {String} mask
 * @returns {String}
 */
const mask = (cc, num = 4, mask = '*') => `${cc}`.slice(num).padStart(`${cc}`.length, mask);

```

## Share

Pay the these services that can level up you knowledge and skills.
It’s a win-win.