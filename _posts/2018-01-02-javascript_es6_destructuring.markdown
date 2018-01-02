---
layout: post
title:      "JavaScript ES6 Destructuring"
date:       2018-01-02 22:21:19 +0000
permalink:  javascript_es6_destructuring
---

Destructuring is a useful ES6 feature for reducing the amount of code when working with objects and arrays.

**Destructuring Objects**

  When working with an object, we may find ourselves in a situation where we want to access a key value just by the key itself. This can be accomplished using the traditional way through explicit variable assignments.

```
const coordinate = {
     x: 10,
     y: 20,
     z: 30
}

const x = coordinate.x;
const y = coordinate.y;
const z = coordinate.z;

x; // => 10
y; // => 20
z; // => 30
```

With ES6 destructuring, we can reduce the assignments of constants x and y from 3 lines to one line here:

```
const coordinate = {
  x: 10,
  y: 20,
  z: 30
}

const { x, y, z } = coordinate;

x; // => 10
y; // => 20
z; // => 30
```

This works because the newly assigned variable name exactly matches the object's key. The curly braces sounding x, y, z does not create a new object.  Because the curly braces are on the left side of the equal sign, it means that a new variable is being declared and it is to reference a property on the object of the same name. This refactor via ES6 destructuring removes duplicate variable declarations.

**Destructuring Arrays**

Destructing can also be applied to arrays as shown below:
```
const fruitsList = ['apple', 'banana', 'orange'];
const [ first, second, third ] = fruitsList;

first; // => apple
second; // => banana
third; // => orange
```

Unlike destructuring objects, variables are assigned based on order in which they appear in the array and uses square brackets instead of curly brackets.

**Destructuring Arrays and Objects Simultaneously**

Taking an array of objects, destructuring can be applied where arrays and objects are involved:
```
const produce = [
     { name: "apple", type: "fruit" },
     { name: "lettuce", type: "vegetable" },
     { name: "banana", type: "fruit" },
     { name: "broccoli", type: "vegetable" }
]

const [ first, { name }] = produce

first; // => { name: "apple", type: "fruit" }
name; // => lettuce
```

**A Practical Use Case for Destructuring**

Destructuring can be useful for easily passing in arguments into functions.  Instead of listing out all the arguments in a call to a function, we can pass an object instead with its keys as parameter names to be used in the function.

```
function printUser ({ name, location, email }) {
  return `The new user is ${name}, from ${location} whose email is: ${email}.`;
}

const newUser = { name: 'Jane', email: 'jane@email.com', location: 'USA'}
printUser(newUser); //=> The new user is Jane, from USA whose email is: jane@email.com.
```

Then, in the function printUser, we can apply destructuring directly to the parameters list and list out the keys we want as parameters available to the function. 

Clear advantages of destructuring here are that: (1) the function does not have to separately assign the object properties to new variables in the code block, and (2) the order in which the destructured parameters are listed does not matter as long as the incoming argument is an object and the parameter names match its keys.

In general, destructuring makes code easier to read by reducing references to object and array names and by directly referencing their keys and elements. 

