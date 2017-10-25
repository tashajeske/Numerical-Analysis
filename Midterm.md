## Math 4610 Midterm

### Nitasha Jeske


**Problem 1:**  Chapter 3: Exercise 21 and 23

The program below minimizes a smooth curve when the function, derivative, second derivative, the interval from a to b, the number of times to divide the interval into subintervals, a tolerance, and the max number of iterations. 
```C++
double func (double x, string f){
if (f=="f1") return sin(x);
else if (f=="f2") {
// make the function a piecewise since the limit of the function as x -> 0 is -1
if (x==0) return -1;
else return -sin(x)/x;
}
else if (f=="df1") return cos(x);
else if (f=="df2") {
// piecewise for derivative as well
if (x==0) return 0;
else return -cos(x)/x+sin(x)/pow(x,2);
}
else if (f=="d2f1") return -sin(x);
else if (f=="d2f2"){
// and piecewise for the second derivative
if (x==0) return 2.0/3.0;
else return sin(x)/x+2*cos(x)/pow(x,2)-2*sin(x)/pow(x,3);
}
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
vector<double> fail={0.0};
return fail;}
// for loop to make sure conditions of error > tolerance and count < 4
for (int n=0; n<(log((b-a)/tol)/log(2)+1) && n < 3; n++){
// take midpoint of a and b, call it c
c=.5* (a+b);
// find value of function at c
double f_c= func(c, f);
// check to see which half of interval contains root and set new endpoints a and b
if (f_c==0) continue;
else if (f_a*f_c < 0){ b=c; f_b=f_c;}
else { a=c; f_a=f_c;}}
vector<double> vec;
vec.push_back(a); vec.push_back(b); vec.push_back(c);
return vec;
}

// ai and bi are the interval for bisection to work, f and df identify which function and derivative in the func function
double hnewton(double ai, double bi, string f, string df, double tol, int maxIter){
// create a vector to add all roots to
vector <double> roots;
// find midpoint for approximating based on given interval
double x0=(ai+bi)/2;
// initialize error so it will enter the while loop, and other variables
double error=10*tol;
int count=0;
double f0=func(x0, f);
double fp0=func(x0,df);
// create a vector from the intervals and midpoint from bisect, retain endpoints in case bisect needs to be called multiple times
vector <double> Ans = bisect(ai,bi,f);
// start new count for the following while loop
int count1=1;
// checks that approximated derivative is not less than machine epsilon, added counter to avoid infinite loop
while(abs(fp0)<1.11022e-16 && count1<maxIter){
count1++;
// call bisect and update values with new guesses obtained from bisect
vector <double> Ans = bisect(ai,bi,f);
ai=Ans[0];
bi=Ans[1];
x0=Ans[2];
f0=func(x0, f);
fp0=func(x0,df);
}
// approximate until desired tolerance or max iterations is met
while(error > tol && count < maxIter){
// another counter for following while loop
int count2=1;
// again check for zero derivative, once in loop call bisect and update values
while(abs(fp0)<1.11022e-16 && count2<maxIter){
count2++;
vector <double> Ans = bisect(ai,bi,f);
ai=Ans[0];
bi=Ans[1];
x0=Ans[2];
f0=func(x0, f);
fp0=func(x0,df);
}
count++;
int count3=1;
double x= x0-f0/fp0;
double error0=abs(x-x0);
// check that the errors are decreasing or that the sequence of approximations is converging
while(count>2 && error < error0 && count3<maxIter){
count3++;
// bisect the function if the sequence is divergent and update everything
vector <double> Ans = bisect(ai,bi,f);
ai=Ans[0];
bi=Ans[1];
x0=Ans[2];
error=error0;
error0=abs(x-x0);
}
// update current erro and function values
error=error0;
if(!isnan(x))
x0=x;
f0=func(x0,f);
fp0=func(x0,df);
}
return x0;
}

void print(string a, vector <double> vec){
cout<< a;
for(int i=0; i<vec.size();i++){
cout << vec[i] << ", ";
}
cout<< endl;
}
// a and b are full interval for desired roots, f, df, and d2f identify which function and derivatives in the func function, nprobe is the number of times we will check the function for sign changes to guarantee root through bisection
void allnewton(double a, double b, string f, string df, string d2f, int nprobe, double tol, int maxIter){
// find length of given interval
double fullint=b-a;
// divide it by the number of probes
double subint=fullint/nprobe;
vector <double> subints;
// create a vector containing endpoints for the subintervals
for(int i=0; i<=nprobe; i++){
subints.push_back(a+subint*i);
}
vector <double> cpoints;
// for loop goes through each subinterval, calls the newton method to find the root in each interval
for(int i=1; i<subints.size(); i++){
double ai=subints[i-1];
double bi=subints[i];
double f_ai=func(subints[i-1], df);
double f_bi=func(subints[i], df);
if(f_ai*f_bi<0)
// add roots to a vector
cpoints.push_back(hnewton(ai, bi, df, d2f, tol, maxIter));
}
string cp= "The critical points of the function are: ";
print(cp, cpoints);
// check when 2nd derivative is positive to find minima and add those values to a vector
vector <double> locmin={};
for (int i=0; i<cpoints.size();i++){
if(func(cpoints[i], d2f)>0)
locmin.push_back(cpoints[i]);
}
string lm= "The local minima of the function are at x= ";
print(lm, locmin);

// need to find global minimum and the value associated with it
vector <double> glomin={locmin[0]};
for (int i=1; i<locmin.size(); i++){
if (func(locmin[i], f)==func(glomin[0],f))
glomin.push_back(locmin[i]);
else if (func(locmin[i], f)<func(glomin[0], f))
glomin[0]=locmin[i];
}
string gm= "The global min(s) is/are at x= ";
print(gm, glomin);

cout<< "The value of the global min(s) is " << func(glomin[0], f) << endl;
}
```
The code is tested on two examples (a) &phi;(x)=sin(x) and (b) &phi;(x)=-sin(x)/x




**Problem 2:**  Chapter 4: Exercise 5 and 7

**Problem 3:**  Chapter 5: Exercise 2

**Problem 4:**  Chapter 5: Exercise 17 and 18


