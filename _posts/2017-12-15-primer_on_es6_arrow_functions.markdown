---
layout: post
title:      "Primer on ES6 Arrow Functions"
date:       2017-12-16 00:14:57 +0000
permalink:  primer_on_es6_arrow_functions
---


[ES6 arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) are a great way to compact function expressions.

Let's examine this example of a traditional function expression:

```
const multiplyTwoNumbers = function (num1, num2) {
  return num1 * num2;
};

multiplyTwoNumbers(1, 2); // 2
```

With an arrow function expression, the above can be transformed into:

```
const multiplyTwoNumbers = (num1, num2) => {
  return num1 * num2;
};

multiplyTwoNumbers(1, 2); // 2
```

Other than saving a couple key strokes by replacing the word 'function' with '=>', arrow functions reduce the code even further by eliminating the curly brackets and the "return" statement.  Arrow functions without curly brackets provide an implicit return, eliminating the need to write it.

```
const multiplyTwoNumbers = (num1, num2) => num1 * num2;

multiplyTwoNumbers(1, 2); // 2
```

Keep in mind that eliminating the curly bracket works when there is a single expression.

In some situations, this function can refactored even further.  If there is only 1 parameter, we can eliminate the enclosing parenthesis.

```
const doubleNumber = num1 => num1 * 2;

doubleNumber(1); // 2
```

Compact arrow expressions work well in situations where functions are a part of other functions or objects, such as callback functions, array helpers, closures to name a few.

Arrow expressions also reduce the need to use `.bind(this)` when some functions are written inside other functions or objects and need to rely on the context of their location.  For example,

```
const cars = {
  maker: 'Ford',
  models: ['F150', 'Fiesta', 'Fusion'],
  descriptions: function() {
  	return this.models.map(function(model) {
      return `${model} is made by ${this.maker}.`;
    }.bind(this));
  }
}         
cars.descriptions();

//  ["F150 is made by Ford.","Fiesta is made by Ford.","Fusion is made by Ford."]
```

With ES6 arrow expression, this can be reduced down to:

```
const cars = {
  maker: 'Ford',
  models: ['F150', 'Fiesta', 'Fusion'],
  descriptions: function() {
    return this.models.map((model) => {
      return `${model} is made by ${this.maker}.`;
    });
  }
}         
cars.descriptions();

//  ["F150 is made by Ford.","Fiesta is made by Ford.","Fusion is made by Ford."]
```

Also known as 'lexical this', it allows the arrow expression to use `this` from within the code that holds the arrow expression.
