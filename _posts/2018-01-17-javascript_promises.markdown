---
layout: post
title:      "JavaScript Promises"
date:       2018-01-17 21:10:58 +0000
permalink:  javascript_promises
---


Promises are expressions that execute after a function is made, most commonly an AJAX or `fetch` call. The asynchronous nature of JavaScript makes Promises a must.  Since JavaScript will still run while waiting for network requests to respond, Promises will wait for those network requests to complete before running its specified callback functions.

Promises can exist in 3 states:

1. 'UNRESOLVED' - waiting for a function to finish executing
2.  'RESOLVED' - function has finished executing and it was successful (usually indicated by a 200 status code)
3.  'REJECTED' - function has finished executing but it was unsuccessful

In order to consume a promise, we encapsulate the callback functions we want to run after the initial function has finished executing using .catch() and .then(). Both functions can be chained directly onto the result of that initial function and in succession with this shorthand (no need to include if statements to check on a request's success and determine which callback function is to be executed):
```
fetch(url)
  .then(response => console.log(response))
  .catch(error => console.log('Oh no! Something when wrong: ', error));
```
If the initial call fails, that is **rejected**, .catch() function will execute its callback function.  On the other hand, if there is not an error and the Promise status returns as **resolved**, .then() function will execute its respective callback function.
