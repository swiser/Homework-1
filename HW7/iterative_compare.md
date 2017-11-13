# Comparing Iterative Methods

### Last Mod Date
November 12, 2017
### Author
Skyler Wiser
### Written For
C++
### Description
Using the 4 iterative methods written, compare their cost.
### Methods

Using slightly modified versions of the below functions, approximate cost of floating point operations and also iterations to converge were saved.

* [Jacobi](https://swiser.github.io/MATH4610/HW7/jacobi)
* [Gauss-Seidel](https://swiser.github.io/MATH4610/HW7/gauss_seidel)
* [Steepest Ascent](https://swiser.github.io/MATH4610/HW7/steepest_ascent)
* [Conjugate Gradient](https://swiser.github.io/MATH4610/HW7/conjugate_gradient)

### Modules Used

* \<vector\>
* \<cmath\>
* \<fstream\>
* \<sstream\>

### Code

#### Additional Structures

```c++
struct cost{
    int n;
    int cost;
    int iteration;
};

vector<cost> J;
vector<cost> GS;
vector<cost> SA;
vector<cost> CG;
```

#### Modified Functions (Long!)

```c++

///////////////////////////////////////////////////////
///////////////    Simple Iterative     ///////////////
///////////////////////////////////////////////////////


vector<double> jacobi(vector<vector<double>> A,vector<double> B,vector<double> guess,double tolerance,int max_iters){
    int flops=0;
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
        //Save computing time by setting x_k to B, subtract from it.
        x_new=B;
        
        // Update x_k, all rows
        for(int i=0; i<n; i++)
        {
            //loop before diagonal
            for (int j=0; j<i; j++)
            {
                x_new[i]=x_new[i]-A[i][j]*x_old[j];
                flops++;
            }
            
            //loop after diagonal
            for (int j=i+1; j<n; j++)
            {
                x_new[i]=x_new[i]-A[i][j]*x_old[j];
                flops++;
            }
        }
        
        // Suedo-back sub, divide diagonal term over
        
        for(int i=0; i<n; i++)
        {
            x_new[i]=x_new[i]/A[i][i];
            flops++;
        }
        
        // L2 norm differnce of x_new and x_old (Root-sum-square)
        double sum=0.0;
        double difference=0.0;
        for(int i=0; i<n; i++)
        {
            difference=abs(x_new[i]-x_old[i]);
            sum+=difference*difference;
            flops++;
        }
        error=sqrt(sum);
        flops++;
        
        x_old=x_new;
        count++;
    }
    
    cost result;
    result.cost=flops;
    result.iteration=count;
    result.n=n;
    J.push_back(result);
    
    return x_new;
}

vector<double> gauss_seidel(vector<vector<double>> A,vector<double> B,vector<double> guess,double tolerance,int max_iters){
    int flops=0;
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
        for(int i=0; i<n; i++)
        {
            //do both inner summations
            double first_sum=0.0;
            double second_sum=0.0;
            
            //loop before diagonal
            for (int j=0; j<i; j++)
            {
                first_sum+=A[i][j]*x_new[j];
                flops++;
            }
            
            //loop after diagonal
            for (int j=i+1; j<n; j++)
            {
                second_sum+=A[i][j]*x_old[j];
                flops++;
            }
            //Update x_new[i] so it can be used in next iteration
            x_new[i]=(B[i]-first_sum-second_sum)/A[i][i];
            flops++;
        }
        
        
        // L2 norm differnce of x_new and x_old (Root-sum-square)
        double sum=0.0;
        double difference=0.0;
        for(int i=0; i<n; i++)
        {
            difference=abs(x_new[i]-x_old[i]);
            sum+=difference*difference;
            flops++;
        }
        error=sqrt(sum);
        count++;
        
        x_old=x_new;
    }
    
    cost result;
    result.cost=flops;
    result.iteration=count;
    result.n=n;
    GS.push_back(result);
    return x_new;
}



///////////////////////////////////////////////////////
///////////////     Steepest Ascent     ///////////////
///////////////////////////////////////////////////////



vector<double> steepest_ascent(vector<vector<double>> A,vector<double> B,vector<double> guess,double tolerance,int max_iters){
    int flops=0;
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
    for(int i=0; i<n; i++)
    {
        //Matrix-Vector Multiplication
        double sum=0.0;
        for(int col=0; col<n;col++){
            sum+=A[i][col]*guess[col];
            flops++;
        }
        residual[i]-=sum;
    }
    
    double deltaK=inner_product(residual,residual);
    double b_delta=inner_product(B,B);
    flops+=2*n;
    
    while (error>(tolerance*tolerance*b_delta) && count<max_iters)
    {
        ///Set s_k, matrix-vector math
        vector<double> s_k(n,0.0);
        for(int i=0; i<n; i++)
        {
            double sum=0.0;
            for(int col=0;col<n;col++)
            {
                sum+=A[i][col]*residual[col];
                flops++;
            }
            s_k[i]=sum;
        }
        
        //determine alpha
        double alpha=deltaK/inner_product(residual, s_k);
        flops+=n;
        
        //Update x vector
        for(int i=0; i<n; i++){x_old[i]=x_old[i]+alpha*residual[i];}
        flops+=n;
        
        //Update R vector
        for(int i=0; i<n; i++){residual[i]=residual[i]-alpha*s_k[i];}
        flops+=n;
        
        deltaK=inner_product(residual,residual);
        flops+=n;
        error=deltaK;
        count++;
        
    }
    
    cost result;
    result.cost=flops;
    result.iteration=count;
    result.n=n;
    SA.push_back(result);
    return x_old;
}


///////////////////////////////////////////////////////
///////////////   Conjugate Gradient    ///////////////
///////////////////////////////////////////////////////


vector<double> conjugate_gradient(vector<vector<double>> A,vector<double> B,vector<double> guess,double tolerance,int max_iters){
    int flops=0;
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
    for(int i=0; i<n; i++)
    {
        //Matrix-Vector Multiplication
        double sum=0.0;
        for(int col=0; col<n;col++){
            sum+=A[i][col]*guess[col];
            flops++;
        }
        residual[i]-=sum;
    }
    
    double deltaK_old=inner_product(residual,residual);
    flops+=n;
    double deltaK_new=0.0;
    double b_delta=inner_product(B,B);
    flops+=n;
    vector<double> p_k=residual;
    
    vector<double> s_k(n,0.0);
    while (error>(tolerance*tolerance*b_delta) && count<max_iters)
    {
        ///Set s_k, matrix-vector math
        for(int i=0; i<n; i++)
        {
            double sum=0.0;
            for(int col=0;col<n;col++)
            {
                sum+=A[i][col]*p_k[col];
                flops++;
            }
            s_k[i]=sum;
        }
        
        //determine alpha
        double alpha=deltaK_old/inner_product(p_k, s_k);
        flops+=n;
        //Update x vector
        for(int i=0; i<n; i++){x_old[i]=x_old[i]+alpha*p_k[i];}
        flops+=n;
        //Update R vector
        for(int i=0; i<n; i++){residual[i]=residual[i]-alpha*s_k[i];}
        flops+=n;
        deltaK_new=inner_product(residual,residual);
        flops+=n;
        //Update p_k vector
        for(int i=0; i<n; i++){p_k[i]=residual[i]+deltaK_new/deltaK_old*p_k[i];}
        flops+=n;
        error=deltaK_new;
        deltaK_old=deltaK_new;
        count++;
        
    }
    
    cost result;
    result.cost=flops;
    result.iteration=count;
    result.n=n;
    CG.push_back(result);
    return x_old;
}
```

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
srand(time(NULL));
int n=100;
while (n<=10000){
    vector<vector<double>> A=rand_matrix(n);
    vector<double> B=rand_B(n);
    vector<double> guess(n,0.0);

    cout << "Size " << n << " Matrix: ";
    vector<double> solution=jacobi(A, B, guess, pow(10,-10),100);
    vector<double> solution2=gauss_seidel(A, B, guess, pow(10,-10),100);
    vector<double> solution3=steepest_ascent(A, B, guess, pow(10,-10), 100);
    vector<double> solution4=conjugate_gradient(A, B, guess, pow(10,-10), 100);
    //This line compares every method's solution back to jacobi, and if the solutions don't match it will print an error to the screen to let you know something went wrong.
    (answer_compare(solution, solution2)&&answer_compare(solution, solution3)&&answer_compare(solution, solution4)) ? (cout << "\n") : (cout << "Matrix mismatch! \n");
    if(n<1000){n+=100;}
    else if (n>=1000 && n<5000){n+=500;}
    else {n+=1000;}
}
stringstream os;

os << "N,Jacobi,Jacobi,Gauss-Seidel,Gauss-Seidel,Steepest,Steepest,CG,CG" <<endl;
os << "N,flops,iterations,flops,iterations,flops,iterations,flops,iterations" <<endl;
for(int i=0; i<J.size(); i++){
    os << J[i].n<<",";
    os << J[i].cost << "," << J[i].iteration << ",";
    os << GS[i].cost << "," << GS[i].iteration << ",";
    os << SA[i].cost << "," << SA[i].iteration << ",";
    os << CG[i].cost << "," << CG[i].iteration << endl 
}
ofstream outfile;
outfile.open("results.csv");
outfile << os.str();
outfile.close();
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

![Flop Comparison](https://swiser.github.io/MATH4610/HW7/iterative_comparison.png)








