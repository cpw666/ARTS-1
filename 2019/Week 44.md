# Week 44

## Algorithm

### [13. Roman to Integer](https://leetcode.com/problems/roman-to-integer/)

#### Description

Roman numberals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D`, and `M`.

| Symbol | Value |
| ——— | —— |
| I      | 1     |
| V      | 5     |
| X      | 10    |
| L      | 50    |
| C      | 100   |
| D      | 500   |
| M      | 1000  |

For example, two is written as `II` in Roman numberal, just two one’s added together. Twelve is written as, `XII`, which is simply `X` + `II`. The number twenty seven is written as `XXVII`, which is `XX` + `V` + `II`. 

Roman numberals are usually written largest to smallest from left to right. However, the numberal for four is not `IIII`. Instead, the number for is written as `IV`. Because one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9.
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90.
- `C` can be place before `D` (500) and `M` (1000) to make 400 and 900.

Given a roman numberal, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.

#### Example 1

```example
Input: “III”
Output: 3
```

#### Example 2

```example
Input: “IV”
Output: 4
```

#### Example 3

```example
Input: “IX”
Output: 9
```

#### Example 4

```example
Input: “LVIII”
Output: 58
Explanation: L = 50, V = 5, III = 3.
```

#### Example 5

```example
Input: “MCMXCIV”
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

#### Solution

```javascript
/**
 * @param {String} s 
 * @returns {Number}
 */
const romanToInt = s => {
  const map = {
    ‘I’: 1,
    ‘V’: 5,
    ‘X’: 10,
    ‘L’: 50,
    ‘C’: 100,
    ‘D’: 500,
    ‘M’: 1000
  };
  const integer = [ …s ].reduce((holder, char, index) => {
    const current = map[char];
    const next = map[s[index + 1]];
    return holder + (current < next ? -current : current);
  }, 0);
  return integer;
};
```

## Review

[What Replaces JavaScript - Young Coder - Medium](https://medium.com/young-coder/what-replaces-javascript-a6493b4e2d6e)

Out of the box, WebAssembly gives developers a way to write optimized code routines, usually in C++. This is powerful ability, but it has a relatively narrow scope. It’s useful if you need to improve the performance of complex calculation. (For example, [fastq.bio](fastq.bio) used WebAssembly to [speed up](https://www.smashingmagazine.com/2019/04/webassembly-speed-web-app/) their DNA sequencing calculation.) It’s also important if you’re porting high-performance games or writing an [emulator](https://win95.ajf.me/) that runs inside your browser. If this is all there were to WebAssembly, it wouldn’t be nearly as exciting and it wouldn’t have any hope of displacing JavaScript. But WebAssembly also opens a narrow pathway for framework developers to squeeze their platforms into the JavaScript environment.

Here’s where things take an interesting turn. WebAssembly can’t sidestep JavaScript, because it’s locked into the JavaScript runtime environment. In fact, WebAssembly need to run alongside at least some ordinary JavaScript code, because it doesn’t have direct access to the page. That means it can’t manipulate the DOM or receive events without going through a layer of JavaScript.

This should like a deal-breaking limitation. But clever developers have found ways to smuggle their runtimes in though WebAssembly. For example, Microsoft [Blazor](https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor) framework downloads a miniature .NET runtime as a compiled WASM file. This runtime deals with the JavaScript interop, and it provides basic services (like garbage collection) and higher-level features (layout, routing, and user interface widgets). In other words Blazor uses a virtual machine that lives inside another virtual machine, which is either an Inception-level paradox or a clever way to create a non-JavaScript application framework that runs in the browser.

Blazor isn’t the only WebAssembly-powered experiment that’s out of the gate, Consider [Pyodide](https://hacks.mozilla.org/2019/04/pyodide-bringing-the-scientific-python-stack-to-the-browser/), which aims to put Python in the browser, complete with an advanced math toolkit for data analysis.

This is the future, WebAssembly, which started out to satisfy C++, Rust, and not much more, is quickly being exploited to create more ambitious experiments. Soon it will allow non-JavaScript frameworks to compete with JavaScript-based standbys like Angular, React and Vue.

And WebAssembly is still evolving rapidly. It’s current implementation is a minimus viable product — just enough to be useful in some important scenarios, but not all all-purpose approach to developing on the web. As WebAssembly is adopted, it will improve. For example, if platform like Blazor catch on, WebAssembly is likely to add support for direct DOM access. Browser makers are already planning to add garbage collection and multithreading, so runtimes don’t need to implement these details themselves.

If this path of evolution seems long and doubtful, consider the lessons of JavaScript. First, we saw that if something is possible in JavaScript, it is done. Then we learned that if something is done often enough, browsers make it work better. And so on. If WebAssembly is popular, it will feed into a virtuous cycle of enhancement that could easily overtake the native advantages of JavaScript.

It’s often said that WebAssembly was not built for replace JavaScript, But that’s true of every revolutionary platform. JavaScript was not designed to replace browser-embedded Java. Web applications were not designed to replace desktop applications, But once they could, they did.

## Technique

### Sibling fade

#### [Check me out](https://codepen.io/charleserious/pen/ZEEvmKG)

Fade out the siblings of a hovered item.

```html
<!DOCTYPE html>
<html lang=“en”>
<head>
  <meta charset=“UTF-8">
  <meta name=“viewport" content=“width=device-width, initial-scale=1.0”>
  <meta http-equiv=“X-UA-Compatible” content=“ie=edge”>
  <link rel=“stylesheet” href=“./main.css”>
  <title>Sibling face</title>
</head>
<body>
  <div class=“sibling-fade”>
    <span>Item 1</span>
    <span>Item 2</span>
    <span>Item 3</span>
    <span>Item 4</span>
    <span>Item 5</span>
    <span>Item 6</span>
  </div>
</body>
</html>
```

```css
html, body {
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
}

body {
  display: flex;
  flex-flow: column nowrap;
  align-items: center;
  justify-content: center;
}

span {
  padding: 0 1rem;
  transition: opacity 0.2s;
}

.sibling-fade:hover span:not(:hover) {
  opacity: 0.5;
}
```

#### Explanation

1. `transition: opacity 0.2s` specifies that changes to opacity will be transitioned over 0.2 seconds.
2. `.sibiling-fade:hover span:not(:hover)` specifies that when the parent is hovered, select any `span` children that are not currently being hovered and change their opacity to `0.5`

## Share

Design a large deployed system from every single line of code to the whole picture, refactoring may help me a looooooot.