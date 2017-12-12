# Math 4610 Take Home Final

## Nitasha Jeske

## Problem 4: 

** #3 on page 325 of text**

Using routines from previous homework assignments, the divided difference table and Newton's approach to polynomial interpolation have been computed given the x values and computed y values for the function sin(x). An example of these routines used on the sin(x) values is shown below. In the results section we see that the polynoimal interpolation of the function produces an approximation of 0.932141 which is very close to the actual value of 0.932039. This produces an error of 1e-04. We would expect this result to be so close since we know the sine function can be approximated very well using polynomials (Taylor series expansion). The degree of the polynomial is 4 since we are given 5 data points. The accuracy would likely be further increased if more abscissae were given. 

**Example:**
```C++
int main(){
    Vec x={0, .5235988, .7853982, 1.0471976, 1.5707963};
    Vec y={0, .5, .7071068, .8660254, 1};
    Print(DividedDiffTable(x, y));
    double P1=PolyInterp(x,y,1.2);
    cout<< "P(1.2) = " << P1 << endl;
    cout<< sin(1.2) << endl;
    cout<< "error = " << abs(P1-sin(1.2)) << endl;
}
```
**Results:**
```C++
0  0.95493  -0.208607  -0.136489  0.0287976  
P(1.2) = 0.932141
0.932039
error = 0.000102389
```


