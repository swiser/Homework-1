# Function Name: quick_newton_method()

### Last Mod Date
October 2, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Newton-Raphson method with no built-in checks, will attempt to find a root of a function.
### Inputs

* function: function *f(x)*
* derivative: derivative of function; *f'(x)*
* x0: initial x-value guess of root
* tolerance: smallest variation between x-values while iterating
* max_iters: maximum iterations to perform before returning

### Outputs

* Root of function

### Modules Used
None
### Code

```python
def quick_newton_method(function,derivative,x0,tolerance,max_iters):
    error=tolerance*10
    count=0
    x_old=x0
    while error>tolerance and count<max_iters:
        x_new=x_old-function(x_old)/float(derivative(x_old))
        error=abs(x_new-x_old)
        x_old=x_new
        count+=1
    return x_old
```

### Example
#### Prompt

```python
function=lambda x: 3*x*math.cos(10*x)
derivative=lambda x: (3*math.cos(10*x)-30*x*math.sin(10*x))

print 'Quick Newton Method: {}'.format(quick_newton_method(function,derivative,.2,10**-10,15))
```

#### Output

```
Quick Newton Method: 0.157079632679
```
