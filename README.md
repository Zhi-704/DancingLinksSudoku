# DancingLinksSudoku
Uses Algorithm X/Dancing Links technique to solve sudoku puzzles. Accepts a 9x9 np array as input.

General description lifted from report:

The algorithm that was implemented to solve the set of sudoku puzzles was based on the 
work of Donald Knuth’s Algorithm X and its implementation of circular doubly linked lists
known as the Dancing Links technique (Knuth, 2000). To extend the algorithm to solve a
sudoku puzzle would first require converting the puzzle into an exact cover matrix, then
creating a circular doubly linked list for each ‘1’ in the matrix, and finally doing a recursive
backtracking search on the linked lists (Knuth, 2000). Additional steps may involve converting
the final solution line of 1s back into a 9x9 solved sudoku numpy array.
To convert the sudoku puzzle into an exact cover matrix requires prior understanding of the
exact cover problem. An exact cover matrix is a binary matrix where each row would contain
a varying amount of singular 1s in some number of columns. To solve this matrix, there must
be some subset of rows where the concatenation of these rows would lead to exactly one 1
in every column of the matrix. This property allows the sudoku puzzle to be converted into an
exact cover problem where its constraints (cell, row, column, and box) can be represented as
columns of 1s. This would then allow it to be solved by Algorithm X, which is a brute-force
depth-first backtracking search that solves exact cover problems. It works by following 6
steps:
1. Choose a column in the matrix with an optional heuristic where this column would
contain the lowest number of 1s.
2. Choose a row that has a 1 in that column non-deterministically and include it into the
partial solution.
3. Remove every column from the matrix where the row has a 1 element in, including
the initial chosen column.
4. Remove every row from the matrix where the rows had a 1 element in any of the
removed columns.
5. Repeat steps 1-4 on the reduced matrix until the matrix has no more columns,
meaning that the partial solution is a correct solution.
6. If no solution can be found at one level, the algorithm backtracks by one level and
chooses a different row at step 2.
However, doing a naïve brute-force search using Algorithm X on the binary matrix will lead to
O(n) time complexity (Harrysson and Laestander, 2014) as it would search through every
element in a column and row, including the 0s. To quicken the search speed, Knuth proposed
using a circular doubly linked list to store only the 1s in nodes to improve search time to O(1)
(Knuth, 2000) as well as creating special nodes called ‘header nodes’ for each column. These
header nodes will then track how many 1s their respective columns have so that searching
for a column with the lowest number of nodes in step 1 would take O(n) complexity rather
than O(nm) complexity.

References:
Knuth, D.E., 2000. Dancing links [Online]. arXiv.org. Available from:
https://arxiv.org/abs/cs/0011047 [Accessed 9 March 2023].
Harrysson, M. and Laestander, H., 2014. Solving Sudoku efficiently with Dancing Links [Online].
www.semanticscholar.org. Available from: https://www.semanticscholar.org/paper/SolvingSudoku-efficiently-with-Dancing-Links-HarryssonLaestander/5f59ccf7aeb1357ad3cf976555e32654f682dbed [Accessed 10 March 2023].
