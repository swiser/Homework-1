# Function Name: matrix_compare()

### Last Mod Date
October 18, 2017
### Author
Skyler Wiser
### Written For
C++
### Description
Compares two matrices of std::vector<vector<double>> format. Returns true if they are the same.
### Inputs

* matrixA: First matrix to compare
* matrixB: Second matrix to compare

### Outputs

* True/False

### Modules Used

* \<vector\>

### Code

```c++
bool matrixCompare(vector<vector<double > > &matrixA, vector<vector<double> > &matrixB){
    int A_rows=matrixA.size();
    int A_cols=matrixA[0].size();
    int B_rows=matrixB.size();
    int B_cols=matrixB[0].size();
    if (A_rows!=B_rows || A_cols!=B_cols){return false;}
    for(int row=0; row<A_rows; row++){
        for(int col=0; col<A_cols; col++){
            if(matrixA[row][col]!=matrixB[row][col]){
                return false;
            }
        }
    }
    return true;
}
```

### Example
#### Prompt

```c++
if(matrixCompare(matrixA,matrixB)){cout <<"Matrices A and B match." <<endl;}
else{cout <<"Matrices A and B don't match." <<endl;}

```
