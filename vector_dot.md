# Function Name: vector_dot()

### Last Mod Date
October 5, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Evaluates the dot product between two vectors.
### Inputs

* vectorA: a list of numbers
* vectorB: a list of numbers

### Outputs

* a list of numbers, vectorA·vectorB

### Modules Used
None
### Code

```python
def vector_dot(vectorA, vectorB):
    return sum([A*B for A,B in zip(vectorA,vectorB)])
```

### Examples
#### Prompt

```python
print '[4,8,10] dot [9,2,7]: '
print vector_dot([4,8,10],[9,2,7])
```

#### Output

```
[4,8,10] dot [9,2,7]: 
122
```
