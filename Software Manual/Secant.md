# Computational Mathematics Software Manual

## **Routine Name:** Secant

**Author:** Nitasha Jeske

**Language:** C++

**Description:** Secant's method approximates the root of the function by taking an initial guess and subtracting off the function value divided by an approximation to the derivative. This difference becomes the new value. While doing that, the routine checks to make sure the derivative is non-zero and the sequence is converging within the interval. 

**Input:** x0 and x1 are the initial guesses at the root, f indicates the desired fucntion, tol is the allowed tolerance and maxIter is the max number of iterations to be run. 

**Output:** The output is an approximation to the root of type double, or an error message telling you to pick a different initial guess. 

**Example:**
```C++
// functions for approximating roots. use a string to identify which function is called
double func (double x, string f){
if (f=="f1") return x*exp(-x);
else if (f=="f2") return 3*x*sin(10*x);
else if (f=="df1") return exp(-x)-x*exp(-x);
else if (f=="df2") return 3*sin(10*x)+30*x*cos(10*x);
else return EXIT_SUCCESS;}
int main(){
cout<< "Secant approximation to the root is: " << secant(0.5, .45, "f1", .0001, 10) <<endl;
}
```

**Code:**
```C++
// xo and x1 are the initial guesses, f indicates which function in the func function
double secant(double x0, double x1, string f, double tol, int maxIter){
// initialize variables, and calculate initial value of function and approximate derivative
double error=10*tol;
int count=0;
double f0=func(x0, f);
double f1=func(x1, f);
double fpa0=(x1-x0)/(f1-f0);
// until the tolerance is less than error or max # of iterations is exceeded
while(error > tol && count < maxIter){
// checks to see if derivative is zero (less than machine epsilon)
if(abs(fpa0)<1.11022e-16){
// if so output error message and quit program
cout <<"Derivative is zero. Pleas input different guess."<< endl;
return EXIT_SUCCESS;}
count++;
//calculate the error
double error0=abs(x1-x0);
// check that the sequence is converging
if(count>4 && error < error0){
// if not output error message and quit program
cout << "Please choose a point with a sufficiently small interval for which the sequence will converge." << endl;
return EXIT_SUCCESS;}
//update values
error=error0;
x0=x1;
f0=f1;
x1= x0-f0/fpa0;
f1=func(x1, f);
fpa0=(x1-x0)/(f1-f0);}
// return approximation to root
return x1;}```

**Results:**  
```C++
Secant approximation to the root is: 2.69781e-12
```

**Last Modification Date:**
Sep. 30, 2017

