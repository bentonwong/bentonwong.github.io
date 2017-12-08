---
layout: post
title:      "7 JavaScript Array Helpers To Know"
date:       2017-12-08 22:52:56 +0000
permalink:  7_javascript_array_helpers_to_know
---

The traditional, go-to method for iterating through an array is the classic [for statement loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for).  For loops provide flexibility and customization on iterating over a code block.

In most cases, a for loop can be overkill if complete iteration is needed.  The set up on a for loop is prone to syntax mistakes:

* missing a semi-colon or substituting the semi-colon for other punctuation (e.g for (let i = 0 i < array.length, i++)
* forgetting to declare the initialization variable (e.g. (i = 0; i < array.length; i++))
* forgetting to apply proper opening and closing parenthesis and curly brackets

In other words, there are many opportunities to make an error on for loop setups.

When applicable, array helpers can reduce this frustration and abstract away some of this set up and focus on what needs to be executed on each element of an array.  Below are 7 popular and useful array helpers to know.

## 1. forEach()

`array.forEach(function(currentValueAtIndex, index, array), thisValue)`

*Example*

```
array.forEach((element) => {
     console.log(element);
     return;
})
```

*Description*

* Applies a function to be applied to each element of an array.
* Iterates through the array in the array's order.
* This can be simple as returning that element's value.
* Does not create a new array.
* Index and array are optional parameters that can be accessed if required by the code block.

## 2. map()

`array.map(function(currentValueAtIndex, index, arr), thisValue)`

*Example*

```
let result =[];
result = [1,2,3,4,5].map((element) => {
  return (element * 2);
});

//result = [2,4,6,8,10]
```

**Description**

* Similar to forEach(), but creates a new array with the result of the function taking in the original array's element as an argument and setting the result as the respective element in the new array.
* Index and array are still optional parameters that can be accessed if required by the code block.

## 3. filter()

`array.filter(function(currentValue, index, arr),thisValue)`

*Example*

```
let result = [];
result = [1,2,3,4,5].filter((element) => {
  return (element < 4);
});

//result = [1,2,3]
```

*Description*

```
* Returns a new array which contains elements from the original array that meets a condition that returns true in the accompanying function.
* The original array is not mutated.
```

## 4. find()

` array.find(function(currentValueAtIndex, index, arr),thisValue)`

*Example*

```
const inputArray = [1, 2, 3, 4, 5]

const result = inputArray.find((element) => {
  return (element === 10);
});

//undefined
```

*Description*

* Similar to filter(), find will return an element from the original array that meets a certain condition.
* However, find will only return the first value in the original array that meets this condition and will not check the remaining values.
* Undefined is returned if no value is found.
* The original array is not mutated.

## 5. every()

`array.every(function(currentValueAtIndex, index, arr),thisValue)`

*Example*

```
const inputArray = [1, 2, 3, 4, 5]

inputArray.every((element) => {
  return (element > 3);
});

//false
```

*Description*

* Returns a true if all elements of the original array that meets a condition that returns true in the accompanying function.
* All elements need to return true for this helper to return true.
* Otherwise, false is returned.  Once a false condition is discovered, the remainder of the array is not evaluated.
* The original array is not mutated.

## 6. some()

`array.some(function(currentValueAtIndex, index, arr), thisValue)`

*Example*

```
const inputArray = [1, 2, 3, 4, 5]

inputArray.some((element) => {
  return (element > 3);
});

//true
```

*Description*

* Returns true if any element of the original array that meets a condition that returns true in the accompanying function.
* Only one element needs to return true for the entire some() method to return true.  Once the true condition is satsified, the remainder of the array is not evaluated.
* Otherwise, false is returned.
* The original array is not mutated.
* No array is not created by it.

## 7. reduce()

`array.reduce(function(total, currentValueAtIndex, currentIndex, arr), initialValue)`

*Example*

```
const inputArray = [1, 2, 3, 4, 5]

const sumOfArray = inputArray.reduce((total, element) => {
  return (total + element);
}, 0);

//sumOfArray = 15
```

*Description*

* Iterates through the original array, reduces it to single value, and returns that value.
* The classic use case is summing up the values of an array and returning its sum.
* Unlike the other array helpers above, reduce() takes on additional arguments in its function: an accumulator/total variable that holds onto some value that is passed onto the following iteration, and take on an initial value for the preceding accumulator/total variable as an additional parameter.
