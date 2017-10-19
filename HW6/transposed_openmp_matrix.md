# Function Name: transposed_openmp_matrix()

### Last Mod Date
October 18, 2017
### Author
Skyler Wiser
### Written For
C++
### Description
Uses openMP to parallelize matrix multiplication. Accesses matrix elements from 1D arrays.
### Inputs

* matrixA: first matrix to multiply
* matrixB: second matrix to multiply
* numthreads: number of threads to run in parallel

### Outputs

* answer: a matrix of numbers

### Modules Used

* \<vector\>
* \<omp.h\>

### Code

```c++
vector<vector<double>> transposed_openmp_matrix (const vector<vector<double>> &matrixA,const vector<vector<double> > &matrixB, int numthreads){
    int A_rows=matrixA.size();
    int A_cols=matrixA[0].size();
    int B_rows=matrixB.size();
    int B_cols=matrixB[0].size();
    if (A_cols!=B_rows){
        cout <<"Dimension Mismatch" <<endl;
        return {{0}};
    }
    //initialize arrays outside of stack
    double* array_A=new double[A_rows*A_cols];
    double* array_B=new double[B_rows*B_cols];
    
    //copy vectors into arrays
    for(int row=0; row<A_rows;row++){
        for(int col=0;col<A_cols;col++){
            array_A[col+row*B_cols]=matrixA[row][col];
        }
    }
    
    for(int row=0; row<B_rows;row++){
        for(int col=0;col<B_cols;col++){
            array_B[col+row*B_cols]=matrixB[row][col];
        }
    }
    
    int rowA=0,colB=0,colA=0;
    vector<vector<double> > answer(A_rows,vector<double>(B_cols,0));
    double* answer_array= new double[A_rows*B_cols];
    omp_set_num_threads(numthreads);
    #pragma omp parallel private(rowA,colB,colA)
    {
        #pragma omp for
        for(rowA=0;rowA<A_rows;rowA++){
            for(colB=0;colB<B_cols;colB++){
                double temp_cell=0;
                for(colA=0;colA<A_cols;colA++){
                    temp_cell+=array_A[colA+rowA*A_cols]*array_B[colB+colA*B_cols];
            }
            answer_array[colB+rowA*B_cols]=temp_cell;
        }
    }
    }
    for(int row=0; row<A_rows; row++){
        for(int col=0; col<B_cols; col++){
            answer[row][col]=answer_array[col+row*B_cols];
        }
    }
    delete [] array_A;
    delete [] array_B;
    delete [] answer_array;
    return answer;
    
}
```

### Example
#### Prompt

```c++
vector<vector<double> > matrixA=transposed_openmp_matrix(matrixA,matrixB,4);
```
