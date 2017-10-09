# Function Name: inf_norm_vector()

### Last Mod Date
October 5, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Calculates the ∞-Norm of a vector.
### Inputs
* vector: A list of numbers
### Outputs
* ∞-Norm
### Modules Used
None
### Code

```python
def inf_norm_vector(vector):
    return max([abs(x) for x in vector])
```

### Examples
#### Prompt

```python
vector=[1,2,3,4]
print 'inf norm: ', inf_norm_vector(vector)
```

#### Output

```
inf norm:  4
```

