# Exam 1 Problem 4

### Last Mod Date
October 25, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description

Problems 17 and 18 from Chapter 5 were solved using this function.

## Main Function: tri_solve()

### Inputs

* function: Function f(x)
* upper_list: Upper numbers in diagonal matrix A, stored in vector form.
* lower_list: Lower numbers in diagonal matrix A, stored in vector form.
* diagonal_list: Diagonal numbers in diagonal matrix A, stored in vector form.
* b_list: Right hand side vector b.


### Outputs

* Prints number of flops used in the tri_solve, and returns the solution vector [x]

### Modules Used

  * numpy
  * math

### Main Code

```python
def tri_solve(upper_list,lower_list,diagonal_list,b_list):
    upper=[x for x in upper_list]
    lower=[x for x in lower_list]
    diag=[x for x in diagonal_list]
    b=[x for x in b_list]
    n=len(diag)
    x=[0]*n
    flop=0;

    #for a1,b1,c1 syntax: diag[k]=upper[k]=lower[k-1]
    

    #forward sweep
    upper[0]=upper[0]/float(diag[0])
    b[0]=b[0]/float(diag[0])
    flop+=2
    for k in xrange(1,n):
        if(k<n-1):
            upper[k]=upper[k]/float(diag[k]-lower[k-1]*upper[k-1])
        b[k]=(b[k]-lower[k-1]*b[k-1])/float(diag[k]-lower[k-1]*upper[k-1])
        flop+=2
        
    # back sub
    x[n-1]=b[n-1]
    flop+=1
    for k in xrange(n-2,-1,-1):
        x[k]=b[k]-upper[k]*x[k+1]
        flop+=1
    print "Size N={:d} took {:d} flops.".format(n,flop)
    return x
```

### Results

#### 5.17

The full matrix was build and solved using Numpy to make sure the tri_solve was functioning correctly.

##### Prompt

```python
upper=[1,1]
diagonal=[4,4,4]
lower=[2,2]
b=[6,6,6]

for i in xrange(5):
    #visualization
    G=[]
    n=len(diagonal)
    print "\n\nLength {:d}".format(n)
    for row in xrange(n):
        temp_row=[]
        for col in xrange(n+1):
            if col<n:
                if col==row-1:
                    temp_row.append(lower[row-1])
                elif row==col:
                    temp_row.append(diagonal[row])
                elif col==row+1:
                    temp_row.append(upper[row])
                else:
                    temp_row.append(0)
            else:
                temp_row.append(b[row])
        G.append(temp_row)
        
    print "Original matrix:"
    for row in G:
        for col in xrange(n+1):
            if col==0:
                print "|{: 3.0f}".format(row[col]),
            elif col>0 and col<n:
                print "{: 3.0f}".format(row[col]),
            else:
                print "|{: 3.0f}".format(row[col]),
        print "|"

    #Tri_solve
    answer=tri_solve(upper,lower,diagonal,b)

    testmatrix=[x[:-1] for x in G]
    bmatrix=[x[-1] for x in G]
    numpyanswer=np.linalg.solve(np.array(testmatrix),np.array(bmatrix).transpose())

    print "\n{:>3s} | {:>10s} | {:>10s}".format('x','Tri_solve','Numpy')
    for x in xrange(len(answer)):
        print "{:3d} | {:10.6f} | {:10.6f}".format(x,answer[x],numpyanswer[x])
    
    upper.append(1)
    lower.append(2)
    diagonal.append(4)
    b.append(6)
```

##### Results

```
Length 3
Original matrix:
|  4   1   0 |  6 |
|  2   4   1 |  6 |
|  0   2   4 |  6 |
Size N=3 took 9 flops.

  x |  Tri_solve |      Numpy
  0 |   1.375000 |   1.375000
  1 |   0.500000 |   0.500000
  2 |   1.250000 |   1.250000


Length 4
Original matrix:
|  4   1   0   0 |  6 |
|  2   4   1   0 |  6 |
|  0   2   4   1 |  6 |
|  0   0   2   4 |  6 |
Size N=4 took 12 flops.

  x |  Tri_solve |      Numpy
  0 |   1.353659 |   1.353659
  1 |   0.585366 |   0.585366
  2 |   0.951220 |   0.951220
  3 |   1.024390 |   1.024390


Length 5
Original matrix:
|  4   1   0   0   0 |  6 |
|  2   4   1   0   0 |  6 |
|  0   2   4   1   0 |  6 |
|  0   0   2   4   1 |  6 |
|  0   0   0   2   4 |  6 |
Size N=5 took 15 flops.

  x |  Tri_solve |      Numpy
  0 |   1.360714 |   1.360714
  1 |   0.557143 |   0.557143
  2 |   1.050000 |   1.050000
  3 |   0.685714 |   0.685714
  4 |   1.157143 |   1.157143


Length 6
Original matrix:
|  4   1   0   0   0   0 |  6 |
|  2   4   1   0   0   0 |  6 |
|  0   2   4   1   0   0 |  6 |
|  0   0   2   4   1   0 |  6 |
|  0   0   0   2   4   1 |  6 |
|  0   0   0   0   2   4 |  6 |
Size N=6 took 18 flops.

  x |  Tri_solve |      Numpy
  0 |   1.358787 |   1.358787
  1 |   0.564854 |   0.564854
  2 |   1.023013 |   1.023013
  3 |   0.778243 |   0.778243
  4 |   0.841004 |   0.841004
  5 |   1.079498 |   1.079498


Length 7
Original matrix:
|  4   1   0   0   0   0   0 |  6 |
|  2   4   1   0   0   0   0 |  6 |
|  0   2   4   1   0   0   0 |  6 |
|  0   0   2   4   1   0   0 |  6 |
|  0   0   0   2   4   1   0 |  6 |
|  0   0   0   0   2   4   1 |  6 |
|  0   0   0   0   0   2   4 |  6 |
Size N=7 took 21 flops.

  x |  Tri_solve |      Numpy
  0 |   1.359375 |   1.359375
  1 |   0.562500 |   0.562500
  2 |   1.031250 |   1.031250
  3 |   0.750000 |   0.750000
  4 |   0.937500 |   0.937500
  5 |   0.750000 |   0.750000
  6 |   1.125000 |   1.125000
```

#### 5.18

##### Prompt

```python
factor=1/(.01**2)
upper_temp=[-1.0*factor]*99
lower_temp=[-1.0*factor]*98
lower_temp.append(-2.0*factor)
diagonal_temp=[2.0*factor]*100

gt=lambda x: (math.pi/2.0)**2*math.sin(math.pi/2.0*(.01*x))
ut=lambda x: math.sin(math.pi/2.0*x*.01)

##g(ih) and u(ih) based on i(0)=1, python starts at i(0)=0.
g_t=[gt(x) for x in xrange(1,101)]
u_t=[ut(x) for x in xrange(1,101)]



v_answer=tri_solve(upper_temp,lower_temp,diagonal_temp,g_t)

difference=[]
##abs(v-u)
for i in xrange(100):
    difference.append(abs(v_answer[i]-u_t[i]))
###inf norm of ||v-u||
print max(difference)
```

##### Results

```
Size N=100 took 300 flops.
2.05619295255e-05
```
