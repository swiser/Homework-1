# Function Name: two_norm_vector()

### Last Mod Date
October 5, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Calculates the 2-Norm of a vector.
### Inputs

* vector: A list of numbers

### Outputs

* 2-Norm

### Modules Used
None
### Code

```python
def two_norm_vector(vector):
    return sum([x**2 for x in vector])**.5
```

### Examples
#### Prompt

```python
vector=[1,2,3,4]
print 'two norm: ', two_norm_vector(vector)
```

#### Output

```
two norm:  5.47722557505
```

