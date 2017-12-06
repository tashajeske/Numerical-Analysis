# Computational Mathematics Software Manual

## **Routine Name:** lufactor

**Author:** Nitasha Jeske

**Language:** C++

**Description:** This code computes the LU factorization of a matrix with scaled partial pivoting. It does this by first identifying the largest scaled pivot in the remaining rows, switching rows if necessary, and then doing a Gaussian elimination step to reduce the rows below. It replaces the lower triagular entries with the l_i,k factor used to reduce rows, while replacing the upper triangular entries with the Gauss reduced matrix. 

**Input:**  The input is a matrix, or a vector of vectors of doubles.

**Output:** The routine provides a matrix, or vector of vector of doubles which contains the L matrix as the entries below the diagonal, and the U matrix as the diagonal and entries above the diagonal. 

**Code:**
```C++
Matrix lufactor(Matrix matrix1){
    int rows = matrix1[0].size();
    int cols = matrix1.size();
    vector <int> map (matrix1[0].size());
    vector <double> S (rows);
    for (int k=0; k<rows; k++){
        S[k]=VnormInf(matrix1[k]);
    }
    for (int k=0; k<rows; k++){
        int maxRow=k;
        double maxVal=matrix1[k][k]/S[k];
        for (int i=k+1; i<rows; i++){
            double val=matrix1[i][k]/S[i];
            if (abs(val)>abs(maxVal)){
                maxVal=val;
                maxRow=i;
                swap(matrix1[maxRow],matrix1[k]);
                swap(map[maxRow], map[k]);
            }
        }
        for (int i=k+1; i<matrix1.size(); i++){
            double lik=matrix1[i][k]/matrix1[k][k];
            for (int j=k+1; j<matrix1[0].size(); j++){
                matrix1[i][j]=matrix1[i][j]-lik*matrix1[k][j];
            }
            matrix1[i][k]=lik;
        }
    }
    return matrix1;
}
```

**Example:**
```C++
typedef vector <vector <double>> Matrix;

double maxEntry (vector <double> vec){
    double current=max(abs(vec[0]), abs(vec[1]));
    for (int i=2; i < vec.size(); i++){
        current=max(current, abs(vec[i]));
    }
    return current;
}

double VnormInf (vector <double> vec){
    double maximum= maxEntry(vec);
    return maximum;
}

Matrix initMatrix (int row, int col){
    Matrix randmatrix (row, vector <double> (col));
    for (int i=0; i<row; i++){
        for (int j=0; j<col; j++){
            randmatrix[i][j]=rand()%50;
        }
    }
    return randmatrix;
}

void Print(Matrix matrix1){
    for (int i=0; i<matrix1.size(); i++){
        for (int j=0; j<matrix1[0].size();j++){
            cout<< matrix1[i][j] << "  ";
        }
        cout << endl;
    }
}

int main(){
  Matrix matrix2={{2,1,-4, 3},{5, -6, 2, 1}, {3, 1, 0, -2}, {4, 5, 0, -3}};
    Print(lufactor(matrix2));
}
```

**Results:**  
```
3  1  0  -2  
1.66667  -7.66667  2  4.33333  
0.666667  -0.0434783  -3.91304  4.52174  
1.33333  -0.478261  -0.244444  2.84444 
```

**Last Modification Date:** Oct. 18, 2017
