# Computational Mathematics Software Manual

## **Routine Name:** Snewton

**Author:** Nitasha Jeske

**Language:** C++

**Description:** This is a simple version of Newton's method without any bells or whistles. It takes the initial guess given and evaluates the function and derivative to find a closer approximation to the root with each iteration of the loop, until a desired tolerance is met or the max number of iterations is met. 

**Input:** x0 is the initial guess at the root, f and df indicate the desired fucntion and derivative, tol is the allowed tolerance and maxIter is the max number of iterations to be run. 

**Output:** The output is an approximation to the root of type double.

**Example:**
```C++
// functions for approximating roots. use a string to identify which function is called
double func (double x, string f){
if (f=="f1") return x*exp(-x);
else if (f=="df1") return exp(-x)-x*exp(-x);
else return EXIT_SUCCESS;}
int main(){
cout<< "Simple Newton's approximation to the root is: " << Snewton(0.5, "f1", "df1", .0001, 10) <<endl;
}
```

**Code:**
```C++
// xo is initial guess, f and df identify which function and derivative in the func function
double Snewton(double x0, string f, string df, double tol, int maxIter){
//initialize variables, and calculate initial value of function and derivative
double error=10*tol;
int count=0;
double f0=func(x0, f);
double fp0=func(x0,df);
// until the tolerance is less than error or max # of iterations is exceeded
while(error > tol && count < maxIter){
count++;
// identify a closer approximation
double x= x0-f0/fp0;
// find the error
error=abs(x-x0);
//take that point to be the new guess
x0=x;
// evaluate the function and derivative at new guess
f0=func(x0,f);
fp0=func(x0,df);
}
// when the tolerance is less than the error the approximation will be returned
return x0;
}
```

**Results:**  
```C++
Simple Newton's approximation to the root is: -9.38962e-14
```

**Last Modification Date:**
Sep. 30, 2017

