---
layout: post
title:      "Quick Comparison of Common Data Structures"
date:       2017-11-02 00:24:41 +0000
permalink:  quick_comparison_of_common_data_structures
---


The common data structures are:

* Arrays
* Linked Lists
* Hash Tables/Maps
* Binary Trees

Below are some basic concepts to remember about each of these structures.

**Arrays**
Arrays store elements using a sequential index.  They are great for indexing, but are slow at searching, inserting, and deletion (except at the end).  For linear arrays, the Big O efficiency is:

* Indexing: O(1)
* Searching: O(log n)
* Insertion: O(n)

**Linked Lists**
Linked lists store data onto nodes which point to other nodes.  Therefore, each node holds at a minimum, (1) a value and a (2) reference to another node.  A chain of these nodes comprises a linked list.  They are great for insertion and deletion but are slow at searching and indexing.  For Linked Lists, the Big O efficiency is:

* Indexing: O(n)
* Searching: O(n)
* Insertion: O(1)

Variations on the linked lists include:

* Circularly linked lists: a linked list whose last node references the first or head node.
* Doubly linked lists: a linked list that also references the previous node.
* Stacks: follows a last in, first out (LIFO) scheme where the last element in will be the first element out of the list.  This is usually implemented by making insertion and deletion only occur at the head.
* Queues: follows a first in, first out (FIFO) scheme where the first element in will be the first element out of the list.  This is usually implemented by using a doubly linked list where the deletion occurs at the head and insertion occurs only at the tail.

**Hash Table**
Hash tables store data in key-value pairs, where a hash function with an input of a specific key will return a specific output value.  Hashes are great at searching, insertion, and deletion. For hash tables, the Big O efficiency is:

* Indexing: O(1)
* Searching: O(1)
* Insertion: O(1)

**Binary Trees**
Binary trees use nodes and each node (the parent node) has two children: a left and right node.  The left node's value is less than the parent node's value and the right node's value is greater than the parent node's value.  This enables binary trees to be great at searching and sorting.  For binary trees, the Big O efficiency is:

* Indexing: O(1og n)
* Searching: O(log n)
* Insertion: O(log n)
