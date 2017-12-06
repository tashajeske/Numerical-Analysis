# Computational Mathematics Software Manual

## **Routine Name:** MnormInf

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The Matrix Infinity Norm takes the maximum absolute row sum by adding the absolute value of the elements in the each row and taking the maximum sum.

**Input:**  The input is a vector of vectors of doubles, or a matrix.

**Output:** The routine provides the Matrix Infinity Norm of type double.

**Code:**
```C++
double MnormInf (vector<vector<double>> matrix){
    double norm=0.0;
    for (int i=0; i<matrix.size(); i++){
        double sum=0.0;
        for (int j=0; j< matrix[i].size(); j++){
            sum+=abs(matrix[i][j]);
        }
        if (sum > norm) norm = sum;
    }
    return norm;
}
```

**Example:**
```C++
int main(){
    vector < vector < double >> matrix1 = {{-5,2,1},{1,2, -9}, {0, -4, 12}};
    cout << MnormInf(matrix1) << endl;
}
```

**Results:**  
```
16
```

**Last Modification Date:** Oct. 3, 2017
