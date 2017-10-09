# Function Name: inf_norm_matrix()

### Last Mod Date
October 5, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Calculates the ∞-Norm of a matrix.
### Inputs

* matrix: A matrix of numbers

### Outputs

* ∞-Norm

### Modules Used
None
### Code

```python
def inf_norm_matrix(matrix):
    norm=0
    for row in matrix:
        row_sum=sum([abs(x) for x in row])
        if row_sum>norm:
            norm=row_sum
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
    
print 'inf norm matrix: ' ,inf_norm_matrix(matrix)
```

#### Output

```
[5, -4, 2]
[-1, 2, 3]
[-2, 1, 0]
inf norm matrix:  11
```
