# Exam 1 Problem 2

### Last Mod Date
October 25, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description

Problems 5 and 7 from Chapter 4 were solved using these functions. The proof that A is diagonal/positive for problem 7 was done by hand.

### Pseudocode, using Numpy

#### 4.5 Prompt

```python
A=np.array([[2,-1,0],[-1,2,-1],[0,-1,2]])
print "Original Matrix, nonsingular S.P.D:"
print A
print "Inverse of Matrix:"
print np.linalg.inv(A)
print "1-norm, A:",
print np.linalg.norm(A,1)
print "1-norm, A^-1:",
print np.linalg.norm(np.linalg.inv(A))
print "Inverse of (1-Norm of A):",
print np.linalg.norm(A)**-1
print "\nProblem 4.5 is deemed false based on these tests."
```
#### 4.5 Results

```
Original Matrix, nonsingular S.P.D:
[[ 2 -1  0]
 [-1  2 -1]
 [ 0 -1  2]]
Inverse of Matrix:
[[ 0.75  0.5   0.25]
 [ 0.5   1.    0.5 ]
 [ 0.25  0.5   0.75]]
1-norm, A: 4.0
1-norm, A^-1: 1.80277563773
Inverse of (1-Norm of A): 0.25

Problem 4.5 is deemed false based on these tests.
```

#### 4.5 Prompt

```python
x=np.array([[1,2,3],[4,5,6],[7,8,9]])
A=np.array([[2,0,0],[0,3,0],[0,0,4]])

print "Matrix A:"
print A

print "Matrix x:"
print x

print "\nsqrt(x_transpose*A*x):"
print (np.matrix.transpose(x)*A*x)**.5
```
#### 4.5 Results

The resultant matrix is a diagonal matrix, which can easily be represented (and considered) as a vector.

```
Matrix A:
[[2 0 0]
 [0 3 0]
 [0 0 4]]
Matrix x:
[[1 2 3]
 [4 5 6]
 [7 8 9]]

sqrt(x_transpose*A*x):
[[  1.41421356   0.           0.        ]
 [  0.           8.66025404   0.        ]
 [  0.           0.          18.        ]]
```
