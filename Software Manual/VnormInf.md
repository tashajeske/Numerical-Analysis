# Computational Mathematics Software Manual

## **Routine Name:** VnormInf

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The Vector Infinity Norm calls a maxEntry function that determines the maximum value of the absolute values of the entries in the vector.

**Input:**  The input is a vector of doubles.

**Output:** The routine provides the Vector Infinity Norm of type double.

**Code:**
```C++
double VnormInf (vector <double> vec){
    double maximum= maxEntry(vec);
    return maximum;
}
```

**Example:**
```C++
double maxEntry (vector <double> vec){
    double current=max(abs(vec[0]), abs(vec[1]));
    for (int i=2; i < vec.size(); i++){
        current=max(current, abs(vec[i]));
    }
    return current;
}

int main(){
    vector <double> vec1={1.0,2.0,3.0,-4.0};
    cout << VnormInf(vec1) << endl;
}
```

**Results:**  
```
4
```

**Last Modification Date:** Oct. 3, 2017
