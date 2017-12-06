# Computational Mathematics Software Manual

## **Routine Name:** matrixvec

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The matrix vector function multiplies a matrix by a vector by running through a nested for loop and in simple terms calculates the dot product for each row in the matrix. 

**Input:**  The input is a vector of vector of doubles, which is a matrix, and a vector of doubles.

**Output:** The routine provides a vector of type double with the dimensions: rows of matrix x 1.

**Code:**
```C++
vector <double> matrixvec (vector<vector<double>> matrix, vector <double> vec){
    vector <double> prod;
    for (int i=0; i<matrix[0].size(); i++){
        prod.push_back(0);
    }
    for (int i=0; i<matrix.size(); i++){
        for (int j=0; j< vec.size(); j++){
            prod[i]+=matrix[i][j]*vec[j];
        }
        cout << prod[i] << "  ";
    }
    cout << endl;
    return prod;
}
```

**Example:**
```C++
int main(){
    vector < vector < double >> matrix1 = {{-5,2,1},{1,2, -9}, {0, -4, 12}};
    vector <double> vec3= {1,2,1};
    matrixvec(matrix1, vec3);
}
```

**Results:**  
```
0  -4  4   
```

**Last Modification Date:** Oct. 3, 2017
