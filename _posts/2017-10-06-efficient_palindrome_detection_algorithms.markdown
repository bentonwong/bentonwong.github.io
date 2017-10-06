---
layout: post
title:      "Efficient Palindrome Detection Algorithms"
date:       2017-10-06 14:56:33 -0400
permalink:  efficient_palindrome_detection_algorithms
---


A palindrome is a string that can be read the same backwards and forwards (i.g. civic, level, etc.).

As an algorithm, the easiest implementation that comes to mind (assuming the string is all lowercase) is to reverse the string and see if it matches the original string:

```
function isPalindrome(string) {
  reverseString = string.split('').reverse().join('')
  return reverseString == string
}
```

Although clean and simple, the time complexity is at O(n) in order to split a copy of the string, reverse it, and rejoin it, and the space complexity is at O(n) in order to store value of the reversed string.

However, the complexity can improved by iterating through the string and doing an in place comparison:

```
function isPalindrome(string) {
  strLength = string.length
  if (strLength === 0) {
    return true
  }

  stringArray = []
  stringArray = string.split('')
  for (let i = 0, j = strLength - 1; i < strLength/2; i++, j--) {
      if (stringArray[i] != stringArray[j]) {
         return false
      }
  }
  
  return true
}
```

This method essentially checks to see if the reflection from the other half matches the first half. There are a couple advantages here:

1. Avoids the need to reverse the string and then rejoin it, which is two additional iterations through the string.  Here, we are only doing an additional 1/2 iteration. 
2. Avoids the creation and use of an additional variable to store the reversed string value.
