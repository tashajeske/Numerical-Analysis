# Computational Mathematics Software Manual

## **Routine Name:** Hsecant

**Author:** Nitasha Jeske

**Language:** C++

**Description:** This routine is a hybrid of Bisection and secant method. When secant method encounters a zero derivative or a sequence that is not converging, instead of printing out an error, it calls a revised form of the bisection method to bisect the given interval 4 times and uses the last midpoint as the new guess. 

**Input:** x0 and x1 are the initial guesses at the root, a and b are the endpoints of the interval, f indicates the desired fucntion, tol is the allowed tolerance and maxIter is the max number of iterations to be run.

**Output:** The output is an approximation to the root of type double.

**Code:**
```C++
// xo and x1 are the initial guesses, a and b are the interval for bisection to work, f and df identify which function and derivative in the func function
double Hsecant(double x0, double x1, double a, double b, string f, double tol, int maxIter){
    // initialize error so it will enter the while loop, and other variables
    double error=10*tol;
    int count=1;
    double f0=func(x0, f);
    double f1=func(x1, f);
    double fpa=(x1-x0)/(f1-f0);
    // create a vector from the intervals and midpoint from bisect, retain endpoints in case bisect needs to be called multiple times
    vector <double> Ans = bisect(a,b,f);
    // start new count for the following while loop
    int count1=1;
    // checks that approximated derivative is not less than machine epsilon, added counter to avoid infinite loop
    while(abs(fpa)<1.11022e-16 && count1 <maxIter){
        count1++;
        // call bisect and update values with new guesses obtained from bisect
        vector <double> Ans = bisect(a,b,f);
        a=Ans[0];
        b=Ans[1];
        x0=x1;
        x1=Ans[2];
        f0=func(x0, f);
        f1=func(x1, f);
        fpa=(x1-x0)/(f1-f0);
    }
    // approximate until desired tolerance or max iterations is met
    while(error > tol && count < maxIter){
        // another counter for following while loop
        int count2=0;
        // again check for zero derivative, once in loop call bisect and update values
        while(abs(fpa)<1.11022e-16 && count2<maxIter){
            count2++;
            a=Ans[0];
            b=Ans[1];
            x0=Ans[2];
            vector <double> Ans = bisect(a,b,f);
            f0=func(x0, f);
            fpa=(x1-x0)/(f1-f0);
        }
        count++;
        double error0=abs(x1-x0);
        int count3=1;
        // check that the errors are decreasing or that the sequence of approximations is converging
        while(count>2 && error < error0 && count3<maxIter){
            count3++;
            // bisect the function if the sequence is divergent and update everything
            vector <double> Ans = bisect(a,b,f);
            a=Ans[0];
            b=Ans[1];
            x0=x1;
            x1=Ans[2];
            f0=func(x0, f);
            f1=func(x1, f);
            fpa=(x1-x0)/(f1-f0);
            error=error0;
            error0=abs(x1-x0);
        }
        error=error0;
        x0=x1;
        f0=f1;
        x1= x0-f0/fpa;
        f1=func(x1, f);
        fpa=(x1-x0)/(f1-f0);
    }
    return x1;
}
```

**Example:** 
```C++
double func (double x, string f){
    if (f=="f1") return x*exp(-x);
    else if (f=="df1") return exp(-x)-x*exp(-x);
    else return EXIT_SUCCESS;
}
// need to pass in interval, pass in which function, pass in tolerance, and a max number of iterations
vector<double> bisect (double a, double b, string f){
    // find the values of function at interval end points
    double tol= 0.0001;
    double f_a = func(a, f);
    double f_b = func(b, f);
    double c=0;
    // if this value is not negative there is not a guaranteed zero in the interval so return an error message
    if (f_a*f_b >= 0.0) {
        cout << "By intermediate value theorem, you are not guaranteed a root in this interval. Please provide a new interval." << endl;
        vector<double> fail;
        fail.push_back(0.0);
        return fail;
    }
    // for loop to make sure conditions of error > tolerance and count < 4
    for (int n=0; n<(log((b-a)/tol)/log(2)+1) && n < 4; n++){
        // take midpoint of a and b, call it c
        c=.5* (a+b);
        // find value of function at c
        double f_c= func(c, f);
        // check to see which half of interval contains root and set new endpoints a and b
        if (f_c==0) continue;
        else if (f_a*f_c < 0){ 
            b=c; 
            f_b=f_c;
        }
        else { 
            a=c; 
            f_a=f_c;
        }
    }
    vector<double> vec;
    vec.push_back(a); vec.push_back(b); vec.push_back(c);
    return vec;
}

int main(){
    cout<< "Bisect/Secant Hybrid approximation to the root is: " << Hsecant(1.0, 1.5, -10, 9, "f1", .0001, 10) << endl;
}   
```

**Results:**  
```C++
Bisect/Secant Hybrid approximation to the root is: -2.32698e-12
```

**Last Modification Date:** Sep. 30, 2017

