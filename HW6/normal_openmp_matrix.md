# Function Name: normal_openmp_matrix()

### Last Mod Date
October 18, 2017
### Author
Skyler Wiser
### Written For
C++
### Description
Uses openMP to parallelize matrix multiplication. Accesses matrix elements from 2D arrays.
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
vector<vector<double>> normal_openmp_matrix (const vector<vector<double>> &matrixA,const vector<vector<double> > &matrixB, int numthreads){
    int A_rows=matrixA.size();
    int A_cols=matrixA[0].size();
    int B_rows=matrixB.size();
    int B_cols=matrixB[0].size();
    if (A_cols!=B_rows){
        cout <<"Dimension Mismatch" <<endl;
        return {{0}};
    }
    //initialize arrays outside of stack
    double** array_A= new double*[A_rows];
    double** array_B= new double*[B_rows];
    double** answer_array=new double*[A_rows];
    for(int row=0;row<A_rows;row++){
        array_A[row]=new double[A_cols];
        answer_array[row]=new double[B_cols];
    }
    for(int row=0;row<B_rows;row++){
        array_B[row]=new double[B_cols];
    }
    //convert vectors to arrays
    for(int row=0; row<A_rows;row++){
        for(int col=0;col<A_cols;col++){
            array_A[row][col]=matrixA[row][col];
        }
    }
    for(int row=0; row<B_rows;row++){
        for(int col=0;col<B_cols;col++){
            array_B[row][col]=matrixB[row][col];
        }
    }
    
    int rowA=0,colB=0,colA=0;
    vector<vector<double> > answer(A_rows,vector<double>(B_cols,0));
    omp_set_num_threads(numthreads);
#pragma omp parallel private(rowA,colB,colA)
    {
#pragma omp for
        for(rowA=0;rowA<A_rows;rowA++){
            for(colB=0;colB<B_cols;colB++){
                double temp_cell=0;
                for(colA=0;colA<A_cols;colA++){
                    temp_cell+=array_A[rowA][colA]*array_B[colA][colB];
                }
                answer_array[rowA][colB]=temp_cell;
            }
        }
    }
    for(int row=0; row<A_rows; row++){
        for(int col=0; col<B_cols; col++){
            answer[row][col]=answer_array[row][col];
        }
    }
    //delete arrays
    for(int row=0;row<A_rows;row++){
        delete [] array_A[row];
        delete [] answer_array[row];
    }

    for(int row=0;row<B_rows;row++){
        delete [] array_B[row];
    }
    delete [] array_A;
    delete [] answer_array;
    delete [] array_B;
    
    return answer;
}
```

### Example
#### Prompt

```c++
vector<vector<double> > matrixA=normal_openmp_matrix(matrixA,matrixB,4);
```
