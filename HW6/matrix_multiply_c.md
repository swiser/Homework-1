# Function Name: matrix_multiply()

### Last Mod Date
October 18, 2017
### Author
Skyler Wiser
### Written For
C++
### Description
Multiplies two matrices together and returns a matrix. Matrix format is std::vector<vector\<double\>>
### Inputs

* matrixA: First matrix
* matrixB: Second matrix

### Outputs

* answer: matrixA x matrixB

### Modules Used

* \<vector\>

### Notes

Does a quick check for correct matrix dimensions, returns empty array and prints message if they cannot be multiplied.

### Code

```c++
vector<vector<double> > matrix_multiply(vector<vector<double> > &matrixA, vector<vector<double>> &matrixB){
    int A_rows=matrixA.size();
    int A_cols=matrixA[0].size();
    int B_rows=matrixB.size();
    int B_cols=matrixB[0].size();
    if (A_cols!=B_rows){
        cout <<"Dimension Mismatch" <<endl;
        return {{0}};
    }
    vector<vector<double>> answer(A_rows,vector<double>(B_cols,0));
    for(int row=0;row<A_rows;row++){
        vector<double> temp_row(B_cols,0.0);
        for(int colB=0;colB<B_cols;colB++){
            double temp_cell=0.0;
            for(int colA=0;colA<A_cols;colA++){
                temp_cell+=matrixA[row][colA]*matrixB[colA][colB];
            }
            temp_row[colB]=temp_cell;
        }
        answer[row]=temp_row;
        
    }
    return answer;
}
```

### Example
#### Prompt

```c++
vector<vector<double>> matrixA=matrix_multiply(matrixA,matrixB);
```
