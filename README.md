## NAME: SMacEps

### Description: 
This routine will calculate the floating point precision of the computer I am working on. The program adds a value to one and divides by two until the value is small enough that the sum is accepted as one. This value provides the machine epsilon of the computer. 

### Input:
Since this routine is specific in the values it uses to calculate the accuracy, there is no input.

### Output: 
The program produces a float, specifically the machine epsilon for a floating point number system. 

### Code:
```C++
void SMacEps(){
float x=1.0;
float x0=1.0;
int Sn=0;
while ((1+x0) != 1){
x0=x;
x=x/2;
Sn++;
}
cout << "The machine epsilon for floating point number system is " << x0 << endl;
}
```

### Example:
```C++
int main(){
SMacEps();
}
```
And the output is as follows: "The machine epsilon for floating point number system is 5.96046e-08"


### Last Modification Date:
Sep. 1, 2017

### Author:
Nitasha Jeske


