# Computational Mathematics Software Manual

## **Routine Name:** matrixmatrix

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The matrix matrix function takes the product of two matrices by applying the dot product for each of the rows in the first matrix paired with each column in the second matrix.

**Input:**  The input is two vectors of vectors of doubles, or technically two matrices.

**Output:** The routine provides a vector of vector of doubles which has the dot product values as the entries.

```C++
int main(){
vector < vector < double >> matrix1 = {{-5,2,1},{1,2, -9}, {0, -4, 12}};
vector < vector < double >> matrix2 = {{1,2,3}, {1,2,3}, {1,2,3}};
matrixmatrix(matrix1,matrix2);
```

**Code:**
```C++
vector<vector<double>> matrixmatrix (vector<vector<double>> matrix1, vector<vector<double>> matrix2){
vector <vector<double>> prod(matrix1[0].size(), vector<double>(matrix2.size(),1));
for (int i=0; i<prod.size(); i++){
for (int j=0; j<prod[i].size(); j++){
prod[i][j]=0.0;
}
}
for (int i=0; i<matrix1[0].size();i++){
for (int j=0; j<matrix2.size(); j++){
for (int k=0; k<matrix1[0].size(); k++){
prod[i][j]+=matrix1[i][k]*matrix2[k][j];
}
cout << prod[i][j] << "  ";
}
cout << endl;
}
return prod;
}
```

**And the output is as follows:**  
```
-2  -4  -6  
-6  -12  -18  
8  16  24  
```

**Last Modification Date:**
Oct. 3, 2017
