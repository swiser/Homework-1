# Step Functions

### Last Mod Date
October 2, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Step functions to be used in hybrid methods. See hybrid methods for use.
### Inputs

* x0: First guess near root
* x1: Second guess near x0
* function: Function, f(x)=0
* derivative: Derivative of given function
* a: Left bound of bisection step
* b: Right bound of bisection step

### Outputs

* newton_step: Next x value using Newton-Raphson method
* secant_step: Next x value using secant approximation of Newton-Raphson method
* bisection_step: A list containing a midpoint between the new bounds, the left bound, and the right bound.

### Modules Used
None
### Code

```python
def newton_step(x0,function,derivative):
    return x0-function(x0)/float(derivative(x0))
def secant_step(x1,x0,function):
    fx0=function(x0)
    fx1=function(x1)
    return x1-(fx1*(x1-x0))/float(fx1-fx0)
def bisection_step(a,b,function):
    cnt=0
    fa=function(a)
    fb=function(b)
    while cnt<4:
        c=(a+b)/2.0
        fc=function(c)
        if fa*fc>0:
            a=c
            fa=fc
        else:
            b=c
            fb=fc
        cnt+=1
    return ((a+b)/2.0,a,b)
```
