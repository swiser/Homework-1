# Function Name: vector_error_two()

### Last Mod Date
October 5, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Calculates the error \|\|X-Y\|\|<sub><sub>2</sub></sub> between two vectors, X and Y1.
### Inputs

* vector_X: a list of numbers
* vector_Y: a list of numbers

### Outputs

* \|\|X-Y\|\|<sub>2</sub> error

### Modules Used
None
### Code

```python
def vector_error_two(vector_X,vector_Y):
    if len(vector_X) != len(vector_Y):
        print 'Vectors not same length.'
        return 0
    return sum([abs(x-y)**2 for x,y in zip(vector_X,vector_Y)])**.5
```

### Examples
#### Prompt

```python
vector_X=[1.1,99,11]
vector_Y=[1,100,9]

print 'vec1: ',vector_X
print 'vec2: ',vector_Y

print 'error 2  : ',vector_error_two(vector_X,vector_Y)
```

#### Output

```
vec1:  [1.1, 99, 11]
vec2:  [1, 100, 9]
error 2  :  2.23830292856
```
