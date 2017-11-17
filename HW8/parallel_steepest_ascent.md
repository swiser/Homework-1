# Function Name: parallel_steepest_ascent()

### Last Mod Date
November 16, 2017
### Author
Skyler Wiser
### Written For
C++
### Description
Use the steepest ascent method to iteratively solve an size *n* square matrix, with parallelization by openMP.
### Inputs

* A: Coefficient matrix A
* B: Solution vector B
* guess: Initial guess *x<sub>o</sub>*
* tolerance: Smallest residual error before returning
* max_iters: Maximum iterations before returning

### Outputs

* x_old: Final iterative approximation of *x*

### Modules Used

* \<vector\>
* \<cmath\>
* \<omp.h\>

### Code

#### Function

```c++
vector<double> parallel_steepest_ascent(vector<vector<double>> A,vector<double> B,vector<double> guess,double tolerance,int max_iters){
    int n=A.size();
    double error=10*tolerance;
    int count=0;
    vector<double> x_old=guess;
    //Check if square, give zeros if not.
    if(n!=A[0].size()){
        cout << "Non square matrix, exiting." <<endl;
        return vector<double>(n,0);
    }
    
    //Calculate Initial residual, B-A*x_0
    vector<double> residual=B;
    int i=0;
#pragma omp parallel private(i)
    {
#pragma omp for
    for(i=0; i<n; i++)
    {
        //Matrix-Vector Multiplication
        double sum=0.0;
        for(int col=0; col<n;col++){
            sum+=A[i][col]*guess[col];
        }
        residual[i]-=sum;
    }
    }
    double deltaK=inner_product(residual,residual);
    double b_delta=inner_product(B,B);
    
    while (error>(tolerance*tolerance*b_delta) && count<max_iters)
    {
        ///Set s_k, matrix-vector math
        vector<double> s_k(n,0.0);
        omp_set_num_threads(2);
#pragma omp parallel private(i)
        {
#pragma omp for
        for(i=0; i<n; i++)
        {
            double sum=0.0;
            for(int col=0;col<n;col++)
            {
                sum+=A[i][col]*residual[col];
            }
            s_k[i]=sum;
        }
        }
        //determine alpha
        double alpha=deltaK/inner_product(residual, s_k);
        
        //Update x vector
        for(int i=0; i<n; i++){x_old[i]=x_old[i]+alpha*residual[i];}
        
        //Update R vector
        for(int i=0; i<n; i++){residual[i]=residual[i]-alpha*s_k[i];}
        
        deltaK=inner_product(residual,residual);
        error=deltaK;
        count++;
        
    }
    
    
    return x_old;
    
}
```

#### Helper Functions

```c++
void print_matrix(vector<vector<double>> matrix){
    
    int n=matrix.size();
    for(int row=0;row<n;row++){
        cout << "|";
        for(int col=0;col<n;col++){
            cout << setw(10) << matrix[row][col] << "  ";
        }
        cout << "|\n";
    }
}

void print_column(vector<double> column,int stop){
    
    int n=column.size();
    for(int row=0;row<stop;row++){
        cout << "|";
        cout << setw(3) << column[row] << "  ";
        cout << "|\n";
    }
}

double inner_product(vector<double> A, vector<double> B){
    double answer=0.0;
    for(int i=0; i<A.size(); i++){
        answer+=A[i]*B[i];
    }
    return answer;
}
```

### Example
#### Prompt

```c++
vector<vector<double>> A={ {5.0,2.0,1.0,1.0},{2.0,6.0,2.0,1.0},{1.0,2.0,7.0,1.0},{1.0,1.0,2.0,8.0} };
vector<double> B={29.0,31.0,25.0,19.0};
vector<double> guess(4,0.0);

vector<double> solution=parallel_steepest_ascent(A, B, guess, pow(10,-10),100);

cout << "Matrix A: " << endl;
print_matrix(A);

cout << "Matrix B: " << endl;
print_column(B);

cout << "SA Solution: " << endl;
print_column(solution);
```

#### Output

```
Matrix A: 
|         5           2           1           1  |
|         2           6           2           1  |
|         1           2           7           1  |
|         1           1           2           8  |
Matrix B: 
| 29  |
| 31  |
| 25  |
| 19  |
SA Solution: 
|  4  |
|  3  |
|  2  |
|  1  |
```









