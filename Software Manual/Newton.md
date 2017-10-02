# Computational Mathematics Software Manual

## **Routine Name:** Newton

**Author:** Nitasha Jeske

**Language:** C++

**Description:** This version of Newton's method contains checks to make sure the initial guess is valid with the given function. It will approximate the root by evaluating the function and derivative at the inital guess, and take that value to be the new guess. While doing that, the routine checks to make sure the derivative is non-zero and the sequence is converging within the interval. 

**Input:** x0 is the initial guess at the root, f and df indicate the desired fucntion and derivative, tol is the allowed tolerance and maxIter is the max number of iterations to be run. 

**Output:** The output is an approximation to the root of type double, or an error message telling you to pick a different initial guess. 

**Example:**
```C++
// functions for approximating roots. use a string to identify which function is called
double func (double x, string f){
if (f=="f1") return x*exp(-x);
else if (f=="f2") return 3*x*sin(10*x);
else if (f=="f3") return x*cos(10*x);
else if (f=="df1") return exp(-x)-x*exp(-x);
else if (f=="df2") return 3*sin(10*x)+30*x*cos(10*x);
else if (f=="df3")return cos(10*x)-10*x*sin(10*x);
else return EXIT_SUCCESS;}
int main(){
cout<< "Newton's approximation to the root is: " << newton(1.0, "f1", "df1", .0001, 10)<<endl;
cout<< "Newton's approximation to the root is: " << newton(0.5, "f1", "df1", .0001, 10)<<endl;
cout<< "Newton's approximation to the root is: " << newton(3.0, "f2", "df2", .0001, 10)<<endl;
}
```

**Code:**
```C++
// xo is initial guess, f and df identify which function and derivative in the func function
double newton(double x0, string f, string df, double tol, int maxIter){
// initialize variables, and calculate initial value of function and derivative
double error=10*tol;
int count=0;
double f0=func(x0, f);
double fp0=func(x0,df);
// until the tolerance is less than error or max # of iterations is exceeded
while(error > tol && count < maxIter){
// checks to see if derivative is zero (less than machine epsilon)
if(abs(fp0)<1.11022e-16){
// if so output error message and quit program
cout <<"Derivative is zero. Pleas input different guess."<< endl;
return EXIT_SUCCESS;}
count++;
// identify a closer approximation
double x= x0-f0/fp0;
// find the error
double error0=abs(x-x0);
// check that the sequence is converging
if(count>2 && error < error0){
// if not output error message and quit program
cout << "Please choose a point with a sufficiently small interval for which the sequence will converge." << endl;
return EXIT_SUCCESS;}
error=error0;
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
Newton's approximation to the root is: Derivative is zero. Pleas input different guess.
0
Newton's approximation to the root is: -9.38962e-14
Newton's approximation to the root is: 3.76991

```

**Last Modification Date:**
Sep. 30, 2017

