# Function Name: power_method()

### Last Mod Date
November 19, 2017
### Author
Skyler Wiser
### Written For
C++
### Description
Use power iteration to find the largest eigenvalue of a matrix.
### Inputs

* A: Matrix A to find eigenvalue of
* v0: Initial guess of eigenvector
* max_iters: Maximum iterations before returning
* tolerance: Smallest difference in eigenvalue approximations before returning

### Outputs

* lambda_old: The last iterative estimate of the largest eigenvalue of matrix A

### Modules Used

* \<vector\>
* \<cmath\>
* \<omp.h\>

### Code

#### Function

```c++
double power_method(vector<vector<double>> A, vector<double> v0, int max_iters,double tolerance){
    int n=A.size();
    vector<double> y(n,0.0);
    vector<double> x(n,0.0);
    int i=0;
    omp_set_num_threads(2);
#pragma omp parallel private(i)
    {
#pragma omp for
        for(i=0;i<n;i++){
            double sum=0.0;
            for(int j=0; j<n;j++){
                sum+=A[i][j]*v0[j];
            }
            y[i]=sum;
        }
    }
    double lambda_old=0.0;
    double error=10*tolerance;
    int count =0;
    while(error>tolerance && count <max_iters){
        double magnitude=0;
        //find vector magnitude, normalize and store in x
        for(int i=0; i<n;i++){
            magnitude+=y[i]*y[i];
        }
        magnitude=pow(magnitude,.5);
        for(int i=0; i<n;i++){
            x[i]=y[i]/magnitude;
        }
        //perform matrix-vector calculation for A*vK which is A*x, store as S
        vector<double> s(n,0.0);
    
#pragma omp parallel private(i)
        {
#pragma omp for
            for(i=0;i<n;i++){
                double sum=0.0;
                for(int j=0; j<n;j++){
                    sum+=A[i][j]*x[j];
                }
                s[i]=sum;
            }
        }
        //generate the eigenvalue, by doing xT*S
        double lambda_new=0.0;
        for(int i=0; i<n;i++){
            lambda_new+=x[i]*s[i];
        }
        
        error=abs(lambda_new-lambda_old);
        y=s;
        lambda_old=lambda_new;
        count++;
    }
    return lambda_old;
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

vector<vector<double>> rand_matrix(int n){
    vector<vector<double>> answer (n,vector<double>(n,0.0));
    for(int row=0;row<n;row++){
        answer[row][row]=2*n+(double)rand()/RAND_MAX;
        for(int col=0;col<row;col++){
            answer[row][col]=(double)rand()/RAND_MAX;
            answer[col][row]=answer[row][col];
            
        }
    }
    return answer;
}
```

### Example
#### Prompt

```c++
    vector<vector<double>> not_diagonally_dominant={ {3,12,5},{4,5,13},{10,3,4} };
    vector<vector<double>> diagonally_dominant={ {10,3,4},{3,12,5},{4,5,13} };
    vector<vector<double>> guess_dependency={ {-2,-2,3},{-10,-1,6},{10,-2,-9} };
    
    vector<double> guess_1={1,1,1};
    vector<double> guess_2={1,0,0};
    
    cout << "Diagonally dominant: " << endl;
    print_matrix(diagonally_dominant);
    
    cout << "Not diagonally dominant: " <<endl;
    print_matrix(not_diagonally_dominant);
    
    cout << "Dependent on guess: " <<endl;
    print_matrix(guess_dependency);
    
    double max_diag_dom=power_method(diagonally_dominant,guess_1,100,pow(10,-10));
    double max_not_diag_dom=power_method(not_diagonally_dominant,guess_1,100,pow(10,-10));
    
    double bad_guess_max=power_method(guess_dependency,guess_1,100,pow(10,-10));
    double good_guess_max=power_method(guess_dependency,guess_2,100,pow(10,-10));
    
    double max_largeMatrix=power_method(rand_matrix(1000),vector<double>(1000,1.0),100,pow(10,-10));
    
    cout <<endl;
    cout << "Diagonally Dominant, largest eigenvalue: " << max_diag_dom <<endl<<endl;
    cout << "Not Diagonally Dominant, largest eigenvalue: " << max_not_diag_dom <<endl<<endl;
    cout << "Bad guess, largest eigenvalue: " << bad_guess_max <<endl<<endl;
    cout << "Good guess, largest eigenvalue: " << good_guess_max <<endl<<endl;
    cout << "Large Matrix, largest eigenvalue: " << max_largeMatrix <<endl<<endl;
    
```

#### Output

```
Diagonally dominant: 
|        10           3           4  |
|         3          12           5  |
|         4           5          13  |
Not diagonally dominant: 
|         3          12           5  |
|         4           5          13  |
|        10           3           4  |
Dependent on guess: 
|        -2          -2           3  |
|       -10          -1           6  |
|        10          -2          -9  |

Diagonally Dominant, largest eigenvalue: 20.0064
Not Diagonally Dominant, largest eigenvalue: 19.5413
Bad guess, largest eigenvalue: -2.33333
Good guess, largest eigenvalue: -12
Large Matrix, largest eigenvalue: 2499.38
```









