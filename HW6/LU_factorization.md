# Function Name: LU_factorization

### Last Mod Date
October 24, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
LU-Factorizes a matrix.
### Inputs

* Matrix: a 2-d array of numbers

### Outputs

* A: The factorized matrix
* P: The index list showing the order of the final matrix. The first entry is the current row location of the 0-row.

### Modules Used
None
### Code

```python
def LU_factorization(Matrix):
    A=[[x for x in row] for row in Matrix]
    n=len(A)
    P=list(xrange(n))
    S=[max([abs(y) for y in x]) for x in A]
    print "s"
    print S
    for k in xrange(n-1):
        max_row=0.0
        for i in xrange(k,n):
            r=abs(A[P[i]][k]/float(S[P[i]]))
            if r>max_row:
                max_row=r
                j=i
        ##J should be the row with the max pivot
        print "Max of step {:d} is {:d}".format(k,j)
        P[j],P[k]=(P[k],P[j])
        for i in xrange(k+1,n):
            z=A[P[i]][k]/float(A[P[k]][k])
            A[P[i]][k]=z
            for j in xrange(k+1,n):
                A[P[i]][j]=A[P[i]][j]-z*A[P[k]][j]
    
    return (A,P)
```

### Examples
#### Prompt

```python
matrix=[[4,2,4,7,5,6],[9,8,6,4,3,5],[9,0,9,7,5,3],[5,7,9,8,6,4],[4,5,7,9,0,7],[3,2,4,5,7,8]]
print "Matrix"
for x in matrix:
    print x
    
LU,P=LU_factorization(matrix)
print "LU:"
for x in LU:
    print "|",
    for cell in x:
        print '{:6.3f}'.format(cell),
    print "|"
print "P:"
print P
```

#### Output

```
Matrix
[4, 2, 4, 7, 5, 6]
[9, 8, 6, 4, 3, 5]
[9, 0, 9, 7, 5, 3]
[5, 7, 9, 8, 6, 4]
[4, 5, 7, 9, 0, 7]
[3, 2, 4, 5, 7, 8]
LU:
|  0.444  0.194  0.113  3.876  2.715  4.101 |
|  9.000  8.000  6.000  4.000  3.000  5.000 |
|  1.000 -8.000  3.000  3.000  2.000 -2.000 |
|  0.556 -0.319  6.625  6.736  4.972  0.583 |
|  0.444 -0.181  0.736  0.724 -6.597  1.018 |
|  0.333  0.083  0.264  0.422 -0.511  5.134 |
P:
[1, 2, 3, 0, 4, 5]
```
