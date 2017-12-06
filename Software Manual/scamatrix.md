# Computational Mathematics Software Manual

## **Routine Name:** scamatrix

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The scalar matrix function takes a double and a matrix and scales/multiplies each value in the matrix by the double value passed in.

**Input:**  The input is a double, the scalar value, and a vector of vector of doubles, which is the matrix.

**Output:** The routine provides a vector of vector of doubles which has the scaled values as the entries.

**Code:**
```C++
vector<vector<double>> scamatrix (vector<vector<double>> matrix, double a){
    for (int j=0; j<matrix.size(); j++){
        for (int i=0; i< matrix[j].size(); i++){
            matrix[j][i]=a*matrix[j][i];
            cout << matrix[j][i] << "  ";
        }
        cout << endl;
    }
    return matrix;
}
```

**Example:**
```C++
int main(){
    vector < vector < double >> matrix1 = {{-5,2,1},{1,2, -9}, {0, -4, 12}};
    double a1=2.0;
    scamatrix (matrix1, a1);
}
```

**Results:**  
```
-10  4  2  
2  4  -18  
0  -8  24  
```

**Last Modification Date:** Oct. 3, 2017
