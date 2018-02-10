---
layout: post
title:      "JavaScript Variable Hoisting"
date:       2018-02-10 06:15:36 +0000
permalink:  javascript_variable_hoisting
---


Hoisting is a behavior in JavaScript that moves variable declaration to the top of their scope before that code is executed.  However, any variable assignment to that same variable is not hoisted.  For example,

```
console.log(value);
```

The console log will raise a **reference error** because `value` is not declared.  Now if we declare and assign the variable `value` below it here:

```
console.log(value);
const value = 1;
```

the console log returns `undefined` instead of a reference error.  Although `value` is declared and assigned a value within the same scope, only the declaration is hoisted to the top.  Declared values return `undefined`.  The assignment of `1` to `value` is not hoisted and will not be displayed in the console log.

