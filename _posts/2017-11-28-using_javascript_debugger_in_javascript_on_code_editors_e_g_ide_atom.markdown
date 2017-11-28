---
layout: post
title:      "Using JavaScript 'debugger' on Code Editors (e.g. IDE/Atom)"
date:       2017-11-28 14:35:57 -0500
permalink:  using_javascript_debugger_in_javascript_on_code_editors_e_g_ide_atom
---


Debugging in JavaScript within code editors can be difficult without a running console.  Most would just run tests to see if their code worked or not. It is not efficient as it takes time to run the test(s) and it still does not entirely help pinpoint where the bug is located inside the code.

JavaScript has a debugger option which can be used even inside a code editor without having to jump over to Chrome to use its developer tools or a go to sites such as JSFiddle or repl.it.  It is just a matter of taking a few extra steps.

**1)     Insert 'debugger' at the desired breakpoint**

Below is a sample function in a file named index.js, which takes in a number and returns the square of it.

```
//index.js

function squareNumber(num) {
     return num**2;
}
```

Now let's say we want to check to see if the parameter is properly taking in the argument, we would insert a break point by adding a 'debugger' statement before the first line of the code block as shown below.

```
//index.js

function squareNumber(num) {
  debugger;
  return num2;
}
```

**2)     Call the function manually from the same file as the function with the 'debugger' statement**

```
//index.js

function squareNumber(num) {
  debugger;
  return num2;
}

//call the function manually and add any necessary arguments
squareNumber(2);
```

Here, we just call the function by writing the name of the function, and use '2' as an argument, below the function itself.

**3)     In the terminal, check to see that the terminal is currently in the same directory as the file that has the code with the debugger statement**
     
If not, change directory (i.e. 'cd') over to it until the terminal is in that directory.

**4)     In the terminal type 'node inspect ' + {name of the file}**

In the above example, you would type into the terminal 'node inspect index.js'.  This should bring up a console with a 'debug>' prompt at the end.

```
< Debugger listening on ws://127.0.0.1:9229/57f2ff75-4be2-46eb-b019-9f7af03c0f4c
< For help see https://nodejs.org/en/docs/inspector
< Debugger attached.
Break on start in index.js:1
> 1 (function (exports, require, module, filename, dirname) { // --- Directions
  2 // Given a string, return a new string with the reversed
  3 // order of characters
debug>
```

You may need to open a new terminal window and repeat this step if an error message (e.g. timeout) appears.  Here is an example:

```
There was an internal error in node-inspect. Please report this bug.
Timeout (2000) waiting for 127.0.0.1:9229 to be free
Error: Timeout (2000) waiting for 127.0.0.1:9229 to be free
  at Timeout.setTimeout [as onTimeout] (node-inspect/lib/inspect.js:63:14)
  at ontimeout (timers.js:475:11)
  at tryOnTimeout (timers.js:310:5)
  at Timer.listOnTimeout (timers.js:270:5)**
```

Again, make sure the terminal is in the *same* directory as the code file when attempting this again from a fresh terminal screen.

**5) Type 'c' to hit the 'debugger' statement**

The 'debug>' prompt above stops at the top of the function.  We need to *continue* to the the next debugger statement by typing in 'c'.

```
debug> c
break in index.js:10
  8
  9 function reverse(str) {
>10 debugger;
 11 return str.split('').reduce((reversed, character) => {
 12 return character + reversed;
debug>
```

After typing in 'c', an arrow is pointing to the 'debugger' statement and we are now at the first break point.

**6) At the 'debug>' prompt, type 'repl'**

```
debug> repl
Press Ctrl + C to leave debug repl
>
```

This will launch a REPL (Read-Eval-Print Loop) session and allow access to variables and functions like one would have in a JavaScript console.  In the above example, we pass in '2' as an argument into 'num'.  In the 'repl' session, we type 'num' to check that it is equal to '2' and it does.  We can also experiment with the parameter in the console as show below.

```
debug> repl
Press Ctrl + C to leave debug repl
> num
2
> num*num
4
>
```

If the REPL session is not launched, an error will be thrown.  For example, if we just typed in 'num' at the 'debug>' prompt, it will throw an error like the one below:

```
ReferenceError: num is not defined
  at repl:1:1
  at ContextifyScript.Script.runInContext (vm.js:59:29)
  at Object.runInContext (vm.js:120:6)
  at REPLServer.controlEval [as eval] (node-inspect/lib/internal/inspectrepl.js:521:25)
  at REPLServer.onLine (repl.js:441:10)
  at emitOne (events.js:116:13)
  at REPLServer.emit (events.js:211:7)
  at REPLServer.Interface.onLine (readline.js:282:10)
  at REPLServer.Interface.line (readline.js:631:8)
  at REPLServer.Interface.ttyWrite (readline.js:911:14)
debug>
```

**7) To exit the 'repl' session, type Ctrl + C**

This will us back to the 'debug>' prompt.

**8) To exit 'debug>', type '.exit'**

This will return the prompt back to the regular terminal.
