# Computational Mathematics Software Manual

## **Routine Name:** Verror1

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The Vector 1 Error takes the difference of two vectors by subtracting each corresponding entry in the vectors and then provides the Vector 1 Norm of the difference vector, which is a sum of the absolute value of the entries. 

**Input:**  The input is two vectors of doubles.

**Output:** The routine returns the Vector 1 Error of type double.

**Example:**
```C++
int main(){
vector <double> vec1={1.0,2.0,3.0,-4.0};
vector <double> vec2={2.0, 1.0, 0.0, 1.0};
cout << Verror1(vec1, vec2) << endl;
}
```

**Code:**
```C++
double Verror1 (vector <double> vec1, vector <double> vec2){
double abssum=0;
for (int i=0; i<vec1.size(); i++){
abssum=abssum+abs(vec1[i]-vec2[i]);
}
return abssum;
}
```

**And the output is as follows:**  
```
10
```

**Last Modification Date:**
Oct. 3, 2017
