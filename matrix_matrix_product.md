# Function Name: matrix_matrix_product()

### Last Mod Date
October 5, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Multiplies a matrix and a matrix together.
### Inputs

* X: a matrix of numbers
* Y: a matrix of numbers

### Outputs

* answer: a matrix of numbers, X*Y

### Modules Used
None
### Code

```python
def matrix_matrix_product(X,Y):
    x_rows=len(X)
    x_cols=len(X[0])
    y_rows=len(Y)
    y_cols=len(Y[0])
    if x_cols!=y_rows:
        print "Shape mismatch."
        return 0
    answer=[]
    ##Count down the rows of X
    for rowA in xrange(x_rows):
        temp_row=[]
        ##Count accross columns of Y
        for colB in xrange(y_cols):
            temp_cell=0
            ##Multiply individual cells, iterate X column and Y row
            for colA in xrange(x_cols):
                temp_cell+=X[rowA][colA]*Y[colA][colB]
            temp_row.append(temp_cell)
        answer.append(temp_row)
    return answer;
```

### Examples
#### Prompt

```python
matrixA=[[0,4,-2],[-4,-3,0]]
matrixB=[[0,1],[1,-1],[2,3]]
print '\n'
print 'Matrix*matrix:'
test=matrix_matrix_product(matrixA,matrixB)
for x in test:
    print x
```

#### Output

```
Matrix*matrix:
[0, -10]
[-3, -1]
```
