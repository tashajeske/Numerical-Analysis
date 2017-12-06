# Computational Mathematics Software Manual

## **Routine Name:** matrixdif

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The matrix difference function takes two matrices and subtracts the corresponding i,j entries to make a new matrice. 

**Input:**  The input is two vectors of vectors of doubles, or technically two matrices.

**Output:** The routine provides a vector of vector of doubles which has the subtracted values as the entries.

**Code:**
```C++
vector<vector<double>> matrixdif (vector<vector<double>> matrix1, vector<vector<double>> matrix2){
    for (int j=0; j<matrix1.size(); j++){
        for (int i=0; i< matrix1[j].size(); i++){
            matrix1[j][i]=matrix1[j][i]-matrix2[j][i];
            cout << matrix1[j][i] << "  ";
        }
        cout << endl;
    }
    return matrix1;
}
```

**Example:**
```C++
int main(){
    vector < vector < double >> matrix1 = {{-5,2,1},{1,2, -9}, {0, -4, 12}};
    vector < vector < double >> matrix2 = {{1,2,3}, {1,2,3}, {1,2,3}};
    matrixdif (matrix1, matrix2);
}
```

**Results:**  
```
-6  0  -2  
0  0  -12  
-1  -6  9  
```

**Last Modification Date:** Oct. 3, 2017
