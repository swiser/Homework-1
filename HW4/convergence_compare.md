# Project: Compare Matrix-Matrix Multiplication

### Last Mod Date
October 2, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description

Using multiple methods to calculate matrix-matrix multiplication, in both C++ and Python 2.7, functions were timed and averaged for different NxN matrices to show the effects of parallelization using openMP. Using values of N ranging from 10 to 2000, and timing each function several times (using different random matrices each time), average times were generated for each function and plotted on a log-log graph. Depending on the time required for each function to run, 3-20 timings were used to generate averages. For Python, 2D list matrices were only tested up to N=500 due to the time required. Similarly, with C++, 2D vectors were only tested up to N=1000.

### Functions Used

* C++
  * [rand_matrix()](https://swiser.github.io/MATH4610/HW6/rand_matrix_c)
  * [matrixCompare()](https://swiser.github.io/MATH4610/HW6/matrix_compare_c)
  * [matrix_multiply()](https://swiser.github.io/MATH4610/HW6/matrix_multiply_c)
  * [vector_openmp_matrix()](https://swiser.github.io/MATH4610/HW6/vector_openmp_matrix)
  * [normal_openmp_matrix()](https://swiser.github.io/MATH4610/HW6/normal_openmp_matrix)
  * [transposed_openmp_matrix()](https://swiser.github.io/MATH4610/HW6/transposed_openmp_matrix)
* Python
  * rand_matrix()
  * matrix_matrix_product()
  * numpy_matrix_compare()

### Modules Used

* C++
  * \<vector\>
  * \<chrono\>
  * \<omp.h\>
  * \<fstream\>
* Python
  * numpy
  * time
  * random

### Timing Example
Times were saved in microseconds (10^-6) to easily preserve digits of accuracy when converting to strings.
* Python

```python
start=time.time()
numpyC=numpyA*numpyB
end=time.time()
elapsed=(end-start)*10**6
```

* C++

```c++
start=std::chrono::high_resolution_clock::now();
auto matrixC=matrix_multiply(matrixA,matrixB);
end=std::chrono::high_resolution_clock::now();
elapsed=std::chrono::duration_cast<std::chrono::microseconds>(end-start).count();
```
* answer: a matrix of numbers



### Graph

Using a log-log graph, we can see that the matrix-matrix operation is an order N<sup>3</sup> operation. The solid black line is a reference to a purely cubic function, with an arbitrary coefficient to show the trend is order N<sup>3</sup>. Because the test was ran on a dual-core computer, results using 4 and 8 threads were not faster than parallelizing with 2 threads. All graphed openMP values used 2 threads.

![Matrix Matrix Graph](https://swiser.github.io/MATH4610/HW6/Matrix_matrix_annotated_small.png)
[Hi-Res Link](https://swiser.github.io/MATH4610/HW6/Matrix_matrix_annotated.png)
