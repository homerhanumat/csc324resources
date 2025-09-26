## Chapter 2 Solutions

```js
function notify(text) {
  console.log(`\nTesting ${text} ...\n`);
}

/****************************************************
Looping a Triangle

 Write a loop that makes seven calls to console.log to 
 output the following triangle:

#
##
###
####
#####
######
#######

Notes on my solution:

I wondered if Javascript had a function like R's rep(),
so I googled "javascript repeat character" and found a
number of sites, including:

https://stackoverflow.com/questions/1877475/repeat-character-n-times

The repeat method for strings turned out to be just what
I was looking for!

*****************************************************/

notify("Looping a Triangle");

for (let i = 1; i <= 7; i++) {
  console.log("#".repeat(i));
}

/**************************************************************
 * 
 * FizzBuzz
 * 
 * Write a program that uses console.log to print all the numbers
 * from 1 to 100, with two exceptions. For numbers divisible by 3, 
 * print "Fizz" instead of the number, and for numbers divisible by 5 
 * (and not 3), print "Buzz" instead.
 * 
 * When you have that working, modify your program to print 
 * "FizzBuzz" for numbers that are divisible by both 3 and 5 
 * (and still print "Fizz" or "Buzz" for numbers divisible by 
 * only one of those).
 * 
 ******************************************************************/

 // Version One
 notify("FizzBuzz, Version 1");
for (let i = 1; i <= 100; i++) {
  if (i % 3 === 0) {
    console.log("Fizz");
  } else if (i % 5 === 0) {
      console.log("Buzz");
  } else {
    console.log(i);
  }
}

// Version Two
notify("FizzBuzz, Version 2");
for (let i = 1; i <= 100; i++) {
  if (i % 15 === 0) {
    console.log("FizzBuzz");
  } else if (i % 3 === 0) {
      console.log("Fizz");
  } else if (i % 5 === 0) {
    console.log("Buzz");
  } else {
    console.log(i);
  }
}

/*******************************************************************
 * 
 * Chessboard
 * 
 * Write a program that creates a string that represents an 8×8 
 * grid, using newline characters to separate lines. At each 
 * position of the grid there is either a space or a "#" 
 * character. The characters should form a chessboard.
 * 
 * Passing this string to console.log should show something like this:

 # # # #
# # # # 
 # # # #
# # # # 
 # # # #
# # # # 
 # # # #
# # # #


 * When you have a program that generates this pattern, define a 
 * binding size = 8 and change the program so that it works 
 * for any size, outputting a grid of the given width and height.
 * 
 ********************************************************************/

// I'll move directly to the more general version

const size = 9;
const pairs = Math.floor(size / 2),
      oddRow = " #".repeat(pairs) + "\n",
      evenRow = "# ".repeat(pairs) + "\n",
      twoRows = oddRow + evenRow,
      board = twoRows.repeat(pairs),
      extraRow = size %2 === 1 ? oddRow : '';

notify(`Chessboard, with size = ${size}`);
console.log(board + extraRow);
```

## Chapter 3 Solutions

```js
function notify(text) {
  console.log(`\nTesting ${text} ...\n`);
}

/****************************************************
 MINIMUM

 The previous chapter introduced the standard function
 Math.min that returns its smallest argument. We can
 do that ourselves now. Write a function min that takes
 two arguments and returns their minimum.
 *****************************************************/

function min(x, y) {
  return x <= y ? x : y;
}

notify("min");
console.log(min(5, 3));
console.log(min(-2, 3));

// another version:
let min2 = (x, y) => x <= y ? x : y;

notify("min2");
console.log("min2", -4, 6, min2(-4, 6));

/*******************************************************
 * RECURSION
 *
 * Recursive function to determine if a number is even
 *******************************************************/

function isEven(n) {
  n = n >= 0 ? n : -n;
  if ( n === 0 ) return true;
  if ( n === 1 ) return false;
  return isEven(n - 2);
}

notify("isEven");
console.log(isEven(50));
console.log(isEven(-27));

/*******************************************************
 * Bean Counting
 *
 * Function to count number of occurences of a character
 * in a string
 *******************************************************/

function countChar(str, char) {
  let count = 0;
  for ( let n = 0; n < str.length; n++ ) {
    count += str[n] === char ? 1 : 0;
  }
  return count;
}

notify("countChar");
console.log(countChar("hello", "l"));
```

## Chapter 4 Solutions

```js
function notify(text) {
    console.log(`\nTesting ${text} ...\n`);
}

/**************************************************************
 * SUM AND RANGE
 * 
 * Write a range function that takes two arguments, start and 
 * end, and returns an array containing all the numbers from 
 * start up to (and including) end.
 * 
 * Next, write a sum function that takes an array of numbers 
 * and returns the sum of these numbers. Run the example 
 * program and see whether it does indeed return 55.
 * 
 * As a bonus assignment, modify your range function to take
 *  an optional third argument that indicates the “step” value
 *  used when building the array. If no step is given, the 
 * elements go up by increments of one, corresponding to the 
 * old behavior. The function call range(1, 10, 2) should return
 *  [1, 3, 5, 7, 9]. Make sure it also works with negative step
 *  values so that range(5, 2, -1) produces [5, 4, 3, 2].
 ****************************************************************/

function range(start, stop, step = 1) {
    let arr = [];
    function finished(c, t) {
        return step > 0 ? c > t : c < t;
    }
    let current = start;
    while (!finished(current, stop)) {
        arr.push(current);
        current += step;
    }
    return arr;
}

function sum(arr) {
    let sum = 0;
    for (let elem of arr) {
        sum += elem;
    }
    return sum;
}

notify("range and sum");
console.log(range(1, 10));
// → [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
console.log(range(5, 2, -1));
// → [5, 4, 3, 2]
console.log(sum(range(1, 10)));
// → 55

/**************************************************************
 * REVERSING AN ARRAY
 * 
 * Arrays have a reverse method which changes the array by 
 * inverting the order in which its elements appear. For this 
 * exercise, write two functions, reverseArray and 
 * reverseArrayInPlace. The first, reverseArray, takes an array 
 * as argument and produces a new array that has the same 
 * elements in the inverse order. The second, reverseArrayInPlace,
 * does what the reverse method does: it modifies the array 
 * given as argument by reversing its elements. Neither may use 
 * the standard reverse method.
 ****************************************************************/

function reverseArray(arr) {
    let reversed = [];
    for (elem of arr) {
        reversed.unshift(elem);
    }
    return reversed;
}

function reverseArrayInPlace(arr) {
    for (let i = 0; i < Math.floor(arr.length / 2); i++) {
        let elem = arr[i];
        let oppositeLocation = arr.length - i - 1;
        arr[i] = arr[oppositeLocation];
        arr[oppositeLocation] = elem;
    }
}

notify("reversing");
console.log(reverseArray(["A", "B", "C"]));
// → ["C", "B", "A"];
let arrayValue = [1, 2, 3, 4, 5];
reverseArrayInPlace(arrayValue);
console.log(arrayValue);
// → [5, 4, 3, 2, 1]
let arrayValue2 = range(1, 6);
reverseArrayInPlace(arrayValue2);
console.log(arrayValue2);
```

## Chapter 5 Solutions

```js
function notify(text) {
  console.log(`\nTesting ${text} ...\n`);
}

/*************************************************************
 * FLATTENING
 *
 * Use the reduce method in combination with the concat method
 * to “flatten” an array of arrays into a single array that has
 * all the elements of the input arrays.
 *************************************************************/

function flatten(arr) {
  return arr.reduce((acc, elem) => acc.concat(elem), []);
}

notify("flatten");
let array1 = [[1, 2], [3, 4], [5, 6, 7], [8]];
console.log(flatten(array1));
// Note that this solution works even when not all elements of the
// array are themselves arrays:
let array2 = [0, [1,2], [3,4,5]];
console.log(flatten(array2));
// But flattening only goes one level deep:
let array3 = [[1], [2, 3, 4], [5, [6, 7]], [8]];
console.log(flatten(array3));

// a verbose version (to help show how reduce works):
function verboseConcatenation(acc, elem) {
  console.log("\nWhat we have so far is:");
  console.log(acc);
  console.log("To this we will append:");
  console.log(elem);
  let more = acc.concat(elem);
  return more;
}

function verboseFlatten(arr) {
  return arr.reduce(verboseConcatenation, []);
}

notify("the verbose form of the flatten function:");
let flat1 = verboseFlatten(array1);
console.log("\nThe result is:");
console.log(flat1);

let flat2 = verboseFlatten(array3);
console.log("\nThe result is:");
console.log(array3);

/*********************************************************************
 * Let's improve our function: have it flatten "deeply", 
 * in the sense that the array that
 * it returns has no elements that are themselves arrays.
 ********************************************************************/


// First, a helper-function:
function isFlat(thing) {
  if (!Array.isArray(thing)) {
    // a non-array counts as "flat":
    return true;
  }
  // if we got this far, thing is an array, so iterate through it:
  for (elem of thing) {
    if (Array.isArray(elem)) {
      // found an array inside thing, so:
      return false;
    }
  }
  // if we got this far then no element of thing was an array, so:
  return true;
}

// Next, a recursive function to flatten deeply:
function deepFlatten(arr) {
  if (isFlat(arr)) {
    return arr;
  }
  return arr.reduce((acc, elem) => acc.concat(deepFlatten(elem)), []);
}

notify("deepFlatten");
let array4 = [[0,[[1]], [[2, 3]]], [[[[4], [[5], [6]]]]], [[7, 8]], 9, [[10]], 11];
console.log(deepFlatten(array4));



/***************************************************************
 * WRITE YOUR OWN LOOP FUNCTION
 ***************************************************************/

function loop(value, test, update, bodyFn) {
  while (test(value)) {
    bodyFn(value);
    value = update(value);
  }
}

notify("loop");
loop(3, n => n > 0, n => n - 1, console.log);

/**************************************************************
 * EVERYTHING
 *
 * Implement every as a function that takes an array and a
 * predicate function as parameters. Write two versions, one
 * using a loop and one using the some method.
 **************************************************************/

// using loop
function every(arr, predFn) {
  for (elem of arr) {
    if (!predFn(elem)) return false;
  }
  return true;
}

let myArray = [1,2,3,4,5,6];

notify("every");
console.log(every(myArray, x => x >= 2));
console.log(every(myArray, x => x >= 1));

// using some method
function every2(arr, predFn) {
  return !arr.some((elem) => !predFn(elem));
}

notify("every2");
console.log(every2(myArray, x => x >= 2));
console.log(every2(myArray, x => x >= 1));
```