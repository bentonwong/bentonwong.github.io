---
layout: post
title:  "Greedy Algorithms: Sometimes Good, Sometimes Bad"
date:   2017-09-22 23:29:46 +0000
---

We often make immediate decisions based on the best choice available to us (e.g. whether to eat extra dessert, buy the new iPhone X, etc.) at the moment and ignore the effect on the future (e.g. having to exercise more to burn it off, higher credit card bill, etc.).  Although this approach sounds imprudent, impulsive, and may be against our long term interests, we do it because it is easier to analyze, make decisions quicker, and receive immediate gratification.  Sometimes this approach results in an optimal overall solution, but sometimes it does not.

![](https://i.imgur.com/euYs66B.jpg)

Greedy algorithms are a programming paradigm that applies a similar approach.  It is an algorithm pattern where the locally optimal choice is made at each stage in the hopes of finding a global optimum.  Typically, it is implemented when comparing a set of values and then selecting the highest/lowest ("greedy") value as the best choice for that current state.

The [traveling salesman problem](https://en.wikipedia.org/wiki/Travelling_salesman_problem) is a good example, in non-trivial cases, of where applying the greedy algorithm is good at making the best local and immediate choice (choosing distance to an intermediate destination based only on the one that is the closest), but may not be the best choice (the total sum of the distances are longer than the shortest possible path) in the long run.

**Pros**
* Simple
* Runs Quickly
* Easy to Implement

**Cons**
* Not always reliable at getting the overall optimal solution
* Likely results in longer run time

**Best Applications of Greedy Algorithms**

Despite some of the short comings of this approach, there are several use cases where the greedy algorithm is ideal:

**[Activity selection problem](https://https//youtu.be/poWB2UCuozA)** (selecting the maximum number of activities that can be performed by a single person/machine within a given time frame)

*Approach*

1. Sort activities according to finishing time
2. Select the first sorted activity
3. Continue onto the next sorted activity that does not overlap (i.e. activity with a start time that is greater or equal the end time of the previous activity) and repeat the selection process until all remaining activities are considered

*Time complexity* (where n = number of activities)

* sorted input: O(n)
* unsorted input: O(n log n)

**[Huffman coding](https://www.youtube.com/watch?v=0kNXhFIEd_w)** (lossless data compression algorithm)

*Approach*

2. 1. Create a frequency histogram for each unique character and make each character and its frequency value a leaf node
2. Sort leaves by frequency in ascending order and add them to a new heap
3. Select the first two nodes and remove from that heap with the lowest frequencies and create an new internal node that is the sum of the first two nodes.  The lowest value node (the first one) becomes the left child and the next lowest value (the second one) becomes the right child.
4. Return the new internal node into the heap and resort
5. Go back and repeat 3 and 4 until the heap is left with one node and it becomes the root node.
6. Generate the code for each character generated from step 1 as a sequence of 0s and 1s by traversing the tree ultimately generated in step 5 from the root to the desired leaf.  Traversing right on the tree generates a 0 and traversing left generates a 1.  The sequence are directions or turn by turn instructions to get to the leaf from the root.

*Time Complexity* (n = number of unique characters)

O(n log n), because it takes log n times to obtain the minimum value for each unique character and insert the new value and we have to do it for each unique character (n iterations)

**[Job sequencing problem](https://www.youtube.com/watch?v=R6Skj4bT1HE)** (select jobs can be completed within their deadlines while giving maximum profit)

*Approach*

1. Sort the jobs by profit in descending order
2. Iterate through the sorted sequence and select only the remaining jobs that can still be completed within the deadline

*Time Complexity* (n = number of jobs)

O(n^2)

**[Fractional knapsack problem](https://youtu.be/m1p-eWxrt6g)** (optimize the packing of items in a container with items providing the best value and weight)

*Approach*

1. Calculate the value/weight ratio for each item
2. Sort the ratios in descending order
3. Start with the highest ratio first, then add the remaining items in order that can fit as a whole in the container with the remaining space until all items are considered

*Time Complexity*

O(n log n), because each sort take log n and we have to perform this for each of the n items.
Minimum spanning tree (find the minimum sum that connects all vertices in a graph)

**[Minimum spanning tree](https://youtu.be/2ZfFIGCD0Mo)** (find the minimum sum that connects all vertices in a graph)

*Approach*
1. Remove all loops and parallel edges
2. Start with a node, any node
3. Look at adjacent, connecting nodes and link to it with the edge that has the lower value
4. Repeat step 3 for all remaining unlinked nodes, by starting from any linked nodes and using edges that have not been traversed, until all nodes are connected

*Time Complexity*

O((v + e) log v) where v is the number of vertices and e is the number of edges; it takes log v time because each vertex insertion takes logarithmic time
