# Function Name: matrix_subtract()

### Last Mod Date
October 5, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Subtracts a matrix from another matrix.
### Inputs

* X: a matrix of numbers
* Y: a matrix of numbers

### Outputs

* answer: a matrix of numbers, X-Y

### Modules Used
None
### Code

```python
def matrix_subtract(X,Y):
    x_rows=len(X)
    x_cols=len(X[0])
    y_rows=len(Y)
    y_cols=len(Y[0])
    
    if x_rows!=y_rows or x_cols!=y_cols:
        print 'Matrices are different shapes'
        return 0
    answer=[]
    for row in xrange(x_rows):
        temp_row=[0]*x_cols
        for col in xrange(x_cols):
            temp_row[col]=X[row][col]-Y[row][col]
        answer.append(temp_row)
    return answer
```

### Examples
#### Prompt

```python
matrix1=[[-1,2,0],[0,3,6]]
matrix2=[[0,-4,3],[9,-4,-3]]

for x in matrix_subtract(matrix1,matrix2):
    print x
```

#### Output

```
[-1, 6, -3]
[-9, 7, 9]
```
