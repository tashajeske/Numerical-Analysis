# Computational Mathematics Software Manual

## **Routine Name:** OMPConjGrad

**Author:** Nitasha Jeske

**Language:** C++

**Description:** Conjugate Gradient is an iterative method to solve a linear system of equations, Ax=b. Using the properties of gradients, this algorithm takes a direction from the starting point and continues iterating in an orthogonal direction until a fixed point is reached. It uses the 2 norm to calculate an error, and uses a tolerance or a max number of iterations to determine the fixed point. This routine is coded to run in Open MP on multiple processors in order to speed up the computing time. 

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
        A[i][i]=rand()%100/100.0+1000;
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

**Code:**
```C++
// function to approximate solution to a linear system using conjugate gradient method
Vec OMPConjGrad(Matrix A,Vec b, Vec x0, float tol, int maxIter){
    chrono::duration<double> time1;
    auto start = chrono::high_resolution_clock::now();
    int n=(int)A.size();
    // initialize this for later
    Vec x1(n);
    // initialize the residual to be b- Ax0 by calling a a vector subtraction function and a matrix vector multiplication function
    Vec r0(n);
    # pragma omp parallel for
    for (int i=0; i<n; i++){
        float temp=0.0;
        for (int j=0; j< n; j++){
            temp+=A[i][j]*x0[j];
        }
        r0[i]=b[i]-temp;
    }
    // initialize delta0 to be r0^Tr0 or the dot product of r0 and r0
    double delta0=0.0;
    for (int i=0; i<n; i++){
        delta0=delta0+r0[i]*r0[i];
    }
    // initialize b_delta to be b^Tb or the dot product of b and b
    double b_delta=0.0;
    for (int i=0; i<n; i++){
        b_delta=b_delta+b[i]*b[i];
    }
    // initialize counter k
    int k=0;
    // take p0 to be the current residual
    Vec p0=r0;
    // this condition is for the while loop, since it won't be updated in the loop, I will just calculate it once
    double condition=tol*tol*b_delta;
    // while loop to run the iterations until the tolerance or max iter is met
    while(delta0 > condition && k<maxIter){
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
        for (int i=0; i<n; i++){
            dotp0=dotp0+p0[i]*s_k[i];
        }
        float alpha_k=delta0/dotp0;
        // new guess will be old guess added to p0 scaled by alpha_k
        for (int i=0; i<n;i++){
            x1[i]=x0[i]+p0[i]*alpha_k;
        }
        // calculate new residual
        for (int i=0; i<n;i++){
            r0[i]=r0[i]-s_k[i]*alpha_k;
        }
        // initialize new delta to be dot product of new residuals
        double delta1=0.0;
        for (int i=0; i<n; i++){
            delta1=delta1+r0[i]*r0[i];
        }
        // initialize a scalar to be ratio of new/old delta
        float scalar=delta1/delta0;
        // update p0 based on new residual and calculated scalar
        for (int i=0; i<n;i++){
            p0[i]=r0[i]+p0[i]*scalar;
        }
        // increase counter
        k++;
        // set old x to be new x
        x0=x1;
        // set old delta to be new delta
        delta0=delta1;
    }
    auto end = chrono::high_resolution_clock::now();
    time1 = end-start;
    cout<<"Time: " <<time1.count() <<endl;
    cout << "k = " << k << endl;
    return x0;
}

```

**And the output is as follows:**  
```
Time: 0.002526
k = 4
```

**Last Modification Date:**
Nov. 16, 2017
