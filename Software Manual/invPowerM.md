# Computational Mathematics Software Manual

## **Routine Name:** invPowerM

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The inverse power iteration/method approximates the largest (in absolute value) eigenvalue and the corresponding eigenvector of the matrix.

**Input:**  The input is a symmetric positive definite matrix of size n x n (A), an initial guess at the eigenvector of size n (v0), a tolerance, and maximum number of iterations.

**Output:** The algorithm prints the time it takes to run and then returns the largest in absolute value of the eigenvalues of type double. 

**Code:**
```C++
double invPowerM (Matrix A, Vec v0, double tol, int maxIter){
    Vec y=ConjGrad(A, v0, v0, tol, maxIter);
    // initialize variables
    int c=0;
    double error=10*tol;
    double lambdaOld=0.0;
    int n=(int)y.size();
    Vec x(n,0);
    double lambdaMax=0.0;
    // loop to approximate eigenvalue
    while(tol<error and c<maxIter){
        // calculate 2 norm
        double p=sqrt(dotprod(y,y));
        // normalize vector
        for(int i=0; i<n; i++){
            x[i]=y[i]/p;
        }
        // use conjgrad to calculate "inverse"
        y = ConjGrad(A, x, x, tol, maxIter);
        // update eigenvalue
        lambdaMax=dotprod(x,y);
        // calculate error
        error=abs(lambdaMax-lambdaOld);
        // update old lambda
        lambdaOld = lambdaMax;
        c++;
    }
    Vec eigenV=x;
    // report inverse of eigenvalue since we took eigenvalue of inverse matrix
    return 1.0/lambdaMax;
}
```

**Example:**

```C++
typedef vector <vector <double>> Matrix;
typedef vector <double> Vec;

// function to calculate matrix vector multiplication
Vec matrixvec (Matrix A, Vec v1){
    Vec prod;
    for (int i=0; i<A[0].size(); i++){
        prod.push_back(0);
    }
    for (int i=0; i<A.size(); i++){
        for (int j=0; j< v1.size(); j++){
            prod[i]+=A[i][j]*v1[j];
        }
    }
    return prod;
}
// function to calculate dot product
double dotprod(vector <double> vec1, vector <double> vec2){
    double sum=0.0;
    for (int i=0; i<vec1.size(); i++){
        sum=sum+vec1[i]*vec2[i];
    }
    return sum;
}
// function to calculate scalar multiplied by a vector
Vec scavec (Vec v1, float a){
    int n=(int)v1.size();
    for (int i=0; i<n;i++){
        v1[i]=v1[i]*a;
    }
    return v1;
}
// function to add two vectors
Vec vecadd (Vec v1, Vec v2){
    for (int i=0; i<v1.size(); i++){
        v1[i]=v1[i]+v2[i];
    }
    return v1;
}
// function to subtract one vector from another
Vec vecsub (Vec v1, Vec v2){
    for (int i=0; i<v1.size(); i++){
        v1[i]=v1[i]-v2[i];
    }
    return v1;
}
// function to approximate solution to a linear system using conjugate gradient method
Vec ConjGrad(Matrix A,Vec b, Vec x0, float tol, int maxIter){
    // initialize the residual to be b- Ax0 by calling a a vector subtraction function and a matrix vector multiplication function
    Vec r0=vecsub(b, matrixvec(A, x0));
    // initialize delta0 to be r0^Tr0 or the dot product of r0 and r0
    double delta0=dotprod(r0, r0);
    // initialize b_delta to be b^Tb or the dot product of b and b
    float b_delta=dotprod(b,b);
    // initialize counter k
    int k=0;
    // take p0 to be the current residual
    Vec p0=r0;
    // this condition is for the while loop, since it won't be updated in the loop, I will just calculate it once
    double condition=tol*tol*b_delta;
    // while loop to run the iterations until the tolerance or max iter is met
    while(delta0 > condition && k<maxIter){
        // initialize a vctor s_k to be the matrix vector multiplication of A and p0
        Vec s_k=matrixvec(A, p0);
        // initialize alpha_k to be delta0 divided by the dot product of p0 and s_k
        float alpha_k=delta0/dotprod(p0,s_k);
        // new guess will be old guess added to p0 scaled by alpha_k
        Vec x1=vecadd(x0, scavec(p0, alpha_k));
        // calculate new residual
        r0=vecsub(r0, scavec(s_k, alpha_k));
        // initialize new delta to be dot product of new residuals
        double delta1=dotprod(r0, r0);
        // initialize a scalar to be ratio of new/old delta
        float scalar=delta1/delta0;
        // update p0 based on new residual and calculated scalar
        p0=vecadd(r0, scavec(p0, scalar));
        // increase counter
        k++;
        // set old x to be new x
        x0=x1;
        // set old delta to be new delta
        delta0=delta1;
    }
    return x0;
}
int main(){
    int n=1000;
    Matrix A(n, Vec(n));
    for (int i=0; i<n;i++){
        // make the diagonals random but add the number of rows to the matrix to make sure it is diagonally     dominant
        A[i][i]=rand()%100/100.0+500;
        for (int j=0; j<i; j++){
            // create random entries for the lower diagonal
            A[i][j]=rand()%100/100.0;
            // set the corresponding transpose entries equal so that it is symmetric
            A[j][i]=A[i][j];
        }
    }
    // initialize a vector v0 of random numbers between 0 and 1
    Vec v0(n);
    for(int i=0; i<n; i++){
        v0[i]=rand()%100/100.0;
    }
    cout << invpowerM(A, v0, .0001, 100) << endl;
}
```


**Results:**  
```
0.559576
501.713
```

**Last Modification Date:** Nov. 29, 2017
