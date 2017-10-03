# Function Name: SinglePrecisionEps()

### Last Mod Date
September 11, 2017
### Author
    Skyler Wiser
### Written For
Python 2.7.13
### Description
Calculates machine epsilon for single precision floating point variable.
### Inputs
None
### Outputs
Machine epsilon
### Modules Used
numpy as np
## Code
```python
def SinglePrecisionEps():
    x_bar=np.float32(1.0)
    n=0
    while np.float32(1)+x_bar/np.float32(2.0)>1:
        x_bar=x_bar/np.float32(2.0)
        n+=1
    return x_bar
```
## Examples
### Prompt
```python
print SinglePrecisionEps()
```
### Output
```
1.19209e-07
```

