# Function Name: generate_from_coeff()

### Last Mod Date
November 30, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Using coefficents from a divided difference table, interpolate all points across a set of new x values, using the Newton form of the interpolating polynomial and taking advantage of nested polynomial calculations.
### Inputs

* coeff: list of coefficients
* x_coeff: x values that were used to generate coefficients
* x_new: list of x values to interpolate f(x) values for

### Outputs

* y: list of interpolated f(x) values for every x in x_new

### Code

```python
def generate_from_coeff(coeff,x_coeff,x_new):
    # Given list of coefficients and the x values used to generate them,
    # generate a f(x) value for each x value in x_new and store in y[]
    y=[]
    for k in xrange(len(x_new)):
        # initialize y_temp as the last coefficient for nested polynomial
        y_temp=coeff[len(coeff)-1]
        for i in xrange(len(x_coeff)-2,-1,-1):
            # nested polynomial form, work from inside to outside
            y_temp=coeff[i]+y_temp*(x_new[k]-x_coeff[i])
        y.append(y_temp)
    return y
```

### Example
#### Prompt

```python
import numpy as np
import matplotlib.pyplot as plt

ig1=plt.figure(1,figsize=(11,7))

# Create y=sin(x) curve and plot in blue, using 0<x<10 (inclusive) with .1 step size
xvals=np.arange(0,10.1,.1)
yvals=np.sin(xvals)
plt.plot(xvals,yvals,'-b',label="y=sin(x)")

## Given X and Y values for y=sin(x), using N points
N=4
X=np.arange(0,10.1,(10)/float(N-1))
Y=np.sin(X)

# Plot the points used to generate interpolation curve
plt.plot(X,Y,'ko',markersize=10,label="Known Values")

# Generate coefficients using given points, and interpolate values for y=f(x) using
# the same xvals from the y=sin(x) curve
coeff=difference_coefficients(X,Y)
y_interpolated=generate_from_coeff(coeff,X,xvals)
plt.plot(xvals,y_interpolated,'-r',markersize=5,label="Interpolated Values")

# Display Graph
fig1.suptitle("Interpolating y=sin(x) using {!s} points".format(N))
plt.xlabel('x')
plt.ylabel('y')
plt.legend(loc='best')
plt.show()
```
#### Output(s)

Using 2,4,8, and 12 points, y=sin(x) was interpolated.

![Interpolation Comparison](https://swiser.github.io/MATH4610/HW10/Interpolation.png)


