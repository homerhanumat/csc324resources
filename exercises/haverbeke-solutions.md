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