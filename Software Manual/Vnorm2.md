# Computational Mathematics Software Manual

## **Routine Name:** Vnorm2

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The Vector 2 Norm takes the square root of the sum of the absolute value of the entries of the vector. 

**Input:**  The input is a vector of doubles.

**Output:** The routine provides the Vector 2 Norm of type double.

**Code:**
```C++
double Vnorm2(vector <double> vec){
    double sumsq=0.0;
    for (int i=0; i<vec.size(); i++){
        sumsq= sumsq + pow(vec[i], 2);
    }
    double norm = sqrt(sumsq);
    return norm;
}
```

**Example:**
```C++
int main(){
    vector <double> vec1={1.0,2.0,3.0,-4.0};
    cout << Vnorm2(vec1) << endl;
}
```

**Results:**  
```
5.47723
```

**Last Modification Date:** Oct. 3, 2017
