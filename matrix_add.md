# Function Name: matrix_add()

### Last Mod Date
October 5, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Adds two matrices together.
### Inputs

* X: a matrix of numbers
* Y: a matrix of numbers

### Outputs

* answer: a matrix of numbers, X+Y

### Modules Used
None
### Code

```python
def matrix_add(X,Y):
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
            temp_row[col]=X[row][col]+Y[row][col]
        answer.append(temp_row)
    return answer
```

### Examples
#### Prompt

```python
matrix1=[[0,1,2],[9,8,7]]
matrix2=[[6,5,4],[3,4,5]]

for x in matrix_add(matrix1,matrix2):
    print x
```

#### Output

```
[6, 6, 6]
[12, 12, 12]
```
