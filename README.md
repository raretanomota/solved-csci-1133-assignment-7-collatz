Download Link: https://assignmentchef.com/product/solved-csci-1133-assignment-7-collatz
<br>
<h1></h1>

The Collatz conjecture (<u><a href="https://en.wikipedia.org/wiki/Collatz_conjecture">https://en.wikipedia.org/wiki/Collatz_conjecture</a></u><a href="https://en.wikipedia.org/wiki/Collatz_conjecture">)</a> is an unproven mathematical rule that says the following:




Take any positive integer <em>n</em>. If <em>n</em> is even, divide it by 2 to get <em>n / 2</em> (use integer division so that you don’t end up with floating point numbers). If <em>n</em> is odd, multiply it by 3 and add 1 to obtain <em>3n + 1</em>. Repeat the process indefinitely, and eventually you will reach 1.




Write a <strong>recursive</strong> function called collatz that takes in a single positive integer argument n and returns the list of numbers in the collatz sequence from n to 1, inclusive.  For example, suppose your initial number was 5.  Then the collatz sequence would be the following:




The initial number is <strong>5</strong>.

5 is odd, so the next number is 5*3 + 1 = <strong>16</strong>

16 is even, so the next number is 16//2 = <strong>8</strong>

8 is even, so the next number is 8//2 = <strong>4</strong>

4 is even, so the next number is 4//2 = <strong>2</strong>

2 is even, so the next number is 2//2 = <strong>1</strong>

We have reached 1, so the sequence is complete, and the function would return the list <sub>[5,16,8,4,2,1]</sub>

<strong> </strong>

<strong>Hints</strong>:

<ul>

 <li>This function returns a list, so both your base case and your recursive case(s) need to return a list. You will need to add elements to the <strong>front </strong>of the list in this problem.</li>

 <li>.append doesn’t add things to the front of a list, so put the element you want to add in brackets to turn it into a list and then use list addition. To put element x at the front of the list ls, you’d use [x] + ls.  For example, note that:</li>

</ul>

collatz(5) = [5]+collatz(16) = [5]+[16,8,4,2,1] = [5,16,8,4,2,1]




<strong>Constraints</strong>:

<ul>

 <li>The collatz function must be implemented using only recursion. Do not use any loop constructs (while or for).</li>

 <li>Do not import any modules (except random, for problem C).</li>

 <li>You may assume that your function will only be called with positive integers.</li>

 <li>Don’t use the input() function, as this will break our grading scripts.</li>

 <li>Your submission should have no code outside of function definitions (comments are fine).</li>

</ul>




<strong>Examples</strong>:




&gt;&gt;&gt; collatz(5)

[5, 16, 8, 4, 2, 1]




&gt;&gt;&gt; collatz(1)

[1]




&gt;&gt;&gt; collatz(123)

[123, 370, 185, 556, 278, 139, 418, 209, 628, 314, 157, 472, 236, 118, 59, 178, 89, 268, 134, 67, 202, 101, 304, 152, 76, 38, 19, 58, 29, 88,

44, 22, 11, 34, 17, 52, 26, 13, 40, 20, 10, 5, 16, 8, 4, 2, 1] <strong><em> </em></strong>




Image source: <u><a href="https://xkcd.com/710/">https://xkcd.com/710/</a></u>







<h1>Problem B. (10<em> points</em>)  Finding the Minimum</h1>

Write a <strong>recursive</strong> function find_min that takes in one argument, a list of integers num_list, and returns the minimum value in that list.  You may assume that num_list contains at least one element.  Note that even if there is a tie, there should still only be one minimum value (it just appears more than once in the list).




<strong>Constraints</strong>:

<ul>

 <li>The find_min function must be implemented using only recursion. Do not use any loop constructs (while or for).</li>

 <li>Built-in functions like min and sorted that trivialize the problem are banned, for obvious reasons.</li>

 <li>Do not import any modules (except random, for problem C).</li>

 <li>Don’t use the input() function, as this will break our grading scripts.</li>

 <li>Your submission should have no code outside of function definitions (comments are fine).</li>

</ul>




<strong>Examples</strong>:




&gt;&gt;&gt; find_min([8])

8




&gt;&gt;&gt; find_min([0, 2, -5, -2, 5, -1, 4, 0, -5, -1])

-5




&gt;&gt;&gt; find_min([20, 34, 32, 34, 48, 43, 21])

20




Problem C. Playing Tic-Tac-Toe Perfectly

In Homework 5, we created a program to play tic-tac-toe by choosing an empty spot at random.  This is generally a very bad strategy: most preschoolers can beat it more than half the time (even when they don’t cheat).  But, with the power of recursion, we can make a much better tic-tac-toe AI: in fact, we can make one that never loses.  To do this, our AI will look at every possible sequence of moves and try to find a strategy that forces a win, or at least forces a draw if that’s not possible.

<em> </em>

Creating a tic-tac-toe AI that can’t lose will require a few steps.  You’ll want to start by copying in all of your tic-tac-toe code from Homework 5: most of the functions there will be useful for this problem as well.  We will post a solution to Homework 5 for those of you who didn’t get all of the functions working.




Write a <strong>recursive</strong> function called force_win(board), which takes in one argument: board is a list representation of a tic-tac-toe board (see Homework 5).  force_win should return an integer that represents the current state of the board.  Board state can be one of three values:

<ul>

 <li><strong>1</strong>         means that X has won, or can force a win: that is, there are moves that X can make so that no matter what O does, X will win</li>

 <li><strong>-1</strong>       means that O has won, or can force a win: that is, there are moves that O can make so that no matter what X does, O will win</li>

 <li><strong>0</strong> means that neither of the above is true: if both players play perfectly, the game will end in a draw</li>

</ul>




This means that when looking at potential next moves, X will attempt to find moves that leave the board in the highest value for board state possible (because X would prefer to win (state 1), over a draw (state 0), over losing to O (state -1)).




Whereas O will attempt to find moves that leave the board in as low of a board state as possible (because O would prefer to win (state -1), over a draw (state 0), over losing to X (state 1)).




The general approach is as follows:

<ol>

 <li>Figure out whose turn it is using the open_slots function. Since we start with 9 open spots and alternate turns, if there are an odd number of open slots it’s X’s turn, otherwise it’s O’s.</li>

 <li>As your base cases, use the winner function and determine whether the game is already over. If it is, return the appropriate board state (1 for X winning, 0 for a draw, -1 for O winning).</li>

 <li>If it is currently X’s turn, then we want to find the move that would result in the highest possible value for the board state. So loop through the possible moves (that is, loop through the open slots in the board), and keep track of the board state you get back for each move: we will return the highest one.  In particular, do the following for each possible move:

  <ol>

   <li>Create a copy of the current board (you can use board[:] for this).</li>

   <li>Place the potential move on the copied board (put an X in that slot).</li>

   <li>Recursively call force_win on that board to see what the board state would be (think about why this is guaranteed to move towards a base case).</li>

  </ol></li>

 <li>At the end of the loop, return the highest board state value that you found.</li>

 <li>If it is O’s turn, do the opposite: return the lowest possible board state you could get from any of O’s potential moves.</li>

</ol>




Test this function using the examples below: only go on to the next part after you are sure that force_win works.




Finally, you will alter the tic_tac_toe function from Homework 5 to use your AI to decide moves for player O (X should still move randomly).




Each time O moves, you should loop through the possible moves (using the open_slots function), and call force_win on each of them, then choose the move that resulted in the lowest board state.  Note that this is a little more complex than the loop within force_win, because you have to keep track of not only the lowest board state you have found, but also what move (i.e. what index in the board) got you that result.




Use the play_games function (also from Homework 5) to test the win rate of your AI.  O should never lose.




<strong>Hints</strong>:

<ul>

 <li>Unlike the previous problem, you will need both a loop AND recursion in this function.</li>

</ul>




<strong>Constraints</strong>:

<ul>

 <li>force_win must use recursion (in addition to a loop).</li>

 <li>You may assume that your function will only be called with valid board states (you won’t be given boards where both X and O have won).</li>

 <li>Don’t use the input() function, as this will break our grading scripts.</li>

 <li>Your submission should have no code outside of function definitions (comments are fine).</li>

 <li>Calling force_win on an empty board will probably take some time, since there are something like 300,000 possible board states to analyze, but it should still run in under a minute on any lab machine.</li>

</ul>




<strong>Examples </strong>(shown below each example is the board it represents, with the optimal move highlighted, if applicable):




&gt;&gt;&gt; force_win([‘O’, ‘X’, ‘O’, ‘X’, ‘X’, ‘O’, ‘X’, ‘O’, ‘X’])

0










&gt;&gt;&gt; force_win([‘X’, ‘X’, ‘O’, ‘O’, ‘X’, ‘X’, ‘O’, ‘X’, ‘O’])

1










&gt;&gt;&gt; force_win([‘X’, ‘-‘, ‘O’, ‘X’, ‘O’, ‘-‘, ‘O’, ‘-‘, ‘X’])

-1










&gt;&gt;&gt; force_win([‘X’, ‘O’, ‘X’, ‘X’, ‘O’, ‘X’, ‘-‘, ‘-‘, ‘O’])

-1







&gt;&gt;&gt; force_win([‘X’, ‘O’, ‘X’, ‘X’, ‘O’, ‘-‘, ‘-‘, ‘X’, ‘O’])

0







&gt;&gt;&gt; force_win([‘X’, ‘O’, ‘X’, ‘X’, ‘O’, ‘-‘, ‘-‘, ‘-‘, ‘O’])

1







<em>(Note: with the next three tests, the upper left corner is only one of multiple optimal moves in each case)</em>

&gt;&gt;&gt; force_win([‘-‘, ‘O’, ‘-‘, ‘-‘, ‘X’, ‘X’, ‘-‘, ‘O’, ‘X’])

1










&gt;&gt;&gt; force_win([‘-‘, ‘O’, ‘-‘, ‘-‘, ‘X’, ‘-‘, ‘-‘, ‘-‘, ‘-‘])

1










&gt;&gt;&gt; force_win([‘-‘, ‘-‘, ‘-‘, ‘-‘, ‘-‘, ‘-‘, ‘-‘, ‘-‘, ‘-‘])

0







<em>(Note: This may take a while: 100 games can take several minutes to complete.  Your number of draws vs. </em>

<em>O wins will vary, but you should have zero X wins) </em>

&gt;&gt;&gt; play_games(1)

X wins: 0

O wins: 1

Draws: 0




&gt;&gt;&gt; play_games(100)

X wins: 0

O wins: 73

Draws: 27


