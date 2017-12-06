# Computational Mathematics Software Manual

## **Routine Name:** SMacEps

**Author:** Nitasha Jeske

**Language:** C++

**Description:** This single machine epsilon routine will calculate the floating point precision of the computer being used. The program adds a value to one. This value is initially one, but is divided by two each iteration, until the sum is accepted as one. The value on the final iteration provides the machine epsilon of the computer. 

**Input:** Since this routine is specific in the values it uses to calculate the accuracy, there is no input.

**Output:** The program produces a float, which represents the machine epsilon for a floating point number system. 

**Code:**
``` C++
void SMacEps(){
    float x=1.0;
    float x0=1.0;
    while ((x+x0) != 1){
        x=x/2;
    }
    cout << "The machine epsilon for floating point number system is " << x << endl;
}
```

**Example:**
``` C++
int main(){
    SMacEps();
}
```

**Results:** 
``` C++
"The machine epsilon for floating point number system is 5.96046e-08"
```

**Last Modification Date:** Sep. 1, 2017


