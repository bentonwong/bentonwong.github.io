---
layout: post
title:      "Using the Ruby Set Library"
date:       2017-11-09 00:26:41 +0000
permalink:  using_the_ruby_set_library
---


Ruby has a cool feature in its standard library called [Set](http://ruby-doc.org/stdlib-2.4.2/libdoc/set/rdoc/Set.html), which allows mathematical set operations (e.g. union, subset, intersection, difference) to be applied to a collection of objects.

![](https://i.imgur.com/gDx0Tk6.png)

Here are examples:
```
require 'set' #an uninitialized constant error will be thrown without this since Set is part of the library, not the core

#Union
Set['a', 'b', 'c'] | Set['d', 'e', 'f']
# => {"a", "b", "c", "d", "e", "f"}

#Subset
Set['d','e','f'].subset?(Set['a','b','c','d','e','f','g'])
# => true

#Intersection
Set['d','e','f'] & Set['a','b','c','d','e','f','g']
# => {"d", "e", "f"}

#Difference
Set['a','b','c','d','e','f','g'] - Set['d','e','f']
# => {"a", "b", "c", "g"} Note: the order of operations do matter here; if the sets are reversed here, the returned set would be empty
```
You can even apply enumerable methods such as ```.each``` or ```.sort```.

**When to use Set over Array**

Set should be used where the sequence contains no duplicate values (i.e. unique objects) and the order does not matter to determine equality.

However, arrays should be used when sequences have duplicates, order does matter, and individual elements do need to be accessed.
