# Computational Mathematics Software Manual

## **Routine Name:** dotprod

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The dot product function takes a two vectors and multiplies corresponding entries in the vectors and returns the sum of these products. 

**Input:**  The input is two vectors of doubles.

**Output:** The routine provides a double value which is the dot product.


**Code:**
```C++
double dotprod(vector <double> vec1, vector <double> vec2){
    double sum=0.0;
    for (int i=0; i<vec1.size(); i++){
        sum=sum+vec1[i]*vec2[i];
    }
    return sum;
}
```

**Example:**
```C++
int main(){
    vector <double> vec1={1.0,2.0,3.0,-4.0};
    vector <double> vec2={2.0, 1.0, 0.0, 1.0};
    cout << dotprod(vec1, vec2) << endl;
}
```

**Results:**  
```
0 
```

**Last Modification Date:** Oct. 3, 2017
