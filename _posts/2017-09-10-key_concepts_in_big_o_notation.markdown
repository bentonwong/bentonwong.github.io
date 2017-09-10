---
layout: post
title:  "Key Concepts in Big O Notation"
date:   2017-09-10 04:54:51 +0000
---

 
Big O is a metric for measuring algorithm efficiency.  It often describes the upper bound, which is the worse case, running time of an algorithm, and can be used to compare the efficiency of one algorith against another.  Here is a quick summary highlighting key big O notation concepts:

**Fastest to Slowest Functions**
Where N is variable representing the actual input or size of the input, the list below ranks big O times from fastest (i.e. slower growing) to slowest:

1. O(1)		             Constant
2. O(log N)	         Logarithmic
3. O(N)		            Linear
4. O(N log N)	     Linearithmic
5. O(N^2)		        Quadratic
6. O(2^N) 	        Exponential
7. O(N!)		          Factorial

**Adding Run Times**
If an algorithm has multiple, consecutive steps, each the run times are added.  For example, if step 1 has a run time of X and step 2 has a run time of Y, the big O notation is O(X+Y).

**Multiplying Run Times**
If an algorithm has a step with a run time of y, which is executed for every element in x, the run times are multiplied.  For example, a step with run time y that is contained in a for loop with x elements will have a runtime of O(X*Y).

**Drop Constants**
With two consecutive steps, both with a run time of N, the big O notation would be O(2N).  But in big O notation analysis, we would drop the constant and notation would be O(N).  With big O notation, we are looking for the relative rate of increase (i.e. how an algorithm scales).

**Drop Non-Dominating Terms**
If there are multiple terms describing an algorithm, the non-dominating terms are dropped in the big O analysis.  For example:

O(2N^2 + N) becomes O(N^2)
O(N + log N) becomes O(N)

The dominating term is the driving factor here, and thus the non-dominant terms are dropped.

