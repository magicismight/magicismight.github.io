---
title: useful-tricks-for-javascript
date: 2019-04-29 16:50:01
tags: javascript
---
[original article](https://davidwalsh.name/javascript-tricks)

# Get Unique Values of an Array
Getting an array of unique values is probably easier than you think:

```
var j = [...new Set([1, 2, 3, 3])]
>> [1, 2, 3]
```

# Array and Boolean
Ever need to filter falsy values (0, undefined, null, false, etc.) out of an array? You may not have known this trick:

```
myArray
    .map(item => {
        // ...
    })
    // Get rid of bad values
    .filter(Boolean);
Just pass Boolean and all those falsy value go away!
```

# Create Empty Objects

Sure you can create an object that seems empty with {}, but that object still has a __proto__ and the usual hasOwnProperty and other object methods. There is a way, however, to create a pure "dictionary" object:

```
let dict = Object.create(null);

// dict.__proto__ === "undefined"
// No object properties exist until you add them
```

There are absolutely no keys or methods on that object that you don't put there!

# Get Query String Parameters
For years we wrote gross regular expressions to get query string values but those days are gone -- enter the amazing URLSearchParams API:

```
// Assuming "?post=1234&action=edit"

var urlParams = new URLSearchParams(window.location.search);

console.log(urlParams.has('post')); // true
console.log(urlParams.get('action')); // "edit"
console.log(urlParams.getAll('action')); // ["edit"]
console.log(urlParams.toString()); // "?post=1234&action=edit"
console.log(urlParams.append('active', '1')); // "?post=1234&action=edit&active=1"
```

Much easier than we used to fight with!
