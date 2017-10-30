---
layout: post
title:      "JavaScript Scope"
date:       2017-10-30 01:15:57 +0000
permalink:  javascript_scope
---

JavaScript scope, which includes the types of global and local, sets the accessibility of variables, objects, and functions.

**Global versus Local Variables**

Local variables are variables declared within a function and can only be accessed within the function.  Such variables are only available when declared and they are deleted when a function has completed.

Global variables are declared outside of a function and all scripts and functions can access it.  For example: 
```
var someVariable = "Hello";

function block() {
     console.log(someVariable);
}

block();
```
The above code will display "Hello" in the console because the block() function has access to *someVariable*, which was declared and assigned outside of the block() function.

Interestingly, undeclared variables (i.e. omitting var, let, const before a variable's first assignment in the code) will become global variables by default, even if used in a function.  Global variables are available as long as the window is open, even if new pages are loaded into that same window.

**What if a global variable and a local variable have the same name?**

The local variable will have priority over the global variable.  Look at the code below:
```
var someVariable = "Hello";

function block() {
     console.log(someVariable);
     var someVariable = "Goodbye";
}

block();
```
"Hello" is not displayed in the console since the variable *someVariable* is declared in the block() function and that local declaration will take over.

**Then, what will be displayed?**

The above code will instead yield "undefined" in the console.  A declared variable yields a value of undefined.  Hoisting will bring the local *someVariable* declaration to the top of the scope and would be interpreted as if it were:
```
var global = "Hello";

function block() {
     var global;
     console.log(global);
     global = "Goodbye";
}

block();
```

**Why isn't "Goodbye" displayed?**

"Goodbye" is not displayed because hoisting only "hoists" or brings the declaration of the variable to the top of the scope of the block() function. The assignment of the value "Goodbye" to *someVariable*, is not brought to the top and is not displayed in the console.
