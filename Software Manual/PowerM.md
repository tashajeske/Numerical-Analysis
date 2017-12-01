# Computational Mathematics Software Manual

## **Routine Name:** PowerM

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The power method approximates the largest (in absolute value) eigenvalue and the corresponding eigenvector of the matrix.

**Input:**  The input is a symmetric positive definite matrix of size n x n (A), an initial guess at the eigenvector of size n (v0), a tolerance, and maximum number of iterations.

**Output:** The algorithm returns the largest in absolute value of the eigenvalues. 

**Example:**

```C++
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
    // initialize a vector v0 of random numbers between 0 and 1
    Vec v0(n);
    for(int i=0; i<n; i++){
        v0[i]=rand()%100/100.0;
    }
    cout << powerM(A, v0, .0001, 100) << endl;
}
```

**Code:**
```C++
double powerM(Matrix A, Vec v0, double tol, int maxIter){
    // initialize y using matrix vector multiplication function
    Vec y=matrixvec(A, v0);
    // initialize variables
    int c=0;
    double error=10*tol;
    double lambdaOld=0.0;
    int n=(int)v0.size();
    Vec x(n,0);
    double lambdaNew=0.0;
    // loop to approximate eigenvalue
    while(tol<error and c<maxIter){
        // calculate 2 norm
        double p=sqrt(dotprod(y,y));
        // normalize vector x
        for(int i=0; i<n; i++){
            x[i]=y[i]/p;
        }
        // update y
        y=matrixvec(A, x);
        // update eigenvalue
        lambdaNew=dotprod(x,y);
        // calculate error
        error=abs(lambdaNew-lambdaOld);
        // update old lambda
        lambdaOld=lambdaNew;
        c ++;
    }
    Vec eigenV=x;
    return lambdaNew;
}
```

**And the output is as follows:**  
```
994.867
```

**Last Modification Date:**
Nov. 29, 2017