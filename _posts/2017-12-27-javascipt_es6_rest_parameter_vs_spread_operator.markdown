---
layout: post
title:      "JavaScipt ES6: Rest Parameter vs. Spread Operator"
date:       2017-12-28 00:44:49 +0000
permalink:  javascipt_es6_rest_parameter_vs_spread_operator
---


Spread operators and rest parameters use the same "..." notation to precede some variable in a function.  However, they act differently when used in different parts of a JavaScript function.

**Spread Operator**

When used in the code block of a function, the spread operator:

* flattens out the elements of an array (e.g. where a = [1, 2], ...a becomes 1, 2) and turns the elements into a list
* it is a great alternative to concat() method (e.g. where a and b are arrays, a.concat(b)) as shown below
* it allows developers to have write less code, have better control over the elements of a new array, and it is visually easier to see

```
const a = [10, 11];
const b = [12, 13];

function spreadOperator(a, b){
  return [...a, ...b];
}

spreadOperator(a, b);  //returns => [10,11,12,13]
```

**Rest Parameter**

When used in the parameters list of a function, it takes a list of values of unknown length and turns them to an array when that parameter name is referenced inside the code block. For example, a series of arguments are passed into the function below.

```
function restParameter(...numbers) {
     return numbers;
};

restParameter(1,2,3,4); //returns => [1,2,3,4]
```

By putting the "..." notation in front of the parameter ```numbers```, ```numbers``` becomes an array in the code block when called.  One of the best use cases for the rest parameter is when there are an unknown number of arguments being passed into a function and we need to be able to access each of those arguments later on in the function's code block.
