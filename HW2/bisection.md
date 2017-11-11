# Function Name: bisection()

### Last Mod Date
September 17, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
A function that bisects over a closed interval to find a root.
### Inputs

* a: left x-bound of interval
* b: right x-bound of interval
* tolerance: smallest variation between a and b before function stops
* function: function to evaluate *f(x)=0*
* max_iters: maximum iterations to run before returning

### Outputs

* c: estimated root of function

### Modules Used

None

### Code

```python
def bisection(a,b,tolerance,function,max_iters):
    '''
    a: Left x value of bisection.
    b: Right x value of bisection.
    tolerance: Smallest variation between a and b before function stops.
    function: Equation to evaluate with. Examples: math.sin, lambda x: x**2
    max_iters: Maximum iterations to run before returning.
    '''
    
    fa=function(a)
    fb=function(b)
    error=10.0*tolerance
    cnt=0
    assert fa*fb<0,'No roots guaranteed in interval.'
    
    while error>tolerance and cnt<max_iters:
        c=(a+b)/2.0
        fc=function(c)
        if fa*fc>0:
            a=c
            fa=fc
        else:
            b=c
            fb=fc
        cnt+=1
        error=abs(a-b)
        print 'iteration:{:3}, c={:.10f}, F(c)={: .10f}, error={:.10f}'.format(cnt,c,fc,error)
        
    return c
```

### Examples
#### Prompt

```python
function=math.sin
print bisection(4,1,10**-5,function,100)
```

#### Output

```
iteration:  1, c=2.5000000000, F(c)= 0.5984721441, error=1.5000000000
iteration:  2, c=3.2500000000, F(c)=-0.1081951345, error=0.7500000000
iteration:  3, c=2.8750000000, F(c)= 0.2634459934, error=0.3750000000
iteration:  4, c=3.0625000000, F(c)= 0.0790102167, error=0.1875000000
iteration:  5, c=3.1562500000, F(c)=-0.0146568216, error=0.0937500000
iteration:  6, c=3.1093750000, F(c)= 0.0322120803, error=0.0468750000
iteration:  7, c=3.1328125000, F(c)= 0.0087800408, error=0.0234375000
iteration:  8, c=3.1445312500, F(c)=-0.0029385922, error=0.0117187500
iteration:  9, c=3.1386718750, F(c)= 0.0029207744, error=0.0058593750
iteration: 10, c=3.1416015625, F(c)=-0.0000089089, error=0.0029296875
iteration: 11, c=3.1401367188, F(c)= 0.0014559343, error=0.0014648438
iteration: 12, c=3.1408691406, F(c)= 0.0007235129, error=0.0007324219
iteration: 13, c=3.1412353516, F(c)= 0.0003573020, error=0.0003662109
iteration: 14, c=3.1414184570, F(c)= 0.0001741966, error=0.0001831055
iteration: 15, c=3.1415100098, F(c)= 0.0000826438, error=0.0000915527
iteration: 16, c=3.1415557861, F(c)= 0.0000368675, error=0.0000457764
iteration: 17, c=3.1415786743, F(c)= 0.0000139793, error=0.0000228882
iteration: 18, c=3.1415901184, F(c)= 0.0000025352, error=0.0000114441
iteration: 19, c=3.1415958405, F(c)=-0.0000031869, error=0.0000057220
3.14159584045
```
