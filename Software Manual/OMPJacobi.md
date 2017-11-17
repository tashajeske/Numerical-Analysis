# Computational Mathematics Software Manual

## **Routine Name:** OMPJacobi

**Author:** Nitasha Jeske

**Language:** C++

**Description:** Jacobi iteration is an iterative method to solve a linear system of equations, Ax=b. Using the properties of linear algebra, this algorithm calculates D^-1(b-(L+U)x) and uses the 2 norm to calculate an error, then iterates until it reaches the desired tolerance or hits a maximum number of iterations. This routine is coded to run in Open MP on multiple processors in order to speed up the computing time. 


**Input:**  The input is a symmetric positive definite matrix of size n x n (A), a resulting vector of size n (b), an initial guess vector of size n (x0), a tolerance, and maximum number of iterations.

**Output:** The algorithm returns a vector, which is the approximate solution, and prints out the number of iterations and the time it takes to compute the resulting vector.

**Example:**

```C++
int main(){
    typedef vector <vector <double>> Matrix;
    typedef vector <double> Vec;
    int n=1000;
    // initialize a symmetric positive definite matrix
    Matrix A(n, Vec(n));
    for (int i=0; i<n;i++){
        // make the diagonals random but add the number of rows to the matrix to make sure it is diagonally dominant
        A[i][i]=rand()%100/100.0+500;
        for (int j=0; j<i; j++){
            // create random entries for the lower diagonal
            A[i][j]=rand()%100/100.0;
            // set the corresponding transpose entries equal so that it is symmetric
            A[j][i]=A[i][j];
        }
    }
    // initialize a vector b of random numbers between 0 and 1
    Vec b(n);
    for (int i=0; i<n; i++){
        b[i]=rand()%100/100.0;
    }
    // initialize a vector x0 of random numbers between 0 and 1
    Vec x0(n);
    for(int i=0; i<n; i++){
        x0[i]=rand()%100/100.0;
    }
    OMPJacobi(A, b, x0, .001, 1000);
}
```

**Code:**
```C++
Vec OMPJacobi(Matrix A, Vec b, Vec x0, float tol, int maxIter){
    chrono::duration<double> time1;
    auto start = chrono::high_resolution_clock::now();
    // let n count the rows in the matrix A
    int n=(int)A.size();
    // initialize a vector of size n to be all zeros
    Vec x1(n,0);
    // initialize error so that the while loop will run
    double error=10*tol;
    // start a count for number of times through while loop
    int cnt=0;
    // when error is still greater than tolerance and count is less than max iterations
    // the the loop will go and find closer approximations to the system Ax=b
        while (error > tol && cnt <maxIter){
        # pragma omp parallel for
        // nested for loop to calculate b-(L+U)x
        for (int i=0; i<n; i++){
            double temp=0.0;
            // calculate Lx
            for (int j=0; j<i; j++){
                temp+=A[i][j]*x0[j];
            }
            // subtract Lx from b and do action of D^-1
            x1[i]=(b[i]-temp)/A[i][i];
            // calculate Ux
            for (int j=i+1; j<n; j++){
                temp+=A[i][j]*x0[j];
            }
            // subtract Ux from b and do action of D^-1
            x1[i]=(b[i]-temp)/A[i][i];
        }
        // initialize a temp variable sum to be zero
        double sum=0.0;
        # pragma omp parallel for
        // this loop sets up the L2 norm
        for (int i=0; i<n; i++){
            //find the absolute value difference between vectors at each entry
            double diff=abs(x1[i]-x0[i]);
            // add up these differences
            sum=sum+diff*diff;
        }
        // take the square root for the error or L2 norm
        error=sqrt(sum);
        // update the old x vector to be the new x vector
        x0=x1;
        cnt++;
    }
    auto end = chrono::high_resolution_clock::now();
    time1 = end-start;
    cout<<"Time: " <<time1.count() <<endl;
    cout << "k = " << cnt << endl;
    return x0;
}
```

**And the output is as follows:**  
```
Time: 0.00799
k = 16
```

**Last Modification Date:**
Nov. 16, 2017
