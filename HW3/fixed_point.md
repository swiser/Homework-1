# Function Name: fixed_point()

### Last Mod Date
September 18, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
A function that uses the fixed-point method to find a root within a function.
### Inputs

* function: function to evaluate *f(x)=0*
* guess: initial guess of x-value near root
* max_iters: maximum iterations to run before function returns
* tolerance: smallest difference between x-values on each iteration before returning
* conditioning: Values to improve convergence. Switching signs/values may improve convergence.

### Outputs

* x_next: x-value once loop condition has been met.

### Convergence Methodology

![Conditioning](https://swiser.github.io/MATH4610/HW3/conditioning.png)

### Code

```python
def fixed_point(function,guess,max_iters,tolerance,conditioning):
    error=10*tolerance
    if function(guess)==0:
        return guess
    x_previous=guess
    cnt=0
    while error>tolerance and cnt<max_iters:
        f_x=function(x_previous)
        if abs(f_x)<tolerance:
            return x_previous
        x_next=(f_x+conditioning*x_previous)*(1.0/conditioning)
        error=abs((x_next-x_previous)/float(x_next))
        x_previous=x_next
        print 'iteration:{:3}, xi={:.10f}, F(c)={: .10f}, error={:.10f}'.format(cnt,x_previous,function(x_previous),error)
        cnt+=1

    return x_next
```

### Example
#### Prompt

```python
function =lambda x: (3*x*math.sin(10*x))
print fixed_point(function,.4,100,10**-5,50)
```

#### Output

```
iteration:  0, xi=0.3818367401, F(c)=-0.7174123054, error=0.0475681305
iteration:  1, xi=0.3674884940, F(c)=-0.5604617048, error=0.0390440690
iteration:  2, xi=0.3562792599, F(c)=-0.4370005428, error=0.0314619327
iteration:  3, xi=0.3475392491, F(c)=-0.3415985733, error=0.0251482700
iteration:  4, xi=0.3407072776, F(c)=-0.2681767631, error=0.0200523203
iteration:  5, xi=0.3353437423, F(c)=-0.2115319345, error=0.0159941415
iteration:  6, xi=0.3311131036, F(c)=-0.1676035276, error=0.0127770198
iteration:  7, xi=0.3277610331, F(c)=-0.1333318695, error=0.0102271784
iteration:  8, xi=0.3250943957, F(c)=-0.1064360694, error=0.0082026557
iteration:  9, xi=0.3229656743, F(c)=-0.0852147902, error=0.0065911691
iteration: 10, xi=0.3212613785, F(c)=-0.0683915114, error=0.0053050130
iteration: 11, xi=0.3198935483, F(c)=-0.0550006495, error=0.0042758919
iteration: 12, xi=0.3187935353, F(c)=-0.0443053961, error=0.0034505499
iteration: 13, xi=0.3179074274, F(c)=-0.0357386868, error=0.0027873143
iteration: 14, xi=0.3171926536, F(c)=-0.0288606277, error=0.0022534372
iteration: 15, xi=0.3166154411, F(c)=-0.0233275490, error=0.0018230714
iteration: 16, xi=0.3161488901, F(c)=-0.0188692845, error=0.0014757318
iteration: 17, xi=0.3157715044, F(c)=-0.0152723128, error=0.0011951227
iteration: 18, xi=0.3154660581, F(c)=-0.0123671111, error=0.0009682381
iteration: 19, xi=0.3152187159, F(c)=-0.0100185720, error=0.0007846686
iteration: 20, xi=0.3150183445, F(c)=-0.0081186706, error=0.0006360628
iteration: 21, xi=0.3148559711, F(c)=-0.0065808054, error=0.0005157070
iteration: 22, xi=0.3147243550, F(c)=-0.0053353954, error=0.0004181949
iteration: 23, xi=0.3146176471, F(c)=-0.0043264340, error=0.0003391670
iteration: 24, xi=0.3145311184, F(c)=-0.0035087723, error=0.0002751037
iteration: 25, xi=0.3144609429, F(c)=-0.0028459701, error=0.0002231611
iteration: 26, xi=0.3144040235, F(c)=-0.0023085863, error=0.0001810390
iteration: 27, xi=0.3143578518, F(c)=-0.0018728150, error=0.0001468763
iteration: 28, xi=0.3143203955, F(c)=-0.0015193941, error=0.0001191660
iteration: 29, xi=0.3142900076, F(c)=-0.0012327292, error=0.0000966874
iteration: 30, xi=0.3142653530, F(c)=-0.0010001903, error=0.0000784515
iteration: 31, xi=0.3142453492, F(c)=-0.0008115436, error=0.0000636566
iteration: 32, xi=0.3142291184, F(c)=-0.0006584953, error=0.0000516530
iteration: 33, xi=0.3142159485, F(c)=-0.0005343219, error=0.0000419136
iteration: 34, xi=0.3142052620, F(c)=-0.0004335717, error=0.0000340110
iteration: 35, xi=0.3141965906, F(c)=-0.0003518237, error=0.0000275988
iteration: 36, xi=0.3141895541, F(c)=-0.0002854922, error=0.0000223956
iteration: 37, xi=0.3141838443, F(c)=-0.0002316688, error=0.0000181736
iteration: 38, xi=0.3141792109, F(c)=-0.0001879941, error=0.0000147476
iteration: 39, xi=0.3141754510, F(c)=-0.0001525540, error=0.0000119675
iteration: 40, xi=0.3141723999, F(c)=-0.0001237955, error=0.0000097115
0.314172399924
```
