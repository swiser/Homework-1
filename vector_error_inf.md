# Function Name: vector_error_inf()

### Last Mod Date
October 5, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Calculates the error \|\|X-Y\|\|<sub><sub>∞</sub></sub> between two vectors, X and Y.
### Inputs

* vector_X: a list of numbers
* vector_Y: a list of numbers

### Outputs

* \|\|X-Y\|\|<sub><sub>∞</sub></sub> error

### Modules Used
None
### Code

```python
def vector_error_inf(vector_X,vector_Y):
    return max([abs(x-y) for x,y in zip(vector_X,vector_Y)])
```

### Examples
#### Prompt

```python
vector_X=[1.1,99,11]
vector_Y=[1,100,9]

print 'vec1: ',vector_X
print 'vec2: ',vector_Y

print 'error inf: ',vector_error_inf(vector_X,vector_Y)
```

#### Output

```
vec1:  [1.1, 99, 11]
vec2:  [1, 100, 9]
error inf:  2
```
