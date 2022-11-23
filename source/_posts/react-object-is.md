---
title: Object.is polyfill
date: 2022-11-23 18:20:48
tags: JavaScript 
---

Found some interesting code in React source code: [Object.is polyfill](https://github.com/facebook/react/blob/main/packages/shared/objectIs.js).

There is something more rather than just using `===` to compare objects.

```javascript
function is(x: any, y: any) {
  return (
    (x === y && (x !== 0 || 1 / x === 1 / y)) || (x !== x && y !== y) // eslint-disable-line no-self-compare
  );
}
```

Found description for `Object.is` ion [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is)

> Object.is() is also not equivalent to the === operator. The only difference between Object.is() and === is in their treatment of signed zeros and NaN values. The === operator (and the == operator) treats the number values -0 and +0 as equal, but treats NaN as not equal to each other.


## +0 & -0 comparison
`x === y && (x !== 0 || 1 / x === 1 / y)` is for comparing `+0` and `-0`.

```javascript
const x = +0;
const y = -0;

console.log(x === y); // true

console.log(x !== 0 || 1 / x === 1 / y); // false
```
`1 / +0` will return Infinity, while `1 / -0` will return -Infinity.

## NaN comparison

`x !== x && y !== y` is for comparing `NaN === NaN`, this condition will return true is `x` and `y` are both NaN.

```javascript
const x = NaN;
const y = NaN;

console.log(x === y); // false

console.log(x !== x && y !== y); // true
```

Just use the wired behavior of NaN to compare itself.
isNaN(x) && isNaN(y) would work also, but `x !== x && y !== y` maybe the performance is better.


