#Computational Mathematics Software Manual

## **Routine Name:** DMacEps

**Author:** Nitasha Jeske

**Language:** C++

**Description:** This double machine epsilon routine will calculate the double precision of the computer being used. The program adds a value to one. This value is initially one, but is divided by two each iteration, until the sum is accepted as one. The value on the final iteration provides the machine epsilon of the computer. 

**Input:** Since this routine is specific in the values it uses to calculate the accuracy, there is no input.

**Output:** The program produces a double, which represents the machine epsilon for a double precision number system. 

**Code:** 
```C++
void DMacEps(){
    double y=1.0;
    double y0=1.0;
    while((y+y0) != 1){
        y=y/2;
    }
    cout << "The machine epsilon for double precision number systems is " << y << endl;
}
```

**Example:**
```C++
int main(){
    DMacEps();
}
```

**Results:** 
```C++
"The machine epsilon for double precision number systems is 1.11022e-16"
```

**Last Modification Date:** Sep. 1, 2017


