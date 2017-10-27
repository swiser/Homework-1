# Exam 1 Problem 1

### Last Mod Date
October 25, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description

Problems 21 and 23 from Chapter 3 were solved using these functions. The intermediate functions are assumed to be self explanatory, the main function is detailed below.

## Main Function: minimize()

### Inputs

* function: Function f(x)
* a: Left x-bound to minimize
* b: Right x-bound to minimize
* nProbes: Number of interval nodes across (a,b) to test for local minimums
* tolerance: Smallest change in x to iterate with when bisecting


### Outputs

* Prints list of local minimums in f(x)=y format. Also lists global minimum.

### Modules Used

  * numpy
  * math

### Main Code

```python
def minimize(function,a,b,nProbes,tolerance):
    #WARNING: Bounds or probes that center over zero may cause fatal errors.
    delta=(b-a)/float(nProbes)
    probelist=[a+i*delta for i in xrange(nProbes)]
    probelist.append(b)
    zeros=[]
    derivatives=[]
    derivative=lambda x:24*x**3-40*x
    for i in xrange(1,nProbes):
        d1=first_central_derivative(function,probelist[i],delta/10.0)
        d2=first_central_derivative(function,probelist[i+1],delta/10.0)
        if(d1==0):
            zeros.append(probelist[i])
        elif (d1*d2<0):
            zeros.append(derivative_bisection(probelist[i],probelist[i+1],tolerance,function,1000))
    local_minimums=[]
    global_minimum=zeros[0]
    for x in zeros:
        if (second_derivative(function,x,delta/10.0)>0):
            local_minimums.append(x)
        if (function(x)<function(global_minimum)):
            global_minimum=x

    print "Local minimums:"
    for x in local_minimums:
        print "f({: 6.3f})={: 6.3f}".format(x,function(x))
    print "Global minimum is:"
    print "f({: 6.3f})={: 6.3f}".format(global_minimum,function(global_minimum))
```

### Intermediate Functions

Approximates the first derivative of x using central difference:

```python
def first_central_derivative(function,x,delta):
    #central derivative approximation
    return (function(x+delta)-function(x-delta))/(2.0*delta)
```

Approximates the first derivative of x using forward difference:

```python
def first_forward_derivative(function,x,delta):
    #central derivative approximation
    return (function(x+delta)-function(x))/(delta)
```

Approximates the second derivative of x using central difference:

```python
def second_derivative(function,x,delta):
    #central derivative approximation
```

Bisection method over sub-interval, using f'(x) instead of f(x):

```python
def derivative_bisection(a,b,tolerance,function,max_iters):
    delta=(a-b)/100.0
    if delta==0:
        fa=first_forward_derivative(function,a,a/100.0)
        fb=first_forward_derivative(function,b,b/100.0)
    else:
        fa=first_central_derivative(function,a,delta)
        fb=first_central_derivative(function,b,delta)
    error=10.0*tolerance
    cnt=0
    assert fa*fb<0,'No roots guaranteed in interval.'
    while error>tolerance and cnt<max_iters:
        c=(a+b)/2.0
        fc=first_central_derivative(function,c,tolerance*100)
        if fa*fc>0:
            a=c
            fa=fc
        else:
            b=c
            fb=fc
        cnt+=1
        error=abs(a-b)        
    return c
```

### Results

Problem 3.21 was to formulate the above code. 3.23(a) and 3.23(b) were to use this method to test two different functions. Graphs of the functions have been added to show proof of results.

#### 3.23(a)

##### Prompt

```python
function=lambda x: math.sin(x)
print "sin(x), -10<x<10:"
minimize(function,-10,10,20,10**-8)
```

##### Results

```
sin(x), -10<x<10:
Local minimums:
f(-7.854)=-1.000
f(-1.571)=-1.000
f( 4.712)=-1.000
Global minimum is:
f(-7.854)=-1.000
```
![3.23(a)](https://swiser.github.io/MATH4610/Exam1/3_23_a.png)

#### 3.23(b)

Note: The book addresses this as the more difficult problem, and asks to state how/why you fixed it. The problem arises from the function being symmetric about 0, with a local minimum at 0. This causes the slope to go to zero on either the endpoint of your probe, or the center of the probe. The solution was to grow the range from [-10,10] to [-10,11], and make sure the results were still in the original range.

##### Prompt

```python
print "\n-sin(x)/x, -10<x<11"
function=lambda x: -1.0*math.sin(x)/x
minimize(function,-10,11,20,10**-8)
```

##### Results

```
-sin(x)/x, -10<x<11
Local minimums:
f(-7.725)=-0.128
f( 0.000)=-1.000
f( 7.725)=-0.128
Global minimum is:
f( 0.000)=-1.000
```
![3.23(b)](https://swiser.github.io/MATH4610/Exam1/3_23_b.png)
