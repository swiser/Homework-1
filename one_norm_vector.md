# Function Name: one_norm_vector()

### Last Mod Date
October 5, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Calculates the 1-Norm of a vector.
### Inputs
* vector: A list of numbers
### Outputs
* 1-Norm
### Modules Used
None
### Code
```python
def one_norm_vector(vector):
    return sum([abs(x) for x in vector])
```
### Examples
#### Prompt
```python
vector=[1,2,3,4]
print 'one norm: ', one_norm_vector(vector)
```
#### Output
```
one norm:  10
```

test2
