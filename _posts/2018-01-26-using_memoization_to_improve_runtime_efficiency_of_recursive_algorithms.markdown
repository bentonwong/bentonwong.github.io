---
layout: post
title:      "Using Memoization to Improve Runtime Efficiency of Recursive Algorithms"
date:       2018-01-26 18:37:14 +0000
permalink:  using_memoization_to_improve_runtime_efficiency_of_recursive_algorithms
---


Memoization is a technique for speeding up algorithms by the storing, or caching, arguments and results of previous function calls.  When a previous function call is repeated, the cached result is returned instead of running that same function call again to rediscover that same result.

Recursive algorithms are great candidates for implementing memoization as recursion will often repeat function calls on the same arguments.

**A Classic Recursive Algorithm: Fibonnaci**

Finding the nth entry in the Fibonnaci is a classic use case of recursion:

```
function fib (n) {
     if (n < 2) {
         return n
		 }
     return fib(n - 1) + fib(n - 2);
}
```

The above function, fib(), will appears to run fast for smaller values of n as it has less recursive calls to make.  However, when attempting to find the Fibonnaci number on higher nth values, there will be a dramatic slow down due to the exponential increase in function calls.  This is inefficient as it repeats calls on lower values of n.  

**Applying Memoization to the Fibonnaci Algorithm**

Memoization can save time here by storing previously arguments and their results into an object.  Looking up a value in an object has a runtime of O(1) and will be much faster than recursion, which has a very slow exponential runtime of (2^n).

To apply memoization to fib(), we can create a memoization function that takes in fib() as an argument in addition to the value of n.

```
function memoize(fn) {
  const cache = {};
  return function(...args) {
  if (cache[args]) {
       return cache[args];
  }

  const result = fn.apply(this, args);
  cache[args] = result;

  return result;
  };
}

function fib(n) {
  if (n < 2) {
      return n;
  }

  return fib(n - 1) + fib(n - 2);
}

const fastFib = memoize(fib);
fastFib(n);
```

Memoize() stores arguments and their results in object form in its cache variable.  If a look up on the cache returns a valid, true value, that value is returned.  Otherwise, memoize() will execute fib().  Since fib() and memoize() will only run fib() for arguments that cache does not have values for, this runs much faster than fib() alone since both will utilize cached values as it makes its way down the recursion chain.
