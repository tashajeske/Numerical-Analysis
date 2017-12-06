# Computational Mathematics Software Manual

## **Routine Name:** OMPSteepDes

**Author:** Nitasha Jeske

**Language:** C++

**Description:** Steepest Descent is an iterative method to solve a linear system of equations, Ax=b. Using the properties of gradients, this algorithm takes a direction from the starting point and continues iterating until a fixed point is reached. It uses the 2 norm to calculate an error, and uses a tolerance or a max number of iterations to determine the fixed point. This routine is coded to run in Open MP on multiple processors in order to speed up the computing time. 

**Input:**  The input is a symmetric positive definite matrix of size n x n (A), a resulting vector of size n (b), an initial guess vector of size n (x0), a tolerance, and maximum number of iterations.

**Output:** The algorithm returns a vector of doubles, which is the approximate solution, and prints out the number of iterations and the time it takes to compute the resulting vector.

**Code:**
```C++
// function to approximate solution to a linear system using steepest descent gradient method
Vec OMPSteepDes(Matrix A,Vec b, Vec x0, float tol, int maxIter){
    chrono::duration<double> time1;
    auto start = chrono::high_resolution_clock::now();
    // initialize the residual to be b- Ax0 by calling a vector subtraction function and a matrix vector multiplication function
    int n=(int)A.size();
    Vec r0(n);
    Vec Ax0(n,0);
    # pragma omp parallel for
    for (int i=0; i<n; i++){
        for (int j=0; j< n; j++){
            Ax0[i]+=A[i][j]*x0[j];
        }
        r0[i]=b[i]-Ax0[i];
    }   
    // initialize delta0 to be x0^Tx0 or the dot product of x0 and x0
    double delta0=0.0;
    # pragma omp parallel for
    for (int i=0; i<n; i++){
        delta0=delta0+x0[i]*x0[i];
    }
    // initialize b_delta to be b^Tb or the dot product of b and b
    double b_delta=0.0;
    # pragma omp parallel for
    for (int i=0; i<n; i++){
        b_delta=b_delta+b[i]*b[i];
    }
    // initialize counter k
    int k=0;
    // take p0 to be the current residual
    Vec p0=r0;
    // this condition is for the while loop, since it won't be updated in the loop, I will just calculate it once
    double condition=tol*tol*b_delta;
    // initialize this for later
    Vec x1(n);
    // while loop to run the iterations until the tolerance or max iter is met
    while(delta0>condition && k<maxIter){
        // initialize a vctor s_k to be the matrix vector multiplication of A and p0
        Vec s_k(n,0);
        # pragma omp parallel for
        for (int i=0; i<n; i++){
            for (int j=0; j< n; j++){
                s_k[i]+=A[i][j]*p0[j];
            }
        }
        // initialize alpha_k to be delta0 divided by the dot product of p0 and s_k
        float dotp0=0.0;
        # pragma omp parallel for
        for (int i=0; i<n; i++){
            dotp0=dotp0+p0[i]*s_k[i];
        }
        float alpha_k=delta0/dotp0;
        // new guess will be old guess added to p0 scaled by alpha_k
        # pragma omp parallel for
        for (int i=0; i<n;i++){
            x1[i]=x0[i]+p0[i]*alpha_k;
        }
        // calculate new residual
        # pragma omp parallel for
        for (int i=0; i<n;i++){
            r0[i]=r0[i]-s_k[i]*alpha_k;
        }
        // update delta0 based on new residual
        delta0=0.0;
        # pragma omp parallel for
        for (int i=0; i<n; i++){
            delta0=delta0+r0[i]*r0[i];
        }
        // increase counter
        k++;
        // update p0
        p0=r0;
        // update x0
        x0=x1;
    }
    auto end = chrono::high_resolution_clock::now();
    time1 = end-start;
    cout<<"Time: " <<time1.count() <<endl;
    cout << "k = " << k << endl;
    return x0;
}
```

**Example:**

```C++
typedef vector <vector <double>> Matrix;
typedef vector <double> Vec;

int main(){
    int n=1000;
    // initialize a symmetric positive definite matrix
    Matrix A(n, Vec(n));
    for (int i=0; i<n;i++){
        // make the diagonals random but add the number of rows to the matrix to make sure it is diagonally dominant
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
    OMPSteepDes(A, b, x0, .001, 1000);
}
```
**Results:**  
```
Time: 0.0844295
k = 9
```

**Last Modification Date:** Nov. 16, 2017
