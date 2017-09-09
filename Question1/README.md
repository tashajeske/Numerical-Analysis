## NAME: DMacEps

### Description: 
This routine will calculate the double precision of the computer I am working on. The program adds a value to one and divides by two until the value is small enough that the quotient is accepted as one. This value provides the machine epsilon of the computer. 

### Input:
Since this routine is specific in the values it uses to calculate the accuracy, there is no input.

### Output: 
The program produces a double, specifically the machine epsilon for a double precision number system. 

### Code:
```C++
void DMacEps(){
double y=1.0;
double y0=1.0;
int Dn=0;
while((1+y0) != 1){
y0=y;
y=y/2;
Dn++;
}
cout << "The machine epsilon for double precision number systems is " << y0 << endl;
}
```

### Example:
```C++
int main(){
DMacEps();
}
```
And the output is as follows: "The machine epsilon for double precision number systems is 1.11022e-16"


### Last Modification Date:
Sep. 1, 2017

### Author:
Nitasha Jeske


