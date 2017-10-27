# Exam 1 Problem 3

### Last Mod Date
October 25, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description

Problem 2 from Chapter 5 was solved using this function. 

## Main Function: gauss_jordan()

### Inputs

* A: Matrix A of input coefficients
* B: Right hand vector of solutions


### Outputs

* Prints augmented orginial matrix, then prints out solved augmentedmatrix along with the number of floating point operations used to solve. Returns solved augmented matrix.

### Code

```python
def gauss_jordan(A,B):
    flop=0;
    rows=len(b)
    cols=len(A[0])
    
    G=[]
    for row in xrange(rows):
        temp_row=[x for x in A[row]]
        temp_row.append(B[row])
        G.append(temp_row)
    print "Augmented Matrix:"
    for p in G:
        print "|",
        for cell in xrange(cols+1):
            if cell==cols:
                print "|{: 3.0f}".format(p[cell]),
            else:
                print "{: 3.0f} ".format(p[cell]),
        print "|"
        
    for k in xrange(cols):

        divisor=G[k][k]        
        for col in xrange(cols+1):
            flop+=1
            if col<k:
                G[k][col]=0.0               
            else:
                G[k][col]=G[k][col]/float(divisor)

        for row in xrange(rows):
            if row!=k:
                multiplier=G[row][k]/float(G[k][k])
                for col in xrange(cols+1):
                    flop+=1
                    if col<k and col!=row:
                        G[row][col]=0.0
                    else:
                        G[row][col]-=multiplier*G[k][col]

    print "Solved Matrix:"
    for p in G:
        print "|",
        for cell in xrange(cols+1):
            if cell==cols:
                print "|{: 3.0f}".format(p[cell]),
            else:
                print "{: 3.0f} ".format(p[cell]),
        print "|"
    print "\n",
    print "N={:d}, {:d} flops".format(rows,flop)
    print "n^3+n^2={:d}\n".format(rows**3+rows**2)
    return G
```

### Results

Note: dummy variable "test" was used to store the function output.

##### Prompt

```python
matrix=[[3,-5],[2,7]]
b=[13,81]
test=gauss_jordan(matrix,b)

matrix=[[1,1,1],[2,3,5],[4,0,5]]
b=[5,8,2]
test=gauss_jordan(matrix,b)

matrix=[[3,3,12,21],[2,4,10,14],[-2,0,-8,-18],[3,0,11,28]]
b=[18,16,-10,11]
test=gauss_jordan(matrix,b)
```

##### Results

```
Augmented Matrix:
|   3   -5  | 13 |
|   2    7  | 81 |
Solved Matrix:
|   1    0  | 16 |
|   0    1  |  7 |

N=2, 12 flops
n^3+n^2=12

Augmented Matrix:
|   1    1    1  |  5 |
|   2    3    5  |  8 |
|   4    0    5  |  2 |
Solved Matrix:
|   1    0    0  |  3 |
|   0    1    0  |  4 |
|   0    0    1  | -2 |

N=3, 36 flops
n^3+n^2=36

Augmented Matrix:
|   3    3   12   21  | 18 |
|   2    4   10   14  | 16 |
|  -2    0   -8  -18  |-10 |
|   3    0   11   28  | 11 |
Solved Matrix:
|   1    0    0    0  |  2 |
|   0    1    0    0  | -1 |
|   0    0    1    0  |  3 |
|   0    0    0    1  | -1 |

N=4, 80 flops
n^3+n^2=80
```
