# Function Name: parallel_gauss_seidel()

### Last Mod Date
November 16, 2017
### Author
Skyler Wiser
### Written For
C++
### Description
Use the Gauss-Seidel method to iteratively solve an size *n* square matrix, with parallelization by openMP.
### Inputs

* A: Coefficient matrix A
* B: Solution vector B
* guess: Initial guess *x<sub>o</sub>*
* tolerance: Smallest residual error before returning
* max_iters: Maximum iterations before returning

### Outputs

* x_new: Final iterative approximation of *x*

### Modules Used

* \<vector\>
* \<cmath\>
* \<omp.h\>

### Code

#### Function

```c++
vector<double> parallel_gauss_seidel(vector<vector<double>> A,vector<double> B,vector<double> guess,double tolerance,int max_iters){
    int n=A.size();
    vector<double> x_new (n,0.0);
    vector<double> x_old=guess;
    double error=10*tolerance;
    int count=0;
    if(n!=A[0].size()){
        cout << "Non square matrix, exiting." <<endl;
        return x_new;
    }
    while(error>tolerance && count < max_iters)
    {
        
        // Update x_k, all rows
        omp_set_num_threads(2);
        int i=0;
#pragma omp parallel private(i)
        {
#pragma omp for
        for(i=0; i<n; i++)
        {
            //do both inner summations
            double first_sum=0.0;
            double second_sum=0.0;
            
            //loop before diagonal
            for (int j=0; j<i; j++)
            {
                first_sum+=A[i][j]*x_new[j];
            }
            
            //loop after diagonal
            for (int j=i+1; j<n; j++)
            {
                second_sum+=A[i][j]*x_old[j];
            }
        
            //Update x_new[i] so it can be used in next iteration
            x_new[i]=(B[i]-first_sum-second_sum)/A[i][i];
        }
        }
        // L2 norm differnce of x_new and x_old (Root-sum-square)
        double sum=0.0;
        double difference=0.0;
        for(int i=0; i<n; i++)
        {
            difference=abs(x_new[i]-x_old[i]);
            sum+=difference*difference;
        }
        error=sqrt(sum);
        count++;
        
        x_old=x_new;
    }
    
    
    return x_new;
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
```

### Example
#### Prompt

```c++
vector<vector<double>> A={ {5.0,2.0,1.0,1.0},{2.0,6.0,2.0,1.0},{1.0,2.0,7.0,1.0},{1.0,1.0,2.0,8.0} };
vector<double> B={29.0,31.0,25.0,19.0};
vector<double> guess(4,0.0);

vector<double> solution=parallel_gauss_seidel(A, B, guess, pow(10,-10),100);

cout << "Matrix A: " << endl;
print_matrix(A);

cout << "Matrix B: " << endl;
print_column(B);

cout << "GS Solution: " << endl;
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
GS Solution: 
|  4  |
|  3  |
|  2  |
|  1  |
```










