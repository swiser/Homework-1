# Function Name: one_norm_matrix()

### Last Mod Date
October 5, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Calculates the 1-Norm of a matrix.
### Inputs

* matrix: A matrix of numbers

### Outputs

* 1-Norm

### Modules Used
None
### Code

```python
def one_norm_matrix(matrix):
    norm=0
    for column in range(len(matrix)):
        col_sum=sum([abs(i[column]) for i in matrix])
        if col_sum>norm:
            norm=col_sum
    return norm
```

### Examples
#### Prompt

```python
matrix=[]
matrix.append([5,-4,2])
matrix.append([-1,2,3])
matrix.append([-2,1,0])

print 'matrix: '
for x in matrix:
    print x
    
print 'one norm matrix: ' ,one_norm_matrix(matrix)
```

#### Output

```
[5, -4, 2]
[-1, 2, 3]
[-2, 1, 0]
one norm matrix:  8
```
