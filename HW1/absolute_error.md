# Function Name: absolute_error()

### Last Mod Date

September 10, 2017

### Author

Skyler Wiser

### Written For

Python 2.7.13

### Description

Calculates the absolute error between two values.

### Inputs

* actual_value: The known value to compare against.
* approx_value: The calculated value to compare against the known value.

### Outputs

* Absolute Error

### Code

```python
def absolute_error(actual_value,approx_value):
    return abs(actual_value-approx_value)
```

### Examples
#### Prompt

```python
print absolute_error(2.0,.2)
```

#### Output

```
1.8
```
