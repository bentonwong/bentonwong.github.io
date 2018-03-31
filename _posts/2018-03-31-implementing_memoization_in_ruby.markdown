---
layout: post
title:      "Implementing Memoization in Ruby"
date:       2018-03-31 05:23:10 +0000
permalink:  implementing_memoization_in_ruby
---


Memoization, a process of caching previously computed values, is very useful for avoiding duplication of work and can reduce the runtime of functions.  

In Ruby, memoization is commonly used with the conditional assignment operator (||=) and can be easily implemented in many common algorithms. This work can include duplicated database calls and repetitive calculations with the same input.

**Reducing database calls**

Multiple database calls take time and can slow down system performance.  If calls to the same information in the same database are not expected to change, it would be faster to make one call and save that result in memory.

For example, an authentication system will often need to check who the current user is.  Rather than calling the database each time the current user is queried, the current user can be set at the beginning of the session with one database call, and that value can be accessed in memory throughout the session.

```
def current_user
    current_user ||= User.find_by(id: session[:user_id])
end
```

With the ||= operator, if current_user is nil, then User.find_by will query the database for a user that matches the session id and (hopefully) return the matching user instance and set the current_user to that instance.  Thereafter, current_user will store that value and will always return that value until the value in current_user is cleared out.

Without the ||= operator, other methods that rely on current_user will slow down because they have to wait for the database call to complete before continuing.  When current_user is called many times throughout a session, these delays add up and result in a poor user experience.

**Reducing repetitive calculations**

Memoization can be used when the same values are frequently queried.  This often occurs in looping or recursive methods.  For example, using recursion to find larger numbers in the Fibonacci sequence will be slow since it will have to calculate the same numbers repeatedly to arrive at the base case:

```
def fib(n)
     if n < 2
         return n
     end

     fib(n-2) + fib(n-1)
end
```

Memoization can be easily applied here:

```
def fib(n, memo={})
     if n < 2
         return n     
     end

     memo[n] ||= fib(n-1, memo) + fib(n-2, memo)
end
```

By using the ||= operator to immediately return the previously queried nth number in the Fibonacci sequence from a hash that has been accumulating these values, the runtime decreases dramatically.  This is because a hash has a constant runtime, in which the lookup time remains the same as the number of hash values increases.  By adding some simple memoization to this recursive method, memoization vastly improves its performance from very slow recursive runtime of n^2.


