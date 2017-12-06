# Computational Mathematics Software Manual

## **Routine Name:** Verror2

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The Vector 2 Error takes the difference of two vectors by subtracting each corresponding entry in the vectors and then provides the Vector 2 Norm of the difference vector, which is the squareroot of the sum of the entries squared. 

**Input:**  The input is two vectors of doubles.

**Output:** The routine returns the Vector 2 Error of type double.

**Code:**
```C++
double Verror2(vector <double> vec1,  vector <double> vec2){
    double sumsq=0.0;
    for (int i=0; i<vec1.size(); i++){
        sumsq= sumsq + pow(vec1[i]-vec2[i], 2);
    }
    double norm = sqrt(sumsq);
    return norm;
}
```

**Example:**
```C++
int main(){
    vector <double> vec1={1.0,2.0,3.0,-4.0};
    vector <double> vec2={2.0, 1.0, 0.0, 1.0};
    cout << Verror2(vec1, vec2) << endl;
}
```

**Results:**  
```
6
```

**Last Modification Date:** Oct. 3, 2017
