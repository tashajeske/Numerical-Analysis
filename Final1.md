
# Math 4610 Take Home Final

## Nitasha Jeske

## Problem 1: 

** #3 on page 211 of text**

Using routines from previous homework assignments, two iterations using Jacobi and one iteration using Gauss-Seidel have been computed on the given linear system and initial guess x0. The code used to compute this specific example is shown below and the software manual entries for the routines are attached following this page. The results are also included below, which show us that the error, l1, is .6 for one iteration of Jacobi, .12 for two iterations of Jacobi, and .308 for one iteration of Gauss-Seidel. Clearly, Gauss-seidel has a smaller error for one iteration. Thus, Gauss-Seidel converges faster. 

**Example:**
```C++
int main(){
    Vec Jvec1=Jacobi({{10,1,1},{1,10,1},{1,1,10}}, {12,12,12}, {0,0,0}, .001, 1);
    Vec Jvec2=Jacobi({{10,1,1},{1,10,1},{1,1,10}}, {12,12,12}, {0,0,0}, .001, 2);
    Vec Gvec=GaussSeidel({{10,1,1},{1,10,1},{1,1,10}}, {12,12,12}, {0,0,0}, .001, 1);
    Print(Jvec1);
    Print(Jvec2);
    Print(Gvec);
    cout<< Verror1(Jvec1, {1,1,1})<< endl;
    cout<< Verror1(Jvec2, {1,1,1})<< endl;
    cout<< Verror1(Gvec, {1,1,1})<< endl;
}
```
**Results:**
```C++
k = 1
k = 2
k = 1
1.2  1.2  1.2  
0.96  0.96  0.96  
0.972  1.08  1.2  
0.6
0.12
0.308
```



## Problem 5:

** #4 on page 325 of text **

ughhh analysis

## Problem 6:

** #10 on page 326 of text

## Problem 7:

** Implement the fast Fourier transform and apply to the problem in example 13.3. Use 32, 64, and 128 samples.


