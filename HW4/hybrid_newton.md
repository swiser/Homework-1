# Function Name: hybrid_newton()

### Last Mod Date
October 2, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Hybrid method that uses both bisection method and Newton-Raphson method to find a root of a function.
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

### Modules Used

* math

### Code

```python
def hybrid_newton(x_0,a,b,tolerance,function,derivative,max_iters):
    print 'iteration {:3d}: x={:13.8f} method: {}'.format(0,x_0,'N/A')
    if (abs(function(x_0)<tolerance)):
        return x_0
    x,a,b=bisection_step(a,b,function)
    print 'iteration {:3d}: x={:13.8f} method: {}'.format(1,x,'Bisection')
    cnt=2;
    while abs(function(x))>tolerance and cnt<max_iters:
        x_newton=newton_step(x,function,derivative)
        if(abs(function(x_newton))<abs(function(x))):
            x=x_newton
            print 'iteration {:3d}: x={:13.8f} method: {}'.format(cnt,x,'Newton')
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
print 'Newton Hybrid:'
hybrid_newton(1.57079632679,.1,3.15,10**-10,function,derivative,40)
print 'Newton-Raphson:'
quick_newton_method(function,derivative,1.57079632679,10**-10,40)
```

#### Output

```
Newton Hybrid:
iteration   0: x=   1.57079633 method: N/A
iteration   1: x=   3.05468750 method: Bisection
iteration   2: x=   3.14181210 method: Newton
iteration   3: x=   3.14159265 method: Newton
Newton-Raphson:
iteration   0: x=-204223803254.40252686
iteration   1: x=-204223803254.62695312
iteration   2: x=-204223803254.62329102
iteration   3: x=-204223803254.62329102
```
