---
layout: post
title:      "Javascript: ‘Undefined’ vs. ‘Null’"
date:       2018-03-03 01:05:31 -0500
permalink:  javascript_undefined_vs_null
---


`Undefined` and `null` may feel similar, as they both relate to absence.  They both produce falsey values. 

However, in JavaScript, these concepts are not exactly the same.  According to the [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined), it states: “null is not equivalent to undefined.”  Using a strict equality operator, we can prove that they are not exactly the same:

```
let x = null
let y = undefined
x === y // => false
```

Inspecting the typeof properties of `null` and `undefined`, we see that `null` returns an object, and `undefined` returns undefined.

```
Typeof null // => object
Typeof undefined //=> undefined
```

A variable with a property of `undefined` indicates that a variable has not been assigned a value.  `Undefined` is the primitive value that is used when trying to access non-existent variables such as uninitialized variables, not existing object properties, and non-existent array elements.  `Undefined` is not a value and it is not recommended to assign a variable a value of undefined.

On the other hand, `null` is an object which can be assigned to a variable.  It is the preferred way to indicate that a variable has no value. 

