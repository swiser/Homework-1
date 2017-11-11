# Function Name: secant_method()

### Last Mod Date
October 2, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Secant variant of Newton-Raphson method with built in print and safety checks. Will attempt to find a root of a function by approximating the derivative using two x-values.
### Inputs

* function: function *f(x)*
* x0: initial x-value guess near root
* x1: second x-value guess near root
* tolerance: smallest variation between x-values while iterating
* max_iters: maximum iterations to perform before returning
* print_it: boolean that turns on/off printing of each iteration

### Outputs

* Root of function

### Modules Used
None
### Code

```python
def secant_method(function,x0,x1,tolerance,max_iters,print_it):
    error=tolerance*10
    count=0
    x_0=x0
    x_1=x1
    if(print_it):
        print 'initial guess: x0={:13.8f} error= N/A'.format(x0)
        print 'initial guess: x1={:13.8f} error= N/A'.format(x1)
    while error>tolerance and count<max_iters:
        f_x0=function(x_0)
        f_x1=function(x_1)
        x_new=x_1-(f_x1*(x_1-x_0))/float(f_x1-f_x0)
        error=abs(x_new-x_1)
        x_0=x_1
        x_1=x_new
        count+=1
        if(print_it):
            print 'iteration {:3d}: x={:13.8f} error={:11.8f}'.format(count,x_1,error)
    return x_1
```

### Examples
#### Prompt

```python
function=lambda x: 3*x*math.cos(10*x)
guess=.2
secant_method(function,guess,guess+.01,10**-10,15,True)
```

#### Output

```
initial guess: x0=   0.20000000 error= N/A
initial guess: x1=   0.21000000 error= N/A
iteration   1: x=   0.16347717 error= 0.04652283
iteration   2: x=   0.15838931 error= 0.00508786
iteration   3: x=   0.15712945 error= 0.00125986
iteration   4: x=   0.15708004 error= 0.00004941
iteration   5: x=   0.15707963 error= 0.00000041
iteration   6: x=   0.15707963 error= 0.00000000
iteration   7: x=   0.15707963 error= 0.00000000
```
