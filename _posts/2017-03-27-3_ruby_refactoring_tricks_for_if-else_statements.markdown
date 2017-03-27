---
layout: post
title:  "3 Ruby Refactoring Tricks for If-Else Statements"
date:   2017-03-27 01:46:08 -0400
---


An area where code can be easily refactored are if-else statements.  If-else statements lends itself to code bloat.  For example, if one needs a block to explicitly return true or false to determine if some variable is “nil”, we could write:


	variable = nil
	if variable
	 true
	else
	 false
	end

	# => false

Writing this method longhand results in minimum 5 lines of code. Let’s attempt to reduce it, and perhaps eliminate the use of “if” and “else” altogether.
	
**1. Use a ternary operator**

The ternary operator is an operator that can collapse the above if-else statement into 1 line:

`variable ? true : false	#=>false`

The format for this operator is: 

`*{conditional expression} ? {execute this statement if true} : {otherwise do this}*`

The expressions here can be something other than returning true or false.  It can be a snippet of executable code (e.g. calling a particular method or a certain view in Sinatra). 

**#2) Apply a “!!” (aka the “Double Bang”)**

In instances where one needs to explicitly convert any value into a boolean statement, the double bang is an easy way to do this.  Taking the example above, we can reduce:

 	`variable ? true : false`

to

	`!!variable`

How does this work? A single “!” negates the variable and forces it to return either true or false, based on it boolean value.  Doing a double negation cancels out the first negation, thus returning the variable’s natural boolean value.

**3) BONUS: Single line if-then statement**

The traditional, longhand way to write this statement is:

	if x == y
	 puts z
	end

This can be reduced from 3 lines to 1 line with this format:

	*{expression to be evaluated if condition is true} if {condition}*

Applying this format here, the above example would be re-written as:

	`puts z if x == y`

