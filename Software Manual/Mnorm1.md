# Computational Mathematics Software Manual

## **Routine Name:** Mnorm1

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The Matrix 1 Norm takes the maximum absolute column sum by adding the absolute value of the elements in the each column and taking the maximum sum.

**Input:**  The input is a vector of vectors of doubles, or a matrix.

**Output:** The routine provides the Matrix 1 Norm of type double.

**Code:**
```C++
double Mnorm1 (vector<vector<double>> matrix){
    double norm=0.0;
    for (int i=0; i<matrix.size(); i++){
        double sum=0.0;
        for (int j=0; j< matrix[i].size(); j++){
            sum+=abs(matrix[j][i]);
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
    cout << Mnorm1(matrix1) << endl;
}
```

**Results:**  
```
22
```

**Last Modification Date:** Oct. 3, 2017
