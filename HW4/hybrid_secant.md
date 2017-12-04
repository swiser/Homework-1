# Function Name: hybrid_secant()

### Last Mod Date
October 2, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Hybrid method that uses both bisection method and a secant approximation of Newton-Raphson method to find a root of a function.
### Inputs

* x_0: First guess near root
* a: Left bound of bisection step
* b: Right bound of bisection step
* tolerance: Largest variation from f(x)=0
* function: Function, f(x)=0
* derivative: Derivative of given function
* max_iters: Maximum iterations before exiting function


### Outputs

* Root of function

### Notes

Because bisection_step redefines the a,b bounds of the root, the built in secant method uses x as x0 in secant_step, and (a+b)/4 as the distance from x0 to the x1 that secant_step needs. This should guarantee that both x0 and x1 always are within bounds of the root, and will adjust in distance as is appropriate with the tolerance.

### Modules Used

* math

### Code

```python
def hybrid_secant(x_0,a,b,tolerance,function,max_iters):
    print 'iteration {:3d}: x={:13.8f} method: {}'.format(0,x_0,'N/A')
    if (abs(function(x_0)<tolerance)):
        return x_0
    x,a,b=bisection_step(a,b,function)
    print 'iteration {:3d}: x={:13.8f} method: {}'.format(1,x,'Bisection')
    cnt=2;
    while abs(function(x))>tolerance and cnt<max_iters:
        x_secant=secant_step(x,x+(a+b)/4.0,function)
        if(abs(function(x_secant))<abs(function(x))):
            x=x_secant
            print 'iteration {:3d}: x={:13.8f} method: {}'.format(cnt,x,'Secant')
        else:
            x,a,b=bisection_step(a,b,function)
            print 'iteration {:3d}: x={:13.8f} method: {}'.format(cnt,x,'Bisection')
        cnt+=1
    return x
```

### Examples
#### Prompt

```python
function= math.sin
derivative=math.cos
print 'Secant Hybrid:'
hybrid_secant(1.57079632679,.1,3.15,10**-10,function,40)
```

#### Output

```
Secant Hybrid:
iteration   0: x=   1.57079633 method: N/A
iteration   1: x=   3.05468750 method: Bisection
iteration   2: x=   3.17762698 method: Secant
iteration   3: x=   3.12054401 method: Secant
iteration   4: x=   3.15209176 method: Secant
iteration   5: x=   3.13587727 method: Secant
iteration   6: x=   3.14456741 method: Secant
iteration   7: x=   3.14000664 method: Secant
iteration   8: x=   3.14242764 method: Secant
iteration   9: x=   3.14115010 method: Secant
iteration  10: x=   3.14182638 method: Secant
iteration  11: x=   3.14146898 method: Secant
iteration  12: x=   3.14165803 method: Secant
iteration  13: x=   3.14155808 method: Secant
iteration  14: x=   3.14161093 method: Secant
iteration  15: x=   3.14158299 method: Secant
iteration  16: x=   3.14159777 method: Secant
iteration  17: x=   3.14158995 method: Secant
iteration  18: x=   3.14159408 method: Secant
iteration  19: x=   3.14159190 method: Secant
iteration  20: x=   3.14159305 method: Secant
iteration  21: x=   3.14159244 method: Secant
iteration  22: x=   3.14159277 method: Secant
iteration  23: x=   3.14159259 method: Secant
iteration  24: x=   3.14159268 method: Secant
iteration  25: x=   3.14159264 method: Secant
iteration  26: x=   3.14159266 method: Secant
iteration  27: x=   3.14159265 method: Secant
iteration  28: x=   3.14159266 method: Secant
iteration  29: x=   3.14159265 method: Secant
iteration  30: x=   3.14159265 method: Secant
iteration  31: x=   3.14159265 method: Secant
iteration  32: x=   3.14159265 method: Secant
iteration  33: x=   3.14159265 method: Secant
iteration  34: x=   3.14159265 method: Secant
```
