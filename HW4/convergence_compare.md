# Project: Compare Matrix-Matrix Multiplication

### Last Mod Date
October 2, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description

Using multiple root-finding methods, compare convergence rates.

### Modules Used

* time
* numpy
* matplotlib

### Helper functions
The following variants of Newton's method, bisection method, and secant method were used to graph convergence:

```python
def valued_bisection(a,b,tolerance,function,max_iters,x_star):
    error_convergence=[]
    fa=function(a)
    fb=function(b)
    error=10.0*tolerance
    cnt=0
    assert fa*fb<0,'No roots guaranteed in interval.'
    
    while error>tolerance and cnt<max_iters:
        c=(a+b)/2.0
        fc=function(c)
        if (abs(c-x_star)>0):
            error_convergence.append(math.log(abs(c-x_star)))
        if fa*fc>0:
            a=c
            fa=fc
        else:
            b=c
            fb=fc
        cnt+=1
        error=abs(a-b)
        
    return error_convergence
        
def valued_secant_method(function,derivative,x0,x1,tolerance,max_iters,x_star):
    error=tolerance*10
    count=0
    x_0=x0
    x_1=x1
    error_convergence=[]
    while error>tolerance and count<max_iters:
        f_x0=function(x_0)
        f_x1=function(x_1)
        x_new=x_1-(f_x1*(x_1-x_0))/float(f_x1-f_x0)
        error=abs(x_new-x_1)
        x_0=x_1
        x_1=x_new
        count+=1
        if(abs(x_1-x_star)>0):
            error_convergence.append(math.log(abs(x_1-x_star)))
    return error_convergence

def valued_newton_method(function,derivative,x0,tolerance,max_iters,x_star):
    error=tolerance*10
    count=0
    x_old=x0
    error_convergence=[]
    error_convergence.append(math.log(abs(x_old-x_star)))
    while error>tolerance and count<max_iters:
        x_new=x_old-function(x_old)/float(derivative(x_old))
        error=abs(x_new-x_old)
        x_old=x_new
        if(abs(x_old-x_star)>0):
            error_convergence.append(math.log(abs(x_old-x_star)))
        count+=1
    return error_convergence
```

### Main Code

```python
start=time.time()
bisection=valued_bisection(a,b,10**-10,function,100,x_star)
end=time.time()
bisection_time=end-start

start=time.time()
secant=valued_secant_method(function,derivative,guess,guess+.01,10**-10,100,x_star)
end=time.time()
secant_time=end-start

start=time.time()
newton=valued_newton_method(function,derivative,guess,10**-10,100,x_star)
end=time.time()
newton_time=end-start

title='Error Convergence for Different Methods\n'+equation

fig1=plt.figure(1,figsize=(11,7))
fig1.suptitle(title)
plt.xlabel('Log(e_k-1)')
plt.ylabel('Log(e_k)')

plt.plot(bisection[:-1],bisection[1:],'go',markersize=3,label='Bisection Method, {:.3f} milliseconds'.format(bisection_time*1000))
bisection_regression_coeff=np.polyfit(bisection[:-1],bisection[1:],1)
bisection_regression=np.poly1d(bisection_regression_coeff)
bisection_x=np.arange(min(bisection[:-1])-1,max(bisection[:-1])+1,abs((min(bisection)+max(bisection))/30.0))
plt.plot(bisection_x,bisection_regression(bisection_x),'-g',label='Bisection Regression, r={:.3f}'.format(bisection_regression_coeff[0]))

plt.plot(secant[:-1],secant[1:],'ko',markersize=3,label='Secant Method, {:.3f} milliseconds'.format(secant_time*1000))
secant_regression_coeff=np.polyfit(secant[:-1],secant[1:],1)
secant_regression=np.poly1d(secant_regression_coeff)
secant_x=np.arange(min(secant[:-1])-1,max(secant[:-1])+1,abs((min(secant)+max(secant))/30.0))
plt.plot(secant_x,secant_regression(secant_x),'-k',label='Secant Regression, r={:.3f}'.format(secant_regression_coeff[0]))

plt.plot(newton[:-1],newton[1:],'bo',markersize=3,label='Newton Method, {:.3f} milliseconds'.format(newton_time*1000))
newton_regression_coeff=np.polyfit(newton[:-2],newton[1:-1],1)
newton_regression=np.poly1d(newton_regression_coeff)
newton_x=np.arange(min(newton[:-2])-1,max(newton[:-2])+1,abs((min(newton)+max(newton))/30.0))
plt.plot(newton_x,newton_regression(newton_x),'-b',label='Newton Regression, r={:.3f}'.format(newton_regression_coeff[0]))

plt.legend(loc='best')


plt.show()
```

### Prompts

```python
Prompt one:
function=lambda x: 3*x*math.cos(10*x)
derivative=lambda x: (3*math.cos(10*x)-30*x*math.sin(10*x))
guess=.16
a=.1
b=.3
x_star=math.pi/20
equation='y=3*x*cos(10*x)'

Prompt two:
function=lambda x: x**3-x+1
derivative=lambda x: 3*x**2-1
guess=-8
a=-4
b=4
x_star=-1.3247179572447
equation='y=x^3-x+1'
```

### Graphs

![Cosine Convergence](https://swiser.github.io/MATH4610/HW4/cos_convergence.png)
![Polynomial Convergence](https://swiser.github.io/MATH4610/HW4/poly_convergence.png)

