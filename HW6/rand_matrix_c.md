# Function Name: rand_matrix()

### Last Mod Date
October 18, 2017
### Author
Skyler Wiser
### Written For
C++
### Description
Generates a random matrix of double precision numbers. Matrix is std::vector<vector\<double\>> format.
### Inputs

* rows: integer number of rows in matrix
* cols: integer number of columns in matrix

### Outputs

* answer: a matrix of numbers

### Modules Used

* \<vector\>

### Notes

Uses a small function to generate random double precision numbers. Function is included below in code.

### Code

```c++
double rand_number(){
return 100*(double)rand() / RAND_MAX;
}

vector<vector<double>> rand_matrix(int rows,int cols){
    vector<vector<double>> answer(rows,{0});
    for(int r=0;r<rows;r++){
        vector<double>temp_row(cols,0.0);
        for(int c=0;c<cols;c++){
            temp_row[c]=rand_number();
        }
        answer[r]=temp_row;
    }
    return answer;
}
```

### Example
#### Prompt

```c++
vector<vector<double> > matrixA=rand_matrix(100,100);
```
