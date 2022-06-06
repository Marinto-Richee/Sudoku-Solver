# Sudoku Solver
## Aim:
To develop a code to solve a given sudoku puzzle.

## Theory:
We create apython program to solve a given sudoku puzzle by using Elimination and Only Choice strategies.<br>
Firstly, we form the puzzle itself, either by getting data in String form or by indexes and values, from the user.<br>
Then we fill the empty boxes with all the possible values, 1-9. We iteratively apply Elimination and Only Choice Strategies to finally end up with a result.

## Design Steps

### Step 1:
We define the puzzle. We initialize those boxes with only one value, with the data provided by the user, either in String format or in the Index & value format.
### Step 2:
We identify the Row units, Column units, and the square units. And then we form a unit list using the prior data. 
### Step 3:
Two Dictionaries with units and peers of each boxes is defined.
### Step 4:
We reduce the puzzle using the two strategies. 
### Step 5:
Search function is defined to find the final solution to a given sudoku puzzle.

## Program:
```
/*
Name: Marinto Richee J
Reg. No: 212220230031
*/
```

## Output:
![image](https://user-images.githubusercontent.com/65499285/172172856-c403b65d-2d3c-4e1c-9f9d-35e15da0a945.png)

## Result:
Hence a python program has been developed to solve a given sudoku puzzle.
