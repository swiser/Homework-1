# Example 1.2 From Textbook

### Last Mod Date

September 10, 2017

### Author

Skyler Wiser

### Written For

Python 2.7.13

### Description

Using a Taylor Series approximation of the derivative of *sin(x)*, approximate *d/dx (sin(x))* at *x*=1.2. Compare the error values as the step size *h* gets smaller and approaches machine epsilon.

### Code

#### Single precision

```python
SinglePrecisionEps()
print '\n\nSingle Precision Test, Example 1.2'

exact_value=np.float32(math.cos(1.2))
initial=1.2
h=.1


for x in range(20):
    approx_value=(np.float32(math.sin(1.2+h))-np.float32(math.sin(1.2)))/np.float32(h)
    print 'h:',h,'Approx:',approx_value,'Absolute Error:',absolute_error(exact_value,approx_value)
    h=h/10.0
```

#### Double precision

```python
DoublePrecisionEps()
print '\n\nDouble Precision Test, Example 1.2'

exact_value=math.cos(1.2)
initial=1.2
h=.1


for x in range(20):
    approx_value=(math.sin(1.2+h)-math.sin(1.2))/h
    print 'h:',h,'Approx:',approx_value,'Absolute Error:',absolute_error(exact_value,approx_value)
    h=h/10.0
```

### Code notes

We see that as *h* approaches machine epsilon, the absolute error levels out because the machine is no longer able to distinguish more accuracy.

#### Output

```
Test: Binary Digits (Single): 23 Epsilon: 1.19209e-07 False True


Single Precision Test, Example 1.2
h: 0.1 Approx: 0.315191 Absolute Error: 0.0471666
h: 0.01 Approx: 0.357693 Absolute Error: 0.00466433
h: 0.001 Approx: 0.361919 Absolute Error: 0.000438392
h: 0.0001 Approx: 0.362396 Absolute Error: 3.84748e-05
h: 1e-05 Approx: 0.363588 Absolute Error: 0.00123057
h: 1e-06 Approx: 0.357628 Absolute Error: 0.0047299
h: 1e-07 Approx: 0.596046 Absolute Error: 0.233689
h: 1e-08 Approx: 0.0 Absolute Error: 0.362358
h: 1e-09 Approx: 0.0 Absolute Error: 0.362358
h: 1e-10 Approx: 0.0 Absolute Error: 0.362358
h: 1e-11 Approx: 0.0 Absolute Error: 0.362358
h: 1e-12 Approx: 0.0 Absolute Error: 0.362358
h: 1e-13 Approx: 0.0 Absolute Error: 0.362358
h: 1e-14 Approx: 0.0 Absolute Error: 0.362358
h: 1e-15 Approx: 0.0 Absolute Error: 0.362358
h: 1e-16 Approx: 0.0 Absolute Error: 0.362358
h: 1e-17 Approx: 0.0 Absolute Error: 0.362358
h: 1e-18 Approx: 0.0 Absolute Error: 0.362358
h: 1e-19 Approx: 0.0 Absolute Error: 0.362358
h: 1e-20 Approx: 0.0 Absolute Error: 0.362358
```

```
Test: Binary Digits (Double): 52 Epsilon: 2.22044604925e-16 False True


Double Precision Test, Example 1.2
h: 0.1 Approx: 0.3151909945 Absolute Error: 0.047166759977
h: 0.01 Approx: 0.357691558616 Absolute Error: 0.00466619586072
h: 0.001 Approx: 0.36189167458 Absolute Error: 0.000466079897112
h: 0.0001 Approx: 0.362311151919 Absolute Error: 4.66025575812e-05
h: 1e-05 Approx: 0.362353094285 Absolute Error: 4.66019133444e-06
h: 1e-06 Approx: 0.362357288508 Absolute Error: 4.65968587549e-07
h: 1e-07 Approx: 0.362357708283 Absolute Error: 4.61932619378e-08
h: 1e-08 Approx: 0.362357754913 Absolute Error: 4.3610509648e-10
h: 1e-09 Approx: 0.362357810424 Absolute Error: 5.59472562722e-08
h: 1e-10 Approx: 0.362357921446 Absolute Error: 1.66969558735e-07
h: 1e-11 Approx: 0.362365693007 Absolute Error: 7.93853073111e-06
h: 1e-12 Approx: 0.36248781754 Absolute Error: 0.00013006306344
h: 1e-13 Approx: 0.361932706028 Absolute Error: 0.000425048448873
h: 1e-14 Approx: 0.366373598126 Absolute Error: 0.00401584364963
h: 1e-15 Approx: 0.44408920985 Absolute Error: 0.0817314553734
h: 1e-16 Approx: 0.0 Absolute Error: 0.362357754477
h: 1e-17 Approx: 0.0 Absolute Error: 0.362357754477
h: 1e-18 Approx: 0.0 Absolute Error: 0.362357754477
h: 1e-19 Approx: 0.0 Absolute Error: 0.362357754477
h: 1e-20 Approx: 0.0 Absolute Error: 0.362357754477
```




