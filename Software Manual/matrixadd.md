# Computational Mathematics Software Manual

## **Routine Name:** matrixadd

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The matrix add function takes two matrices and adds the corresponding i,j entries to make a new matrice. 

**Input:**  The input is two vectors of vectors of doubles, or technically two matrices.

**Output:** The routine provides a vector of vector of doubles which has the summed values as the entries.

```C++
int main(){
vector < vector < double >> matrix1 = {{-5,2,1},{1,2, -9}, {0, -4, 12}};
vector < vector < double >> matrix2 = {{1,2,3}, {1,2,3}, {1,2,3}};
matrixadd (matrix1, matrix2);
```

**Code:**
```C++
vector<vector<double>> matrixadd (vector<vector<double>> matrix1, vector<vector<double>> matrix2){
for (int j=0; j<matrix1.size(); j++){
for (int i=0; i< matrix1[j].size(); i++){
matrix1[j][i]=matrix1[j][i]+matrix2[j][i];
cout << matrix1[j][i] << "  ";
}
cout << endl;
}
return matrix1;
}
```

**And the output is as follows:**  
```
-4  4  4  
2  4  -6  
1  -2  15  
```

**Last Modification Date:**
Oct. 3, 2017
