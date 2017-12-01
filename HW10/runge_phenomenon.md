# Runge Phenomenon

### Last Mod Date
November 30, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Using [difference_coefficients()](https://swiser.github.io/MATH4610/HW10/difference_coefficients) and [generate_from_coeff()](https://swiser.github.io/MATH4610/HW10/generate_from_coeff), show that for a Runge function, increasing the points used to interpolate the Runge function increases error to infinity.

### Code

```python
import numpy as np
import matplotlib.pyplot as plt

# divide interval -1<x<1 equally by N points
N=16
X=np.arange(-1,(1+2.0/N),2.0/N)

# Runge function
function=lambda x: 1/float(1+25*x*x)
xvals=np.arange(-1,1.01,.01)
yvals=[function(i) for i in xvals]
Y=[function(i) for i in X]

# Interpolate using n points
coeff=difference_coefficients(X,Y)
y_test=generate_from_coeff(coeff,X,xvals)


fig1=plt.figure(1,figsize=(11,7))
fig1.suptitle("Runge Function vs Interpolation Approximation, {!s} points".format(N))
plt.xlabel('x')
plt.ylabel('y')
plt.axhline(0,color='gray',linewidth=1)
plt.axvline(0,color='gray',linewidth=1)

# Plot Runge Function
plt.plot(xvals,yvals,'-b',label="Runge Function")
# Plot X,Y values used for interpolation
plt.plot(X,Y,'ko',markersize=10,label="Known Values")
# Plot interpolation function
plt.plot(xvals,y_test,'-r',markersize=5,label="Interpolated Values")
         
plt.legend(loc='best')

plt.show()
```

#### Output(s)

Using 2,5,10, and 50 points, the Runge function was interpolated.

![Runge Phenomenon](https://swiser.github.io/MATH4610/HW10/runge_phenomenon.png)


