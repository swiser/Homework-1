# Function Name: relative_error()

### Last Mod Date

September 10, 2017

### Author

Skyler Wiser

### Written For

Python 2.7.13

### Description

Calculates the relative error between two values.

### Inputs

* actual_value: The known value to compare against.
* approx_value: The calculated value to compare against the known value.

### Outputs

* Relative Error as a decimal

### Code

```python
def relative_error(actual_value,approx_value):
    if actual_value==0:
        print "Cannot be relative to zero."
        return 0
    return abs((actual_value-approx_value)/float(actual_value))
```

### Examples
#### Prompt

```python
print relative_error(2.0,.2)
#90 percent relative error
```

#### Output

```
0.9
```
