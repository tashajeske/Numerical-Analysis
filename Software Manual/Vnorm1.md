# Computational Mathematics Software Manual

## **Routine Name:** Vnorm1

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The Vector 1 Norm sums the absolute values of each entry in the vector.

**Input:**  The input is a vector of doubles.

**Output:** The routine provides the Vector 1 Norm of type double.

**Example:**
```C++
int main(){
vector <double> vec1={1.0,2.0,3.0,-4.0};
cout << Vnorm1(vec1) << endl;
}
```

**Code:**
```C++
double Vnorm1(vector <double> vec){
double abssum=0;
for (int i=0; i<vec.size(); i++){
abssum=abssum+abs(vec[i]);
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

