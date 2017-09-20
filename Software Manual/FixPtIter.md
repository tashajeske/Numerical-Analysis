# Computational Mathematics Software Manual

## **Routine Name:** FixPtIter

**Author:** Nitasha Jeske

**Language:** C++

**Description:** This routine will approximate the root of a function when given a valid estimate for the root. It uses convergence of a sequence to evaluate the root. A function g is picked such that since f(x)=0, g(x)=x. Then the routine iterates through increasingly closer values of x0 to find the 

**Input:** The inputs for this program are double x0, string f, double tol, and int maxIter. x0 is the initial guess of the root. f is which function is being used as long as the fucntion is defined in func(). tol is the level of accuracy. maxIter is a maximum number of iterations the routine will run through 

**Output:** The program will output an approximation to the root of type double. The approximation will be to the closest root of the estimate provided, and only if the estimate is sufficiently close to a root. 

**Example:** This example approximates the roots for the functions: 3*x*sin(10*x) and x*exp(-x) 
```C++
double func(double x, string f){
if (f=="f1"){
double y=3*x*sin(10*x);
// using x_(k+1) = g(x_k)=x_k-f(x_k)
// g'(x) is too large so divide y by 100
double g=x-y/100;
return g;
}
if (f=="f2"){
double y=x*exp(-x);
double g=x-y;
return g;
}
else return 0;
}

int main(){
fixpt(5, "f1", .000001, 10000);
fixpt(1, "f2", .000001, 10000);
}
```

**Code:**
```C++
// need an initial guess x0, a string which declares which function to find roots of, a tolerance, and max number of iterations
void fixpt(double x0, string f, double tol, int maxIter){
// start a counter i
int i=1;
// g will be the value of x_k - f(x_k)
double g = func(x0, f);
// runs through loop and finds closer values to the root as long as conditions are not met
while(i < maxIter && abs(x0-g)> tol){
x0=g;
g = func(x0, f);
i++;
}
// if reaches maxIter but is still larger than tolerance than an adequate solution is not found. tell user to input better guess.
if (i>= maxIter){
cout << "Solution not found. Try inputing a valid guess. Or method may diverge." << endl;
return;
}
cout<< "The approximation for solution of " << f << " is " << g << endl;
}
```

**And the output is as follows:**  
```C++
The approximation for solution of f1 is 5.02655
The approximation for solution of f2 is 8.90987e-19
```

**Last Modification Date:**
Sep. 19, 2017

