# Computational Mathematics Software Manual

## **Routine Name:** VerrorInf

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The Vector Infinity Error takes the difference of two vectors by subtracting each corresponding entry in the vectors and then provides the Vector Infinity Norm of the difference vector, which is the maximum of the absolute values of the entries. 

**Input:**  The input is two vectors of doubles.

**Output:** The routine returns the Vector Infinity Error of type double.

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
vector <double> vec2={2.0, 1.0, 0.0, 1.0};
cout << VerrorInf(vec1, vec2) << endl;
}
```

**Code:**
```C++
double VerrorInf (vector <double> vec1,  vector <double> vec2){
vector <double> vecdiff;
for (int i=0; i<vec1.size(); i++){
vecdiff.push_back(vec1[i]-vec2[i]);
}
double maximum= maxEntry(vecdiff);
return maximum;
}
```

**And the output is as follows:**  
```
5
```

**Last Modification Date:**
Oct. 3, 2017
