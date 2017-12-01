# Function Name: difference_coefficients()

### Last Mod Date
November 30, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
A function that computes the coefficients in a divided difference table, to be used in the Newton form of the interpolating polynomial.
### Inputs

* x: x values to generate coefficients
* y: f(x) values to generate coefficients

### Outputs

* coeff: a list of coefficients to use in the Newton form of the interpolating polynomial.

### Code

```python
def difference_coefficients(x,y):
    n=len(x)
    #initialize coefficient list as f(x)
    coeff=[float(j) for j in y]
    for k in xrange(n):
        for i in xrange(n-1,k,-1):
            #work from bottom up, write new coefficients over themselves
            coeff[i]=(coeff[i]-coeff[i-1])/float(x[i]-x[i-(k+1)])
    return coeff
```

### Example
#### Prompt

```python
import numpy as np
## Given X and Y values for y=sin(x), using N points
N=4
X=np.arange(0,10.1,(10)/float(N-1))
Y=np.sin(X)
coeff=difference_coefficients(X,Y)
print coeff
```

#### Output

```
[0.0, -0.05717038886264561, 0.033987922034498574, -0.010071804110532686]
```
