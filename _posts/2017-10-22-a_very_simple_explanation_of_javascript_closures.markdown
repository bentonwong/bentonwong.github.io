---
layout: post
title:      "A Very Simple Explanation of JavaScript Closures"
date:       2017-10-23 02:42:01 +0000
permalink:  a_very_simple_explanation_of_javascript_closures
---


A javascript closure is a function that can access variables defined outside of itself.  Here is a simple example:
```
var someOutsideVariable = 1;

function increaseOutsideVariable() {
     return someOutsideVariable + 1;
}
```
If we run "increaseOutsideVariable()", then the return value will be 2.  Amazingly, this value was returned without having to explicitly pass in someOutsideVariable as an argument into the function.  This closure feature of the increaseOutsideVariable function started looking in itself, but could not find it. So, it looked outside of itself and accessed someOutsideVariable.

In other programming languages that do not support closures, we would have to pass in the value as an argument into a function because that function would not have access to the outside variable.

Closures have a lot of utility in JavaScript.  A common use case is in callbacks for AJAX requests, which use closures to access variables outside of the AJAX request (a function).  Without closures, the easy to read AJAX request would become very unreadable quickly.

Another neat feature of closure is that a closure nested in a function will still run and have access to variables in its parent function even after the parent function has finished running.  
```
function sayFullName(firstName) {
  var intro = "Hello, ";
  function joinWords(lastName) {
    return intro + firstName + ' ' + lastName;
  }
  return joinWords;
}

var greeting = sayFullName("Bob");
greeting ("Barker");
```
Looking at the above code, function sayFullName() will finish executing before joinWords does.  Also, note that function joinWords was able to pull in the last name "Barker" from the variable greeting.

In other programming languages without closures, the inner function would not be accessible after the parent function has finished running since that inner function would only exist as long as the parent function is running.
