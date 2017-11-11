# Compute the Taylor Series expansion of e^x at x=1

### Last Mod Date

September 10, 2017

### Author

Skyler Wiser

### Written For

Python 2.7.13

### Modules Used

* math

### Code

```python
def exampleTaylor(terms,x):
    running_total=1
    running_factorial=1
    for n in xrange(1,terms,1):
        running_factorial*=n
        running_total+=(x-1.0)**n/running_factorial
    return running_total*math.exp(1)

print math.exp(5)
print exampleTaylor(30,5)
```

### Code notes

Because the derivative of e^x is e^x, the Taylor Series expansion was greatly simplified by hand before generating this code. The speed of the algorithm was improved by calculated new factorial terms based on the previous loop iteration, instead of trying to calculate the entire factorial each loop iteration.

#### Output

```
148.413159103
148.413159103
```



