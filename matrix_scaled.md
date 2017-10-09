# Function Name: matrix_scaled()

### Last Mod Date
October 5, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Multiplies a matrix by a scalar.
### Inputs

* matrix: a matrix of numbers
* scalar: a scalar number

### Outputs

* a matrix of numbers, matrix*scalar

### Modules Used
None
### Code

```python
def matrix_scaled(matrix,scalar):
    return [[col*scalar for col in row] for row in matrix]
```

### Examples
#### Prompt

```python
test_matrix=[[2,4,6,8],[1,3,5,7]]
print 'original:'
for row in test_matrix:
    print row

print '\n'
print 'original * .5:'
for row in matrix_scaled(test_matrix,.5):
    print row
```

#### Output

```
original:
[2, 4, 6, 8]
[1, 3, 5, 7]


original * .5:
[1.0, 2.0, 3.0, 4.0]
[0.5, 1.5, 2.5, 3.5]
```
