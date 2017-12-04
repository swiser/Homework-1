# Function Name: LU_solve()

### Last Mod Date
October 24, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Solves Ax=b for x using an LU-Factorized matrix A.
### Inputs

* A: The factorized matrix
* P: The index list showing the order of the matrix. The first entry is the current row location of the 0-row.
* b: The vector of solutions in the form A*x=b

### Outputs

* x: The vector x from solving A*x=b

### Modules Used
None
### Code

```python
def LU_solve(A,P,b):
    ## assumes that matrix A is an LU-decomposed matrix
    ## P is permutation list
    n=len(b)
    y=[b[P[i]] for i in xrange(n)]
    x=[b[P[i]] for i in xrange(n)]
    
    ### Forward Substitution of L to Y
    for k in xrange(n):
        total=0.0
        for i in xrange(k):
            total+=A[P[k]][i]*y[i]
        y[k]=(y[k]-total)
        
    ### Back Substitution of U to X
    for k in xrange(n-1,-1,-1):
        total=y[k]
        for i in xrange(k+1,n):
            total-=x[i]*A[P[k]][i]
        x[k]=total/float(A[P[k]][k])
        
    return x
```

### Examples
#### Prompt

```python
import numpy as np
import scipy.linalg as linalg

matrix=[[4,2,4,7,5,6],[9,8,6,4,3,5],[9,0,9,7,5,3],[5,7,9,8,6,4],[4,5,7,9,0,7],[3,2,4,5,7,8]]
b=[7,7,3,3,5,0]

print "Matrix"
for x in matrix:
    print x
    
LU,P=LU_factorization(matrix)

numpy_test=linalg.lu_solve(linalg.lu_factor(np.array(matrix)),np.array(b).transpose())
my_answer=LU_solve(LU,P,b)

print "\n",
print "My answer:"
for l in answer:
    print l
print "\n",
print "Their answer:"
for x in numpy_test:
    print x

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

My answer:
1.34259436674
0.579740691065
-2.36756722233
2.07044772306
0.00319345979434
-0.761448553363

Their answer:
1.34259436674
0.579740691065
-2.36756722233
2.07044772306
0.00319345979434
-0.761448553363
```
