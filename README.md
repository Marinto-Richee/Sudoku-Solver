# Sudoku Solver
## AIM
To develop a code to solve a given sudoku puzzle.

## THEORY
We create apython program to solve a given sudoku puzzle by using Elimination and Only Choice strategies.<br>
Firstly, we form the puzzle itself, either by getting data in String form or by indexes and values, from the user.<br>
Then we fill the empty boxes with all the possible values, 1-9. We iteratively apply Elimination and Only Choice Strategies to finally end up with a result.

## DESIGN STEPS

### STEP 1:
We define the puzzle. We initialize those boxes with only one value, with the data provided by the user, either in String format or in the Index & value format.
### STEP 2:
We identify the Row units, Column units, and the square units. And then we form a unit list using the prior data. 
### STEP 3:
Two Dictionaries with units and peers of each boxes is defined.
### STEP 4:
We reduce the puzzle using the two strategies. 
### STEP 5:
Search function is defined to find the final solution to a given sudoku puzzle.

## PROGRAM
```python
def cross(x,y):
    return[s+b for s in x for b in y]
    
rows="ABCDEFGHI"
columns="123456789"
boxes=cross(rows,columns)

def input_dict():
    sudoku=dict().fromkeys(boxes,'123456789')
    no_of_predefined_values=int(input("Enter the number of index with predefined values: "))
    for i in range(1,no_of_predefined_values+1):
        index_=str(input("Enter the index: ")).capitalize()
        if index_[0] in rows and index_[1] in columns and len(index_)==2:
            pass
        else:
            print("Invalid Index!")
            break
        value_=(input("Enter the value: "))
        if value_.isnumeric() and len(str(value_))==1:
            str(value_)
        else:
            print("Invalid input!")
            break
        sudoku[index_]=value_
    return sudoku
def grid_values(grid):
    values = []
    all_digits = '123456789'
    for c in grid:
        if c == '.':
            values.append(all_digits)
        elif c in all_digits:
            values.append(c)
    assert len(values) == 81
    boxes = cross(rows, columns)
    return dict(zip(boxes, values))

Choice=int(input("1)Index: Values\n 2)String format\n3) Default Puzzle"))
if Choice==1:
    sudoku=input_dict()
elif Choice==2:
    String=input("Enter the String:")
    sudoku=grid_values(String)
elif Choice==3:
    sudoku=grid_values("...5....6...87.3.227.3...81....349..793.5.614..879....92...3.575.6.87...3....5...")
else:
    print("Invalid Input!!")
    
row_units=[cross(r,columns) for r in rows]
column_units=[cross(rows,c) for c in columns]
square_units=[cross(rs,cs) for rs in ('ABC','DEF','GHI') for cs in ('123','456','789')]
unitlist =row_units+column_units+square_units
units=dict((s,[u for u in unitlist if s in u])for s in boxes)
peers=dict((s, set(sum(units[s],[])) - set([s]))for s in boxes)

def display(sudoku_dict):
    width=1+max(len(sudoku_dict[s]) for s in boxes)
    line='+'.join(['-'*(width*3)]*3)
    for r in rows:
        print(''.join(sudoku_dict[r+c].center(width)+("|" if c in '36' else '')for c in columns))
        if r in 'CF': print(line)
    return
    
def eliminate(values):
    solved_values=[box for box in values.keys() if len(values[box]) == 1]
    for box in solved_values:
        digit=values[box]
        for peer in peers[box]:
            values[peer]=values[peer].replace(digit, '')
    return values           

def onlychoice(values):
    for unit in unitlist:
        for digit in columns:
            dplace=[box for box in unit if digit in values[box]]
            if len(dplace)==1:
                values[dplace[0]]=digit
    return values
    
                                                                                                                                                       
def reduce_puzzle(values):
    stalled=False
    while not stalled:
        solved_values_before= len([box for box in values.keys() if len(values[box])==1])
        eliminate(values)
        onlychoice(values)
        solved_values_after=len([box for box in values.keys() if len(values[box])==1])
        stalled=solved_values_before==solved_values_after
        if len([box for box in values.keys() if len(values[box])==0]):
            return False
    return values

def search(values):
    values_reduced=reduce_puzzle(values)
    if not values_reduced:
        return False
    else:
        values=values_reduced
    if len([b1 for b1 in boxes if len(values[b1])==1 ])==81:
        return values
    possibility_count_list= [(len(values[b1]),b1) for b1 in boxes if len(values[b1])>1]
    possibility_count_list.sort()
    for (_,t_box_min) in possibility_count_list:
        for i_digit in values[t_box_min]:
            new_values=values.copy()
            new_values[t_box_min]=i_digit
            new_values=search(new_values)
            if new_values:
                return new_values
    return False
    
print("\n\tSudoku before Solving\n")
display(sudoku)
result=search(sudoku)
if result:
    print("\n\nSudoku after Solving\n")
    display(result)
else:
    print("Failed!!")    

```
## OUTPUT
![image](https://user-images.githubusercontent.com/65499285/172666345-c07447c6-7c4e-4db1-8f3e-4cba96d4b750.png)

## RESULT
Hence a python program has been developed to solve a given sudoku puzzle.
