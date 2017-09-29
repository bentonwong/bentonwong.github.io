---
layout: post
title:  "Interesting applications for XOR"
date:   2017-09-29 15:46:58 -0400
---


**'Exclusive or' (XOR) Defined**

XOR is a bitwise operation that compares two sets of bits where it returns 1 if only and only one of the two bits is 1.  Otherwise, the operator returns a 0.  Wikipedia uses this very precise definition: "a logical operation that outputs true only when inputs differ".  Using the the ^ symbol, the XOR operator works like this:

```
1 ^ 1 = 0
1 ^ 0 = 1
0 ^ 1 = 1
1 ^ 1 = 0
```

**Interesting and Useful Applications for XOR**

*1) Performing Error Checking via Checksum*

XOR is often used to perform error checking when transmitting data.  An additional bit, or the checksum, is also transmitted along with that data.

That checksum is the result of an XOR on a bitstring (e.g. 10110011, checksum = 1).  If there are an even number of 1's, the checksum is 0 since all the 1's cancel each other out (i.e. even parity), while an odd number of 1's will leave a single 1 (i.e. odd parity) as its checksum.

By verifying the checksum value against the XOR of the data at the receiving end and seeing that they match, the receiving end can check to see if the data may have been corrupted during transmission.

*2) Cancel out matching numbers*

XOR are useful for finding a unique value among an array of integers where duplicates exist.   Without using XOR, one could try to iterate over the array and the store the array values and using the array values as its keys.  The keys could then be used to store the frequency in which that key appears in the array. For example:

```
array_of_integers = [ 1, 3, 5, 6, 3, 1, 5]

hash = {}
array_of_integers.each do |integer|
     hash[integer] ?  hash[integer]  += 1 : hash[integer]  = 1
end
```

However, that would also requiring iterating over the resulting hash to identify and return the key whose hash value is 1.  This method requires a runtime of O(n), but also adds O(n) space to store the hash.

With XOR, we can bring the space to O(1) and iterate over the array once.  XOR operators can cancel out matching numbers as it iterates through the array through this implementation:

```
def find_unique_integer(array_of_integers)

  unique_integer = 0

  array_of_integers.each do |integer|
         unique_integer ^= integer
  end

  return unique_integer
end
```

By starting the variable unique integer with 0 and then individually XOR with every integer from the array, the bits for unique integer change.  When the XOR sees the same integer again, it will cancel out the earlier integer remove the duplicate.  At the end, it will return the value that only appears once.

Conversely, XOR could be used to see if each element in an array has a matching element.

*3) Swapping numbers without using a temporary variable*

When swapping variables, it is easy to implement using "temp" variable to hold the value while the swap is made.

```
temp = x;
x = y;
y = temp;
```

Using a temporary variable uses additional space.   We can do away with using the temporary variable by applying this method:

```
x = x ^ y;
y = x ^ y;
x = x ^ y;
```

Try it!



