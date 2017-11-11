# Function Name: newton_method()

### Last Mod Date
October 2, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Newton-Raphson method with built in print and safety checks. Will attempt to find a root of a function.
### Inputs

* function: function *f(x)*
* derivative: derivative of function; *f'(x)*
* x0: initial x-value guess of root
* tolerance: smallest variation between x-values while iterating
* max_iters: maximum iterations to perform before returning
* print_it: boolean that turns on/off printing of each iteration

### Outputs

* Root of function

### Modules Used
None
### Code

```python
def newton_method(function,derivative,x0,tolerance,max_iters,print_it):
    error=tolerance*10
    count=0
    if (abs(function(x0))<tolerance):
        print 'Initial x is root'
        return x0
    if (abs(derivative(x0))<tolerance):
        print 'Bad initial x'
        return 0
    x_old=x0
    if(print_it):
        print 'initial guess: x={:13.8f} error= N/A'.format(x0)
    while error>tolerance and count<max_iters:
        x_new=x_old-function(x_old)/float(derivative(x_old))
        error=abs(x_new-x_old)
        x_old=x_new
        count+=1
        if(print_it):
            print 'iteration {:3d}: x={:13.8f} error={:11.8f}'.format(count,x_old,error)
    return x_old
```

### Examples
#### Prompt

```python
function=lambda x: 3*x*math.cos(10*x)
derivative=lambda x: (3*math.cos(10*x)-30*x*math.sin(10*x))

print 'Newton Method: {}\n'.format(newton_method(function,derivative,.2,10**-10,15,True))
```

#### Output

```
initial guess: x=   0.20000000 error= N/A
iteration   1: x=   0.16275661 error= 0.03724339
iteration   2: x=   0.15726527 error= 0.00549133
iteration   3: x=   0.15707985 error= 0.00018542
iteration   4: x=   0.15707963 error= 0.00000022
iteration   5: x=   0.15707963 error= 0.00000000
Newton Method: 0.157079632679
```

#### Prompt, comparing quick and slow

```python
start1=time.time()
print 'Quick Newton Method: {}\n'.format(quick_newton_method(function,derivative,.2,10**-10,15))
end1=time.time()
start=time.time()
print 'Newton Method: {}\n'.format(newton_method(function,derivative,.2,10**-10,15,False))
end=time.time()
print 'Quick: {} seconds'.format(end1-start1)
print 'Slow: {} seconds'.format(end-start)
```

#### Output

```
Quick Newton Method: 0.157079632679

initial guess: x=   0.20000000 error= N/A
iteration   1: x=   0.16275661 error= 0.03724339
iteration   2: x=   0.15726527 error= 0.00549133
iteration   3: x=   0.15707985 error= 0.00018542
iteration   4: x=   0.15707963 error= 0.00000022
iteration   5: x=   0.15707963 error= 0.00000000
Newton Method: 0.157079632679

Quick: 0.0857391357422 seconds
Slow: 0.499821901321 seconds
```
