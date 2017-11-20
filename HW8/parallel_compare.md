# Comparing Parallel Iterative Methods

### Last Mod Date
November 16, 2017
### Author
Skyler Wiser
### Written For
C++
### Description
Using the 4 iterative methods written, compare their non-parallel vs parallel times.
### Methods

Using the below functions, approximate cost of floating point operations and also iterations to converge were saved.

* [Jacobi](https://swiser.github.io/MATH4610/HW7/jacobi)
* [Parallel Jacobi](https://swiser.github.io/MATH4610/HW8/parallel_jacobi)
* [Gauss-Seidel](https://swiser.github.io/MATH4610/HW7/gauss_seidel)
* [Parallel Gauss-Seidel](https://swiser.github.io/MATH4610/HW8/parallel_gauss_seidel)
* [Steepest Ascent](https://swiser.github.io/MATH4610/HW7/steepest_ascent)
* [Parallel Steepest Ascent](https://swiser.github.io/MATH4610/HW8/parallel_steepest_ascent)
* [Conjugate Gradient](https://swiser.github.io/MATH4610/HW7/conjugate_gradient)
* [Parallel Conjugate Gradient](https://swiser.github.io/MATH4610/HW8/parallel_conjugate_gradient)


### Modules Used

* \<vector\>
* \<cmath\>
* \<fstream\>
* \<sstream\>
* \<omp.h\>
* \<chrono\>

### Code

#### Helper Functions

```c++
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

vector<double> rand_B(int n){
    vector<double> answer(n,0.0);
    for(int row=0;row<n;row++){
        answer[row]=(double)rand()/RAND_MAX;
    }
    return answer;
}

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

bool answer_compare(vector<double> A,vector<double> B){
    bool compare=true;
    double max1;
    double max2;
    double max_diff=0.0;
    if (A.size()!=B.size()){return false;}
    for(int row=0;row<A.size();row++){
        if(abs(A[row]-B[row])>pow(10,-8)){compare=false;}
        if(abs(A[row]-B[row])>max_diff){
            max_diff=abs(A[row]-B[row]);
            max1=A[row];
            max2=B[row];
        }

    }
   // cout << "Max difference, between (" << max1 << " and " << max2 << "): " << max_diff <<" ";
    return compare;
}
```

#### Main Code

```c++
int main() {
    srand(time(NULL));
    stringstream os;
    
    os << "N,Jacobi,Parallel Jacobi,Gauss-Seidel,Parallel Gauss-Seidel,Steepest,Parallel Steepest,CG,Parallel CG" <<endl;
    
    for(int n=1000; n<10001;n+=1000){
        auto begin=std::chrono::high_resolution_clock::now();

        vector<chrono::microseconds::rep> timings(8,0);
        
        cout << "Size " << n << " Matrix: " <<endl;
        for (int average=0; average<=5; average++){
            
            vector<vector<double>> A=rand_matrix(n);
            vector<double> B=rand_B(n);
            vector<double> guess(n,0.0);
            
            ///Jacobi
            auto start=std::chrono::high_resolution_clock::now();
            vector<double> jacobi_regular=jacobi(A, B, guess, pow(10,-10),100);
            auto end=std::chrono::high_resolution_clock::now();
            timings[0]+=std::chrono::duration_cast<std::chrono::microseconds>(end-start).count();
            
            start=std::chrono::high_resolution_clock::now();
            vector<double> jacobi_parallel=parallel_jacobi(A, B, guess, pow(10,-10),100);
            end=std::chrono::high_resolution_clock::now();
            timings[1]+=std::chrono::duration_cast<std::chrono::microseconds>(end-start).count();
            
            ///Gauss-Seidel
            start=std::chrono::high_resolution_clock::now();
            vector<double> GS_regular=gauss_seidel(A, B, guess, pow(10,-10),100);
            end=std::chrono::high_resolution_clock::now();
            timings[2]+=std::chrono::duration_cast<std::chrono::microseconds>(end-start).count();
            
            start=std::chrono::high_resolution_clock::now();
            vector<double> GS_parallel=parallel_gauss_seidel(A, B, guess, pow(10,-10),100);
            end=std::chrono::high_resolution_clock::now();
            timings[3]+=std::chrono::duration_cast<std::chrono::microseconds>(end-start).count();
            
            //Steepest Ascent
            start=std::chrono::high_resolution_clock::now();
            vector<double> SA_regular=steepest_ascent(A, B, guess, pow(10,-10), 100);
            end=std::chrono::high_resolution_clock::now();
            timings[4]+=std::chrono::duration_cast<std::chrono::microseconds>(end-start).count();

            start=std::chrono::high_resolution_clock::now();
            vector<double> SA_parallel=parallel_steepest_ascent(A, B, guess, pow(10,-10), 100);
            end=std::chrono::high_resolution_clock::now();
            timings[5]+=std::chrono::duration_cast<std::chrono::microseconds>(end-start).count();
            
            
            //Conjugate Gradient
            start=std::chrono::high_resolution_clock::now();
            vector<double> CG_regular=conjugate_gradient(A, B, guess, pow(10,-10), 100);
            end=std::chrono::high_resolution_clock::now();
            timings[6]+=std::chrono::duration_cast<std::chrono::microseconds>(end-start).count();
            
            start=std::chrono::high_resolution_clock::now();
            vector<double> CG_parallel=parallel_conjugate_gradient(A, B, guess, pow(10,-10), 100);
            end=std::chrono::high_resolution_clock::now();
            timings[7]+=std::chrono::duration_cast<std::chrono::microseconds>(end-start).count();
            
            if(average==0){
                (answer_compare(jacobi_regular, jacobi_parallel)&&
                 answer_compare(jacobi_regular, GS_regular)&&
                 answer_compare(jacobi_regular, GS_parallel)&&
                 answer_compare(jacobi_regular, SA_regular)&&
                 answer_compare(jacobi_regular, SA_parallel)&&
                 answer_compare(jacobi_regular, CG_regular)&&
                 answer_compare(jacobi_regular, CG_parallel)
                 ) ? (cout << "All matched. \n") : (cout << "Matrix mismatch! \n");
            }
        }
        os << n <<",";
        for(int i=0; i<8;i++){
            timings[i]/=5.0;
            os<<timings[i];
            if(i!=7){os<<",";}
            else{os <<endl;}
        }
        auto finish=std::chrono::high_resolution_clock::now();
        auto time_taken=std::chrono::duration_cast<std::chrono::milliseconds>(finish-begin).count();
        cout << n <<" complete. Took " << time_taken/1000.0 << " seconds. " <<endl;
    }
    
    ofstream outfile;
    outfile.open("results.csv");
    outfile << os.str();
    outfile.close();
    
    return 0;
}
```

#### Output

```
Size 100 Matrix: 
Size 200 Matrix: 
Size 300 Matrix: 
Size 400 Matrix: 
Size 500 Matrix: 
Size 600 Matrix: 
Size 700 Matrix: 
Size 800 Matrix: 
Size 900 Matrix: 
Size 1000 Matrix: 
Size 1500 Matrix: 
Size 2000 Matrix: 
Size 2500 Matrix: 
Size 3000 Matrix: 
Size 3500 Matrix: 
Size 4000 Matrix: 
Size 4500 Matrix: 
Size 5000 Matrix: 
Size 6000 Matrix: 
Size 7000 Matrix: 
Size 8000 Matrix: 
Size 9000 Matrix: 
Size 10000 Matrix: 
```
### Results

The number of floating point operations was plotted against the size *n* of the matrix. With the plot being log-log, the slope of each should show that each is close to *O(n<sup>2</sup>)* in complexity, as shown by the black line.

![Flop Comparison](https://swiser.github.io/MATH4610/HW8/parallelcomparison.png)







