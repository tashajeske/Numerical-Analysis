# Computational Mathematics Software Manual

## **Routine Name:** PolyInterp

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The Polynomial Interpolation routine will evaluate the polynomial found using Newton's method at a point that does not exist in the data set. It does this by calling the Divided Differnce Table function to calculate the coefficients of the polynomial and then interpolating to points not in the data set. 

**Input:**  Two vectors x and y representing the data set are inputs to the function and a point at which to iterpolate of type double.

**Output:**  The outpute is a double which represents the value of the function evaluated at the given point.

**Example:**

```C++
// divide an interval from -1 to 1 n times
Vec x(int n){
    Vec x(n+1);
    for (int i=0; i<n+1; i++){
        x[i]=-1.0+2.0/n*i;
    }
    return x;
}

// Runge's phenomenon function
Vec func(Vec x){
    Vec y(x.size());
    for (int i=0; i<x.size(); i++){
        y[i]=1/(1+25*pow(x[i],2));
    }
    return y;
}

int main(){
    cout<<PolyInterp({1,2,4},{1,3,3},1.5)<< endl;
    cout << PolyInterp(x(5), func(x(5)), .25) <<endl;
    cout << PolyInterp(x(10), func(x(10)), .25) << endl;
    cout << PolyInterp(x(20), func(x(20)), .25) << endl;
    cout << PolyInterp(x(50), func(x(50)), .25) << endl;
    cout << PolyInterp(x(100), func(x(100)), .25) << endl;
    cout << PolyInterp(x(200), func(x(200)), .25) << endl;
    cout << PolyInterp(x(500), func(x(500)), .25) << endl;
    cout << PolyInterp(x(1000), func(x(1000)), .25) << endl;
}
```

**Code:**
```C++
double PolyInterp (Vec x, Vec y, double t){
    // need coefficients so call Divided Difference Table function to calculate them
    Vec coeff=DividedDiffTable(x, y);
    // intialize variables
    double eval=0.0;
    int n=(int)x.size();
    // loop to evaluate the function created using the coefficients and vector x with a given t
    // f(x)=c0+c1(t-x0)+c2(t-x0)(t-x1)+...
    for (int i=0; i<n; i++){
        // start with the coefficient
        double temp=coeff[i];
        // then multiply in t-x0 or however many needed factors
        for (int j=0; j<i; j++){
            temp=temp*(t-x[j]);
        }
        // add up all the temp variables to get the final value
        eval+=temp;
    }
    return eval;
}
```

**And the output is as follows:**  
```
1  2  -0.666667
0.0384615  0.153846  0.432692  -0.707799  0.5441 
```

**Last Modification Date:**
Nov. 30, 2017
