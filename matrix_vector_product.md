# Function Name: matrix_vector_product()

### Last Mod Date
October 5, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Multiplies a matrix and a vector together.
### Inputs

* matrix: a matrix of numbers
* vector: a list of numbers

### Outputs

* answer: a vector of numbers, matrix*vector

### Modules Used
None
### Notes
Multiplying a matrix by a vector, by using lists, is equivalent to multiplying a matrix by a matrix, where one matrix is either nx1 or 1xn. If you run into issues of needing a vector*matrix, use [matrix_matrix_product()](https://swiser.github.io/MATH4610/matrix_matrix_product), it is equivalent in that case.
### Code

```python
def matrix_vector_product(matrix,vector):
    matrix_rows=len(matrix)
    matrix_cols=len(matrix[0])
    vector_rows=len(vector)
    if matrix_cols != vector_rows:
        print "Shape mismatch."
        return 0
    answer=[]
    for row in xrange(matrix_rows):
        temp_cell=0;
        for col in xrange(matrix_cols):
            temp_cell+=matrix[row][col]*vector[col][0]
        answer.append([temp_cell])
    return answer;
```

### Examples
#### Prompt

```python
matrixA=[[1,-1,2],[0,-3,1]]
vectorA=[[2],[1],[0]]
print 'Matrix*vector:'
for x in matrix_vector_product(matrixA,vectorA):
    print x
```

#### Output

```
Matrix*vector:
[1]
[-3]
```
