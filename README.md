# Computational Mathematics Software Manual

## **Routine Name** Bisection Method

**Author:** Nitasha Jeske

**Language:** C++

**Description:** This routine uses the intermediate value theorem to determine if there is a root on the given interval. if so it can approximate the root by dividing the interval in half until a pre-determined maximum number of iterations or tolerance is met. 

**Input:** The inputs for this program are double a, double b, string f, double tol and int maxIter. a and b are the left and right bounds for the interval, respectively. The string f represents which function will be used to determine roots, as long as the function is declared and defined. Double tol is a measure of accuracy of the root, and int maxIter sets a maximum number of iterations for the interval to be divided if the tolerance is not met first. 

**Output:** The program will provide the first root it finds in the function on the interval, or print an error message telling the user to input a valid function or different interval. 

**Example:**
```C++
double func(string f, double x){
if (f == "f1") {
double y=3*x*sin(10*x); // looking for interval [0, 7]
return y;
}
else if (f=="f2"){ // looking for interval (-infinity, + infinity)
double y=x*exp(-x);
return y;
}

int main (){
cout<< "Unbounded intervals can be represented with suffiiciently large numbers." << endl;
cout<< bisection(0, 7, "f1", .000000000001, 1000000000) << endl;
cout<< bisection(-100, 100, "f2", .000000000001, 1000000000) << endl;
}
``

**Code:**
```C++
// need to pass in interval, pass in which function, pass in tolerance, and a max number of iterations
double bisection (double a, double b, string f, double tol, int maxIter){
double error=10.0*tol;
// find the values of function at interval end points
double f_a = func(f, a);
double f_b = func(f, b);
double c=0;
// if this value is not negative there is not a guaranteed zero in the interval so return an error message
if (f_a*f_b > 0.0) {
cout << "By intermediate value theorem, you are not guaranteed a root in this interval. Please provide a new interval." << endl;
return 0;
}// initialize count variable
// for loop to make sure conditions of error > tolerance and count < maxIter
for (int n=0; n<(log((b-a)/tol)/log(2)+1) && n <maxIter; n++){
// take midpoint of a and b, call it c
c=.5* (a+b);
// find value of function at c
double f_c= func(f, c);
// check to see which half of interval contains root and set new endpoints a and b
if (f_c==0){
continue;
}
else if (f_a*f_c < 0){
b=c;
f_b=f_c;
}
else {
a=c;
f_a=f_c;
}
// the error will be the remaining interval
error=b-a;
}
cout << "A root of the function can be found at ";
// the best guess of the root will be at the midpoint c
return c;
}
```

And the output is as follows: 
Unbounded intervals can be represented with suffiiciently large numbers.
A root of the function can be found at 5.02655
A root of the function can be found at 0


Last Modification Date:
Sep. 14, 2017

Author:
Nitasha Jeske
