---
layout: post
title:      "JavaScript ES6:  ```let``` and ```const``` are the new ```var```"
date:       2017-12-21 20:06:02 +0000
permalink:  javascript_es6_let_and_const_are_the_new_var
---

ES6 introduce two new variable declarations: ```let``` and ```const```.

*  ```let``` is used when it is expected for a variable to change over time.
*  ```const``` is used when it is expected for a variable to NOT change over time (i.e. stays constant).

An immediate benefit of having these additional variable declarations is that it makes code easier to read.  When code grows to many lines and contains many variables, it can become difficult to keep track which variables will change over time.  With the ```const``` declaration, developers can easily reference which variables will stay constant, where to look up the source of that value, and to better understand the intent of the coder.  Moreover, it prevents accidental overwriting of ```const``` variables as any attempt to mutate them will throw an error.

```let```  is also found in other languages such as Basic for variable declaration, and adding ```let``` provides a touch of familiarity for programmers coming from those other languages.

Before ES6, ```var``` was the only way to declare a variable.  When a ```var``` variable is declared inside a closure of a function, it is hoisted and enabling its scope to include the entire enclosing function.   However, ```let``` variables are limited to the closure and are not hoisted into the enclosing outer function, as shown here:

![](https://i.imgur.com/BfbgtbZ.png)

Source: MDN web docs - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Description

```let``` variables have "as their scope the block in which they are defined, as well as in any contained sub-blocks", according to the [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Description ).  This keeps the code of inner functions cleaner and more separate from the outer function in which those ```let``` variables are used.

 ```let```'s limited scope also prevents the creation of a global object property, keeping those variables truly local.
 
 ![](https://i.imgur.com/y2j8gVn.png)
 
 Source: MDN web docs - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Description
