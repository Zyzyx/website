
---
title: "Brute Forcing AI"
date: "2010-12-30T11:49:00-04:00"
draft: false
---

Similar to cracking passwords, computers can brute-force solve single-player puzzles too, as long as the following criteria is met:

* The puzzle has a well defined start state.
* There are 1 or more states where the game is said to be won.
* There is a finite number of moves a player can make.

During the flights to and from St. Louis to visit Muffin's family, I occupied my time putting this hypothesis to the test with Sudoku. She's been working on a Not-so-easy collection of Sudoku puzzles and I figured I could help her along with a script that could give her hints. I'm sure you can find this sort of thing on the internet already, but I had time to kill on a few planes. I wasn't interested in the most performant program, just something quick to help her, and demonstrate to myself that I remembered a few things from an AI class I took while I was still in college.

I opted to go with a "Brute Force AI" methodology which probably has a more respectable name I have since forgotten, so that is what I'm calling it. Using this approach the program must have a structure that represents the "state" of the puzzle: moves that have been made so far, where the pieces are, the layout of the board, etc. In Sudoku, that just means where the numbers we have placed are. The algorithm also needs two lists: one that tracks puzzle states we want to proceed from, and one that tracks what states we have already seen.

I'll try to walk through the algorithm here, in case the previous paragraph was too confusing or vague. If it was I doubt that is the fault of you, dear reader, but I am assuming you are familiar with the rules of Sudoku. The process begins with the starting state of the puzzle, and in the first iteration, all possible states you can get to in one single move are calculated. In Sudoku that means putting numbers anywhere it is possible without duplicates in a row, column, or region. There may be hundreds of such states, and all of them are put into both of the lists I described.

We then select a state from the first list, and from there, figure out all of the valid states we can get to in one move, just as we did before. From those valid states, we discard the ones that are already in the seen list, because we have already seen/tried them. What remains we put in both lists, and we remove the state we are currently working on from the first list, the list of moves we want to proceed from. We then repeat this process until one of the following conditions is met: the current puzzle state we're working from is the winning state (all numbers are placed without any duplicates in rows, columns or regions), or the current puzzle state does not have any valid moves you can make (i.e.: the game is insolvable with the numbers we have placed so far). If we hit the first condition, we're done; if we hit the second, we simply remove this state from the first list, and select another one.

What you end up with is a process where the computer is just making arbitrary moves until it ends up in the desired puzzle state. If it hits puzzle states it cannot proceed from, it throws them aside and picks a different (older) one. There is nothing intelligent about this approach; it is slow and blunt, but because computers are so fast, that usually doesn't matter with simple games.

It took me about 5 hours to implement. It requires a text file that has the starting Sudoku puzzle state as shown below. You then run the program like so: sudoku.py [check|solve|hint] path-to-puzzle-text. Setting the first argument to check just has it report if the puzzle is solvable. Solve obviously solves it and prints out the answer, and hint has it print out the puzzle with 1 more number added in. It will ask if you want additional hints, and each time you answer "y", it will fill in another one.
```
_,_,_,_,_,_,_,_,3
_,_,2,_,_,8,7,6,_
9,4,_,7,6,_,_,1,_
_,3,_,8,_,_,_,_,_
7,_,_,_,4,_,6,_,_
_,9,_,6,_,_,_,_,_
3,7,_,9,2,_,_,4,_
_,_,8,_,_,1,3,9,_
_,_,_,_,_,_,_,_,5
```
My Python implementation usually takes about a minute to compute a solution, and I've included here. I'm sure there are Sudoku-specific optimizations that can be added to make it faster, but I myself am not a skilled Sudoku player, so some of that logic is beyond me. I did add one condition where if the system figures out it cannot put any number in a given space, it discards the puzzle state immediately instead of moving on to another space. This is because in Sudoku if you cannot put any number in a space, no future move will ever make numbers valid there.

I haven't used anything I learned in AI in a professional context yet, just hobby stuff like this. But at least I know I remember some of it.

